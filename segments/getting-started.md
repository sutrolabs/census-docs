# Getting started

It's really easy to get started building segments and syncing them to your tools. There are three main steps:

1. Approve you model
2. Build your segment using the Visual Builder
3. Sync your segment

### 1. Approve your model

For a model to be available to build segments on top of, it needs to be explicitly approved. This works for both Census models and dbt models. This means you have more control over making sure segments are only built on top of trustworthy data.&#x20;

To approve a model:

* Choose your model
* Under the **Overview** tab, select **Approve**.&#x20;

![](<../.gitbook/assets/2021-12-10 17.47.22.gif>)

{% hint style="info" %}
Access controls for you can approve models versus create segments is coming soon. Today all users will be able to approve models and make them available for Segments.
{% endhint %}

### 2. Build your segment using the Visual Builder

Click on **Segments** to **Add a new Segment** and use the visual builder to filter your segment.

![](<../.gitbook/assets/2021-12-06 17.06.32.gif>)

### 3. Sync your Segment

Once you save your segment, it will now be available to sync in the regular sync workflow. You can sync segments to all over our supported destinations such as [Facebook Ads](../destinations/facebook-ads.md), [Google Ads](../destinations/google-ads/) and [Marketo](../destinations/marketo.md). To learn more about Syncs [go here](../basics/core-concept.md) or select your desired destination for the menu on the left.



### FAQs

**What happens if you un-approve a model after segments have been built on top of it?**

Census won't delete the segments or syncs related to that model, but you won't be able to use that model to create new segments.&#x20;

