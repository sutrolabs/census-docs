# Relationships

Datasets support the ability to be related to one another. The supported relationships are one-to-one, one-to-many, many-to-one, and many-to-many. Datasets relationships are an optional feature. However, defining relationships between datasets in Census unlocks advanced functionality across the product.

* Enables advance dataset segmentation and filtering off information that exists in other related datasets.
* Enables syncs that send data from other related datasets.
* Enables creating rollup columns for a given dataset.

Datasets can have many relationships defined and the relationship will appear on both related datasets once defined.

The relationship definition includes two pieces of information:

* The type of relationship - Specify Many-to-One or One-to-Many relationship types here. These can be used to indicate when an dataset is "owned" or "belongs to" one thing, or when an dataset has many "children".
* The matching identifiers - The columns that contain identifiers that should match (be equivalent) on both sides of the relationship. In database terms, this is the primary key and foreign key that would sit on either side of a JOIN condition.

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

To specify a Many-to-Many relationship type, use a `Join Table` type:

* Any dataset can be used as a join table, not just ones that are typed `Join Table`. All the `Join Table` type does is drop the requirement of specifying a `Unique Id` for that entity since join tables often do not have unique Ids for rows.
* Aside from the specific many-to-many filtering use case, this change lets you filter on related datasets inside filters on related datasets. So you can now segment for things like “Pets who belong to users who have 5 purchase events in the last month”

Note that Census does not check or enforce the validity of the data on either side of your relationship. Duplicate values on either side of the relationship can cause issues using the relationships used in segmentation so please make sure the relationship's data remains valid via tools like dbt testing.

