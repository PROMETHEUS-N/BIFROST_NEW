# Route Table — Module Reference

![Bicep](https://img.shields.io/badge/IaC-Bicep-0078D4?logo=azuredevops&logoColor=white) ![Azure](https://img.shields.io/badge/Platform-Microsoft%20Azure-0078D4?logo=microsoftazure&logoColor=white) ![Workflow](https://img.shields.io/badge/Workflow-GitHub%20Actions-2088FF?logo=githubactions&logoColor=white)

> **Module:** `modules/networking/routetable.bicep`  
> **Workflow job:** `deploy-route-table`  
> **Deployment scope:** Resource-group scope (`az deployment group`)

## 1. Purpose

This reusable Bicep module provisions the route table resource. The workflow reads the resource definition from the root `input.json`, maps the fields to Bicep parameters, creates a temporary ARM parameter file, runs What-If, and then deploys the module.

## 2. Inputs and their sources

The workflow does not pass the whole JSON object directly. It explicitly maps the following fields:

| Bicep parameter | Source / JSON path | Value source |
|---|---|---|
| `routeTableName` | `landingZones.routeTables&#91;&#93;.name` | `input.json` |
| `location` | `landingZones.routeTables&#91;&#93;.location` | `input.json` |
| `disableBgpRoutePropagation` | `landingZones.routeTables&#91;&#93;.disableBgpRoutePropagation` | `input.json` |
| `routes` | `landingZones.routeTables&#91;&#93;.routes` | `input.json` |
| `tags` | `landingZones.routeTables&#91;&#93;.tags` | `input.json` |

**Secret handling:** No resource-specific password is consumed by this module. 

## 3. Prerequisites and dependencies

- Target resource group must exist.
- Region and route table configuration must be supplied in `input.json`.
- Each route object must include `name`, `addressPrefix` and `nextHopType`; `nextHopIpAddress` is optional.
- Identity needs `Microsoft.Network/routeTables/write` permission at the target scope.

### Deployment ordering



```mermaid
flowchart TD
 A["deploy-nsg completes"] --> B["deploy-route-table job"]
 C["input.json: routeTables array"] --> D["Map route table properties"]
 D --> E["Temporary ARM parameters"]
 E --> F["What-If"]
 F --> G["routetable.bicep"]
 G --> H["Create route table"]
 H --> I["Azure Route Tables and deployment outputs"]
```

## 4. Resource naming structure

Exact `name` from input (example `rt-pikehex-dev-001`); no generated suffix.

**Important:** The workflow deployment name (for example `pike-...` plus `github.run_id`) is an ARM deployment-history label. It is **not** the Azure resource name. The Azure resource name is determined by the naming rule above.

## 5. Outputs and where to find them

The module declares these Bicep outputs:

| Output name | Meaning |
|---|---|
| `routeTableId` | Full Azure resource ID. |
| `routeTableNameOut` | Actual route table name. |

Outputs are returned by the ARM deployment operation. The workflow currently invokes `az deployment group create` (or `az deployment sub create` for this subscription-scope module) but does not explicitly export the output object to a GitHub Actions artifact or summary. To inspect it, query the deployment record:

```bash
# Resource-group deployment (replace placeholders)
az deployment group show --resource-group <resourceGroupName> --name <deploymentName> --query properties.outputs -o json

# Subscription-scope deployment (Resource Group module)
az deployment sub show --name <deploymentName> --query properties.outputs -o json
```

`az network route-table show -g <resourceGroupName> -n <routeTableName> -o json`; outputs via `az deployment group show ... --query properties.outputs -o json`.

### Where to see the resource in Azure Portal

Open **Azure Portal → Resource groups → <target resource group> → <resource>**. For the Resource Group module, open **Subscriptions → <subscription> → Resource groups**. The deployment record and its outputs are available under the relevant scope's **Deployments** history.

## 6. How the workflow calls this module

The `deploy-route-table` job in `.github/workflows/deploy.yml`:

1. Runs after its declared `needs` dependency/dependencies complete.
2. Checks out the repository and authenticates with `azure/login@v2` using OIDC secrets (`AZURE_CLIENT_ID`, `AZURE_TENANT_ID`, `AZURE_SUBSCRIPTION_ID`).
3. Reads `input.json` and loops over `landingZones.<collection>[]`.
4. Maps JSON properties to Bicep parameter names and writes a temporary ARM parameter JSON file under `$env:RUNNER_TEMP`.
5. Runs Azure deployment **What-If** against `routetable.bicep`.
6. Runs Azure deployment **create** if What-If succeeds.

**Job timing:** After `deploy-nsg`; before VNet and subnet deployment.

| Workflow item | Current implementation |
|---|---|
| Job ID | `deploy-route-table` |
| Display name | See the job's `name` in `.github/workflows/deploy.yml` |
| Template path | `modules/networking/routetable.bicep` |
| Input collection | `landingZones.routeTables&#91;&#93;` |
| Azure CLI operation | `az deployment group what-if`, followed by `create` |

## 7. Operational notes

- The workflow uses a temporary parameter file; it is not committed back to the repository.
- The module's declared outputs are available in Azure deployment history even though the current workflow does not publish them separately.
- Resource deployment names in Azure deployment history are run-scoped labels and should not be confused with resource names.
- A successful What-If is a preview, not proof that the deployment will succeed; Azure policy, provider registration, quota, naming availability and RBAC can still affect deployment.

---

*Reference generated from the `WorkingMark1` branch implementation. If the module or workflow mapping changes, update this reference alongside the code.*
