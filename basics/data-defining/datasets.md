# 🆕 Datasets

Datasets are a simple and powerful way to model the customer data that serves as the foundation of reverse ETL.&#x20;

Previously this definition layer was handled in Census via models and entities. To streamline your work, this is now combined together as "datasets" where you can manage source details (e.g. SQL query) along with powerful enhancements such as property mappings and relationships.\
\
Datasets can be found through the new nav item in the left sidebar. All previously created datasets (or models) will be displayed here. Select a dataset to edit or create new using the top right button.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Creating a new dataset will take you to the dataset creation screen. &#x20;

* Enter the name of the dataset
* The Warehouse source
* The type of definition
  * SQL Query
  * Source Table
  * DBT, Looker & Sigma can be added in the integrations page

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

After entering the SQL query, you can preview the results of the query in the query window.  On pressing save you will be taken to the datasets details page.&#x20;

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

The dataset can also be enriched further by adding a type and mapping to the dataset. &#x20;

### Data Type

Letting Census know what "type" of data your dataset is will let Census be smarter when segmenting or syncing later on. Census currently supports three specific data types in addition to a Generic type.

| Type       | Description                                                                                                                               |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Generic    | Any unspecified type of data. **If in doubt**, you can always use Generic for any of your datasets.                                       |
| Person     | Humans that engage with your business in some form. They may be subscribers or free users or email recipients depending on your business. |
| Event      | Analytics events that capture different types of a person's action at an exact moment in time                                             |
| Company    | For a dataset representing company information                                                                                            |
| Audience   | This is used in [warehouse-managed-audiences.md](../audience-hub/warehouse-managed-audiences.md "mention")                                |
| Join Table | This can be used to specify a many-to-many relationship.                                                                                  |

Depending on the type of data selected, you can add in various mappings to allow for more context within the product and to streamline [1-click syncs for Ad platforms](../audience-hub/syncing-segments.md#one-click-experience-for-a-d-platforms).  If the dataset is to be used in [segments](../audience-hub/getting-started.md), the unique ID should be mapped as a minimum.&#x20;
