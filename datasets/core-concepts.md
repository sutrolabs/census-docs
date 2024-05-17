# Core Concepts

## Dataset Source <a href="#data-source" id="data-source"></a>

Datasets require a source to be defined. The source represent the external infrastructure from which we will be reading the rows and columns for your dataset. You can learn more on how to connect a source through our [Source Documentation](broken-reference). All connected sources will appear at dataset creation time.

Different data sources have different behaviors and functionality. We encode these differences through different Dataset Types. You can learn more of the specific requirements, capabilities and limitations for each within each section.&#x20;

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Once a dataset is created you can view the source information through the right sidebar of your Dataset page. Dataset source is not editable after creation, however some sub properties such as Census defined queries are.&#x20;

## Dataset Metadata

Datasets allow you to set icons and descriptions to help you identify and describe your data. For data that is countable (such as materialized data), you can also see the latest row count next to the dataset name.

## Dataset Columns & Annotations

The Dataset details view list all columns available through the source along with type metadata.

You will also find two other columns here, PII and Enumerations.

* PII - Mark a column as PII to prevent this column's values from being displayed anywhere in the Census ecosystem. Only Admins have permissions to toggle this feature. If you use DBT and have PII information encoded in your yaml metadata we will automatically import it and set it in our systems.
* Enumerated - Mark a column as Enumerated to indicate that your source data contains categorical data, wher the options in that column are limited to a finite set of potential values. For example a `country` attribute which has a fixed set of 195+ options, or a `plan` attribute which only has a couple different options. Enumerated columns will then be represented as select or multiselect experiences anywhere in the Census ecosystem where you need to interact with the values for this column, such as segmentation. Enumerated column values are cached in our system on a daily cadence, but we expose a manual refresh option within any selector if you are looking to consume a recent change.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

To provide performant experience this information is cached and refreshed on a consistent cadence. If you notice a change you just made in your external source is not represented, simply hit the refresh button.

## Dataset Type & Property Mappings

Your data often times describes standard universal concepts such as people, organizations or time based events. Datasets currently supports several specific dataset types to help you encode this information into Census.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Assigning a type to your dataset is the first step to unlocking more powerful and smarter capabilities within Census - read ahead for each type and property mapping description and what features it unlocks.

<table><thead><tr><th width="199">Type</th><th>Description</th></tr></thead><tbody><tr><td>Generic</td><td>Represents any unspecified type of data. By default all datasets have a generic type.</td></tr><tr><td>Person</td><td>Represents datasets that contain humans that engage with your business in some form. They may be subscribers or free users or email recipients depending on your business.</td></tr><tr><td>Event</td><td>Represents datasets that capture time bound data or events. It may be a user's website behavior, purchase history etc.</td></tr><tr><td>Company</td><td>Represents datasets that contain organizations in some form. Often times it the overarching object to which some of your Person datasets belong to. It may be organizations that use your product, potential companies for outreach.</td></tr><tr><td>Audience</td><td>Represents datasets that contain Audiences within your external source. This dataset is used to power <a data-mention href="../audience-hub/warehouse-managed-audiences.md">warehouse-managed-audiences.md</a>.</td></tr><tr><td>Join Table</td><td>This can be used to specify a many-to-many relationship.  </td></tr></tbody></table>

Dataset Types go hand in hand with Dataset Property Mappings. Property Mappings allow you to highlight key columns that also represent universal concepts, such as email, and carry special implications. There are several property mappings supported for each Dataset Type.

<table><thead><tr><th width="222">Property Mapping</th><th>Description</th></tr></thead><tbody><tr><td>Unique Identifier</td><td>A column that can be used to unique identify each row in your dataset. If your dataset doesn't already have one, you can create a column by combining values from other columns into a unique identifier.<br><br>Currently all dataset types aside from Generic require setting a unique identifier.<br><br>Unique Identifiers unlock the use of the Dataset API, and advance Segmentation.</td></tr><tr><td>Email</td><td>A column that contains emails. Only available on the Person dataset, for which it's required.<br><br>Supports the use of columns with hashed emails via the Hashed checkbox.<br><br>Emails unlock the use of One Click Syncs to audience focused destinations.</td></tr><tr><td>Event Timestamp</td><td>A column that contains the timestamp the event occurred (ideally in UTC). Only available on the Event dataset, for which it's required.<br><br>Event timestamp unlocks the use of advanced event specific Segmentation as well as Metric tracking for Segmentation Experiments.</td></tr><tr><td>Event Name</td><td>A column that contains the human readable label for the action the event record refers to. Only available on the Event dataset, for which it's required.<br><br>Event timestamp unlocks the use of advanced event specific Segmentation as well as Metric tracking for Segmentation Experiments.</td></tr><tr><td>Name</td><td>A column that contains the name for a given organization. Only available on the Company dataset, for which it's optional.<br><br>Name will be used as the pinned column when viewing a Dataset via the Dataset Explorer.</td></tr><tr><td>Domain</td><td>A column that contains the domain for a given organization. Only available on the Company dataset, for which it's optional.<br><br>Name will be used to display website logos when viewing a Dataset via the Dataset Explorer.</td></tr></tbody></table>

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Don't worry, all of your dataset's existing columns will be available for syncing and segmenting. Property Mappings just indicate the columns on your entity that have special value for Census.

## Relationships

Datasets support the ability to be related to one another. The supported relationships are one-to-one, one-to-many, many-to-one, and many-to-many. Datasets relationships are an optional feature. However, defining relationships between datasets in Census unlocks advance functionality across the product.

* Enabled advance dataset segmentation and filtering off information that exists in other related datasets.
* Enabled syncs that send data from other related datasets.
* Enables creating rollup columns for a given dataset.

Datasets can have many relationships defined and the relationship will appear on both related datasets once defined.

The relationship definition includes two pieces of information:

* The type of relationship - Specify Many-to-One or One-to-Many relationship types here. These can be used to indicate when an dataset is "owned" or "belongs to" one thing, or when an dataset has many "children".
* The matching identifiers - The columns that contain identifiers that should match (be equivalent) on both sides of the relationship. In database terms, this is the primary key and foreign key that would sit on either side of a JOIN condition.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

To specify a Many-to-Many relationship type, use a `Join Table` type:

* Any dataset can be used as a join table, not just ones that are typed `Join Table`. All the `Join Table` type does is drop the requirement of specifying a `Unique Id` for that entity since often join tables do not have unique Ids for rows.
* Aside from the specific many-to-many filtering use case, this change lets you filter on related datasets inside filters on related datasets. So you can now segment for things like “Pets who belong to users who have 5 purchase events in the last month”

Note that Census does not check or enforce the validity of the data on either side of your relationship. Duplicate values on either side of the relationship can cause issues using the relationships used in segmentation so please make sure the relationship's data remains valid via tools like dbt testing.

## FAQ

{% hint style="info" %}
**What happened with my models and entities?**

All the data you had encoded in your models and entities is still available and now has a new representation through Datasets. If you need help navigating this change [contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
{% endhint %}

{% hint style="info" %}
**Do these Dataset changes impact my syncs?**

No. All your syncs will continue to work exactly the same way and sync the same data. However, your sync source will now be a Dataset.&#x20;
{% endhint %}

