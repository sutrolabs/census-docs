---
description: Manage audiences programmatically from your data warehouse.
---

# Warehouse-Managed Audiences

Warehouse-Managed Audiences enable data teams to manage audiences programmatically from the warehouse, while taking full advantage of all the features that come with Audience Hub.

### Data Models

<figure><img src="../../.gitbook/assets/erd.png" alt=""><figcaption></figcaption></figure>

To get started with Warehouse-Managed Audiences, you'll need to define three models in Census that map to tables in your warehouse:

1. **Audiences**: A list of all audiences you plan to model in your warehouse.
   1. Required columns: `id` and `name`
   2. Optional columns: `description`
2. **People**: Also known as contacts, customers, users, etc., this is a list of all people belonging to every audience you plan to model in your warehouse.
   1. Required columns: `id`
   2. Optional columns: other user attributes (email, phone, first/last name, IDFA, GAID, etc.)
3. **Audience Memberships**: A join table that tells Census which people are in each audience. Each row must include a unique pair of person and audience identifiers.
   1. Required columns: `person_id` and `audience_id`

#### **Example Data**

_Audiences_

<table><thead><tr><th width="108.33333333333331">id</th><th width="232">name</th><th>description</th></tr></thead><tbody><tr><td>201</td><td>VIP Customers</td><td>A list of all VIP customers.</td></tr><tr><td>202</td><td>All Customers (US)</td><td>Customers in the US only.</td></tr><tr><td>203</td><td>All Customers (EU)</td><td>Customers in the EU only.</td></tr><tr><td>204</td><td>Webinar Attendees</td><td>From webinar on Feb 22.</td></tr></tbody></table>

_People_

<table><thead><tr><th width="108">id</th><th width="323">email</th><th>phone</th></tr></thead><tbody><tr><td>101</td><td>michaelorr@stanley-dunlap.com</td><td>762-947-7170</td></tr><tr><td>102</td><td>brendasmith@hotmail.com</td><td>619-362-2778</td></tr><tr><td>103</td><td>kevin12@gmail.com</td><td>612-550-3366</td></tr><tr><td>104</td><td>jerryrichardson@young.com</td><td>258-830-6056</td></tr><tr><td>105</td><td>shane87@gmail.com</td><td>505-903-2266</td></tr></tbody></table>

_Audience Membership (Join Table)_

| person\_id | audience\_id |
| ---------- | ------------ |
| 101        | 201          |
| 101        | 203          |
| 102        | 201          |
| 103        | 204          |

### Dataset Definitions

{% hint style="info" %}
This process should be done with the help of your Census representative, who can talk through any questions during setup.
{% endhint %}

#### **Part 1**: Entities

Next, create a dataset for each of the three models. This will allow you to provide some additional metadata to help Census understand the shape of your data and how its related.

Audiences model -> Create an **Audience** type dataset:

<figure><img src="../../.gitbook/assets/CleanShot 2024-01-11 at 16.30.25@2x.png" alt=""><figcaption></figcaption></figure>

Person model -> Create a **Person** type dataset:

<figure><img src="../../.gitbook/assets/CleanShot 2024-01-11 at 16.29.45@2x.png" alt=""><figcaption></figcaption></figure>

Audience Membership model -> Create a **Join Table** type dataset:

<figure><img src="../../.gitbook/assets/CleanShot 2024-01-11 at 16.30.14@2x.png" alt=""><figcaption></figcaption></figure>

#### **Part 2**: Dataset relationships

<figure><img src="../../.gitbook/assets/CleanShot 2024-01-11 at 16.33.42@2x.png" alt=""><figcaption></figcaption></figure>

Finally, specify how these entities relate to each other by setting up relationships between them.

Connect the **Person** dataset to the **Audience Membership** dataset with a **One-to-Many** relationship:

<figure><img src="../../.gitbook/assets/CleanShot 2024-01-11 at 16.30.52@2x.png" alt=""><figcaption></figcaption></figure>

Connect the **Audience** dataset to the **Audience Membership** dataset with a **One-to-Many** relationship:

<figure><img src="../../.gitbook/assets/CleanShot 2024-01-11 at 16.35.00@2x.png" alt=""><figcaption></figcaption></figure>

### Finalize Setup

Once your datasets are set up, your Census representative can finalize your configuration. You should see your imported audience segments populate in Census. You can distinguish them from audiences defined in the UI based on the "Managed" tag that appears next to the segment name.

<figure><img src="../../.gitbook/assets/audience-list (2).png" alt=""><figcaption></figcaption></figure>

## FAQ

**How do I update the membership of an audience?**

Audience membership information lives in the audience membership model (join table). Any time a Warehouse-Managed Audience is queried in Census, we make a just-in-time query to this table. Thus, adding and removing rows from the audience membership model will update the membership of an audience.

**How often are audiences refreshed by Census?**

To determine the list of Warehouse-Managed Audiences shown in the Census UI (see below), Census runs a background job every 15 minutes which looks at your Audiences model and creates/updates/deletes the audiences accordingly.

<figure><img src="../../.gitbook/assets/audience-list (3).png" alt=""><figcaption></figcaption></figure>

Census determines which people are members of those audiences by querying your Audience membership table in real-time. Thus, if you preview a Warehouse-Managed Audience or run a sync based on one, Census will always be looking at the most current data in the data warehouse.

**What happens if a row is added/updated/deleted from my audiences table?**

Any changes to the Audiences table will be reflected in the respective audiences during the audience refresh:

* **Row was added**: A new audience will be created on the next refresh
* **Row was updated**: The matching audience will be renamed in Census on the next refresh. This will not impact the name of any audiences in your downstream destinations.
* ⚠️ **Row was removed**: The matching audience will be marked as invalid on the next refresh. Any related syncs will begin to fail. You will have the option to manually delete the audience in Census, or re-add the row (if it was removed by mistake).

**What happens if I delete my Person/Audience/Join Table dataset?**

Any audience segments managed by the Warehouse-Managed Audience feature will no longer be considered valid. Refreshes may not work properly.

**What happens if I modify my Person/Audience/Join Table relationships?**

Any audiences managed by the Warehouse-Managed Audience feature will no longer be considered valid. Refreshes may not work properly.

**Can I delete audiences managed by this feature?**

You are not able to manually delete managed audiences through the Census UI. If you’d like to remove all of your managed audiences and disable this feature, please reach out to a Census representative.

**Can I use \<X> feature with Warehouse-Managed Audiences?**

Any feature that is available for audiences built in the Census UI is available for Warehouse-Managed Audiences.

**How can I turn off Warehouse-Managed Audiences and opt back out of this feature?**

Reach out to your Census account manager, or email support@getcensus.com.
