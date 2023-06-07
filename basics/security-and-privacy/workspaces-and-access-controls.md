---
description: >-
  Role-Based Access Controls (RBAC) & Workspaces give Census users the ability
  to control which members of the organization can access information or take
  particular actions.
---

# Workspaces & Access Controls

RBAC provides peace of mind, ensuring only those with appropriate permissions can access sensitive user information or take potentially destructive actions with Census Syncs or Census configuration.

{% hint style="info" %}
Role-Based Access Controls are available on Platform plans only. Core plans can create up to two Workspaces.
{% endhint %}

### Organization Administrators

Members of a Census Organization may be promoted to Administrators, which will give them Owner permissions in all [Workspaces](workspaces-and-access-controls.md#workspaces) and the ability to manage billing, and Organization level settings.

### Workspaces

Census Workspaces allow you to manage permissions granularly for different teams or use-cases. Give your Sales team and your Marketing team their own little slice of Census or keep your staging environment separate from prod. The list of Workspaces in your organization is always visible to all members of your organization, but you can control the level of access for members by assigning them a role.

#### Workspace Roles

Workspace members each have one of four different roles:

* **Owner** – This is the default permission for [Organization Administrators](workspaces-and-access-controls.md#account-administrators) within a Census Organization. It gives the user access to everything, including managing warehouse & destination connections, API keys, and adding/removing users.
* **Editor** – This role grants access to most things in the workspaces including adding destination connections, in addition to creating and editing syncs and models.
* **Operator** – The Operator Role is a special role within Census. It fits between the Editor and Viewer permissions, allowing members with this role to primarily work with Segments. Operators are able to create and edit [audience-hub](../audience-hub/ "mention") on top of [entities.md](../data-models-and-entities/entities.md "mention"), as well as manage syncing entities and segments. They won't be able create new models, entities, or modify any existing connections details
* **Viewer** - The read-only viewer on Census. They can view syncs and segments, and approved models, but cannot modify or take any action within Census.

**Access Details**

<table><thead><tr><th width="295">Action</th><th width="108">Viewer</th><th width="112">Operator</th><th width="101">Editor</th><th width="119">Owner</th></tr></thead><tbody><tr><td>View Warehouse Connections</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create &#x26; Manage Warehouse Connections</td><td></td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create &#x26; Manage dbt / Looker Connections</td><td></td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>View Destination Connections</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create Destination Connections</td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Manage Destination Connections</td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Preview Sample for Entities</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Query Models</td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create &#x26; Edit Models &#x26; Entities</td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create &#x26; Edit Segments</td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>View Syncs</td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create, Edit &#x26; Run Syncs on Approved Models</td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create, Edit &#x26; Run Syncs on Non-Approved Models</td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Invite new users</td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Manage member roles</td><td></td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>View API Key</td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr><tr><td>Create &#x26; Delete API Key</td><td></td><td></td><td></td><td><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></td></tr></tbody></table>

#### Creating a Workspace

To get started creating a new Workspace, hit the "Create Workspace" button from your [organization dashboard](https://app.getcensus.com/home). Then simply name your new Workspace and you're done!

<figure><img src="../../.gitbook/assets/Screen Shot 2022-11-22 at 12.12.58 PM.png" alt=""><figcaption></figcaption></figure>

## Disabling Data Previews

Census provides sample data when working with models, segments, and syncs to help users understand their data sets, as well as what's being synced. Some organizations may prefer to restrict the ability to preview data to specific tools.

<figure><img src="../../.gitbook/assets/Disable Data Previews (2).png" alt=""><figcaption></figcaption></figure>

In this case, you can choose to disable the ability to preview data in Census on a per workspace basis. To disable data previews in Census, reach out to your success manager or send an email to [Census Support](mailto:support@getcensus.com).
