# Computed Columns

Datasets support the ability to define no-code calculations and aggregation from other datasets as new calculated columns without making changes in your warehouse. These columns can be then used as any other column in your dataset, as a sync attribute or during segmentation building.

You can create computed columns via the "New Computed Column" button in the Properties page of any of your datasets. Computed Columns support two operations: Lookup Columns and Rollup Columns

## Lookup Columns

Lookup Columns allow you to pull in a value into your dataset from any other dataset related through a one-to-one or many-to-one mapping.

For example:

* User team name
* User organization sign up date

## Rollup Columns

Rollup Columns allow you to create an aggregate value over your datasets relationships to help you obtain insights into your data. You are also able to filter down the related datasets over which you want to aggregate.

For example:

* Number of transactions performed last 30 days
* Number of payment failures last 90 days
* Number of current active admin users
* Most frequent purchase SKU
* Average order value in the last 30 days

Rollups require you to define three properties: the related dataset which to aggregate/join to, the column from this dataset to use, and the aggregation method to apply to the related values. You are also able to use our rich filtering editor to narrow down the target rows. The current supported aggregation methods are listed below. We will continue to expand this list to allow for richer operations.

| Related dataset column type | Supported aggregation methods      |
| --------------------------- | ---------------------------------- |
| number                      | most frequent, count, sum, average |
| any other type              | most frequent                      |
