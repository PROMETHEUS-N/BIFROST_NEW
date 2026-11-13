# 🎯 RBAC — Resource scope

Assigns an Azure role to an existing principal on an existing Azure Storage Account.

> **Scope note:** Bicep requires the target resource's resource type and API version at compile time. This implementation uses `Microsoft.Storage/storageAccounts@2023-05-01`. For another resource type, add a matching typed existing-resource declaration (or a dedicated resource-scope template) rather than passing an arbitrary resource ID as a deployment scope.

## Inputs

| Parameter | Description |
|---|---|
| `storageAccountName` | Existing Storage Account name in the deployment resource group |
| `principalId` | Existing Microsoft Entra object ID |
| `roleDefinitionGuid` | Role definition GUID |
| `principalType` | `User`, `Group`, or `ServicePrincipal` |

## Deployment

```powershell
az deployment group what-if --resource-group "<RESOURCE_GROUP>" --template-file modules/RBAC/RBAC_resource.bicep --parameters storageAccountName="<STORAGE_ACCOUNT>" principalId="<OBJECT_ID>" roleDefinitionGuid="acdd72a7-3385-48ef-bd42-f606fba81ae7" principalType="User"
az deployment group create --name "rbac-resource" --resource-group "<RESOURCE_GROUP>" --template-file modules/RBAC/RBAC_resource.bicep --parameters storageAccountName="<STORAGE_ACCOUNT>" principalId="<OBJECT_ID>" roleDefinitionGuid="acdd72a7-3385-48ef-bd42-f606fba81ae7" principalType="User"
```

The example GUID is the built-in **Reader** role.

## Prerequisites

- The Storage Account and Microsoft Entra principal must already exist.
- The deploying identity must be allowed to create role assignments at the resource scope.
- This module does not create managed groups, users, or identities.

## Outputs

- `roleAssignmentId`
- `assignedResourceId`
