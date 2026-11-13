# Azure built-in roles

Azure role-based access control (Azure RBAC) has several Azure built-in roles that you can assign to users, groups, service principals, and managed identities. Role assignments are the way you control access to Azure resources. If the built-in roles don't meet the specific needs of your organization, you can create your own Azure custom roles. For information about how to assign roles, see Steps to assign an Azure role.

This article lists the Azure built-in roles. If you are looking for administrator roles for Microsoft Entra ID, see Microsoft Entra built-in roles.

The following table provides a brief description of each built-in role. Click the role name to see the list of Actions, NotActions, DataActions, and NotDataActions for each role. For information about what these actions mean and how they apply to the control and data planes, see Understand Azure role definitions.

## Privileged

| SNo | Built-in Role | Description | ID |
|---|---|---|---|
| 1 | Contributor | Grants full access to manage all resources, but does not allow you to assign roles in Azure RBAC, manage assignments in Azure Blueprints, or share image galleries. | b24988ac-6180-42a0-ab88-20f7382dd24c |
| 2 | Owner | Grants full access to manage all resources, including the ability to assign roles in Azure RBAC. | 8e3af657-a8ff-443c-a75c-2fe8c4bcb635 |
| 3 | Reservations Administrator | Lets one read and manage all the reservations in a tenant | a8889054-8d42-49c9-bc1c-52486c10e7cd |
| 4 | Role Based Access Control Administrator | Manage access to Azure resources by assigning roles using Azure RBAC. This role does not allow you to manage access using other ways, such as Azure Policy. | f58310d9-a9f6-439a-9e8d-f62e7b41a168 |
| 5 | User Access Administrator | Lets you manage user access to Azure resources. | 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9 |

---

## General

| SNo | Built-in | role | Description ID |
|-----|----------|------|----------------|
| 1 | Reader | View all resources, but does not allow you to make any changes. | acdd72a7-3385-48ef-bd42-f606fba81ae7 |

---

## Compute

| SNo | Built-in Role | Description | ID |
|---|---|---|---|
| 1 | Azure Arc VMware VM Contributor | Arc VMware VM Contributor has permissions to perform all VM actions. | b748a06d-6150-4f8a-aaa9-ce3940cd96cb |
| 2 | Azure Batch Account Contributor | Grants full access to manage all Batch resources, including Batch accounts, pools and jobs. | 29fe4964-1e60-436b-bd3a-77fd4c178b3c |
| 3 | Azure Batch Account Reader | Lets you view all resources including pools and jobs in the Batch account. | 11076f67-66f6-4be0-8f6b-f0609fd05cc9 |
| 4 | Azure Batch Data Contributor | Grants permissions to manage Batch pools and jobs but not to modify accounts. | 6aaa78f1-f7de-44ca-8722-c64a23943cae |
| 5 | Azure Batch Job Submitter | Lets you submit and manage jobs in the Batch account. | 48e5e92e-a480-4e71-aa9c-2778f4c13781 |
| 6 | Classic Virtual Machine Contributor | Lets you manage classic virtual machines, but not access to them, and not the virtual network or storage account they're connected to. | d73bb868-a0df-4d4d-bd69-98a00b01fccb |
| 7 | Compute Fleet Contributor | Allows users to manage Compute Fleet resources. | 2bed379c-9fba-455b-99e4-6b911073bcf2 |
| 8 | Compute Gallery Artifacts Publisher | This is the role for publishing gallery artifacts. | 85a2d0d9-2eba-4c9c-b355-11c2cc0788ab |
| 9 | Compute Gallery Image Reader | This is the role for reading gallery images. | cf7c76d2-98a3-4358-a134-615aa78bf44d |
| 10 | Compute Gallery Sharing Admin | This role allows user to share gallery to another subscription/tenant or share it to the public. | 1ef6a3be-d0ac-425d-8c01-acb62866290b |
| 11 | Compute Limit Operator | Read and manage compute limits using compute limit operations. | 980cf6f7-edec-4fd1-8e9e-28f70b1d5258 |
| 12 | Data Operator for Managed Disks | Provides permissions to upload data to empty managed disks, read, or export data of managed disks (not attached to running VMs) and snapshots using SAS URIs and Azure AD authentication. | 959f8984-c045-4866-89c7-12bf9737be2e |
| 13 | Desktop Virtualization Application Group Contributor | Contributor of the Desktop Virtualization Application Group. | 86240b0e-9422-4c43-887b-b61143f32ba8 |
| 14 | Desktop Virtualization Application Group Reader | Reader of the Desktop Virtualization Application Group. | aebf23d0-b568-4e86-b8f9-fe83a2c6ab55 |
| 15 | Desktop Virtualization Contributor | Contributor of Desktop Virtualization. | 082f0a83-3be5-4ba1-904c-961cca79b387 |
| 16 | Desktop Virtualization Host Pool Contributor | Contributor of the Desktop Virtualization Host Pool. | e307426c-f9b6-4e81-87de-d99efb3c32bc |
| 17 | Desktop Virtualization Host Pool Reader | Reader of the Desktop Virtualization Host Pool. | ceadfde2-b300-400a-ab7b-6143895aa822 |
| 18 | Desktop Virtualization Power On Contributor | Provide permission to the Azure Virtual Desktop Resource Provider to start virtual machines. | 489581de-a3bd-480d-9518-53dea7416b33 |
| 19 | Desktop Virtualization Power On Off Contributor | Provide permission to the Azure Virtual Desktop Resource Provider to start and stop virtual machines. | 40c5ff49-9181-41f8-ae61-143b0e78555e |
| 20 | Desktop Virtualization Reader | Reader of Desktop Virtualization. | 49a72310-ab8d-41df-bbb0-79b649203868 |
| 21 | Desktop Virtualization Session Host Operator | Operator of the Desktop Virtualization Session Host. | 2ad6aaab-ead9-4eaa-8ac5-da422f562408 |
| 22 | Desktop Virtualization User | Allows user to use the applications in an application group. | 1d18fff3-a72a-46b5-b4a9-0b38a3cd7e63 |
| 23 | Desktop Virtualization User Session Operator | Operator of the Desktop Virtualization User Session. | ea4bfff8-7fb4-485a-aadd-d4129a0ffaa6 |
| 24 | Desktop Virtualization Virtual Machine Contributor | This role is in preview and subject to change. Provide permission to the Azure Virtual Desktop Resource Provider to create, delete, update, start, and stop virtual machines. | a959dbd1-f747-45e3-8ba6-dd80f235f97c |
| 25 | Desktop Virtualization Workspace Contributor | Contributor of the Desktop Virtualization Workspace. | 21efdde3-836f-432b-bf3d-3e8e734d4b2b |
| 26 | Desktop Virtualization Workspace Reader | Reader of the Desktop Virtualization Workspace. | 0fa44ee9-7a7d-466b-9bb2-2bf446b1204d |
| 27 | Disk Backup Reader | Provides permission to backup vault to perform disk backup. | 3e5e47e6-65f7-47ef-90b5-e5dd4d455f24 |
| 28 | Disk Pool Operator | Provide permission to StoragePool Resource Provider to manage disks added to a disk pool. | 60fc6e62-5479-42d4-8bf4-67625fcc2840 |
| 29 | Disk Restore Operator | Provides permission to backup vault to perform disk restore. | b50d9833-a0cb-478e-945f-707fcc997c13 |
| 30 | Disk Snapshot Contributor | Provides permission to backup vault to manage disk snapshots. | 7efff54f-a5b4-42b5-a1c5-5411624893ce |
| 31 | Quantum Workspace Data Contributor | Create, read, and modify jobs and other Workspace data. This role is in preview and subject to change. | c1410b24-3e69-4857-8f86-4d0a2e603250 |
| 32 | Virtual Machine Administrator Login | View Virtual Machines in the portal and login as administrator | 1c0163c0-47e6-4577-8991-ea5c82e286e4 |
| 33 | Virtual Machine Contributor | Create and manage virtual machines, manage disks, install and run software, reset password of the root user of the virtual machine using VM extensions, and manage local user accounts using VM extensions. This role does not grant you management access to the virtual network or storage account the virtual machines are connected to. This role does not allow you to assign roles in Azure RBAC. | 9980e02c-c2be-4d73-94e8-173b1dc7cf3c |
| 34 | Virtual Machine Data Access Administrator (preview) | Manage access to Virtual Machines by adding or removing role assignments for the Virtual Machine Administrator Login and Virtual Machine User Login roles. Includes an ABAC condition to constrain role assignments. | 66f75aeb-eabe-4b70-9f1e-c350c4c9ad04 |
| 35 | Virtual Machine Local User Login | View Virtual Machines in the portal and login as a local user configured on the Arc server. | 602da2ba-a5c2-41da-b01d-5360126ab525 |
| 36 | Virtual Machine User Login | View Virtual Machines in the portal and login as a regular user. | fb879df8-f326-4884-b1cf-06f3ad86be52 |
| 37 | VM Restore Operator | Create and Delete resources during VM Restore. This role is in preview and subject to change. | dfce8971-25e3-42e3-ba33-6055438e3080 |
| 38 | Windows 365 Network Interface Contributor | This role is used by Windows 365 to provision required network resources and join Microsoft-hosted VMs to network interfaces. | 1f135831-5bbe-4924-9016-264044c00788 |
| 39 | Windows 365 Network User | This role is used by Windows 365 to read virtual networks and join the designated virtual networks. | 7eabc9a4-85f7-4f71-b8ab-75daaccc1033 |
| 40 | Windows Admin Center Administrator Login | Let's you manage the OS of your resource via Windows Admin Center as an administrator. | a6333a3e-0164-44c3-b281-7a577aff287f |

