# Entity Resolution

Business teams are dependent on trusted data to execute their growth initiatives. However, often the data is messy. One core reason for the messy data is to have duplicate records for various entities - Users, Organizations, Customers, Products or other objects.

These duplicate entities lead to chaos in CRM tools, inefficient marketing campaigns, incorrect analysis and wasted resources.

### Quickstart — Using Entity Resolution

The Entity Resolution flow can be kicked off from 2 places.

1. From the Datasets tab, select the dataset you would like to deduplicate from the list, and click the "Deduplicate" button on top of the list.
2. From a given Dataset, click "Deduplicate" in the top header to kick off the flow for that dataset.

{% @arcade/embed flowId="8nKaVuFmfhlp5sQ31qxF" url="https://app.arcade.software/share/8nKaVuFmfhlp5sQ31qxF" %}

### Entity Resolution

Entity Resolution helps you de-duplicate and associate records across all your data sources. Some key users cases include:

* Removing duplicate records from your CRM (Salesforce, Hubspot, etc) applications.
* Creating golden customer records from across various data sources.
* Identity Resolution - Resolving anonymous users into real users
* Associating different users into a common unit. For e.g. creating a household record from individual users

Entity Resolution helps you build out your Golden Record — a single source of truth for your business applications.

<figure><img src="https://lh7-rt.googleusercontent.com/slidesz/AGV_vUdv4Vnla_1aCELSCq5jLhwZ4rGfJNQhvaX6D87Mf4G8XAuvc2e-BMjs7inXYT-4Ycg1ZA6_tMZLlnP8wcZ7U1BEPtjUmQVOoVZeczZDyjRIv_3GJpXsb9COj99Wv_yPBgyZsyqm21F9XcKE6li3NYJyQgMsEio=s2048?key=oMbocqBtb6khj3dRV8q_UA" alt=""><figcaption><p>Census Entity Resolution - De-duplication and Association</p></figcaption></figure>

### Core Concepts

