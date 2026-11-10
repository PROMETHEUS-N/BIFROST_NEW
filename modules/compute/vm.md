# Windows Virtual Machine — Module Reference

![Bicep](https://img.shields.io/badge/IaC-Bicep-0078D4?logo=azuredevops&logoColor=white) ![Azure](https://img.shields.io/badge/Platform-Microsoft%20Azure-0078D4?logo=microsoftazure&logoColor=white) ![Workflow](https://img.shields.io/badge/Workflow-GitHub%20Actions-2088FF?logo=githubactions&logoColor=white)

> **Module:** `modules/compute/vm.bicep`  
> **Workflow job:** `deploy-vm`  
> **Deployment scope:** Resource-group scope (`az deployment group`)

## 1. Purpose

This reusable Bicep module provisions the windows virtual machine resource and its supporting network interface. The workflow reads the resource definition from the root `input.json`, maps the fields to Bicep parameters, creates a temporary ARM parameter file, runs What-If, and then deploys the module.

## 2. Inputs and their sources

The workflow does not pass the whole JSON object directly. It explicitly maps the following fields:

| Bicep parameter | Source / JSON path | Value source |
|---|---|---|
| `location` | `landingZones.vms[].location` | `input.json` |
| `computerName` | `landingZones.vms[].computerName` | `input.json` |
| `vmName` | `landingZones.vms[].name` | `input.json` |
| `adminUsername` | `landingZones.vms[].adminUsername` | `input.json` |
| `vmAdminPassword` | `secrets.VM_ADMIN_PASSWORD` mapped to `VM_ADMIN_PASSWORD`, then passed as secure Bicep parameter | GitHub Actions secret; never stored in `input.json` |
| `vmSize` | `landingZones.vms[].vmSize` | `input.json` |
| `tags` | `landingZones.vms[].tags` | `input.json` |
| `vnetName` | `landingZones.vms[].vnetName` | `input.json` |
| `subnetName` | `landingZones.vms[].subnetName` | `input.json` |
| `nicName` | `landingZones.vms[].nicName` | `input.json` |
| `privateIpAllocationMethod` | `landingZones.vms[].privateIpAllocationMethod` | `input.json` |
| `imagePublisher / imageOffer / imageSku / imageVersion` | Corresponding fields in `landingZones.vms[]` | `input.json` |
| `osDiskStorageAccountType / osDiskCreateOption / osDiskSizeGB` | Corresponding fields in `landingZones.vms[]` | `input.json` |
| `enableBootDiagnostics` | `landingZones.vms[].enableBootDiagnostics` | `input.json` |

**Secret handling:** The VM administrator password comes only from GitHub Actions secret `VM_ADMIN_PASSWORD`. The secret is exposed to the job step as an environment variable and passed as a secure Bicep parameter; it must not be placed in `input.json`.

## 3. Prerequisites and dependencies

- Target resource group, VNet and subnet must already exist; VNet/subnet are declared `existing` in Bicep.
- NIC name, VNet and subnet names must resolve in the same deployment resource group.
- VM size must be available in the selected region and image reference must be valid.
- `VM_ADMIN_PASSWORD` must exist as a GitHub Actions secret; it is passed as a secure Bicep parameter and must satisfy Azure Windows password complexity.
- Identity needs permissions to create NICs and VMs and attach the NIC to the subnet.

### Deployment ordering



```mermaid
flowchart TD
  A[deploy-openai completes] --> B[deploy-vm job]
  C[input.json: vms[]] --> D[Map VM, image, disk and network settings]
  E[Existing VNet + subnet] --> F[Resolve network resource IDs]
  G[GitHub secret: VM_ADMIN_PASSWORD] --> H[Secure parameter injection]
  D --> I[What-If + vm.bicep]
  F --> I
  H --> I
  I --> J[Create NIC]
  J --> K[Create Windows VM attached to NIC]
  K --> L[Azure VM + deployment outputs]
```

## 4. Resource naming structure

VM name, computer name and NIC name are all taken exactly from `input.json` (`name`, `computerName`, `nicName`). No generated suffix is applied. The NIC IP configuration is named `${nicName}-ipconfig`.

**Important:** The workflow deployment name (for example `pike-...` plus `github.run_id`) is an ARM deployment-history label. It is **not** the Azure resource name. The Azure resource name is determined by the naming rule above.

## 5. Outputs and where to find them

The module declares these Bicep outputs:

| Output name | Meaning |
|---|---|
| `vmId` | Full VM resource ID. |
| `vmNameOut` | Actual VM name. |
| `networkInterfaceId` | Full NIC resource ID. |

Outputs are returned by the ARM deployment operation. The workflow currently invokes `az deployment group create` (or `az deployment sub create` for this subscription-scope module) but does not explicitly export the output object to a GitHub Actions artifact or summary. To inspect it, query the deployment record:

```bash
# Resource-group deployment (replace placeholders)
az deployment group show --resource-group <resourceGroupName> --name <deploymentName> --query properties.outputs -o json

# Subscription-scope deployment (Resource Group module)
az deployment sub show --name <deploymentName> --query properties.outputs -o json
```

`az vm show -g <resourceGroupName> -n <vmName> -o json`; `az network nic show -g <resourceGroupName> -n <nicName> -o json`; deployment outputs via `az deployment group show ... --query properties.outputs -o json`.

### Where to see the resource in Azure Portal

Open **Azure Portal → Resource groups → <target resource group> → <resource>**. For the Resource Group module, open **Subscriptions → <subscription> → Resource groups**. The deployment record and its outputs are available under the relevant scope's **Deployments** history.

## 6. How the workflow calls this module

The `deploy-vm` job in `.github/workflows/deploy.yml`:

1. Runs after its declared `needs` dependency/dependencies complete.
2. Checks out the repository and authenticates with `azure/login@v2` using OIDC secrets (`AZURE_CLIENT_ID`, `AZURE_TENANT_ID`, `AZURE_SUBSCRIPTION_ID`).
3. Reads `input.json` and loops over `landingZones.<collection>[]`.
4. Maps JSON properties to Bicep parameter names and writes a temporary ARM parameter JSON file under `$env:RUNNER_TEMP`.
5. Runs Azure deployment **What-If** against `vm.bicep`.
6. Runs Azure deployment **create** if What-If succeeds.

**Job timing:** Last resource deployment stage, after `deploy-openai`. Requires the VNet and subnet created earlier.

| Workflow item | Current implementation |
|---|---|
| Job ID | `deploy-vm` |
| Display name | See the job's `name` in `.github/workflows/deploy.yml` |
| Template path | `modules/compute/vm.bicep` |
| Input collection | `landingZones.vms[]` |
| Azure CLI operation | `az deployment group what-if`, followed by `create` |

## 7. Operational notes

- The workflow uses a temporary parameter file; it is not committed back to the repository.
- The module's declared outputs are available in Azure deployment history even though the current workflow does not publish them separately.
- Resource deployment names in Azure deployment history are run-scoped labels and should not be confused with resource names.
- A successful What-If is a preview, not proof that the deployment will succeed; Azure policy, provider registration, quota, naming availability and RBAC can still affect deployment.

---

*Reference generated from the `WorkingMark1` branch implementation. If the module or workflow mapping changes, update this reference alongside the code.*