---
## Networking

| SNo | Built-in Role | Description | ID |
|---|---|---|---|
| 1 | Azure Front Door Domain Contributor | For internal use within Azure. Can manage Azure Front Door domains, but can't grant access to other users. | 0ab34830-df19-4f8c-b84e-aa85b8afa6e8 |
| 2 | Azure Front Door Domain Reader | For internal use within Azure. Can view Azure Front Door domains, but can't make changes. | 0f99d363-226e-4dca-9920-b807cf8e1a5f |
| 3 | Azure Front Door Profile Reader | Can view AFD standard and premium profiles and their endpoints, but can't make changes. | 662802e2-50f6-46b0-aed2-e834bacc6d12 |
| 4 | Azure Front Door Secret Contributor | For internal use within Azure. Can manage Azure Front Door secrets, but can't grant access to other users. | 3f2eb865-5811-4578-b90a-6fc6fa0df8e5 |
| 5 | Azure Front Door Secret Reader | For internal use within Azure. Can view Azure Front Door secrets, but can't make changes. | 0db238c4-885e-4c4f-a933-aa2cef684fca |
| 6 | CDN Endpoint Contributor | Can manage CDN endpoints, but can't grant access to other users. | 426e0c7f-0c7e-4658-b36f-ff54d6c29b45 |
| 7 | CDN Endpoint Reader | Can view CDN endpoints, but can't make changes. | 871e35f6-b5c1-49cc-a043-bde969a0f2cd |
| 8 | CDN Profile Contributor | Can manage CDN and Azure Front Door standard and premium profiles and their endpoints, but can't grant access to other users. | ec156ff8-a8d1-4d15-830c-5b80698ca432 |
| 9 | CDN Profile Reader | Can view CDN profiles and their endpoints, but can't make changes. | 8f96442b-4075-438f-813d-ad51ab4019af |
| 10 | Classsic Network Contributor | Lets you manage classic networks, but not access to them. | b34d265f-36f7-4a0d-a4d4-e158ca92e90f |
| 11 | DNS Zone Contributor | Lets you manage DNS zones and record sets in Azure DNS, but does not let you control who has access to them. | bebefa01-2a29-4197-83a8-272ff33ce314 |
| 12 | Network Contributor | Lets you manage networks, but not access to them. This role does not grant you permission to deploy or manage Virtual Machines. | 4d97b98b-1d4f-4787-a291-c67834d212e7 |
| 13 | Private DNS Zone Contributor | Lets you manage private DNS zone resources, but not the virtual networks they are linked to. | b12aa53e-6015-4669-85d0-8515ebb3ae7f |
| 14 | Traffic Manager Contributor | Lets you manage Traffic Manager profiles, but does not let you control who has access to them. | a4b10055-b0c7-44c2-b00f-c7b5b3550cf7 |

## Storage

