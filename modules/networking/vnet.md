# Virtual Network (VNet) — Module Reference

![Bicep](https://img.shields.io/badge/IaC-Bicep-0078D4?logo=azuredevops&logoColor=white) ![Azure](https://img.shields.io/badge/Platform-Microsoft%20Azure-0078D4?logo=microsoftazure&logoColor=white) ![Workflow](https://img.shields.io/badge/Workflow-GitHub%20Actions-2088FF?logo=githubactions&logoColor=white)

> **Module:** `modules/networking/vnet.bicep`  
> **Workflow job:** `deploy-vnet`  
> **Deployment scope:** Resource-group scope (`az deployment group`)

## 1. Purpose

This reusable Bicep module provisions the virtual network (vnet) resource. The workflow reads the resource definition from the root `input.json`, maps the fields to Bicep parameters, creates a temporary ARM parameter file, runs What-If, and then deploys the module.

## 2. Inputs and their sources

The workflow does not pass the whole JSON object directly. It explicitly maps the following fields:

| Bicep parameter | Source / JSON path | Value source |
|---|---|---|
| `location` | `landingZones.vnets[].location` | `input.json` |
| `vnetName` | `landingZones.vnets[].name` | `input.json` |
| `addressPrefixes` | `landingZones.vnets[].addressPrefixes` | `input.json` |
| `tags` | `landingZones.vnets[].tags` | `input.json` |
| `dnsServers` | `landingZones.vnets[].dnsServers` | `input.json` |
| `subnets` | Hard-coded as an empty array `[]` in the workflow parameter map | Workflow logic (not `input.json`) |

**Secret handling:** No resource-specific password is consumed by this module. 

## 3. Prerequisites and dependencies

- Target resource group must exist.
- VNet name, region, CIDR address prefixes, DNS list and tags come from `input.json`.
- Address prefixes must be valid and non-overlapping with connected networks.
- The workflow deliberately passes `subnets: []`; subnet resources are created later by the dedicated subnet module.
- Identity needs VNet write permission in the target resource group.

### Deployment ordering



```mermaid
flowchart TD
  A[deploy-route-table completes] --> B[deploy-vnet job]
  C[input.json: vnets[]] --> D[Check whether VNet exists]
  D -->|Exists| S[Skip VNet template]
  D -->|Missing| E[Map VNet properties; subnets = empty]
  E --> F[What-If]
  F --> G[vnet.bicep]
  G --> H[Create VNet]
  H --> I[Azure VNet + deployment outputs]
  I --> J[deploy-subnet can proceed]
```

## 4. Resource naming structure

Exact `name` from input (example `vnet-pikehex-dev-001`); no suffix. If it already exists, workflow logs a skip and does not invoke Bicep.

**Important:** The workflow deployment name (for example `pike-...` plus `github.run_id`) is an ARM deployment-history label. It is **not** the Azure resource name. The Azure resource name is determined by the naming rule above.

## 5. Outputs and where to find them

The module declares these Bicep outputs:

| Output name | Meaning |
|---|---|
| `vnetId` | Full VNet resource ID. |
| `vnetNameOut` | Actual VNet name. |

Outputs are returned by the ARM deployment operation. The workflow currently invokes `az deployment group create` (or `az deployment sub create` for this subscription-scope module) but does not explicitly export the output object to a GitHub Actions artifact or summary. To inspect it, query the deployment record:

```bash
# Resource-group deployment (replace placeholders)
az deployment group show --resource-group <resourceGroupName> --name <deploymentName> --query properties.outputs -o json

# Subscription-scope deployment (Resource Group module)
az deployment sub show --name <deploymentName> --query properties.outputs -o json
```

`az network vnet show -g <resourceGroupName> -n <vnetName> -o json`; outputs via `az deployment group show ... --query properties.outputs -o json`. A skipped existing VNet has no new deployment outputs for that run.

### Where to see the resource in Azure Portal

Open **Azure Portal → Resource groups → <target resource group> → <resource>**. For the Resource Group module, open **Subscriptions → <subscription> → Resource groups**. The deployment record and its outputs are available under the relevant scope's **Deployments** history.

## 6. How the workflow calls this module

The `deploy-vnet` job in `.github/workflows/deploy.yml`:

1. Runs after its declared `needs` dependency/dependencies complete.
2. Checks out the repository and authenticates with `azure/login@v2` using OIDC secrets (`AZURE_CLIENT_ID`, `AZURE_TENANT_ID`, `AZURE_SUBSCRIPTION_ID`).
3. Reads `input.json` and loops over `landingZones.<collection>[]`.
4. Maps JSON properties to Bicep parameter names and writes a temporary ARM parameter JSON file under `$env:RUNNER_TEMP`.
5. Runs Azure deployment **What-If** against `vnet.bicep`.
6. Runs Azure deployment **create** if What-If succeeds.

**Job timing:** After `deploy-route-table`; before subnet deployment. Workflow checks for an existing VNet first and skips this template if found.

| Workflow item | Current implementation |
|---|---|
| Job ID | `deploy-vnet` |
| Display name | See the job's `name` in `.github/workflows/deploy.yml` |
| Template path | `modules/networking/vnet.bicep` |
| Input collection | `landingZones.vnets[]` |
| Azure CLI operation | `az deployment group what-if`, followed by `create` |

## 7. Operational notes

- The workflow uses a temporary parameter file; it is not committed back to the repository.
- The module's declared outputs are available in Azure deployment history even though the current workflow does not publish them separately.
- Resource deployment names in Azure deployment history are run-scoped labels and should not be confused with resource names.
- A successful What-If is a preview, not proof that the deployment will succeed; Azure policy, provider registration, quota, naming availability and RBAC can still affect deployment.

---

*Reference generated from the `WorkingMark1` branch implementation. If the module or workflow mapping changes, update this reference alongside the code.*
