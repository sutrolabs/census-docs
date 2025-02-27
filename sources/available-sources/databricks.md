---
description: >-
  Learn how to configure Databricks for use by Census and why those permissions
  are needed.
---

# Databricks

Databricks is a popular data warehouse for data engineering and data science thanks to its deep emphasis on Apache Spark, as well as SQL.

Census supports a wide set of Databricks deployments including

* Unity Catalog
* SQL Warehouses (including Serverless)
* All Databricks LTS versions up to and including 14.3, and new versions typically work without issue.

Census supports both [Basic and Advanced Sync Engines](../overview/#sync-engines) on Databricks.

{% hint style="success" %}
If you'd like to skip these steps, you can use [Databricks built-in Partner Connect](https://docs.databricks.com/en/partners/reverse-etl/census.html) to set up a new connection to Census.
{% endhint %}

## Required Permissions

If using the Advanced Sync Engine and the CENSUS schema has not already been created, you'll need to create the schema and grant permissions. Databricks uses a different form of authentation that most databases. When connecting to Databricks, you'll be able to use either a [Personal Access Tokens](https://docs.databricks.com/en/dev-tools/auth/pat.html) or a [Service Principal](https://docs.databricks.com/en/admin/users-groups/service-principals.html).

For Personal Access Tokens, run:

```
CREATE SCHEMA IF NOT EXISTS CENSUS;

-- For personal access tokens, use an email address:
GRANT USE SCHEMA, SELECT, CREATE TABLE, MODIFY ON SCHEMA [your_default_catalog].CENSUS TO `user_you_plan_use_with_pat@yourcompany.com`;

-- For service principals, use the client ID:
GRANT USE SCHEMA, SELECT, CREATE TABLE, MODIFY ON SCHEMA [your_default_catalog].CENSUS TO `service-principal-clientid-guid`;
```

## Configuring a new Databricks connection

1. First, you'll need to select which form of access credentials to use: [Service Principal](https://docs.databricks.com/en/admin/users-groups/service-principals.html) (Recommended, but a bit more work) or [Personal Access Tokens](https://docs.databricks.com/en/dev-tools/auth/pat.html).
   * If you're using a Service Principal, within your Databricks Account Console, go to the [User management page and Service Principals tab](https://accounts.cloud.databricks.com/users/serviceprincipals/).
     1. Create a new service principal with the **Add service principal** button. Give it a name you'll remember such as Census. You can also reuse an existing one.
     2. Once created, click **Generate secret** which will create a new Client ID and Secret pair. Keep this somewhere safe as you won't be able to access it again.
     3. Now you'll need to add the service principal as an admin on the specific Workspace you are connecting to. In your Databricks Account console, go the [Workspaces page](https://accounts.cloud.databricks.com/workspaces). Click on the name of your workspace and go to the **Permissions** tab.
     4. Select your new service principal and mark them as **admin** on the workspace.
   * If you're using **Personal Access Token**, you can create this for yourself. Alternatively, may want to create a new specific user account for Census to use for auditing and access control.
     1. You'll first need to navigate into the specific Workspace you are connecting to. In your Databricks Account console, go the [Workspaces page](https://accounts.cloud.databricks.com/workspaces). Select the workspace you'd like Census to connect to and then click **Open workspace** in the top right.
     2. Clicking on your **Profile Icon** in the top right and selecting **Settings**. Then click the **Developer** option in the left settings menu and click on **Manage** next to Access Tokens. We recommend you create a new Access Token:
        * Name: Census (or some other details)
        * Lifetime: (clear the box) - This will prevent the token from expiring ![](../../.gitbook/assets/screely-1619628186696.png)
2. If you're not already, go into your target workspace by visiting the [Workspaces page](https://accounts.cloud.databricks.com/workspaces) and clicking the **Open** link next to it. Now within your selected Workspace, select **Compute** from the left menu. Census can connect to a SQL Warehouse or All Purpose Cluster. You can reuse an existing compute resource, or create a new one here. Click on the Compute you've decided to use.

* Note: Service Principals cannot be connected to All Purpose Clusters that are in the **Single User Access Mode**.

3.  You'll need to collect three credentials to connect to your compute:

    * Hostname
    * Port
    * HTTP Path

    For SQL Warehouses, switch to the **Connection details** tab.

    For All Purpose Clusters, in the **Configuration** tab, open the **Advanced Options** section at the bottom, then select the **JDBC/ODBC** section.

    ![](../../.gitbook/assets/screely-1619627622845.png)
4.  **All Purpose Clusters only** - Add the following configuration parameters to your cluster. These are also in **Advanced Options** section at the bottom under the **Spark** section.

    ```
    spark.hadoop.fs.s3n.impl.disable.cache true
    spark.hadoop.fs.s3.impl.disable.cache true
    spark.hadoop.fs.s3a.impl.disable.cache true
    ```
5. Now you're ready to add the connection to Census. Visit the [Sources page](https://app.getcensus.com/sources) in Census, and click **New Source**, selecting **Databricks** from the menu.
   * Select the [Sync Engine](../overview/#sync-engines) you'd like to use. Note that this cannot be changed once the connection is created.
   * Provide the connection credentials: Hostname, Port, HTTP Path
   * Select your credential type (Personal Access Token or Service Principal), and provide the corresponding Access Token, or Client ID & Secret.
   * Optionally, set the Database Allow List. This will filter the SCHEMAS that appear in Census. Note that if you are using unity catalog, this filtering will apply across all catalogs.
6. After the connection is saved, go ahead and press the **Test** button. This will validate that you've completed the above steps correctly. Once you've got a checkmark for all four steps, you're good to go!

## Allowed IP Addresses

If you're using Databricks's Allowed IPs network policy, you'll need to add these Census IP addresses to your list. You can find Census's set of IP address for your region in [Regions & IP Addresses](../../misc/security-and-privacy/regions-and-ip-addresses.md#ip-addresses). Visit the [Databricks Documentation](https://docs.databricks.com/en/security/network/front-end/ip-access-list.html) for more details on how to specify these IPs as part of your network policy.

## Need help connecting to Databricks?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