| Sno | Built-in role | Description | ID |
|---|---|---|---|
| 1 | Avere Contributor | Can create and manage an Avere vFXT cluster. | 4f8fab4f-1852-4a58-a46a-8eaf358af14a |
| 2 | Avere Operator | Used by the Avere vFXT cluster to manage the cluster | c025889f-8102-4ebf-b32c-fc0c6f0c6bd9 |
| 3 | Azure File Sync Administrator | Provides full access to manage all Azure File Sync (Storage Sync Service) resources. Also allows read/write access to all data contained in a storage account via access to storage account keys. | 92b92042-07d9-4307-87f7-36a593fc5850 |
| 4 | Azure File Sync Reader | Provides read access to Azure File Sync service (Storage Sync Service). | 754c1a27-40dc-4708-8ad4-2bffdeee09e8 |
| 5 | Backup Contributor | Lets you manage backup service, but can't create vaults and give access to others | 5e467623-bb1f-42f4-a55d-6e525e11384b |
| 6 | Backup MUA Admin | Backup MultiUser-Authorization. Can create/delete ResourceGuard | c2a970b4-16a7-4a51-8c84-8a8ea6ee0bb8 |
| 7 | Backup MUA Operator | Backup MultiUser-Authorization. Allows user to perform critical operation protected by resourceguard | f54b6d04-23c6-443e-b462-9c16ab7b4a52 |
| 8 | Backup Operator | Lets you manage backup services, except removal of backup, vault creation and giving access to others | 00c29273-979b-4161-815c-10b084fb9324 |
| 9 | Backup Reader | Can view backup services, but can't make changes | a795c7a0-d4a2-40c1-ae25-d81f01202912 |
| 10 | Classsic Storage Account Contributor | Lets you manage classic storage accounts, but not access to them. | 86e8f5dc-a6e9-4c67-9d15-de283e8eac25 |
| 11 | Classsic Storage Account Key Operator Service Role | Classsic Storage Account Key Operators are allowed to list and regenerate keys on Classic Storage Accounts | 985d6b00-f706-48f5-a6fe-d0ca12fb668d |
| 12 | Data Box Contributor | Lets you manage everything under Data Box Service except giving access to others. | add466c9-e687-43fc-8d98-dfcf8d720be5 |
| 13 | Data Box Reader | Lets you manage Data Box Service except creating order or editing order details and giving access to others. | 028f4ed7-e2a9-465e-a8f4-9c0ffdfdc027 |
| 14 | Data Lake Analytics Developer | Lets you submit, monitor, and manage your own jobs but not create or delete Data Lake Analytics accounts. | 47b7735b-770e-4598-a7da-8b91488b4c88 |
| 15 | Def ender for Storage Data Scanner | Grants access to read blobs and update index tags. This role is used by the data scanner of Defender for Storage. | 1e7ca9b1-60d1-4db8-a914-f2ca1ff27c40 |
| 16 | Elas tic SAN Network Admin | Allows access to create Private Endpoints on SAN resources, and to read SAN resources | fa6cecf6-5db3-4c43-8470-c540bcb4eafa |
| 17 | Elas tic SAN Owner | Allows for full access to all resources under Azure Elastic SAN including changing network security policies to unblock data path access | 80dcbedb-47ef-405d-95bd-188a1b4ac406 |
| 18 | Elas tic SAN Reader | Allows for control path read access to Azure Elastic SAN | af6a70f8-3c9f-4105-acf1-d719e9fca4ca |
| 19 | Elas tic SAN Volume Group Owner | Allows for full access to a volume group in Azure Elastic SAN including changing network security policies to unblock data path access | a8281131-f312-4f34-8d98-ae12be9f0d23 |
| 20 | Reader and Data Access | Lets you view everything but will not let you delete or create a storage account or contained resource. It will also allow read/write access to all data contained in a storage account via access to storage account keys. | c12c1c16-33a1-487b-954d-41c89c60f349 |
| 21 | Storage Account Backup Contributor | Lets you perform backup and restore operations using Azure Backup on the storage account. | e5e2a7ff-d759-4cd2-bb51-3152d37e2eb1 |
| 22 | Storage Account Contributor | Permits management of storage accounts. Provides access to the account key, which can be used to access data via Shared Key authorization. | 17d1049b-9a84-46fb-8f53-869881c3d3ab |
| 23 | Storage Account Key Operator Service Role | Permits listing and regenerating storage account access keys. | 81a9662b-bebf-436f-a333-f67b29880f12 |
| 24 | Storage Actions Blob Data Operator | Used by the Storage Actions - Storage Task to list & perform operations on the Storage Account blobs | 4bad4d9e-2a13-4888-94bb-c8432f6f3040 |
| 25 | Storage Actions Contributor | Used by the Storage Actions author to create, read, update, and delete Storage Actions | bd8acdb0-202c-4493-a7fe-ef98eefbfbc4 |
| 26 | Storage Actions Task Assignment Contributor | Used by the Storage Actions assigner to create a Task Assignment on their target Storage Account, with RBAC privileges for Managed Identity | 77789c21-1643-48a2-8f27-47f858540b51 |
| 27 | Storage Blob Data Contributor | Read, write, and delete Azure Storage containers and blobs. To learn which actions are required for a given data operation, see Permissions for calling data operations. | ba92f5b4-2d11-453d-a403-e96b0029c9fe |
| 28 | Storage Blob Data Owner | Provides full access to Azure Storage blob containers and data, including assigning POSIX access control. To learn which actions are required for a given data operation, see Permissions for calling data operations. | b7e6dc6d-f1e8-4753-8033-0f276bb0955b |
| 29 | Storage Blob Data Reader | Read and list Azure Storage containers and blobs. To learn which actions are required for a given data operation, see Permissions for calling data operations. | 2a2b9908-6ea1-4ae2-8e65-a410df84e7d1 |
| 30 | Storage Blob Delegator | Get a user delegation key, which can then be used to create a shared access signature for a container or blob that is signed with Azure AD credentials. For more information, see Create a user delegation SAS. | db58b8e5-c6ad-4a2a-8342-4190687cbf4a |
| 31 | Storage Connector Contributor | Allows creating and managing storage connectors to access remote data sources in-place in a storage account. This role is in preview and subject to change. | 9d819e60-1b9f-4871-b492-4e6cdee0b50a |
| 32 | Storage DataShare Contributor | Allows creating and managing storage dataShares to share data from storage accounts in-place. This role is in preview and subject to change. | 35c49d44-ccc1-4b18-8267-cfb3bacdd396 |
| 33 | Storage File Data Privileged Contributor | Allows for read, write, delete, and modify ACLs on files/directories in Azure file shares by overriding existing ACLs/NTFS permissions. This role has no built-in equivalent on Windows file servers. | 69566ab7-960f-475b-8e7c-b3118f30c6bd |
| 34 | Storage File Data Privileged Reader | Allows for read access on files/directories in Azure file shares by overriding existing ACLs/NTFS permissions. This role has no built-in equivalent on Windows file servers. | b8eda974-7b85-4f76-af95-65846b26df6d |
| 35 | Storage File Data SMB Admin | Allows for admin access equivalent to storage account key for end users over SMB. | bbf004e3-0e4b-4f86-ae4f-1f8fb47b357b |
| 36 | Storage File Data SMB MI Admin | Allows for admin-level access for managed identities on files/directories in Azure file shares. | a235d3ee-5935-4cfb-8cc5-a3303ad5995e |
| 37 | Storage File Data SMB Share Contributor | Allows for read, write, and delete access on files/directories in Azure file shares. This role has no built-in equivalent on Windows file servers. | 0c867c2a-1d8c-454a-a3db-ab2ea1bdc8bb |
| 38 | Storage File Data SMB Share Elevated Contributor | Allows for read, write, delete, and modify ACLs on files/directories in Azure file shares. This role is equivalent to a file share ACL of change on Windows file servers. | a7264617-510b-434b-a828-9731dc254ea7 |
| 39 | Storage File Data SMB Share Reader | Allows for read access on files/directories in Azure file shares. This role is equivalent to a file share ACL of read on Windows file servers. | aba4ae5f-2193-4029-9191-0cb91df5e314 |
| 40 | Storage File Data SMB Take Ownership | Allows end user to assume ownership of a file/directory | 5d9bac3f-34b2-432f-bde5-78aa8e73ce6b |
| 41 | Storage File Delegator | Get a user delegation key, which can then be used to create a shared access signature for a file or Azure file share that is signed with Azure AD credentials. For more information, see Create a user delegation SAS. | 765a04e0-5de8-4bb2-9bf6-b2a30bc03e91 |
| 42 | Storage Queue Data Contributor | Read, write, and delete Azure Storage queues and queue messages. To learn which actions are required for a given data operation, see Permissions for calling data operations. | 974c5e8b-45b9-4653-ba55-5f855dd0fb88 |
| 43 | Storage Queue Data Message Processor | Peek, retrieve, and delete a message from an Azure Storage queue. To learn which actions are required for a given data operation, see Permissions for calling data operations. | 8a0f0c08-91a1-4084-bc3d-661d67233fed |
| 44 | Storage Queue Data Message Sender | Add messages to an Azure Storage queue. To learn which actions are required for a given data operation, see Permissions for calling data operations. | c6a89b2d-59bc-44d0-9896-0f6e12d7b80a |
| 45 | Storage Queue Data Reader | Read and list Azure Storage queues and queue messages. To learn which actions are required for a given data operation, see Permissions for calling data operations. | 19e7f393-937e-4f77-808e-94535e297925 |
| 46 | Storage Queue Delegator | Get a user delegation key, which can then be used to create a shared access signature for an Azure Storage queue that is signed with Azure AD credentials. For more information, see Create a user delegation SAS. | 7ee386e9-84f0-448e-80a6-f185f6533131 |
| 47 | Storage Table Data Contributor | Allows for read, write and delete access to Azure Storage tables and entities | 0a9a7e1f-b9d0-4cc4-a60d-0319b160aaa3 |
| 48 | Storage Table Data Reader | Allows for read access to Azure Storage tables and entities | 76199698-9eea-4c19-bc75-cec21354c6b6 |
| 49 | Storage Table Delegator | Get a user delegation key, which can then be used to create a shared access signature for an Azure Storage table that is signed with Azure AD credentials. For more information, see Create a user delegation SAS. | 965033a5-c8eb-4f35-b82f-fef460a3606d |

---

## Web and Mobile

