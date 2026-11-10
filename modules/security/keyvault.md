# Azure Key Vault — Module Reference

![Bicep](https://img.shields.io/badge/IaC-Bicep-0078D4?logo=azuredevops&logoColor=white) ![Azure](https://img.shields.io/badge/Platform-Microsoft%20Azure-0078D4?logo=microsoftazure&logoColor=white) ![Workflow](https://img.shields.io/badge/Workflow-GitHub%20Actions-2088FF?logo=githubactions&logoColor=white)

> **Module:** `modules/security/keyvault.bicep`  
> **Workflow job:** `deploy-keyvault`  
> **Deployment scope:** Resource-group scope (`az deployment group`)

## 1. Purpose

This reusable Bicep module provisions the azure key vault resource. The workflow reads the resource definition from the root `input.json`, maps the fields to Bicep parameters, creates a temporary ARM parameter file, runs What-If, and then deploys the module.

## 2. Inputs and their sources

The workflow does not pass the whole JSON object directly. It explicitly maps the following fields:

| Bicep parameter | Source / JSON path | Value source |
|---|---|---|
| `keyVaultName` | `landingZones.keyVaults&#91;&#93;.name` | `input.json` (base name) |
| `location` | `landingZones.keyVaults&#91;&#93;.location` | `input.json` |
| `tenantId` | Retrieved at runtime using `az account show --query tenantId -o tsv` | Authenticated Azure context; not `input.json` and not a GitHub secret parameter |
| `skuName` | `landingZones.keyVaults&#91;&#93;.skuName` | `input.json` |
| `skuFamily` | `landingZones.keyVaults&#91;&#93;.skuFamily` | `input.json` |
| `enableRbacAuthorization` | `landingZones.keyVaults&#91;&#93;.enableRbacAuthorization` | `input.json` |
| `enablePurgeProtection` | `landingZones.keyVaults&#91;&#93;.enablePurgeProtection` | `input.json` |
| `softDeleteRetentionInDays` | `landingZones.keyVaults&#91;&#93;.softDeleteRetentionInDays` | `input.json` |
| `publicNetworkAccess` | `landingZones.keyVaults&#91;&#93;.publicNetworkAccess` | `input.json` |
| `tags` | `landingZones.keyVaults&#91;&#93;.tags` | `input.json` |

**Secret handling:** No resource-specific password is consumed by this module. 

## 3. Prerequisites and dependencies

- Target resource group must exist.
- Azure subscription context must be authenticated so the workflow can query the tenant ID.
- Key Vault name must meet Azure constraints (3–24 characters; letters, numbers and hyphens; starts with a letter).
- The Bicep expression appends a deterministic five-character `uniqueString` fragment; see naming section.
- Identity needs Key Vault resource write permission.

### Deployment ordering



```mermaid
flowchart TD
  A[deploy-subnet completes] --> B[deploy-keyvault job]
  C[input.json: keyVaults&#91;&#93;] --> D[Map configuration]
  E[Azure CLI account show] --> F[Resolve tenantId]
  D --> G[Build parameters]
  F --> G
  G --> H[What-If]
  H --> I[keyvault.bicep]
  I --> J[Generate final name: base + 5-char hash]
  J --> K[Create Key Vault]
  K --> L[Azure Key Vault + outputs]
```

## 4. Resource naming structure

`substring(keyVaultName, 0, min(length(keyVaultName), 15))` + first 5 characters of `uniqueString(subscription().id, resourceGroup().id, keyVaultName)`. Up to 20 characters for the current implementation; actual output is authoritative.

**Important:** The workflow deployment name (for example `pike-...` plus `github.run_id`) is an ARM deployment-history label. It is **not** the Azure resource name. The Azure resource name is determined by the naming rule above.

## 5. Outputs and where to find them

The module declares these Bicep outputs:

| Output name | Meaning |
|---|---|
| `keyVaultId` | Full Key Vault resource ID. |
| `keyVaultNameOut` | Final generated Key Vault name. |

Outputs are returned by the ARM deployment operation. The workflow currently invokes `az deployment group create` (or `az deployment sub create` for this subscription-scope module) but does not explicitly export the output object to a GitHub Actions artifact or summary. To inspect it, query the deployment record:

```bash
# Resource-group deployment (replace placeholders)
az deployment group show --resource-group <resourceGroupName> --name <deploymentName> --query properties.outputs -o json

# Subscription-scope deployment (Resource Group module)
az deployment sub show --name <deploymentName> --query properties.outputs -o json
```

`az keyvault show --name <finalKeyVaultName> -o json`; retrieve final name from deployment output using `az deployment group show -g <resourceGroupName> -n <deploymentName> --query properties.outputs.keyVaultNameOut.value -o tsv`.

### Where to see the resource in Azure Portal

Open **Azure Portal → Resource groups → <target resource group> → <resource>**. For the Resource Group module, open **Subscriptions → <subscription> → Resource groups**. The deployment record and its outputs are available under the relevant scope's **Deployments** history.

## 6. How the workflow calls this module

The `deploy-keyvault` job in `.github/workflows/deploy.yml`:

1. Runs after its declared `needs` dependency/dependencies complete.
2. Checks out the repository and authenticates with `azure/login@v2` using OIDC secrets (`AZURE_CLIENT_ID`, `AZURE_TENANT_ID`, `AZURE_SUBSCRIPTION_ID`).
3. Reads `input.json` and loops over `landingZones.<collection>[]`.
4. Maps JSON properties to Bicep parameter names and writes a temporary ARM parameter JSON file under `$env:RUNNER_TEMP`.
5. Runs Azure deployment **What-If** against `keyvault.bicep`.
6. Runs Azure deployment **create** if What-If succeeds.

**Job timing:** After `deploy-subnet`; before Storage Accounts.

| Workflow item | Current implementation |
|---|---|
| Job ID | `deploy-keyvault` |
| Display name | See the job's `name` in `.github/workflows/deploy.yml` |
| Template path | `modules/security/keyvault.bicep` |
| Input collection | `landingZones.keyVaults&#91;&#93;` |
| Azure CLI operation | `az deployment group what-if`, followed by `create` |

## 7. Operational notes

- The workflow uses a temporary parameter file; it is not committed back to the repository.
- The module's declared outputs are available in Azure deployment history even though the current workflow does not publish them separately.
- Resource deployment names in Azure deployment history are run-scoped labels and should not be confused with resource names.
- A successful What-If is a preview, not proof that the deployment will succeed; Azure policy, provider registration, quota, naming availability and RBAC can still affect deployment.

---

*Reference generated from the `WorkingMark1` branch implementation. If the module or workflow mapping changes, update this reference alongside the code.*
