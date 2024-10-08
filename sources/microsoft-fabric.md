---
description: This page describes how to use Microsoft Fabric as a source in Census.
---

# Microsoft Fabric

Microsoft Fabric is an all-in-one analytics platform created for businesses and data professionals. It unifies several Microsoft and Azure data products together under one operating console. Because it includes many different data products, it can be configured in a number of different ways. We'll cover the most common deployment model of Census and Microsoft Fabric together but other approaches may make more sense for your particular environment.

The process of requires a number of steps:

1. Creating a service principal
2. Granting that service principal access to your Fabric workspace
3. Selecting (or provisioning) the data resource within the workspace
4. Creating a Census connection using that service principal and SQL endpoint

## Creating a service principal

The first step is to create a service principal and their associated credentials. You'll give Census access to this service principal to access Fabric resources. You should create a new service principal for Census, but you can use the service principal to give Census access to multiple Fabric resources if necessary.

Microsoft's terminology is a bit scattered here. They also refer to a Service Principal as an Application, App registration, or Registration.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. In the navigation menu, select **Microsoft Entra ID** (formerly Azure Active Directory).
3. Click **App registrations** under **Manage** and then click **+ New registration**.
4. Enter a Name for your application such as "Fabric Connection for Census". In the **Supported account types** section, select **Accounts in this organizational directory only** and click **Register**.
5. Make a note of the Application (client) ID and Directory (tenant) ID. You will use them later to connect Census.
6. Now we'll need to create a secret for this application. Re-select the application you just created.
7. On the navigation menu, click **Certificates & secrets** and then click **+ New client secret**.
8. In the Add a client secret pane, enter a Description for the client secret, eg "Census Credentials"
9. In the Expires drop-down menu, select the longest expiry period you are comfortable with. Unlimited is unfortunately not an option. We recommend setting a reminder prior to when this credential will expire to refresh it.
10. Click Add.
11. Make a note of the client secret.

### Configuring Fabric to allow external access via service principals
If you're already using Fabric with other external integrations, you likely have performed these steps already but nonetheless, please confirm your configuration matches these options.

1. Log in to your [Microsoft Fabric account](https://app.fabric.microsoft.com/home).
2. Click **Synapse Data Engineering**.
3. In the top right, click the **Settings** icon, under **Governance and insights**, select **Admin portal**.
4. In the navigation menu, select **Tenant** settings.
5. In the **Developer settings** section, set the **Service principals can use Fabric APIs** toggle to ON.
6. In the **OneLake settings** section, set the **Users can access data stored in OneLake with apps external to Fabric** toggle to ON.

## Granting the service principal access to your workspace

Any resources you wish to connect to must also be placed in a shared workspace. If you've only been using the default "My Workspace", you will need to create a new shared workspace:

1. On the navigation menu, click **Workspaces** and then click **+ New workspace**.
2. Enter a **Name** for the workspace (example "Shared Workspace") and click **Apply**.

Once you have a shared workspace, you'll need to grant your new service principal access to the workspace.

1. Select the workspace and then click **Manage Access**.
2. Click **+ Add people or groups**.
3. Select the name of the service principal you created in Step 1. If it doesn't appear, make sure you've enabled the Service principals can use Fabric APIs setting above.
4. In the drop-down menu, select Contributor.

The service principal can now access any resource within the workspace given the appropriate SQL Endpoint.

## Configuring access to warehouse or other SQL endpoint

Census can access any resource that exposes a SQL Endpoint. Census recommends using a Warehouse resource or Lakehouse.

If you do not already have a Lakehouse, you can create one:
1. Enter your workspace and click **+ New Item**.
2. From the various data engineering items, select **Warehouse**.
3. Enter a unique Name for your lakehouse and click **Create**.

Whether you're creating a new warehouse or using an existing one, the last detail you'll need is its SQL Endpoint
1. Within the top level items list of your workspace, hover over the warehouse, lakehouse, or other resource and click on the **...** to open the menu and then click **Settings**.
2. Make a note of the **SQL connection string**, this will be the hostname.

You should now have everything you need to connect to Microsoft Fabric.

## Creating a connection

Once you've created your credentials, you can create a source connection within Census.

* Open Census and navigate to the **Sources** page.
* Click **New Source** and select Microsoft Fabric from the list.
* Provide the four credential details you created in the last step:
  * Hostname (aka SQL endpoint or SQL connection string),
  * Yenant ID (aka Directory ID),
  * Client ID (aka Application ID)
  * Client secret (aka Client secret value, __not__ Client secret ID)
* You’re all set! Head over to the **Syncs** page to activate your data.

## Allowed IP Addresses

You can add Census's IP addresses in your firewall to only allow traffic originating from Census to access your Microsoft Fabric account. You can specify IP addresses to allow as part of [Microsoft Entra's conditional access](https://learn.microsoft.com/en-us/fabric/security/protect-inbound-traffic#entra-conditional-access).

You can find Census's set of IP address for your region in [Regions & IP Addresses](../basics/security-and-privacy/regions-and-ip-addresses.md#ip-addresses).

## Notes

As of October 2024, Microsoft Fabric only supports our [Basic Sync Engine](overview.md#sync-engines).

## Need help connecting to Microsoft Fabric?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
