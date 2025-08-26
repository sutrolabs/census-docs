# Columns & Annotations

The dataset **Overview** page lists all columns in the source with their type and extra metadata for each column like **PII** and **Enumerated**.

* PII - Mark a column as PII to prevent this column's values from being displayed anywhere in Census. Only Admins have permissions to toggle this feature. If you use dbt and have PII specified in your YAML metadata we will automatically import it and set it in our systems.
* Enumerated - Mark a column as Enumerated to indicate that your source data contains categorical data, where the options in that column are limited to a finite set of potential values. For example a `country` attribute which has a fixed set of 195+ options, or a `plan` attribute which only has a couple different options. Enumerated columns will then be represented as select or multiselect experiences anywhere in the Census ecosystem where you need to interact with the values for this column, such as segmentation. Enumerated column values are cached in our system on a daily cadence, but we expose a manual refresh option within any selector if you are looking to consume a recent change. We cache up to 100,000 distinct values for enumerated columns, which can be searched and selected throughout the product.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

Census caches and refreshes this metadata regularly to optimize performance. If you notice a change you just made in your external source is not represented, simply hit the refresh button.

## FAQ

{% hint style="info" %}
**What happened with my models and entities?**

All the data you had encoded in your models and entities is still available and now has a new representation through Datasets. If you need help navigating this change contact the support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
{% endhint %}

{% hint style="info" %}
**Do these changes impact my syncs?**

No. All your syncs will continue to work exactly the same way and sync the same data. However, your sync source will now be a dataset.
{% endhint %}
