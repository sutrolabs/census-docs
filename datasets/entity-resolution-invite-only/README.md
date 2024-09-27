# Entity Resolution (Invite Only)

Business teams are dependent on trusted data to execute their growth initiatives. However, often the data is messy. One core reason for the messy data is to have duplicate records for various entities - Users, Organizations, Customers, Products or other objects.

These duplicate entities lead to chaos in CRM tools, inefficient marketing campaigns, incorrect analysis and wasted resources.

### Entity Resolution

Entity Resolution helps you de-duplicate and associate records across all your data sources. Some key users cases include:

* Removing duplicate records from your CRM (Salesforce, Hubspot, etc)  applications.
* Creating golden customer records from across various data sources.
* Identity Resolution - Resolving anonymous users into real users
* Associating different users into a common unit. For e.g. creating a household record from individual users

Entity Resolution is a way to structure your data to help create Golden Record—a single source of truth for your business applications.

<figure><img src="https://lh7-rt.googleusercontent.com/slidesz/AGV_vUdv4Vnla_1aCELSCq5jLhwZ4rGfJNQhvaX6D87Mf4G8XAuvc2e-BMjs7inXYT-4Ycg1ZA6_tMZLlnP8wcZ7U1BEPtjUmQVOoVZeczZDyjRIv_3GJpXsb9COj99Wv_yPBgyZsyqm21F9XcKE6li3NYJyQgMsEio=s2048?key=oMbocqBtb6khj3dRV8q_UA" alt=""><figcaption><p>Census Entity Resolution - De-duplication and Association</p></figcaption></figure>



### Core Concepts

Census supports Deterministic Entity Resolution with [Fuzzy Match](./#fuzzy-match) at the column level. Deterministic Entity Resolution uses human-defined rules-based approach to identify duplicate records or associated users and merge them into a single record.&#x20;

#### Match Rules

Match Rules are the criteria we use to identify duplicate or associated records. You can define these rules with a number of possible operations including Exact Match and [Fuzzy Match](./#fuzzy-match).&#x20;

Some of the most common rules include&#x20;

* Matching users based on email address, mailing address or customer IDs
* Matching companies based on their domain, company name or location

You can create complex rules using AND and OR operators across the rules.

<figure><img src="../../.gitbook/assets/Screenshot 2024-08-30 at 10.17.00 AM.png" alt=""><figcaption></figcaption></figure>



#### Fuzzy Match

Fuzzy matching is a technique used to identify and match similar strings that may not be identical. In Census, we want to ensure you always get a predictable & deterministic match. We use [Jaro-Winkler similarity](https://en.wikipedia.org/wiki/Jaro–Winkler_distance).

Jaro-Winkler similarity compares two strings to determine how similar they are, taking into account variations such as typos, order differences, and abbreviations. This algorithm is especially effective in handling messy real-world data and is commonly used in places like the US Census 🙂.

We provide three customizable thresholds for determining similarity:

- Low Confidence (0.6):
  - Matches strings with significant differences.
  - Ideal for broad, preliminary matches to capture potential duplicates.
- Medium Confidence (0.8):
  - Balances accuracy and inclusivity.
  - Suitable for identifying likely duplicates while allowing minor variations.
- High Confidence (0.9):
  - Requires strict similarity for matches.
  - Best for high-accuracy scenarios, minimizing false positives.

When building your match rules, you can choose whether what matching method you want to use for each column separately. You can mix exact match and fuzzy match rules in the same configuration.

#### Merge Rules

Merge rules help you identify the winning record among the duplicates. The ID of the winning record becomes the primary ID and is useful while syncing back to your business applications.&#x20;

Census supports waterfall structure rules. So, the first rule is evaluated first and then the next until a record becomes a winning record.&#x20;

When you leave your merge rules empty, Census uses a record with lowest ID as the winning record.

&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2024-08-30 at 10.24.48 AM.png" alt=""><figcaption><p>Census Entity Resolution - Merge Rules</p></figcaption></figure>



#### Column Overrides

Column Overrides help you override column values on the winning record. You can conditionally choose values for the final / resolved record.

<figure><img src="../../.gitbook/assets/Screenshot 2024-08-30 at 10.23.50 AM.png" alt=""><figcaption><p>Census Entity Resolution - Column Overrides</p></figcaption></figure>



#### Materialization

Entity Resolution generates a new dataset that is written back to your data warehouse under the Census Schema.

Entity Resolution is supported on Snowflake, BigQuery, Redshift and Postgres with support for other warehouses and data sources coming soon.
