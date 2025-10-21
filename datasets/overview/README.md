# Datasets

Datasets are the way to model all your customer data in Census. Datasets expose your best data to business teams so they can explore and self serve data. At its core datasets represent the set of rows-and-columns that Census has access to, so they can take a lot of different forms:

* [Basic Datasets](basic-datasets.md) - These are datasets that exist in your warehouse or can be generated on top of it. It includes:
  * Tables or Views already in your data warehouse – This is the most common place to start. Chances are your data warehouse contains many tables and views already that can be reused in Census.
  * Census defined queries – You can also just use SQL to model your data inside Census. It's a fast way to get started syncing the exact set of data you need for a particular destination.
* [CSV Datasets](csv-datasets.md) - These are datasets created by uploading CSV files.

External repositories – Census also supports directly connecting to existing repositories such as [dbt Models](external-dataset-repositories/dbt-integration.md), [Sigma](external-dataset-repositories/sigma-integration.md), and [Looker](external-dataset-repositories/looker-integration.md). These tools make it easy to build and maintain sophisticated data transforms that keep your models up to date. Census connects with these tools to enable singular business logic to be sent to downstream business applications.

Datasets provide a complete interface to govern data across all sources, transform and enrich data, and activate your data from a trusted data layer.

## Dataset source <a href="#data-source" id="data-source"></a>

Datasets require a source to be defined. The source represents the external infrastructure from which we will be reading the rows and columns for your dataset. You can learn more on how to connect a source [here](../../sources/overview.md). All connected sources will appear at dataset creation time.

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

Once you've created a dataset, you can see & manage the source information on the **Dataset Overview** page. You cannot change the source after the dataset is created, but some attributes can be (eg. you can edit the queries to the source defined in Census).
