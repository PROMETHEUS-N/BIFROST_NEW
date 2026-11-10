# Azure Resource Group — Module Reference

![Bicep](https://img.shields.io/badge/IaC-Bicep-0078D4?logo=azuredevops&logoColor=white) ![Azure](https://img.shields.io/badge/Platform-Microsoft%20Azure-0078D4?logo=microsoftazure&logoColor=white) ![Workflow](https://img.shields.io/badge/Workflow-GitHub%20Actions-2088FF?logo=githubactions&logoColor=white)

> **Module:** `modules/RG/resourcegroup.bicep`  
> **Workflow job:** `deploy-rg`  
> **Deployment scope:** Subscription scope (`targetScope = 'subscription'`)

## 1. Purpose

This reusable Bicep module provisions the azure resource group resource. The workflow reads the resource definition from the root `input.json`, maps the fields to Bicep parameters, creates a temporary ARM parameter file, runs What-If, and then deploys the module.

## 2. Inputs and their sources

The workflow does not pass the whole JSON object directly. It explicitly maps the following fields:

| Bicep parameter | Source / JSON path | Value source |
|---|---|---|
| `rgname` | `landingZones.resourceGroups[].rgName` | `input.json` |
| `location` | `landingZones.resourceGroups[].location` | `input.json` |
| `tags` | `landingZones.resourceGroups[].tags` | `input.json` |

**Secret handling:** No resource-specific password is consumed by this module. 

## 3. Prerequisites and dependencies

- A valid Azure subscription selected through `AZURE_SUBSCRIPTION_ID` GitHub secret.
- Azure region supplied by `location` in `input.json`.
- OIDC-authenticated identity (`AZURE_CLIENT_ID`, `AZURE_TENANT_ID`) must have permission to create resource groups at subscription scope.

### Deployment ordering

Resource group creation is the first provisioning stage.

```mermaid
flowchart TD
  A[GitHub Actions: deploy-rg] --> B[input.json: resourceGroups[]]
  C[GitHub secret: AZURE_SUBSCRIPTION_ID] --> D[Azure OIDC context]
  B --> E[Build ARM parameter file]
  D --> F[Subscription-scope What-If]
  E --> F
  F --> G[resourcegroup.bicep]
  G --> H[Create resource group]
  H --> I[Azure Resource Groups / deployment history]
```

## 4. Resource naming structure

Exact `rgName` from input. No Bicep suffix or generated unique string is applied.

**Important:** The workflow deployment name (for example `pike-...` plus `github.run_id`) is an ARM deployment-history label. It is **not** the Azure resource name. The Azure resource name is determined by the naming rule above.

## 5. Outputs and where to find them

The module declares these Bicep outputs:

| Output name | Meaning |
|---|---|
| `resource group` | `rg.id`, `rg.name`, `rg.location` are implicit resource properties; this module declares no explicit Bicep outputs. |

Outputs are returned by the ARM deployment operation. The workflow currently invokes `az deployment group create` (or `az deployment sub create` for this subscription-scope module) but does not explicitly export the output object to a GitHub Actions artifact or summary. To inspect it, query the deployment record:

```bash
# Resource-group deployment (replace placeholders)
az deployment group show --resource-group <resourceGroupName> --name <deploymentName> --query properties.outputs -o json

# Subscription-scope deployment (Resource Group module)
az deployment sub show --name <deploymentName> --query properties.outputs -o json
```

`az group show --name <rgName> --query '{name:name,id:id,location:location,tags:tags}' -o json` and `az deployment sub list --query "[?contains(name, 'pike-rg-')].{name:name,state:properties.provisioningState}" -o table`.

### Where to see the resource in Azure Portal

Open **Azure Portal → Resource groups → <target resource group> → <resource>**. For the Resource Group module, open **Subscriptions → <subscription> → Resource groups**. The deployment record and its outputs are available under the relevant scope's **Deployments** history.

## 6. How the workflow calls this module

The `deploy-rg` job in `.github/workflows/deploy.yml`:

1. Runs after its declared `needs` dependency/dependencies complete.
2. Checks out the repository and authenticates with `azure/login@v2` using OIDC secrets (`AZURE_CLIENT_ID`, `AZURE_TENANT_ID`, `AZURE_SUBSCRIPTION_ID`).
3. Reads `input.json` and loops over `landingZones.<collection>[]`.
4. Maps JSON properties to Bicep parameter names and writes a temporary ARM parameter JSON file under `$env:RUNNER_TEMP`.
5. Runs Azure deployment **What-If** against `resourcegroup.bicep`.
6. Runs Azure deployment **create** if What-If succeeds.

**Job timing:** After `prechecks` and `azure-login-check`; first resource deployment stage.

| Workflow item | Current implementation |
|---|---|
| Job ID | `deploy-rg` |
| Display name | See the job's `name` in `.github/workflows/deploy.yml` |
| Template path | `modules/RG/resourcegroup.bicep` |
| Input collection | `landingZones.resourceGroups[]` |
| Azure CLI operation | `az deployment sub what-if`, followed by `create` |

## 7. Operational notes

- The workflow uses a temporary parameter file; it is not committed back to the repository.
- The module's declared outputs are available in Azure deployment history even though the current workflow does not publish them separately.
- Resource deployment names in Azure deployment history are run-scoped labels and should not be confused with resource names.
- A successful What-If is a preview, not proof that the deployment will succeed; Azure policy, provider registration, quota, naming availability and RBAC can still affect deployment.

---

*Reference generated from the `WorkingMark1` branch implementation. If the module or workflow mapping changes, update this reference alongside the code.*
