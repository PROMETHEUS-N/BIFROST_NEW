
# RBAC Basics

### How to determine the scope for a resource

Azure portal to assign a role temporarily at the resource scope and then use Azure PowerShell or Azure CLI to list the role assignment. 

In the output, the scope will be listed as a property.

```Bash
{
    "canDelegate": null,
    "condition": null,
    "conditionVersion": null,
    "description": null,
    "id": "/subscriptions/{subscriptionId}/resourceGroups/Example-Storage-rg/providers/Microsoft.Storage/storageAccounts/azurestorage12345/blobServices/default/containers/blob-container-01/providers/Microsoft.Authorization/roleAssignments/{roleAssignmentId}",
    "name": "{roleAssignmentId}",
    "principalId": "{principalId}",
    "principalName": "user@contoso.com",
    "principalType": "User",
    "resourceGroup": "test-rg",
    "roleDefinitionId": "/subscriptions/{subscriptionId}/providers/Microsoft.Authorization/roleDefinitions/2a2b9908-6ea1-4ae2-8e65-a410df84e7d1",
    "roleDefinitionName": "Storage Blob Data Reader",
    "scope": "/subscriptions/{subscriptionId}/resourceGroups/Example-Storage-rg/providers/Microsoft.Storage/storageAccounts/azurestorage12345/blobServices/default/containers/blob-container-01",
    "type": "Microsoft.Authorization/roleAssignments"
  }
```

### BICEP MODULE

```bicep
param location string = resourceGroup().location
param storageAccountName string = 'stor${uniqueString(resourceGroup().id)}'
param storageSkuName string = 'Standard_LRS'
param roleDefinitionResourceId string
param principalId string

resource storageAccount 'Microsoft.Storage/storageAccounts@2025-06-01' = {
  name: storageAccountName
  location: location
  kind: 'StorageV2'
  sku: {
   name: storageSkuName
  }
}

resource roleAssignment 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
  scope: storageAccount
  name: getRoleAssignmentName({
    scope: storageAccount.id
    principalId: principalId
    roleDefinitionId: roleDefinitionResourceId
  })
  properties: {
    roleDefinitionId: roleDefinitionResourceId
    principalId: principalId
    principalType: 'ServicePrincipal'
  }
}
```
> If you don't explicitly specify the scope, Bicep uses the file's targetScope. In the following example, no scope property is specified, so the role assignment is scoped to the subscription:

```bicep
param roleDefinitionResourceId string
param principalId string

targetScope = 'subscription'

resource roleAssignment 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
  name: getRoleAssignmentName({
    scope: subscription().id
    principalId: principalId
    roleDefinitionId: roleDefinitionResourceId
  })
  properties: {
    roleDefinitionId: roleDefinitionResourceId
    principalId: principalId
    principalType: 'ServicePrincipal'
  }
}
```

#### Tip
> Use the smallest scope that you need to meet your requirements.

> For example, if you need to grant a managed identity access to a single storage account, it's good security practice to create the role assignment at the scope of the storage account and not at the resource group or subscription scope.

---

### Name
> A role assignment's resource name must be a **globally unique identifier** (**GUID**).

> Role assignment resource names must be unique within the Microsoft Entra tenant, even if the scope is narrower.
> For your Bicep deployment to be repeatable, it's important for the name to be deterministic; that is, use the same name every time you deploy. For new role assignments, use the getRoleAssignmentName() function to create a deterministic GUID from the scope, principal ID, and fully qualified role definition ID:

```bicep
name: getRoleAssignmentName({
  scope: subscription().id
  principalId: principalId
  roleDefinitionId: roleDefinitionResourceId
})
```
---

### Role Definition ID

The role you assign can be a built-in role definition or a custom role definition. To use a built-in role definition, find the appropriate role definition ID. For example, the Contributor role has a role definition ID of b24988ac-6180-42a0-ab88-20f7382dd24c.

When you create the role assignment resource, you need to specify a fully qualified resource ID. Built-in role definition IDs are subscription-scoped resources. It's recommended to use an existing resource to refer to the built-in role and to use the .id property to access its fully qualified resource ID:

```bicep
param principalId string

@description('This is the built-in Contributor role. See https://learn.microsoft.com/azure/role-based-access-control/built-in-roles#contributor')
resource contributorRoleDefinition 'Microsoft.Authorization/roleDefinitions@2022-04-01' existing = {
  scope: subscription()
  name: 'b24988ac-6180-42a0-ab88-20f7382dd24c'
}

resource roleAssignment 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
  name: getRoleAssignmentName({
    scope: resourceGroup().id
    principalId: principalId
    roleDefinitionId: contributorRoleDefinition.id
  })
  properties: {
    roleDefinitionId: contributorRoleDefinition.id
    principalId: principalId
    principalType: 'ServicePrincipal'
  }
}
```

---

### Principal

The principalId property must be set to a GUID that represents the Microsoft Entra identifier for the principal. In Microsoft Entra ID, this is sometimes referred to as the object ID.

The principalType property specifies whether the principal is a user, a group, or a service principal. Managed identities are a form of service principal.

#### Tip

> It's important to set the principalType property when you create a role assignment in Bicep. Otherwise, you might get intermittent deployment errors, especially when you work with service principals and managed identities.

> ***The following example shows how to create a user-assigned managed identity and a role assignment:***
>> This example retains guid() with the identity's resource ID because the identity's principal ID isn't available at the start of the deployment, when the role assignment name must be calculated. To use getRoleAssignmentName() instead, create the role assignment in a module and pass managedIdentity.properties.principalId as a module parameter.

```bicep
param location string = resourceGroup().location
param roleDefinitionResourceId string

var managedIdentityName = 'MyManagedIdentity'

resource managedIdentity 'Microsoft.ManagedIdentity/userAssignedIdentities@2025-01-31-preview' = {
  name: managedIdentityName
  location: location
}

resource roleAssignment 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
  name: guid(resourceGroup().id, managedIdentity.id, roleDefinitionResourceId)
  properties: {
    roleDefinitionId: roleDefinitionResourceId
    principalId: managedIdentity.properties.principalId
    principalType: 'ServicePrincipal'
  }
}
```

---

### Custom role definitions

Custom role definitions enable you to define a set of permissions that can then be assigned to a principal by using a role assignment. For more information on role definitions, see Understand Azure role definitions.

To create a custom role definition, define a resource of type Microsoft.Authorization/roleDefinitions. See the Create a new role def via a subscription-level deployment quickstart for an example.

Role definition resource names must be unique within the Microsoft Entra tenant, even if the assignable scopes are more narrow.

> Note
>> Some services manage their own role definitions and assignments. For example, Azure Cosmos DB maintains its own Microsoft.DocumentDB/databaseAccounts/sqlRoleAssignments and Microsoft.DocumentDB/databaseAccounts/sqlRoleDefinitions resources. For more information, see the specific service's documentation.

---
