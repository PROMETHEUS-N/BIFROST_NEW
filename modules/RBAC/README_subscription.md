# 🔐 RBAC — Subscription scope

Assigns an Azure role to an existing Microsoft Entra principal at the subscription scope.

## Inputs

| Parameter | Description |
|---|---|
| `principalId` | Existing user, group, or service principal object ID |
| `roleDefinitionGuid` | Role definition GUID |
| `principalType` | `User`, `Group`, or `ServicePrincipal` |
| `assignmentSeed` | Optional seed for a distinct assignment |

## Deployment

Run from an authenticated Azure CLI session with `Microsoft.Authorization/roleAssignments/write` permission:

```powershell
az deployment sub what-if --location EastUS --template-file modules/RBAC/RBAC_subscription.bicep --parameters principalId="<OBJECT_ID>" roleDefinitionGuid="acdd72a7-3385-48ef-bd42-f606fba81ae7" principalType="User"
az deployment sub create --name "rbac-subscription" --location EastUS --template-file modules/RBAC/RBAC_subscription.bicep --parameters principalId="<OBJECT_ID>" roleDefinitionGuid="acdd72a7-3385-48ef-bd42-f606fba81ae7" principalType="User"
```

The example GUID is the built-in **Reader** role. Use a different role GUID only when approved.

## Prerequisites

- The principal must already exist in Microsoft Entra ID.
- The deploying identity must be authorized to create role assignments at subscription scope (typically User Access Administrator or Owner, subject to Azure's role-assignment conditions).
- This module does not create users, groups, or managed identities. Create/provision the principal separately, then supply its object ID.

## Outputs

- `roleAssignmentId`
