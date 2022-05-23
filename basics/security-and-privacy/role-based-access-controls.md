# Role-Based Access Controls

Role-Based Access Controls (RBAC) give Census users the ability to control which members of the organization can access information or take particular actions. RBAC provides peace of mind, ensuring only those with appropriate permissions can access sensitive user information or take potentially destructive actions with Census Syncs or Census configuration.

{% hint style="info" %}
Role-Based Access Controls are available for Business and Platform plans.&#x20;
{% endhint %}

### Managing Roles

Each member of a Census Organization has a specific role associated with them. When new members are invited, you will need to indicate what permissions they should have once they've joined. Admins and Editors invite others, but only up to the level of permissions they themselves have.&#x20;

Census provides four different roles:

* **Admin** – This is the default permission inside a new Census Organization. It gives the user access to everything, including managing authentication mechanisms, billing and plan details, API keys, and adding/removing users.&#x20;
* **Editor** – This role grants access to most things in Census including adding and removing connections, in addition to creating and editing syncs and models.&#x20;
* **Operator** – The Operator Role is a special role with Census. It fits between the Editor and Viewer permissions, allowing members with this role to create and edit syncs as long as they're associated with [Broken link](broken-reference "mention").
* **Viewer** - The read-only viewer on Census. They can view syncs and segments, and approved models, but cannot modify or take any action within Census.&#x20;



Access Details

| Permission              | Viewer      | Operator           | Editor       | Admin                |
| ----------------------- | ----------- | ------------------ | ------------ | -------------------- |
| **Data Source**         |             |                    |              |                      |
| Warehouse Configuration | View        | View               | View         | Manage               |
| dbt / Looker            |             |                    | View         | Manage               |
| **Destinations**        |             |                    |              |                      |
| Connection              | View        | View               | Create       | Manage               |
| **Models**              |             |                    |              |                      |
| Query                   | On Approved | On Approved        | All          | All                  |
| Create/Edit             |             |                    | Yes          | Yes                  |
| Approve                 |             |                    | Yes          | Yes                  |
| **Segments**            |             |                    |              |                      |
| Create/Edit             |             | Yes                | Yes          | Yes                  |
| **Syncs**               |             |                    |              |                      |
| Configuration           | View        | Manage on Approved | Manage       | Manage               |
| Run                     |             | On Approved        | Yes          | Yes                  |
| **User Manage**         |             |                    |              |                      |
| Invite                  |             |                    | Up to Editor | With Any Permissions |
| Manage Users            |             |                    |              | Yes                  |
| Manage SSO              |             |                    |              | Yes                  |
| **Administration**      |             |                    |              |                      |
| Billing & Plan          |             |                    |              | Yes                  |
| dbt Cloud               |             |                    |              | Yes                  |
| GitHub                  |             |                    |              | Yes                  |
| API Keys                | View        | View               | View         | Manage               |

