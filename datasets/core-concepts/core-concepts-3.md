# Computed Columns

Datasets support the ability to define no-code calculations and aggregation from other datasets as new calculated columns without making changes in your warehouse yet still being fully governed, tracked, and observed by your data stack.

These columns can be then used as any other column in your dataset, as a sync attribute or during segmentation building.

<figure><img src="../../.gitbook/assets/Screenshot 2024-06-09 at 5.17.32 AM.png" alt=""><figcaption><p>Census Computed Columns using Formula</p></figcaption></figure>

You can create computed columns, through the "New Computed Column" button in the Properties page of any of your datasets.&#x20;

Computed Columns support following operations:

## Lookup Columns&#x20;

Lookup Columns allow you to pull in a value into your dataset from any other dataset related through a  one to one or many to one mapping.

For example:

* User team name
* User organization sign up date

## Rollup Columns&#x20;

Rollup Columns allow you to create an aggregate value over your datasets relationships to help you obtain insights into your data. You are also able to filter down the related datasets over which you want to aggregate.

For example:&#x20;

* Number of transactions performed last 30 days
* Number of payment failures last 90 days
* Number of current active admin users
* Most frequent purchase sku
* Average order value in the last 30 days
* First time purchased at
* Last login at

Rollups require you to define three properties. The related dataset which to aggregate/join to, the column from this dataset to display, and the aggregation method to apply to the related values. You are also able to use our rich filtering editor to narrow down the target rows. The current supported aggregation methods are listed below. We will continue to expand this list to allow for richer operations.

| Related dataset column type | Supported aggregation methods  |
| --------------------------- | ------------------------------ |
| number                      | most frequent, count, sum, avg |
| any other type              | most frequent                  |

## Calculated Columns

Calculated Columns allow you to do quick calculations over your dataset columns in a no code environment.

For example:

* Weekly growth rates of feature usage
* Difference month over month of documents shared

The current supported calculations are difference and percentage change.

## GPT Columns

GPT Columns enable you to dynamically generate unique content for each row in your dataset using ChatGPT. With GPT Columns, you can define a prompt and use liquid templating to reference values from other columns. This setup allows you to send a customized ChatGPT request for each row, with the response automatically written back to your GPT Column.

For example:

1. Automatically generate personalized email content or messages based on customer data.
2. Generate insights or recommendations from transactional data, such as suggesting complementary products based on purchase history.
3. Sentiment analysis of email received by sales team from outbound campaign to help with categorization and reporting
4. Summarize product usage among specific features by “high” or “low” to identify upsell fits and run PLG playbooks

GPT Columns require you to define several properties.&#x20;

* The ChatGPT model to use - you can select from the provided list or manually enter a valid model.&#x20;
* The expected output type - there are several optional properties to help you guarantee data quality.

The prompt to run against each row of your data. Your prompt can leverage liquid templating to reference column values. To learn more about Liquid Templating [click here](../../basics/core-concept/liquid-templates.md).&#x20;

{% hint style="info" %}
GPT Columns are currently supported on Snowflake, Redshift, BigQuery, and Postgres with more warehouses coming soon.
{% endhint %}

