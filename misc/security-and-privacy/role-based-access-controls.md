---
description: >-
  Role-Based Access Controls (RBAC) let you manage the set of permissions an
  individual user has.
---

# Role-based Access Controls

RBAC provides peace of mind, ensuring only those with appropriate permissions can access sensitive user information or take potentially destructive actions with Census Syncs or Census configuration.

{% hint style="info" %}
Role-Based Access Controls are available on Enterprise plans only. Professional plans can create up to two Workspaces.
{% endhint %}

## Organization Administrators

Members of a Census organization may be promoted to Administrators, which will give them Owner permissions in all [Workspaces](workspaces.md) and the ability to manage billing, and Organization level settings.

Users who are not an admin are simply Members of the organization. Members must be added to each workspace individually.

## Workspaces and Roles

Each member of a workspace has a role within each (and their roles can vary across workspaces).

* **Owner** – This gives access to everything within the workspace, including managing warehouse & destination connections, API keys, and adding/removing users. Organization Admins have all the same permissions as Owners within a workspace.&#x20;
* **Editor** – This role allows users to create datasets, segments, and syncs, but does not give the ability to create or manage connections
* **Operator** – The Operator Role is a special role within Census. It fits between the Editor and Viewer permissions, allowing members with this role to primarily work with Segments. Operators are able to create and edit segments, as well as manage syncing datasets and segments. They won't be able create new datasets, or modify any existing connections details.
* **Viewer** - The read-only viewer on Census. They can view syncs and segments, and approved models, but cannot modify or take any action within Census.

<table><thead><tr><th width="295">Action</th><th width="108">Viewer</th><th width="112">Operator</th><th width="101">Editor</th><th width="119">Owner</th></tr></thead><tbody><tr><td>View Warehouse Connections</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create &#x26; Manage Warehouse Connections</td><td></td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create &#x26; Manage dbt / Looker Connections</td><td></td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create &#x26; Manage Org-level Fivetran &#x26; dbt Cloud Integrations</td><td></td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>View Destination Connections</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create Destination Connections</td><td></td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Manage Destination Connections</td><td></td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create custom objects, audiences, and tables in destination</td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Preview Sample for Datasets</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Query Models</td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create &#x26; Edit Datasets</td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create &#x26; Edit Segments</td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create &#x26; Modify Exclusion Lists</td><td></td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>View Syncs</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create, Edit &#x26; Run Syncs on Segments &#x26; Datasets*</td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create, Edit &#x26; Run Syncs on Datasets, Tables &#x26; Views</td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Invite New Users</td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Manage Member Roles</td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Remove Members from Workspaces</td><td></td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create, Manage, Delete Workspaces</td><td></td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create &#x26; Manage API Keys</td><td></td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr></tbody></table>

## Custom Roles

You can also create custom roles by combining the required set of fine-grained permissions into a role that is then assignable to users in any workspace. Custom roles give you the ability to create narrow roles for specific use cases such as connection administration or data definition.&#x20;

{% hint style="info" %}
Note: Custom Roles do not yet give access to Organization-level management permissions such as billing managements.
{% endhint %}

To create a new custom role,

