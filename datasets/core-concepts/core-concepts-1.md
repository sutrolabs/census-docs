# Type & Property Mappings

Your data often times describes standard universal concepts such as people, organizations or time based events. Datasets currently supports several specific dataset types to help you encode this information into Census.

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

## Type

Assigning a type to your dataset is the first step to unlocking more powerful and smarter capabilities within Census - read ahead for each type and property mapping description and what features it unlocks.

<table><thead><tr><th width="199">Type</th><th>Description</th></tr></thead><tbody><tr><td>Generic</td><td>Represents any unspecified type of data. By default all datasets have a generic type.</td></tr><tr><td>Person</td><td>Represents datasets that contain humans that engage with your business in some form. They may be subscribers or free users or email recipients depending on your business.</td></tr><tr><td>Event</td><td>Represents datasets that capture time bound data or events. It may be a user's website behavior, purchase history etc.</td></tr><tr><td>Company</td><td>Represents datasets that contain organizations in some form. Often times it the overarching object to which some of your Person datasets belong to. It may be organizations that use your product, potential companies for outreach.</td></tr><tr><td>Audience</td><td>Represents datasets that contain Audiences within your external source. This dataset is used to power <a data-mention href="../../basics/audience-hub/warehouse-managed-audiences.md">warehouse-managed-audiences.md</a>.</td></tr><tr><td>Join Table</td><td>This can be used to specify a many-to-many relationship.  </td></tr></tbody></table>

## Property Mappings

Dataset Types go hand in hand with Dataset Property Mappings. Property Mappings allow you to highlight key columns that also represent universal concepts, such as email, and carry special implications. There are several property mappings supported for each Dataset Type.

<table><thead><tr><th width="222">Property Mapping</th><th>Description</th></tr></thead><tbody><tr><td>Unique Identifier</td><td>A column that can be used to unique identify each row in your dataset. If your dataset doesn't already have one, you can create a column by combining values from other columns into a unique identifier.<br><br>Currently all dataset types aside from Generic require setting a unique identifier.<br><br>Unique Identifiers unlock the use of the Dataset API, and advance Segmentation.</td></tr><tr><td>Email</td><td>A column that contains emails. Only available on the Person dataset, for which it's required.<br><br>Supports the use of columns with hashed emails via the Hashed checkbox.<br><br>Emails unlock the use of One Click Syncs to audience focused destinations.</td></tr><tr><td>Event Timestamp</td><td>A column that contains the timestamp the event occurred (ideally in UTC). Only available on the Event dataset, for which it's required.<br><br>Event timestamp unlocks the use of advanced event specific Segmentation as well as Metric tracking for Segmentation Experiments.</td></tr><tr><td>Event Name</td><td>A column that contains the human readable label for the action the event record refers to. Only available on the Event dataset, for which it's required.<br><br>Event timestamp unlocks the use of advanced event specific Segmentation as well as Metric tracking for Segmentation Experiments.</td></tr><tr><td>Name</td><td>A column that contains the name for a given organization. Only available on the Company dataset, for which it's optional.<br><br>Name will be used as the pinned column when viewing a Dataset via the Dataset Explorer.</td></tr><tr><td>Domain</td><td>A column that contains the domain for a given organization. Only available on the Company dataset, for which it's optional.<br><br>Name will be used to display website logos when viewing a Dataset via the Dataset Explorer.</td></tr></tbody></table>

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

Don't worry, all of your dataset's existing columns will be available for syncing and segmenting. Property Mappings just indicate the columns on your entity that have special value for Census.

