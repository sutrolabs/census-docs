# Type & Property Mappings

Your data oftentimes describes standard universal concepts such as people, organizations or time-based events. Datasets currently support several specific dataset types to help you encode this information into Census.

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

## Type

Assigning a type to your dataset is the first step to unlocking more powerful capabilities within Census – read ahead for each type and property mapping description and what features it unlocks.

| Type       | Description                                                                                                                                                                                                                                                   |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Generic    | Represents any unspecified type of data. By default all datasets have a generic type.                                                                                                                                                                         |
| Person     | Represents datasets that contain humans that engage with your business in some form. They may be subscribers or free users or email recipients depending on your business.                                                                                    |
| Event      | <p>Represents datasets that capture time-bound data or events. It may be a user's website behavior, purchase history etc.<br><br>These datasets support special event-based conditions in segments, as well as metrics for tracking audience performance.</p> |
| Company    | Represents datasets that contain organizations in some form. Often it is the object tha Person datasets relate or belong to. It may be organizations that use your product or potential companies for outreach.                                               |
| Audience   | Represents datasets that contain audiences within your external source. This dataset is used to power [warehouse managed audiences](../../audience-hub/getting-started/warehouse-managed-audiences.md).                                                       |
| Join Table | This can be used to specify a many-to-many relationship.                                                                                                                                                                                                      |

## Property Mappings

Dataset Types go hand in hand with Dataset Property Mappings. Property Mappings allow you to highlight key columns that also represent universal concepts, such as email, and carry special implications. There are several property mappings supported for each Dataset Type.

| Property Mapping  | Description                                                                                                                                                                                                                                                                                                                                                                   |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Unique Identifier | A column that can be used to uniquely identify each row in your dataset. If your dataset doesn't already have one, you can create a column by combining values from other columns into a unique identifier.Currently all dataset types aside from Generic require setting a unique identifier.Unique Identifiers unlock the use of the Dataset API, and advance Segmentation. |
| Email             | A column that contains emails. Only available on the Person dataset, for which it's required.Supports the use of columns with hashed emails via the Hashed checkbox.Emails unlock the use of One Click Syncs to audience focused destinations.                                                                                                                                |
| Event Timestamp   | A column that contains the timestamp the event occurred (ideally in UTC). Only available on the Event dataset, for which it's required.Event timestamp unlocks the use of advanced event specific Segmentation as well as Metric tracking for Segmentation Experiments.                                                                                                       |
| Event Name        | A column that contains the human readable label for the action the event record refers to. Only available on the Event dataset, for which it's required.                                                                                                                                                                                                                      |
| Name              | A column that contains the name for a given organization. Only available on the Company dataset, for which it's optional. Name will be used as the pinned column when viewing a Dataset via the Dataset Explorer.                                                                                                                                                             |
| Domain            | A column that contains the domain for a given organization. Only available on the Company dataset, for which it's optional. Domain will be used to display website logos when viewing a Dataset via the Dataset Explorer.                                                                                                                                                     |

<figure><img src="../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

Don't worry, all of your dataset's existing columns will be available for syncing and segmenting. Property Mappings just indicate the columns on your entity that have special value for Census.
