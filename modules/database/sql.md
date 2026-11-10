# Azure SQL Server and Database — Module Reference

![Bicep](https://img.shields.io/badge/IaC-Bicep-0078D4?logo=azuredevops&logoColor=white) ![Azure](https://img.shields.io/badge/Platform-Microsoft%20Azure-0078D4?logo=microsoftazure&logoColor=white) ![Workflow](https://img.shields.io/badge/Workflow-GitHub%20Actions-2088FF?logo=githubactions&logoColor=white)

> **Module:** `modules/database/sql.bicep`  
> **Workflow job:** `deploy-sql`  
> **Deployment scope:** Resource-group scope (`az deployment group`)

## 1. Purpose

This reusable Bicep module provisions the azure sql server and database resource (logical server and database). The workflow reads the resource definition from the root `input.json`, maps the fields to Bicep parameters, creates a temporary ARM parameter file, runs What-If, and then deploys the module.

## 2. Inputs and their sources

The workflow does not pass the whole JSON object directly. It explicitly maps the following fields:

| Bicep parameter | Source / JSON path | Value source |
|---|---|---|
| `location` | `landingZones.sqlDatabases[].location` | `input.json` |
| `serverName` | `landingZones.sqlDatabases[].serverName` | `input.json` |
| `databaseName` | `landingZones.sqlDatabases[].databaseName` | `input.json` |
| `administratorLogin` | `landingZones.sqlDatabases[].administratorLogin` | `input.json` |
| `administratorLoginPassword` | `secrets.SQL_ADMIN_PASSWORD` mapped to `SQL_ADMIN_PASSWORD`, then passed as secure Bicep parameter | GitHub Actions secret; never stored in `input.json` |
| `sqlServerVersion` | `landingZones.sqlDatabases[].sqlServerVersion` | `input.json` |
| `databaseSkuName` | `landingZones.sqlDatabases[].databaseSkuName` | `input.json` |
| `databaseSkuTier` | `landingZones.sqlDatabases[].databaseSkuTier` | `input.json` |
| `databaseCapacity` | `landingZones.sqlDatabases[].databaseCapacity` | `input.json` |
| `databaseMaxSizeBytes` | `landingZones.sqlDatabases[].databaseMaxSizeBytes` | `input.json` |
| `publicNetworkAccess` | `landingZones.sqlDatabases[].publicNetworkAccess` | `input.json` |
| `minimumTlsVersion` | `landingZones.sqlDatabases[].minimumTlsVersion` | `input.json` |
| `tags` | `landingZones.sqlDatabases[].tags` | `input.json` |

**Secret handling:** The SQL administrator password comes only from GitHub Actions secret `SQL_ADMIN_PASSWORD`. The secret is exposed to the job step as an environment variable and passed as a secure Bicep parameter; it must not be placed in `input.json`.

## 3. Prerequisites and dependencies

- Target resource group must exist.
- SQL logical server name must be globally unique and comply with Azure SQL naming rules.
- Administrator login is plain configuration; password must be configured as GitHub secret `SQL_ADMIN_PASSWORD`.
- The server is created first; database is a child resource and depends on the server (`parent: sqlServer`).
- Identity needs SQL server and database write permissions.

### Deployment ordering



```mermaid
flowchart TD
  A[deploy-storage completes] --> B[deploy-sql job]
  C[input.json: sqlDatabases[]] --> D[Map server/database configuration]
  E[GitHub secret: SQL_ADMIN_PASSWORD] --> F[Secure parameter injection]
  D --> G[What-If + sql.bicep]
  F --> G
  G --> H[Create SQL logical server]
  H --> I[Create child database]
  I --> J[Azure SQL resources + deployment outputs]
```

## 4. Resource naming structure

Both names are used exactly as supplied: `serverName` for logical server and `databaseName` for its database. No Bicep suffix is added.

**Important:** The workflow deployment name (for example `pike-...` plus `github.run_id`) is an ARM deployment-history label. It is **not** the Azure resource name. The Azure resource name is determined by the naming rule above.

## 5. Outputs and where to find them

The module declares these Bicep outputs:

| Output name | Meaning |
|---|---|
| `sqlServerId` | Full SQL logical server resource ID. |
| `sqlServerNameOut` | Logical server name. |
| `sqlDatabaseId` | Full database resource ID. |
| `sqlDatabaseNameOut` | Database name. |

Outputs are returned by the ARM deployment operation. The workflow currently invokes `az deployment group create` (or `az deployment sub create` for this subscription-scope module) but does not explicitly export the output object to a GitHub Actions artifact or summary. To inspect it, query the deployment record:

```bash
# Resource-group deployment (replace placeholders)
az deployment group show --resource-group <resourceGroupName> --name <deploymentName> --query properties.outputs -o json

# Subscription-scope deployment (Resource Group module)
az deployment sub show --name <deploymentName> --query properties.outputs -o json
```

`az sql server show -g <resourceGroupName> -n <serverName> -o json`; `az sql db show -g <resourceGroupName> -s <serverName> -n <databaseName> -o json`; deployment outputs via `az deployment group show ... --query properties.outputs -o json`.

### Where to see the resource in Azure Portal

Open **Azure Portal → Resource groups → <target resource group> → <resource>**. For the Resource Group module, open **Subscriptions → <subscription> → Resource groups**. The deployment record and its outputs are available under the relevant scope's **Deployments** history.

## 6. How the workflow calls this module

The `deploy-sql` job in `.github/workflows/deploy.yml`:

1. Runs after its declared `needs` dependency/dependencies complete.
2. Checks out the repository and authenticates with `azure/login@v2` using OIDC secrets (`AZURE_CLIENT_ID`, `AZURE_TENANT_ID`, `AZURE_SUBSCRIPTION_ID`).
3. Reads `input.json` and loops over `landingZones.<collection>[]`.
4. Maps JSON properties to Bicep parameter names and writes a temporary ARM parameter JSON file under `$env:RUNNER_TEMP`.
5. Runs Azure deployment **What-If** against `sql.bicep`.
6. Runs Azure deployment **create** if What-If succeeds.

**Job timing:** After `deploy-storage`; before Azure OpenAI.

| Workflow item | Current implementation |
|---|---|
| Job ID | `deploy-sql` |
| Display name | See the job's `name` in `.github/workflows/deploy.yml` |
| Template path | `modules/database/sql.bicep` |
| Input collection | `landingZones.sqlDatabases[]` |
| Azure CLI operation | `az deployment group what-if`, followed by `create` |

## 7. Operational notes

- The workflow uses a temporary parameter file; it is not committed back to the repository.
- The module's declared outputs are available in Azure deployment history even though the current workflow does not publish them separately.
- Resource deployment names in Azure deployment history are run-scoped labels and should not be confused with resource names.
- A successful What-If is a preview, not proof that the deployment will succeed; Azure policy, provider registration, quota, naming availability and RBAC can still affect deployment.

---

*Reference generated from the `WorkingMark1` branch implementation. If the module or workflow mapping changes, update this reference alongside the code.*