| SNo | Built-in Role | Description | ID |
|---|---|---|---|
| 1 | Azure Maps Data Contributor | Grants access to read, write, and delete access to map related data from an Azure maps account. | 8f5e0ce6-4f7b-4dcf-bddf-e6f48634a204 |
| 2 | Azure Maps Data Reader | Grants access to read map related data from an Azure maps account. | 423170ca-a8f6-4b0f-8487-9e4eb8f49bfa |
| 3 | Azure Maps Search and Render Data Reader | Grants access to very limited set of data APIs for common visual web SDK scenarios. Specifically, render and search data APIs. | 6be48352-4f82-47c9-ad5e-0acacefdb005 |
| 4 | Azure Spring Apps Application Configuration Service Config File Pattern Reader Role | Read content of config file pattern for Application Configuration Service in Azure Spring Apps | 25211fc6-dc78-40b6-b205-e4ac934fd9fd |
| 5 | Azure Spring Apps Application Configuration Service Log Reader Role | Read real-time logs for Application Configuration Service in Azure Spring Apps | 6593e776-2a30-40f9-8a32-4fe28b77655d |
| 6 | Azure Spring Apps Connect Role | Azure Spring Apps Connect Role | 80558df3-64f9-4c0f-b32d-e5094b036b0b |
| 7 | Azure Spring Apps Job Log Reader Role | Read real-time logs for jobs in Azure Spring Apps | b459aa1d-e3c8-436f-ae21-c0531140f43e |
| 8 | Azure Spring Apps Remote Debugging Role | Azure Spring Apps Remote Debugging Role | a99b0159-1064-4c22-a57b-c9b3caa1c054 |
| 9 | Azure Spring Apps Spring Cloud Gateway Log Reader Role | Read real-time logs for Spring Cloud Gateway in Azure Spring Apps | 4301dc2a-25a9-44b0-ae63-3636cf7f2bd2 |
| 10 | Azure Spring Cloud Config Server Contributor | Allow read, write and delete access to Azure Spring Cloud Config Server | a06f5c24-21a7-4e1a-aa2b-f19eb6684f5b |
| 11 | Azure Spring Cloud Config Server Reader | Allow read access to Azure Spring Cloud Config Server | d04c6db6-4947-4782-9e91-30a88feb7be7 |
| 12 | Azure Spring Cloud Data Reader | Allow read access to Azure Spring Cloud Data | b5537268-8956-4941-a8f0-646150406f0c |
| 13 | Azure Spring Cloud Service Registry Contributor | Allow read, write and delete access to Azure Spring Cloud Service Registry | f5880b48-c26d-48be-b172-7927bfa1c8f1 |
| 14 | Azure Spring Cloud Service Registry Reader | Allow read access to Azure Spring Cloud Service Registry | cff1b556-2399-4e7e-856d-a8f754be7b65 |
| 15 | SignalR AccessKey Reader | Read SignalR Service Access Keys | 04165923-9d83-45d5-8227-78b77b0a687e |
| 16 | SignalR App Server | Lets your app server access SignalR Service with AAD auth options. | 420fcaa2-552c-430f-98ca-3264be4806c7 |
| 17 | SignalR REST API Owner | Full access to Azure SignalR Service REST APIs | fd53cd77-2268-407a-8f46-7e7863d0f521 |
| 18 | SignalR REST API Reader | Read-only access to Azure SignalR Service REST APIs | ddde6b66-c0df-4114-a159-3618637b3035 |
| 19 | SignalR Service Owner | Full access to Azure SignalR Service REST APIs | 7e4f1700-ea5a-4f59-8f37-079cfe29dce3 |
| 20 | SignalR/Web PubSub Contributor | Create, Read, Update, and Delete SignalR service resources | 8cf5e20a-e4b2-4e9d-b3a1-5ceb692c2761 |
| 21 | Web Plan Contributor | Manage the web plans for websites. Does not allow you to assign roles in Azure RBAC. | 2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b |
| 22 | Web PubSub Service Owner | Full access to Azure Web PubSub Service REST APIs | 12cf5a90-567b-43ae-8102-96cf46c7d9b4 |
| 23 | Web PubSub Service Reader | Read-only access to Azure Web PubSub Service REST APIs | bfb1c7d2-fb1a-466b-b2ba-aee63b92deaf |
| 24 | Website Contributor | Manage websites, but not web plans. Does not allow you to assign roles in Azure RBAC. | de139f84-1756-47ae-9be6-808fbbe84772 |

---

## Containers