1. Click on the **Workspaces selector** at the top of the left navigation and click [Organization Home](https://app.getcensus.com/home/workspaces).
2. Click on the **Roles** tab.
3. Click **+ New Role**
4. Give your New Role a name.&#x20;
5. You may also optionally pick an existing role to use as a starting point. Note that once your new role is created, there's no lasting association with this role, this is purely to save yourself some clicks setting up your new role.&#x20;
6. Select the combination of permissions your new role needs and then click **Save**.

You can also manage the permissions of existing roles here. Modifying the permissions of an existing will take effect immediately on any user assigned to that role (though they may need to refresh their browser session to see it in the Census UI, it will be enforced immediately if they try to take a now blocked action).

### Available Permissions

Custom roles are a collection of permissions granted to the user within that workspace. They are organized as follows:

* **Subject** - The type of resource (or group of related resources) that the set of permissions apply to, such as a connection, sync or dataset.
* **Permission** - The specific allowed type of action that can be taken on the subject.

<table><thead><tr><th width="218">Subject</th><th width="190">Permissions</th><th>Description</th></tr></thead><tbody><tr><td><a href="../developers/">API Token</a></td><td>Read, Manage </td><td>Most Census API endpoints today are accessed via a shared API token defined for each Workspace.</td></tr><tr><td><a href="workspaces.md">Workspace</a></td><td>Update, Read Members, Remove User</td><td>Manage the configuration associated with the workspace, including listing and removing members.</td></tr><tr><td>Workspace Member</td><td>Manage [Role]</td><td>Specifically grants the ability to invite, assign, or revoke a particular role for members in the workspace. <br><br>The Custom Role version applies to all custom roles so should only be used for admin roles. </td></tr><tr><td>Connections</td><td>Test, Create, Update, or Destroy</td><td>Permissions that apply to the creation and management of both <a href="../../sources/">source</a> and <a href="../../destinations/available-destinations/">destination</a> connections. <br><br>Note: All members of the workspace will be able to see the existence of any connections regardless of permissions.</td></tr><tr><td><a href="../../audience-hub/getting-started/">Segment</a></td><td>Read, Create, Update, Destroy</td><td>Permissions related to listing, creating, updating, and destroying Segments.</td></tr><tr><td><a href="../../audience-hub/getting-started/segment-priorities.md">Segment Priority Lists</a></td><td>Read, Create, Update, Destroy</td><td>Permissions scoped specifically to the Segment Priority List functionality used to manage overlapping segments.</td></tr><tr><td><a href="../../audience-hub/data-preparation-1/exclusion-lists.md">Segment Exclusion Lists</a></td><td>Read, Create, Update, Destroy</td><td>Similarly scoped permissions for managing exclusion lists set up within Audience Hub.</td></tr><tr><td><a href="../../audience-hub/analyzing-segments/">Cohorts</a></td><td>Read, Create, Update, Destroy</td><td>Similarly scoped permissions for managing experiments created on top of Audience Hub segments</td></tr><tr><td><a href="../../datasets/ai-columns/">Smart Columns</a></td><td>Read, Create, Update, Destroy</td><td>Permissions controlling access to smart columns, including computed columns, formula columns, and AI columns</td></tr><tr><td><a href="../../audience-hub/analyzing-segments/">Metrics</a></td><td>Read, Create, Update, Destroy</td><td>Scoped permissions for setting up performance metrics used to measure segment performance in Audience Hub.</td></tr><tr><td><a href="broken-reference">Sync Configuration</a></td><td>Read, Create, Update, Destroy</td><td>Standard operations for creating and managing syncs</td></tr><tr><td></td><td>Read, Create, Update, Destroy from dataset or segment</td><td>Scoped versions of the above operations limiting sync creation to only existing datasets or segments. Used by the built-in Operator role. </td></tr><tr><td></td><td>Run, Full Sync</td><td>Grants the ability to manually trigger a sync or full sync</td></tr><tr><td></td><td>Access Sync Tracking</td><td>Download and search detailed <a href="../../syncs/sync-monitoring/sync-tracking.md">sync tracking logs</a></td></tr><tr><td></td><td>Manage Subscriptions</td><td>Control which users will be <a href="../../syncs/sync-monitoring/alerts.md">alerted if a sync</a> encounters an issue.</td></tr><tr><td><a href="../../sources/integrations/looker.md">Project</a></td><td>Read, Create, Update, Destroy</td><td>Standard operations for managing Dataset project/repositories.</td></tr><tr><td><a href="broken-reference">Dataset</a></td><td>Read, Create, Update, Destroy</td><td>Standard operations for creating and editing datasets, such as SQL queries.</td></tr><tr><td><a href="../developers/gitlink.md">Gitops Project</a></td><td>Read, Create, Update, Destroy</td><td>Standard operations for enabling and managing Git Link [Available in Private Beta]</td></tr><tr><td><a href="../developers/entity-api.md">Dataset API</a></td><td>Read, Create, Update, Destroy</td><td>Standard operations for enabling and managing Dataset API</td></tr><tr><td><a href="../../syncs/sync-monitoring/datadog-integration.md">Datadog Integration</a></td><td>Read, Create, Update, Destroy</td><td>Standard operations for enabling and managing the datadog integration for each workspace</td></tr><tr><td>Navigation</td><td>Visit Syncs, Segments, Datasets, Connections, Settings</td><td>Controls access to the various navigation sections of Census. These permission primarily controls navigation itself, not access to underlying resources, which are managed by other permissions.  </td></tr></tbody></table>





## Disabling Data Previews

Census provides sample data when working with models, segments, and syncs to help users understand their data sets, as well as what's being synced. Some organizations may prefer to restrict the ability to preview data to specific tools.

<figure><img src="../../.gitbook/assets/Disable Data Previews (2).png" alt=""><figcaption></figcaption></figure>

In this case, you can choose to disable the ability to preview data in Census on a per workspace basis. To disable data previews in Census, reach out to your success manager or send an email to [Census Support](mailto:support@getcensus.com).
