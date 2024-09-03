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

Refer to the GPT Columns and how to get started [here](gpt-columns/).

