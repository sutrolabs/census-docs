# Overview

Datasets are the way to model all your customer data in Census. Datasets expose your best data to business teams so they can explore and self serve data. At its core datasets represent the set of rows-and-columns that Census has access to, so they can take a lot of different forms:

* [Basic Datasets](./basic-datasets/README.md) - These are datasets that exist in your warehouse or can be generated on top of it. It includes:
  * Tables or Views already in your data warehouse – This is the most common place to start. Chances are your data warehouse contains many tables and views already that can be reused in Census.
  * Census defined queries – You can also just use SQL or Python to model your data inside Census. It's a fast way to get started syncing the exact set of data you need for a particular destination.
  * External repositories – Census also supports directly connecting to existing repositories such as [dbt Models](./basic-datasets/dbt-integration.md), [Sigma](./basic-datasets/sigma-integration.md), and [Looker](./basic-datasets/looker-integration.md). These tools make it easy to build and maintain sophisticated data transforms that keep your models up to date. Census connects with these tools to enable singular business logic to be sent to downstream business applications.
* [SaaS Datasets](./saas-datasets/README.md) - These are datasets created directly from your CRM systems (like HubSpot and Salesforce). They allow you to work with your business data alongside your warehouse data, with automatic refreshes and full access to Census features like AI columns and enrichments.
* [CSV Datasets](./csv-datasets/README.md) - These are datasets created by uploading CSV files.
* [Streaming Datasets](./streaming-datasets/README.md) - These are datasets that model event based data and enable our real-time usecases.

Datasets provide a complete interface to govern data across all sources, transform and enrich data, and activate your data from a trusted data layer.

## Lore

Previously this definition layer was handled in Census via models and entities. To streamline your work, this is now combined together in Datasets, where you can manage source details (e.g. SQL query) along with powerful enhancements such as property mappings and relationships.\
\
Datasets can be found through the new nav item in the left sidebar. All previously created models and entities will be displayed here in a unified view automatically and ready to be used next time you log in. Select a dataset to edit or create new using the top right button.