| SNo | Built-in Role | Description | ID |
|---|---|---|---|
| 1 | AcrDelete | Delete repositories, tags, or manifests from a container registry. | c2f4ef07-c644-48eb-af81-4b1b4947fb11 |
| 2 | AcrImageSigner | Avoid using this role. Content Trust in Azure Container Registry and the AcrImageSigner role are being deprecated and will be completely removed on March 31, 2028. For details and transition guidance, see [https://aka.ms/acr/dctdeprecation.%20|%206cef56e8-d556-48e5-a04f-b8e64114680f%20|](https://aka.ms/acr/dctdeprecation.%20|%206cef56e8-d556-48e5-a04f-b8e64114680f%20|)
| 3 | AcrPull | Pull artifacts from a container registry. | 7f951dda-4ed3-4680-a7ca-43fe172d538d |
| 4 | AcrPush | Push artifacts to or pull artifacts from a container registry. | 8311e382-0749-4cb8-b61a-304f252e45ec |
| 5 | AcrQuarantineReader | Pull quarantined images from a container registry. | cdda3590-29a3-44f6-95f2-9f980659eb04 |
| 6 | AcrQuarantineWriter | Push quarantined images to or pull quarantined images from a container registry. | c8d4ff99-41c3-41a8-9f60-21dfdad59608 |
| 7 | Azure Arc Enabled Kubernetes Cluster User Role | List cluster user credentials action. | 00493d72-78f6-4148-b6c5-d3ce8e4799dd |
| 8 | Azure Arc Kubernetes Admin | Lets you manage all resources under cluster/namespace, except update or delete resource quotas and namespaces. | dffb1e0c-446f-4dde-a09f-99eb5cc68b96 |
| 9 | Azure Arc Kubernetes Cluster Admin | Lets you manage all resources in the cluster. | 8393591c-06b9-48a2-a542-1bd6b377f6a2 |
| 10 | Azure Arc Kubernetes Viewer | Lets you view all resources in cluster/namespace, except secrets. | 63f0a09d-1495-4db4-a681-037d84835eb4 |
| 11 | Azure Arc Kubernetes Writer | Lets you update everything in cluster/namespace, except (cluster)roles and (cluster)role bindings. | 5b999177-9696-4545-85c7-50de3797e5a1 |
| 12 | Azure Container Instances Contributor Role | Grants read/write access to container groups provided by Azure Container Instances | 5d977122-f97e-4b4d-a52f-6b43003ddb4d |
| 13 | Azure Container Storage Contributor | Install Azure Container Storage and manage its storage resources. Includes an ABAC condition to constrain role assignments. | 95dd08a6-00bd-4661-84bf-f6726f83a4d0 |
| 14 | Azure Container Storage Operator | Enable a managed identity to perform Azure Container Storage operations, such as manage virtual machines and manage virtual networks. | 08d4c71a-cc63-4ce4-a9c8-5dd251b4d619 |
| 15 | Azure Container Storage Owner | Install Azure Container Storage, grant access to its storage resources, and configure Azure Elastic storage area network (SAN). Includes an ABAC condition to constrain role assignments. | 95de85bd-744d-4664-9dde-11430bc34793 |
| 16 | Azure Kubernetes Fleet Manager Contributor Role | Grants read/write access to Azure resources provided by Azure Kubernetes Fleet Manager, including fleets, fleet members, fleet update strategies, fleet update runs, etc. | 63bb64ad-9799-4770-b5c3-24ed299a07bf |
| 17 | Azure Kubernetes Fleet Manager Hub Agent Role | Grants access to Azure resources needed by Azure Kubernetes Fleet Manager hub agents. | de2b316d-7a2c-4143-b4cd-c148f6a355a1 |
| 18 | Azure Kubernetes Fleet Manager Hub Cluster User Role | Grants read access to Azure Kubernetes Fleet Manager as well as the Kubernetes config file to connect to the fleet-managed hub cluster. | 850c5848-fc51-4a9a-8823-f220370626e3 |
| 19 | Azure Kubernetes Fleet Manager RBAC Admin | Grants read/write access to Kubernetes resources within a namespace in the fleet-managed hub cluster - provides write permissions on most objects within a namespace, with the exception of ResourceQuota object and the namespace object itself. Applying this role at cluster scope will give access across all namespaces. | 434fb43a-c01c-447e-9f67-c3ad923cfaba |
| 20 | Azure Kubernetes Fleet Manager RBAC Admin for Member Clusters | This role grants admin access - provides write permissions on most objects within a namespace, with the exception of ResourceQuota object and the namespace object itself. Applying this role at cluster scope will give access across all namespaces. | d1f699ed-700a-4c77-a22f-29890ac7b115 |
| 21 | Azure Kubernetes Fleet Manager RBAC Cluster Admin | Grants read/write access to all Kubernetes resources in the fleet-managed hub cluster. | 18ab4d3d-a1bf-4477-8ad9-8359bc988f69 |
| 22 | Azure Kubernetes Fleet Manager RBAC Cluster Admin for Member Clusters | Lets you manage all resources in the member clusters in the fleet. | 79a36d98-eb96-4a76-ae1d-481dc98d2c23 |
| 23 | Azure Kubernetes Fleet Manager RBAC Reader | Grants read-only access to most Kubernetes resources within a namespace in the fleet-managed hub cluster. It does not allow viewing roles or role bindings. This role does not allow viewing Secrets, since reading the contents of Secrets enables access to ServiceAccount credentials in the namespace, which would allow API access as any ServiceAccount in the namespace (a form of privilege escalation). Applying this role at cluster scope will give access across all namespaces. | 30b27cfc-9c84-438e-b0ce-70e35255df80 |
| 24 | Azure Kubernetes Fleet Manager RBAC Reader for Member Clusters | Allows read-only access to see most objects in a namespace. It does not allow viewing roles or role bindings. This role does not allow viewing Secrets, since reading the contents of Secrets enables access to ServiceAccount credentials in the namespace, which would allow API access as any ServiceAccount in the namespace (a form of privilege escalation).  Applying this role at cluster scope will give access across all namespaces. | 463ad26c-fcce-4469-9c7f-5653d8acbab5 |
| 25 | Azure Kubernetes Fleet Manager RBAC Writer | Grants read/write access to most Kubernetes resources within a namespace in the fleet-managed hub cluster. This role does not allow viewing or modifying roles or role bindings. However, this role allows accessing Secrets as any ServiceAccount in the namespace, so it can be used to gain the API access levels of any ServiceAccount in the namespace.  Applying this role at cluster scope will give access across all namespaces. | 5af6afb3-c06c-4fa4-8848-71a8aee05683 |
| 26 | Azure Kubernetes Fleet Manager RBAC Writer for Member Clusters | Allows read/write access to most objects in a namespace. This role does not allow viewing or modifying roles or role bindings. However, this role allows accessing Secrets and running Pods as any ServiceAccount in the namespace, so it can be used to gain the API access levels of any ServiceAccount in the namespace.  Applying this role at cluster scope will give access across all namespaces. | 50346970-0998-40f2-b47d-f3b8809840f8 |
| 27 | Azure Kubernetes Service Arc Cluster Admin Role | List cluster admin credential action. | b29efa5f-7782-4dc3-9537-4d5bc70a5e9f |
| 28 | Azure Kubernetes Service Arc Cluster User Role | List cluster user credential action. | 233ca253-b031-42ff-9fba-87ef12d6b55f |
| 29 | Azure Kubernetes Service Arc Contributor Role | Grants access to read and write Azure Kubernetes Services hybrid clusters | 5d3f1697-4507-4d08-bb4a-477695db5f82 |
| 30 | Azure Kubernetes Service Cluster Admin Role | List cluster admin credential action. | 0ab0b1a8-8aac-4efd-b8c2-3ee1fb270be8 |
| 31 | Azure Kubernetes Service Cluster Monitoring User | List cluster monitoring user credential action. | 1afdec4b-e479-420e-99e7-f82237c7c5e6 |
| 32 | Azure Kubernetes Service Cluster User Role | List cluster user credential action. | 4abbcc35-e782-43d8-92c5-2d3f1bd2253f |
| 33 | Azure Kubernetes Service Contributor Role | Grants access to read and write Azure Kubernetes Service clusters | ed7f3fbd-7b88-4dd4-9017-9adb7ce333f8 |
| 34 | Azure Kubernetes Service Namespace Contributor | Allows users to create and manage Azure Kubernetes Service namespace resources. | 289d8817-ee69-43f1-a0af-43a45505b488 |
| 35 | Azure Kubernetes Service Namespace User | Allows users to read Azure Kubernetes Service namespace resources. In-cluster namespace access further requires assignment of Azure Kubernetes Service RBAC roles to the namespace resource for an Entra ID enabled cluster. | c9f76ca8-b262-4b10-8ed2-09cf0948aa35 |
| 36 | Azure Kubernetes Service RBAC Admin | Lets you manage all resources under cluster/namespace, except update or delete resource quotas and namespaces. | 3498e952-d568-435e-9b2c-8d77e338d7f7 |
| 37 | Azure Kubernetes Service RBAC Cluster Admin | Lets you manage all resources in the cluster. | b1ff04bb-8a4e-4dc4-8eb5-8693973ce19b |
| 38 | Azure Kubernetes Service RBAC Reader | Allows read-only access to see most objects in a namespace. It does not allow viewing roles or role bindings. This role does not allow viewing Secrets, since reading the contents of Secrets enables access to ServiceAccount credentials in the namespace, which would allow API access as any ServiceAccount in the namespace (a form of privilege escalation). Applying this role at cluster scope will give access across all namespaces. | 7f6c6a51-bcf8-42ba-9220-52d62157d7db |
| 39 | Azure Kubernetes Service RBAC Writer | Allows read/write access to most objects in a namespace. This role does not allow viewing or modifying roles or role bindings. However, this role allows accessing Secrets and running Pods as any ServiceAccount in the namespace, so it can be used to gain the API access levels of any ServiceAccount in the namespace. Applying this role at cluster scope will give access across all namespaces. | a7ffa36f-339b-4b5c-8bdf-e2c188b2c0eb |
| 40 | Azure Red Hat OpenShift Cloud Controller Manager | Manage and update the cloud controller manager deployed on top of OpenShift. | a1f96423-95ce-4224-ab27-4e3dc72facd4 |
| 41 | Azure Red Hat OpenShift Cluster Ingress Operator | Manage and configure the OpenShift router. | 0336e1d3-7a87-462b-b6db-342b63f7802c |
| 42 | Azure Red Hat OpenShift Disk Storage Operator | Install Container Storage Interface (CSI) drivers that enable your cluster to use Azure Disks. Set OpenShift cluster-wide storage defaults to ensure a default storageclass exists for clusters. | 5b7237c5-45e1-49d6-bc18-a1f62f400748 |
| 43 | Azure Red Hat OpenShift Federated Credential | Create, update and delete federated credentials on user assigned managed identities in order to build a trust relationship between the managed identity, OpenID Connect (OIDC), and the service account. | ef318e2a-8334-4a05-9e4a-295a196c6a6e |
| 44 | Azure Red Hat OpenShift File Storage Operator | Install Container Storage Interface (CSI) drivers that enable your cluster to use Azure Files. Set OpenShift cluster-wide storage defaults to ensure a default storageclass exists for clusters. | 0d7aedc0-15fd-4a67-a412-efad370c947e |
| 45 | Azure Red Hat OpenShift Image Registry Operator | Enables permissions for the operator to manage a singleton instance of the OpenShift image registry. It manages all configuration of the registry, including creating storage. | 8b32b316-c2f5-4ddf-b05b-83dacd2d08b5 |
| 46 | Azure Red Hat OpenShift Machine API Operator | Manage the lifecycle of specific-purpose custom resource definitions (CRD), controllers, and Azure RBAC objects that extend the Kubernetes API to declare the desired state of machines in a cluster. | 0358943c-7e01-48ba-8889-02cc51d78637 |
| 47 | Azure Red Hat OpenShift Network Operator | Install and upgrade the networking components on an OpenShift cluster. | be7a6435-15ae-4171-8f30-4a343eff9e8f |
| 48 | Azure Red Hat OpenShift Service Operator | Maintain machine health, network configuration, monitoring, and other features that are specific to an OpenShift cluster's continued functionality as a managed service. | 4436bae4-7702-4c84-919b-c4069ff25ee2 |
| 49 | Connected Cluster Managed Identity CheckAccess Reader | Built-in role that allows a Connected Cluster managed identity to call the checkAccess API | 65a14201-8f6c-4c28-bec4-12619c5a9aaa |
| 50 | Container Apps ConnectedEnvironments Contributor | Full management of Container Apps ConnectedEnvironments, including creation, deletion, and updates. | 6f4fe6fc-f04f-4d97-8528-8bc18c848dca |
| 51 | Container Apps ConnectedEnvironments Reader | Read access to Container Apps ConnectedEnvironments. | d5adeb5b-107f-4aca-99ea-4e3f4fc008d5 |
| 52 | Container Apps Contributor | Full management of Container Apps, including creation, deletion, and updates. | 358470bc-b998-42bd-ab17-a7e34c199c0f |
| 53 | Container Apps Jobs Contributor | Full management of Container Apps jobs, including creation, deletion, and updates. | 4e3d2b60-56ae-4dc6-a233-09c8e5a82e68 |
| 54 | Container Apps Jobs Operator | Read, start, and stop Container Apps jobs. | b9a307c4-5aa3-4b52-ba60-2b17c136cd7b |
| 55 | Container Apps Jobs Reader | Read access to ContainerApps jobs | edd66693-d32a-450b-997d-0158c03976b0 |
| 56 | Container Apps ManagedEnvironments Contributor | Full management of Container Apps ManagedEnvironments, including creation, deletion, and updates. | 57cc5028-e6a7-4284-868d-0611c5923f8d |
| 57 | Container Apps ManagedEnvironments Reader | Read access to ContainerApps managedenvironments. | 1b32c00b-7eff-4c22-93e6-93d11d72d2d8 |
| 58 | Container Apps Operator | Read, logstream and exec into Container Apps. | f3bd1b5c-91fa-40e7-afe7-0c11d331232c |
| 59 | Container Apps SessionPools Contributor | Full management of Container Apps SessionPools, including creation, deletion, and updates. | f7669afb-68b2-44b4-9c5f-6d2a47fddda0 |
| 60 | Container Apps SessionPools Reader | Read access to ContainerApps sessionpools. | af61e8fc-2633-4b95-bed3-421ad6826515 |
| 61 | Container Registry Cache Rule Administrator | Create, Read, Update, and Delete Cache Rules in Container Registry. This role doesn't grant permissions to manage Credential Sets. | df87f177-bb12-4db1-9793-a413691eff94 |
| 62 | Container Registry Cache Rule Reader | Read the configuration of Cache Rules in Container Registry. This permission doesn't grant permission to read Credential Sets. | c357b964-0002-4b64-a50d-7a28f02edc52 |
| 63 | Container Registry Configuration Reader and Data Access Configuration Reader | Provides permissions to list container registries and registry configuration properties. Provides permissions to list data access configuration such as admin user credentials, scope maps, and tokens, which can be used to read, write or delete repositories and images. Does not provide direct permissions to read, list, or write registry contents including repositories and images. Does not provide permissions to modify data plane content such as imports, Artifact Cache or Sync, and Transfer Pipelines. Does not provide permissions for managing Tasks. | 69b07be0-09bf-439a-b9a6-e73de851bd59 |
| 64 | Container Registry Contributor and Data Access Configuration Administrator | Provides permissions to create, list, and update container registries and registry configuration properties. Provides permissions to configure data access such as admin user credentials, scope maps, and tokens, which can be used to read, write or delete repositories and images. Does not provide direct permissions to read, list, or write registry contents including repositories and images. Does not provide permissions to modify data plane content such as imports, Artifact Cache or Sync, and Transfer Pipelines. Does not provide permissions for managing Tasks. | 3bc748fc-213d-45c1-8d91-9da5725539b9 |
| 65 | Container Registry Credential Set Administrator | Create, Read, Update, and Delete Credential Sets in Container Registry. This role doesn't affect the needed permissions for storing content inside Azure Key Vault. This role also doesn't grant permissions to manage Cache Rules. | f094fb07-0703-4400-ad6a-e16dd8000e14 |
| 66 | Container Registry Credential Set Reader | Read the configuration of Credential Sets in Container Registry. This permission doesn't allow permission to see content inside Azure Key vault only the content inside Container Registry. This permission doesn't grant permission to read Cache Rules. | 29093635-9924-4f2c-913b-650a12949526 |
| 67 | Container Registry Data Importer and Data Reader | Provides the ability to import images into a registry through the registry import operation. Provides the ability to list repositories, view images and tags, get manifests, and pull images. Does not provide permissions for importing images through configuring registry transfer pipelines such as import and export pipelines. Does not provide permissions for importing through configuring Artifact Cache or Sync rules. | 577a9874-89fd-4f24-9dbd-b5034d0ad23a |
| 68 | Container Registry Repository Catalog Lister | Allows for listing all repositories in an Azure Container Registry. | bfdb9389-c9a5-478a-bb2f-ba9ca092c3c7 |
| 69 | Container Registry Repository Contributor | Allows for read, write, and delete access to Azure Container Registry repositories, but excluding catalog listing. | 2efddaa5-3f1f-4df3-97df-af3f13818f4c |
| 70 | Container Registry Repository Reader | Allows for read access to Azure Container Registry repositories, but excluding catalog listing. | b93aa761-3e63-49ed-ac28-beffa264f7ac |
| 71 | Container Registry Repository Writer | Allows for read and write access to Azure Container Registry repositories, but excluding catalog listing. | 2a1e307c-b015-4ebd-883e-5b7698a07328 |
| 72 | Container Registry Tasks Contributor | Provides permissions to configure, read, list, trigger, or cancel Container Registry Tasks, Task Runs, Task Logs, Quick Runs, Quick Builds, and Task Agent Pools. Permissions granted for Tasks management can be used for full registry data plane permissions including reading/writing/deleting container images in registries. Permissions granted for Tasks management can also be used to run customer authored build directives and run scripts to build software artifacts. | fb382eab-e894-4461-af04-94435c366c3f |
| 73 | Container Registry Transfer Pipeline Contributor | Provides the ability to transfer, import, and export artifacts through configuring registry transfer pipelines that involve intermediary storage accounts and key vaults. Does not provide permissions to push or pull images. Does not provide permissions to create, manage, or list storage accounts or key vaults. Does not provide permissions to perform role assignments. | bf94e731-3a51-4a7c-8c54-a1ab9971dfc1 |
| 74 | Def ender Kubernetes API Access | Grants Microsoft Defender for Cloud access to Azure Kubernetes Services | d5a2ae44-610b-4500-93be-660a0c5f5ca6 |
| 75 | Kubernetes Cluster - Azure Arc Onboarding | Role definition to authorize any user/service to create connectedClusters resource | 34e09817-6cbe-4d01-b1a2-e0eac5743d41 |
| 76 | Kubernetes Extension Contributor | Can create, update, get, list and delete Kubernetes Extensions, and get extension async operations | 85cb6faf-e071-4c9b-8136-154b5a04f717 |
| 77 | Service Fabric Cluster Contributor | Manage your Service Fabric Cluster resources. Includes clusters, application types, application type versions, applications, and services. You will need additional permissions to deploy and manage the cluster's underlying resources such as virtual machine scale sets, storage accounts, networks, etc. | b6efc156-f0da-4e90-a50a-8c000140b017 |
| 78 | Service Fabric Managed Cluster Contributor | Deploy and manage your Service Fabric Managed Cluster resources. Includes managed clusters, node types, application types, application type versions, applications, and services. | 83f80186-3729-438c-ad2d-39e94d718838 |

---

## Databases

| SNo | Built-in Role | Description | ID |
|---|---|---|---|
| 1 | Azure Connected SQL Server Onboarding | Allows for read and write access to Azure resources for SQL Server on Arc-enabled servers. | e8113dce-c529-4d33-91fa-e9b972617508 |
| 2 | Azure Managed Redis Contributor | Create and manage Azure Managed Redis resources. Cannot read or write data stored in the cache. | 3015e5ed-6856-4ab3-b2f0-b8492aa30ca6 |
| 3 | Azure Managed Redis Reader | Read Azure Managed Redis resources and their configuration. Cannot modify resources, retrieve access keys, or read data stored in the cache. | f287ba2f-f923-4464-a5bd-721c3951d32d |
| 4 | Cosmos DB Account Reader Role | Can read Azure Cosmos DB account data. See DocumentDB Account Contributor for managing Azure Cosmos DB accounts. | fbdf93bf-df7d-467e-a4d2-9458aa1360c8 |
| 5 | Cosmos DB Operator | Lets you manage Azure Cosmos DB accounts, but not access data in them. Prevents access to account keys and connection strings. | 230815da-be43-4aae-9cb4-875f7bd000aa |
| 6 | CosmosBackupOperator | Can submit restore request for a Cosmos DB database or a container for an account | db7b14f2-5adf-42da-9f96-f2ee17bab5cb |
| 7 | CosmosRestoreOperator | Can perform restore action for Cosmos DB database account with continuous backup mode | 5432c526-bc82-444a-b7ba-57c5b0b5b34f |
| 8 | DocumentDB Account Contributor | Can manage Azure Cosmos DB accounts. Azure Cosmos DB is formerly known as DocumentDB. | 5bd9cd88-fe45-4216-938b-f97437e15450 |
| 9 | PostgreSQL Flexible Server Long Term Retention Backup Role | Role to allow backup vault to access PostgreSQL Flexible Server Resource APIs for Long Term Retention Backup. | c088a766-074b-43ba-90d4-1fb21feae531 |
| 10 | Redis Cache Contributor | Create and manage Azure Cache for Redis resources. Cannot read or write data stored in the cache. | e0f68234-74aa-48ed-b826-c38b57376e17 |
| 11 | Semantic Reranker User | Execute semantic reranking operations against registered inference accounts. This role should be assigned to users who need to run semantic reranking workloads but do not need to manage the accounts themselves. | 6c74a7c5-4a87-40f9-bb03-61e49aecbc78 |
| 12 | SQL DB Contributor | Lets you manage SQL databases, but not access to them. Also, you can't manage their security-related policies or their parent SQL servers. | 9b7fa17d-e63e-47b0-bb0a-15c516ac86ec |
| 13 | SQL Managed Instance Contributor | Lets you manage SQL Managed Instances and required network configuration, but can't give access to others. | 4939a1f6-9ae0-4e48-a1e0-f2cbe897382d |
| 14 | SQL Security Manager | Lets you manage the security-related policies of SQL servers and databases, but not access to them. | 056cd41c-7e88-42e1-933e-88ba6a50c9c3 |
| 15 | SQL Server Contributor | Lets you manage SQL servers and databases, but not access to them, and not their security-related policies. | 6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437 |

---

## Analytics

| SNo | Built-in Role | Description | ID |
|---|---|---|---|
| 1 | Azure Event Hubs Data Owner | Allows for full access to Azure Event Hubs resources. | f526a384-b230-433a-b45c-95f59c4a2dec |
| 2 | Azure Event Hubs Data Receiver | Allows receive access to Azure Event Hubs resources. | a638d3c7-ab3a-418d-83e6-5f17a39d4fde |
| 3 | Azure Event Hubs Data Sender | Allows send access to Azure Event Hubs resources. | 2b629674-e913-4c01-ae53-ef4638d8f975 |
| 4 | Data Factory Contributor | Create and manage data factories, as well as child resources within them. | 673868aa-7521-48a0-acc6-0f60742d39f5 |
| 5 | HDInsight Cluster Operator | Lets you read and modify HDInsight cluster configurations. | 61ed4efc-fab3-44fd-b111-e24485cc132a |
| 6 | HDInsight Domain Services Contributor | Can Read, Create, Modify and Delete Domain Services related operations needed for HDInsight Enterprise Security Package | 8d8d5a11-05d3-4bda-a417-a08778121c7c |
| 7 | HDInsight on AKS Cluster Admin | Grants a user/group the ability to create, delete and manage clusters within a given cluster pool. Cluster Admin can also run workloads, monitor, and manage all user activity on these clusters. | fd036e6b-1266-47a0-b0bb-a05d04831731 |
| 8 | HDInsight on AKS Cluster Pool Admin | Can read, create, modify and delete HDInsight on AKS cluster pools and create clusters | 7656b436-37d4-490a-a4ab-d39f838f0042 |
| 9 | Schema Registry Contributor | Read, write, and delete Schema Registry groups and schemas. | 5dffeca3-4936-4216-b2bc-10343a5abb25 |
| 10 | Schema Registry Reader | Read and list Schema Registry groups and schemas. | 2c56ea50-c6b3-40a6-83c0-9d98858bc7d2 |
| 11 | Stream Analytics Query Tester | Lets you perform query testing without creating a stream analytics job first | 1ec5b3c1-b17e-4e25-8312-2acb3c3c5abf |

---

## AI + machine learning

| SNo | Built-in Role | Description | ID |
|---|---|---|---|
| 1 | Azure AI Administrator | A Built-In Role that has all control plane permissions to work with Azure AI and its dependencies. Applies to Azure Machine Learning and Foundry hubs only. | b78c5d69-af96-48a3-bf8d-a8b4d589de94 |
| 2 | Azure AI Developer | Can perform all actions within an Azure Machine Learning workspace besides managing the workspace itself. For Foundry project access, use the Foundry User or Foundry Owner roles instead. | 64702f94-c441-49e6-a78b-ef80e0188fee |
| 3 | Azure AI Enterprise Network Connection Approver | Can approve private endpoint connections to Azure AI common dependency resources | b556d68e-0be0-4f35-a333-ad7ee1ce17ea |
| 4 | Azure AI Inference Deployment Operator | Can perform all actions required to create a resource deployment within a resource group. | 3afb7f49-54cb-416e-8c09-6dc049efa503 |
| 5 | AzureML Compute Operator | Can access and perform CRUD operations on Machine Learning Services managed compute resources (including Notebook VMs). | e503ece1-11d0-4e8e-8e2c-7a6c3bf38815 |
| 6 | AzureML Data Scientist | Can perform all actions within an Azure Machine Learning workspace, except for creating or deleting compute resources and modifying the workspace itself. | f6c7c914-8db3-469d-8ca1-694a8f32e121 |
| 7 | AzureML Metrics Writer (preview) | Lets you write metrics to AzureML workspace | 635dd51f-9968-44d3-b7fb-6d9a6bd613ae |
| 8 | AzureML Registry User | Can perform all actions on Machine Learning Services Registry assets as well as get Registry resources. | 1823dd4f-9b8c-4ab6-ab4e-7397a3684615 |
| 9 | Cognitive Services Contributor | Lets you create, read, update, delete and manage keys of Cognitive Services. | 25fbc0a9-bd7c-42a3-aa1a-3b75d497ee68 |
| 10 | Cognitive Services Custom Vision Contributor | Full access to the project, including the ability to view, create, edit, or delete projects. | c1ff6cc2-c111-46fe-8896-e0ef812ad9f3 |
| 11 | Cognitive Services Custom Vision Deployment | Publish, unpublish or export models. Deployment can view the project but can't update. | 5c4089e1-6d96-4d2f-b296-c1bc7137275f |
| 12 | Cognitive Services Custom Vision Labeler | View, edit training images and create, add, remove, or delete the image tags. Labelers can view the project but can't update anything other than training images and tags. | 88424f51-ebe7-446f-bc41-7fa16989e96c |
| 13 | Cognitive Services Custom Vision Reader | Read-only actions in the project. Readers can't create or update the project. | 93586559-c37d-4a6b-ba08-b9f0940c2d73 |
| 14 | Cognitive Services Custom Vision Trainer | View, edit projects and train the models, including the ability to publish, unpublish, export the models. Trainers can't create or delete the project. | 0a5ae4ab-0d65-4eeb-be61-29fc9b54394b |
| 15 | Cognitive Services Data Reader | Lets you read Cognitive Services data. | b59867f0-fa02-499b-be73-45a86b5b3e1c |
| 16 | Cognitive Services Face Recognizer | Lets you perform detect, verify, identify, group, and find similar operations on Face API. This role does not allow create or delete operations, which makes it well suited for endpoints that only need inferencing capabilities, following 'least privilege' best practices. | 9894cab4-e18a-44aa-828b-cb588cd6f2d7 |
| 17 | Cognitive Services Immersive Reader User | Provides access to create Immersive Reader sessions and call APIs | b2de6794-95db-4659-8781-7e080d3f2b9d |
| 18 | Cognitive Services Language Owner | Has access to all Read, Test, Write, Deploy and Delete functions under Language portal | f07febfe-79bc-46b1-8b37-790e26e6e498 |
| 19 | Cognitive Services Language Reader | Has access to Read and Test functions under Language portal | 7628b7b8-a8b2-4cdc-b46f-e9b35248918e |
| 20 | Cognitive Services Language Writer | Has access to all Read, Test, and Write functions under Language Portal | f2310ca1-dc64-4889-bb49-c8e0fa3d47a8 |
| 21 | Cognitive Services LUIS Owner | Has access to all Read, Test, Write, Deploy and Delete functions under LUIS | f72c8140-2111-481c-87ff-72b910f6e3f8 |
| 22 | Cognitive Services LUIS Reader | Has access to Read and Test functions under LUIS. | 18e81cdc-4e98-4e29-a639-e7d10c5a6226 |
| 23 | Cognitive Services LUIS Writer | Has access to all Read, Test, and Write functions under LUIS | 6322a993-d5c9-4bed-b113-e49bbea25b27 |
| 24 | Cognitive Services Metrics Advisor Administrator | Full access to the project, including the system level configuration. | cb43c632-a144-4ec5-977c-e80c4affc34a |
| 25 | Cognitive Services Metrics Advisor User | Access to the project. | 3b20f47b-3825-43cb-8114-4bd2201156a8 |
| 26 | Cognitive Services OpenAI Contributor | Full access including the ability to fine-tune, deploy and generate text | a001fd3d-188f-4b5d-821b-7da978bf7442 |
| 27 | Cognitive Services OpenAI User | Read access to view files, models, deployments. The ability to create completion and embedding calls. | 5e0bd9bd-7b93-4f28-af87-19fc36ad61bd |
| 28 | Cognitive Services QnA Maker Editor | Let's you create, edit, import and export a KB. You cannot publish or delete a KB. | f4cc2bf9-21be-47a1-bdf1-5c5804381025 |
| 29 | Cognitive Services QnA Maker Reader | Let's you read and test a KB only. | 466ccd10-b268-4a11-b098-b4849f024126 |
| 30 | Cognitive Services Speech Contributor | Full access to Speech projects, including read, write and delete all entities, for real-time speech recognition and batch transcription tasks, real-time speech synthesis and long audio tasks, custom speech and custom voice. | 0e75ca1e-0464-4b4d-8b93-68208a576181 |
| 31 | Cognitive Services Speech User | Access to the real-time speech recognition and batch transcription APIs, real-time speech synthesis and long audio APIs, as well as to read the data/test/model/endpoint for custom models, but can't create, delete or modify the data/test/model/endpoint for custom models. | f2dc8367-1007-4938-bd23-fe263f013447 |
| 32 | Cognitive Services Usages Reader | Minimal permission to view Cognitive Services usages. | bba48692-92b0-4667-a9ad-c31c7b334ac2 |
| 33 | Cognitive Services User | Lets you read and list keys of Cognitive Services. | a97b65f3-24c7-4388-baec-2e87135dc908 |
| 34 | Foundry Account Owner | Grants full access to manage AI projects and accounts. Includes an ABAC condition to constrain role assignments. Grants conditional assignment of the Foundry User role to other user principles. Applies for new Foundry resources. | e47c6f54-e4a2-4754-9501-8e0985b135e1 |
| 35 | Foundry Owner | Grants full to manage AI project and accounts. Grants reader access to AI projects, reader access to AI accounts, and data actions for an AI project. Applies for new Foundry resources. | c883944f-8b7b-4483-af10-35834be79c4a |
| 36 | Foundry Project Manager | Lets you perform developer actions and management actions on Foundry Projects. Includes an ABAC condition to constrain role assignments. Allows for making role assignments, but limited to Foundry User role. Applies for new Foundry resources. | eadc314b-1a2d-4efa-be10-5d325db5065e |
| 37 | Foundry User | Grants reader access to Foundry projects, reader access to Foundry accounts, and data actions for an Foundry project. | 53ca6127-db72-4b80-b1b0-d745d6d5456d |
| 38 | Healthcare Agent Admin | Users with admin access can sign in, view and edit all of the bot resources, scenarios and configuration setting including the bot instance keys & secrets. | f1082fec-a70f-419f-9230-885d2550fb38 |
| 39 | Healthcare Agent Editor | Users with editor access can sign in, view and edit all the bot resources, scenarios and configuration setting except for the bot instance keys & secrets and the end-user inputs (including Feedback, Unrecognized utterances and Conversation logs). A read-only access to the bot skills and channels. | af854a69-80ce-4ff7-8447-f1118a2e0ca8 |
| 40 | Healthcare Agent Reader | Users with reader access can sign in, have read-only access to the bot resources, scenarios and configuration setting except for the bot instance keys & secrets (including Authentication, Data Connection and Channels keys) and the end-user inputs (including Feedback, Unrecognized utterances and Conversation logs). | eb5a76d5-50e7-4c33-a449-070e7c9c4cf2 |
| 41 | Search Index Data Contributor | Grants full access to Azure Cognitive Search index data. | 8ebe5a00-799e-43f5-93ac-243d3dce84a7 |
| 42 | Search Index Data Reader | Grants read access to Azure Cognitive Search index data. | 1407120a-92aa-4202-b7e9-c0e197c71c8f |
| 43 | Search Service Contributor | Lets you manage Search services, but not access to them. | 7ca78c08-252a-4471-8644-bb5ff32d4ba0 |

---

## Internet of Things

| SNo | Built-in Role | Description | ID |
|---|---|---|---|
| 1 | Azure Device Registry Administrator | Azure Device Registry Administrator | 12675fd7-7f59-493f-9201-f7944860a2f1 |
| 2 | Azure Device Registry Contributor | Allows for full access to IoT devices within Azure Device Registry Namespace. | a5c3590a-3a1a-4cd4-9648-ea0a32b15137 |
| 3 | Azure Device Registry Credentials Contributor | Allows for full access to manage credentials and policies within Azure Device Registry Namespace. | 09267e11-2e06-40b5-8fe4-68cea20794c9 |
| 4 | Azure Device Registry Onboarding | Allows for full access to Azure Device Registry Namespace and X.509 certificate provisioning. | 547f7f0a-69c0-4807-bd9e-0321dfb66a84 |
| 5 | Azure Digital Twins Data Owner | Full access role for Digital Twins data-plane | bcd981a7-7f74-457b-83e1-cceb9e632ffe |
| 6 | Azure Digital Twins Data Reader | Read-only role for Digital Twins data-plane properties | d57506d4-4c8d-48b1-8587-93c323f6a5a3 |
| 7 | Azure IoT Operations Administrator | View, create, edit and delete AIO resources. Manage all resources, including instance and its downstream resources. | 5bc02df6-6cd5-43fe-ad3d-4c93cf56cc16 |
| 8 | Azure IoT Operations Onboarding | User can Azure arc connect and deploy Azure IoT Operations securely. | 7b7c71ed-33fa-4ed2-a91a-e56d5da260b5 |
| 9 | Device Provisioning Service Data Contributor | Allows for full access to Device Provisioning Service data-plane operations. | dfce44e4-17b7-4bd1-a6d1-04996ec95633 |
| 10 | Device Provisioning Service Data Reader | Allows for full read access to Device Provisioning Service data-plane properties. | 10745317-c249-44a1-a5ce-3a4353c0bbd8 |
| 11 | Device Update Administrator | Gives you full access to management and content operations | 02ca0879-e8e4-47a5-a61e-5c618b76e64a |
| 12 | Device Update Content Administrator | Gives you full access to content operations | 0378884a-3af5-44ab-8323-f5b22f9f3c98 |
| 13 | Device Update Content Reader | Gives you read access to content operations, but does not allow making changes | d1ee9a80-8b14-47f0-bdc2-f4a351625a7b |
| 14 | Device Update Deployments Administrator | Gives you full access to management operations | e4237640-0e3d-4a46-8fda-70bc94856432 |
| 15 | Device Update Deployments Reader | Gives you read access to management operations, but does not allow making changes | 49e2f5d2-7741-4835-8efa-19e1fe35e47f |
| 16 | Device Update Reader | Gives you read access to management and content operations, but does not allow making changes | e9dba6fb-3d52-4cf0-bce3-f06ce71b9e0f |
| 17 | Firmware Analysis Admin | Administrative user that can upload/view firmwares & configure firmware workspaces | 9c1607d1-791d-4c68-885d-c7b7aaff7c8a |
| 18 | Firmware Analysis Reader | View firmware images but not upload them or perform any workspace configuration | 2a94a2fd-3c4f-45d1-847d-6585ba88af94 |
| 19 | Firmware Analysis User | Upload and analyze firmware images but not perform any workspace configuration | 53b2724d-1e51-44fa-b586-bcace0c82609 |
| 20 | IoT Hub Data Contributor | Allows for full access to IoT Hub data plane operations. | 4fc6c259-987e-4a07-842e-c321cc9d413f |
| 21 | IoT Hub Data Reader | Allows for full read access to IoT Hub data-plane properties | b447c946-2db7-41ec-983d-d8bf3b1c77e3 |
| 22 | IoT Hub Registry Contributor | Allows for full access to IoT Hub device registry. | 4ea46cd5-c1b2-4a8e-910b-273211f9ce47 |
| 23 | IoT Hub Twin Contributor | Allows for read and write access to all IoT Hub device and module twins. | 494bdba2-168f-4f31-a0a1-191d2f7c028c |

---

## Identity

| SNo | Built-in Role | Description | ID |
|---|---|---|---|
| 1 | Domain Services Contributor | Can manage Azure AD Domain Services and related network configurations | eeaeda52-9324-47f6-8069-5d5bade478b2 |
| 2 | Domain Services Reader | Can view Azure AD Domain Services and related network configurations | 361898ef-9ed1-48c2-849c-a832951106bb |
| 3 | Managed Identity Contributor | Create, Read, Update, and Delete User Assigned Identity | e40ec5ca-96e0-45a2-b4ff-59039f2c2b59 |
| 4 | Managed Identity Operator | Read and Assign User Assigned Identity | f1a07417-d97a-45cb-824c-7a7467783830 |



