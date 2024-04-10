---
description: >-
  The data warehouse can often turn into a data maze. Census helps highlight the
  most important business data so your teams can get going quickly.
---

# Data Defining

Models & Entities will be retired shortly, for the new, simpler approach to defining data please see [datasets.md](datasets.md "mention")\
\
By design, a data warehouse is meant to store massive amounts of data, and it does so very well. It's one of the reasons it's such a powerful platform for companies to build on top of. But all of that data makes navigating a warehouse a challenge, particularly for the members of your team that don't spend their day thinking about schemas and organizational structures.

There are many different methodologies for organizing a data warehouse. dbt has a [recommended approach](https://docs.getdbt.com/guides/best-practices/how-we-structure/1-guide-overview) and the [Kimball approach](https://www.kimballgroup.com/data-warehouse-business-intelligence-resources/kimball-techniques/dimensional-modeling-techniques/) is still common. Census most often deals with data at the end of those pipelines, stored in the final step (often the "publish" step, or data mart if you use that terminology).

For the users of your data, the vast majority of what happens in the warehouse is not important to them, and often only a subset of final data is intended to be used.

Census provides two concepts on top of your data warehouse to make it easier to control how data is used in Syncs and Segments.

1. [models](models/ "mention") are any defined SQL query that returns data from your warehouse. You can save [census-models.md](models/census-models.md "mention") directly in Census or you connect external model repositories such as [native-dbt-integration.md](models/native-dbt-integration.md "mention"), [sigma.md](models/sigma.md "mention"), and [looker.md](models/looker.md "mention").&#x20;
2. [entities.md](entities.md "mention") are the most important models in your warehouse. They're the ones that most of your company should be using for everything they do in Census. Entities also let you define a bunch of additional metadata about _how_ to use those models.
3. Simply use any table or view available in your warehouse as well.

For your data team members, most of the management required to use Census is curating and managing your set of entities that matter for the business teams at your company from the set of models you already have, and extending the set of properties available to them.

Need a hand getting a handle on your data warehouse? [Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat to let us know what questions we can help with!