Census supports Deterministic Entity Resolution with [Fuzzy Match](entity-resolution.md#fuzzy-match) at the column level. Deterministic Entity Resolution uses human-defined rules-based approach to identify duplicate records or associated users.

#### Match Rules

Match Rules are the criteria we use to identify duplicate or associated records. You can define these rules with a number of possible operations including Exact Match and [Fuzzy Match](entity-resolution.md#fuzzy-match).

Some of the most common rules include

* Matching users based on email address, mailing address or customer IDs
* Matching companies based on their domain, company name or location

You can create complex rules using AND and OR operators across the rules.

<figure><img src="../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

**Fuzzy Match**

Fuzzy matching is a technique used to identify and match similar strings that may not be identical. In Census, we want to ensure you always get a predictable & deterministic match. We use [Jaro-Winkler similarity](https://en.wikipedia.org/wiki/Jaro%E2%80%93Winkler_distance).

Jaro-Winkler similarity compares two strings to determine how similar they are, taking into account variations such as typos, order differences, and abbreviations. This algorithm is especially effective in handling messy real-world data and is commonly used in places like the US Census 🙂.

We provide three customizable thresholds for determining similarity:

| Confidence Level | Matched                                                                                                                                       | Not Matched                                                                                                               | Explanation                                                                                                |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Low (0.85)       | <p>John Smith vs. Jonathon Smythe, </p><p><br>ABC Technologies Inc. vs. ACB Tech</p>                                                          | <p>John Smith vs. Johnathan Smithson, </p><p><br>ABC Technologies Inc. vs. XYZ Tech</p>                                   | The names have some phonetic similarity, but the spelling and length differences result in low confidence. |
| Medium (0.9)     | <p>Acme Corporation vs. Acme Corp,</p><p><br>The Baker’s Delight vs. Baker’s Delight</p>                                                      | <p>Acme Corporation vs. Apex Corp,</p><p><br>The Baker’s Delight vs. The Delight</p>                                      | The names are similar, but abbreviations and structural differences lower the match confidence to medium.  |
| High (0.95)      | <p>Census Data Inc. vs. Census Data,</p><p></p><p>Incorporated<br>International Business Machines vs. IBM International Business Machines</p> | <p>Census Data Inc. vs. Census Analytics Inc.,</p><p><br>International Business Machines vs. Global Business Machines</p> | The strings are nearly identical, with minor differences, leading to a high confidence match.              |



When building your match rules, you can choose what matching method you want to use for each column separately. You can mix exact match and fuzzy match rules in the same configuration.&#x20;

**Output Type**

Census allows you to either merge duplicate records into one or mark them as duplicates. If marked as duplicate, Census will add additional columns to note its parent ID and if it's a duplicate. In addition, for marked as duplicate mode, when fuzzy match rules are applied,  a similarity score column against the parent, is added for every fuzzy match rule.&#x20;

If your source dataset looks like below, examples of how your deduplicated dataset will look like is shown below.&#x20;

**Source Dataset:**&#x20;

| ID | EMAIL              | FULL\_NAME   | PHONE        |
| -- | ------------------ | ------------ | ------------ |
| 1  | john@example.com   | John Doe     | 123-356-6891 |
| 2  | john@gmail.com     | Johnny Doe   | 123-356-6891 |
| 3  | jannet@example.com | Jannet Smith | 245-891-9012 |



**Merged Dataset:** Fuzzy Match on Full Name with Medium Similarity, Resolve to Longest Email

| ID | \_census\_id                  | EMAIL              | FULL\_NAME   | PHONE        |
| -- | ----------------------------- | ------------------ | ------------ | ------------ |
| 1  | cid\_a209634ab08e48eeab7fd79f | john@example.com   | John Doe     | 123-356-6891 |
| 3  | cid\_b6447e18e2954750a369bb16 | jannet@example.com | Jannet Smith | 245-891-9012 |



**Marked as Duplicate Dataset:** Fuzzy Match on Full Name with Medium Similarity, Resolve to Longest Email

<table><thead><tr><th width="62.59765625">ID</th><th>_census_id</th><th width="155.49609375" data-type="number">_census_parent_id</th><th width="284.76171875">_census_email_similarity_with_parent</th><th width="194.90625">_census_has_duplicates</th><th width="205.1953125">EMAIL</th><th width="181.34765625">FULL_NAME</th><th>PHONE</th></tr></thead><tbody><tr><td>1</td><td>cid_a209634ab08e48eeab7fd79f</td><td>1</td><td>1.0</td><td>true</td><td>john@example.com</td><td>John Doe</td><td>123-356-6891</td></tr><tr><td>2</td><td>cid_a209634ab08e48eeab7fd79f</td><td>1</td><td>0.96</td><td>true</td><td>john@gmail.com</td><td>Johnny Doe</td><td>123-356-6891</td></tr><tr><td>3</td><td>cid_b6447e18e2954750a369bb16</td><td>3</td><td>1.0</td><td>false</td><td>jannet@example.com</td><td>Jannet Smith</td><td>245-891-9012</td></tr></tbody></table>

#### Census IDs

All records in a resolved dataset will automatically be assigned a unique ID called the "Census ID" (`_census_id`). This is a Census-generated ID that represents a single resolved entity in your dataset. For instance, if 2 records in the base dataset get resolved into a single entity, they will both have the same `_census_id` value.

Census IDs will remain "stable" as your dataset changes. For instance, if a group of records make up the "John Smith" entity in your resolved dataset, that entity will retain the same Census ID even as individual records that contribute to the entity enter or leave your base dataset.

#### Merge Rules

Merge rules help you identify the winning record amongst the duplicates. The ID of the winning record becomes either the primary ID (aka the column configured as the unique ID on your source dataset) when merged, or the `_census_parent_id` when unmerged, and is useful while syncing back to your business applications.

Census supports waterfall structure rules. So, the first rule is evaluated first and then the next until a record becomes a winning record.

<figure><img src="../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

#### Column Overrides

Column Overrides help you override column values on the winning record. You can conditionally choose values for the final / resolved record.

<figure><img src="../.gitbook/assets/Screenshot 2024-08-30 at 10.23.50 AM.png" alt=""><figcaption><p>Census Entity Resolution - Column Overrides</p></figcaption></figure>

#### Default Internal Variables

There are multiple internal variables that determine how Census will run the Entity Resolution algorithm. Below is a list of these parameters and their default values. Contact Census if you would like to change any of these.&#x20;

* **bands:** how many slices of the signature will be used to determine if records are likely to be identical; the default is 4
* **hashes\_per\_band:** the number of hash values from the signature will be used per band; the default is 8
* **use\_first\_char\_blocking:** only compare records that start with the same letter during fuzzy matches; default is false
* **use\_lsh:** enable [Locality Sensitive Hashing](https://en.wikipedia.org/wiki/Locality-sensitive_hashing) to find fuzzy matches; turned on by default
* **use\_sorted\_neighborhood:** enable fuzzy matching through sorting and comparing within a small window; turned on by default
* **use\_deletion\_key**: enables comparing records to those with deleted characters from other records to catch variations with typos or missing letters; tuned on by default
* **number of passes**: how many times the algorithm will run on the records; default is once

#### Materialization

Entity Resolution generates a new dataset that is written back to [Census Store](https://docs.getcensus.com/misc/data-storage/census-store), allowing you to query and sync from it. If you want to bring your own S3 bucket for Census store, checkout our docs [here](https://docs.getcensus.com/misc/data-storage/bring-your-own-bucket).&#x20;

Entity resolution is performed by internal Census syncs that you can view the statuses of on the dataset page. You can also change the frequency at which these syncs run and manually trigger refreshes.&#x20;

<figure><img src="../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

### FAQ

#### How does Census handle NULLs for fields that are used in matching and column overrides?

For matching, records with NULL values for that match rule will be ignored. For instance, if you have a rule to match records when they have the exact same email, we will not match 2 records that have NULL emails.

For merging and column overrides, you can be explicit about how you want NULLs to be treated in your configuration. For instance, you can set a column override on the winning record to select non-NULL values for specific columns:

<figure><img src="../.gitbook/assets/Screenshot 2025-06-05 at 2.33.37 PM.png" alt=""><figcaption></figcaption></figure>

#### Can I be alerted when an Entity Resolution refresh fails?

Yes, you can be notified if a refresh fails by subscribing to [Sync Alerts](https://docs.getcensus.com/syncs/sync-monitoring/alerts) for the syncs powering Entity Resolution, which are linked to from the Deduplicate dataset status bar:

<figure><img src="../.gitbook/assets/Screenshot 2025-06-05 at 2.38.47 PM.png" alt=""><figcaption></figcaption></figure>
