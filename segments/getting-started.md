# Getting Started

It's easy to get started building segments and syncing them to your destinations. There are three main steps:

1. Approve you source model
2. Build your segment using the Visual Builder
3. Sync your segment

### 1. Approve your model

Segments can be built on any model as long as it has been approved for use. This works for any models in Census: saved query models, dbt models, as well as Looker Looks. This means you have more control over making sure segments are only built on top of trustworthy data.&#x20;

{% hint style="info" %}
Only users with Admin or Editor role can approve models
{% endhint %}

To approve a model:

* Choose your model
* Under the **Overview** tab, select **Approve**.&#x20;

![](<../.gitbook/assets/2021-12-10 17.47.22.gif>)

### 2. Build your segment using the visual builder

Once your models have been approved, you're ready to start creating segments

Click on **Segments** tab in the left-hand menu to go to the segments page. Click **Add a New Segment** and use the visual builder to define your segment. At any point, you can press **Preview** to get a look at what data will be available in your segment. When you're happy with your segment conditions, give you segment a name and press **Save**.

You can click preview to see a sampled list of users who match your segment criteria.

![](<../.gitbook/assets/segments\_cropped (1).gif>)

### 3. Sync your segment

Your newly created segment will now be available to sync in the standard Census sync workflow. You can sync segments to all over our supported destinations such as [Facebook Ads](../destinations/facebook-ads.md), [Google Ads](../destinations/google-ads/) and [Marketo](../destinations/marketo.md). \
\
At this point, you're good to go with Segments, but there's more to read if you need:

* Want to learn about Syncs? Check out the [Core Concepts](../basics/core-concept/) section
* Need to get your favorite app connected to Census? Take a look at Destinations in the menu on the left.

### FAQs

**What happens if you un-approve a model that's already been used to create segments and syncs?**

Census won't delete any segments or syncs related to that model, but you won't be able to use that model to create new segments.&#x20;



**Which string comparison operators are case sensitive and insensitive?**

_Case sensitive:_ Census will consider the "is" and "is not" operators to be case sensitive.

_Case insensitive:_ Census will consider the "contains", "does not contain", "starts with", and "ends with" operators to be case insensitive.

