# Overview

By design, a data warehouse is meant to store massive amounts of data, and it does so very well. It's one of the reasons it's such a powerful platform for companies to build on top of. But all of that data makes navigating a warehouse a challenge, particularly for the members of your team that don't spend their day thinking about schemas and organizational structures.&#x20;

Datasets are the way to model all your customer data in Census. Datasets expose your best data to business teams so they can explore and self serve data.  At its core datasets represent the set of rows-and-columns that Census has access, so they can take a lot of different forms:

* Materialized datasets -  These are datasets that exist in your warehouse or can be generated on top of it. It includes:
  * Tables or Views already in your data warehouse – This is the most common place to start. Chances are your data warehouse contains many tables and views already that can be reused in Census.
  * Census defined queries – You can also just use SQL or Python to model your data inside Census. It's a fast way to get started syncing the exact set of data you need for a particular destination.
  * External repositories – Census also supports directly connecting to existing repositories such as [dbt Models](https://docs.getcensus.com/sources/native-dbt-integration), [Sigma](https://docs.getcensus.com/basics/data-defining/models/sigma), and [Looker](https://docs.getcensus.com/basics/data-defining/models/looker). These tools make it easy to build and maintain sophisticated data transforms that keep your models up to date. Census connects with these tools to enable singular business logic to be sent to downstream business applications.
* Streaming Datasets - These are datasets that model event based data and enable our real-time usecases.

Datasets provide a complete interface to govern data across all sources, transform and enrich data, and activate your data from a trusted data layer.

{% hint style="info" %}
Need a hand getting a handle on your data warehouse? [Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat to let us know what questions we can help with!
{% endhint %}

## Lore

Previously this definition layer was handled in Census via models and entities. To streamline your work, this is now combined together in Datasets, where you can manage source details (e.g. SQL query) along with powerful enhancements such as property mappings and relationships.\
\
Datasets can be found through the new nav item in the left sidebar. All previously created models and entities will be displayed here in a unified view automatically and ready to be used next time you log in. Select a dataset to edit or create new using the top right button.
