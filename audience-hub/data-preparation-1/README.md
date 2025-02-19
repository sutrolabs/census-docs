# Data Preparation

Audience Hub is built from the ground up to let marketing teams target effectively without having to know any SQL. But unlike other segmentation tools, Census Segments runs directly on top of a data warehouse or other data source. Marketing teams love this because it gives them access to the full world of a company's up-to-date and approved data.

Working with a warehouse directly can be overwhelming. Census provides a number of tools for the data teams to make preparing their data for use with segments and easy and straightforward.

## Creating Datasets For Segmentation

Segments are built on top of your company's [Datasets](../../datasets/overview.md). Each Dataset requires a [unique ID](../../datasets/core-concepts/) to be able to get started segmenting your data. Optionally, you can also define [relationships](../../datasets/core-concepts/) for your dataset which will unlock further functionality.

### Working Across Relationships

When creating segments, you can also create advance conditions by leveraging related datasets and filtering based on its attributes as well.

<figure><img src="../../.gitbook/assets/Related Entity.png" alt=""><figcaption></figcaption></figure>

Relationships defined in datasets are one-to-many, but segments can also take advantage of implicit many-to-many relationships and multi-step relationships automatically. Users simply need to select the related dataset they care about and Census will take care of building the series of joins to associate them.

### Segmenting on Event Streams

Datasets also provide the ability to set [Dataset Types](../../datasets/core-concepts/). For segmentation, one of the most powerful types is the Event type. By highlighting the datasets that contain event data, marketers can create segments that filter on depth of engagement, engagement in certain time periods, specific interactions, as well as filtering on any other data point.

<figure><img src="../../.gitbook/assets/Example Segment (3).png" alt=""><figcaption></figcaption></figure>

