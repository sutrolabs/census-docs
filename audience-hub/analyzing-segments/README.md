# Experiments and Analysis

Census provides several tools to help you manage and analyze your segments after creation. This guide walks through the different tabs available in the Segment interface and their functionality. For information about creating segments and using the Definition tab, see the [Getting Started guide](../getting-started/).

## Experiments Tab

The Experiments tab allows you to create and manage split tests to measure the impact of your campaigns.

### Setting up Split Tests

A split test divides the people in your segment randomly into one or more **treatments** as well as a **control** cohort, which should be used as a baseline to compare the impact of your campaign. Each cohort has a percentage size you control, letting you set the relative sizes of each size.

<figure><img src="../../.gitbook/assets/Screenshot 2023-06-08 at 3.16.39 PM.png" alt=""><figcaption></figcaption></figure>

Split testing enables a number of marketing efforts:

* Create a simple treatment with control group and measure the increased conversion rate over users that received the treatment.&#x20;
* Divide a segment into multiple treatments for different channels and compare relative conversion rates of the same segment across each.
* Use a treatment and control group to "ramp up" a very large campaign over time. Start with 10% of segment and grow the treatment once you're confident it's performing as expected.

Each cohort can be [synced to their own set of destinations](../syncing-segments.md), including back to warehouse, and users appearing in each cohort are available in Warehouse Writeback (see [below](./#detailed-segment-performance)).

### Cohort Behavior and Management
* **Cohort Stability**: Within a segment, users are deterministically assigned to cohorts and will not change unless cohort percentages are modified
* **Minimum Requirements**: Experiments must maintain at least 2 cohorts at all times
* **Cohort Deletion**: 
  - When a cohort is deleted, its users are distributed evenly among the remaining cohorts
  - The total percentage allocation must always equal 100%
  - If there are only 2 cohorts, neither can be deleted (must maintain minimum of 2)
* **Cohort Size Changes**:
  - When reducing a cohort's percentage (e.g., 50% to 25%), affected users are distributed evenly among other cohorts
  - Distribution is approximately even but not guaranteed to be exactly equal
  - The same users will consistently move together when cohort percentages are adjusted

{% hint style="info" %}
**Best Practice**: When running experiments that involve multiple phases (e.g., testing with 5% then expanding to 100%), consider using your destination platform's deduplication features or create new segments with exclusion rules to prevent double-targeting of users.
{% endhint %}

## Destinations Tab

The Destinations tab shows all active syncs from your segment and provides one-click sync toggles for easy management. Each cohort can be [synced to their own set of destinations](../../basics/audience-hub/syncing-segments.md), including back to your warehouse.

Census will capture and report the audience match rates for segments synced to various ad destinations. For more information on how to view match rates and which services are supported, see [Audience Match Rates](audience-match-rates.md).

## Performance Tab

{% hint style="info" %}
**Note**: The Performance tab is only available for Experiments. You must set up an Experiment with cohorts to use these features.
{% endhint %}

The Performance tab allows you to track and analyze the results of your experiments over time. You can create customized metrics to compare performance across your control and treatment cohorts.

<figure><img src="../../.gitbook/assets/Snag_2f5839b5.png" alt=""><figcaption></figcaption></figure>

### Setting Up Metrics

To measure experiment performance, you first need to define the metrics that Census should measure. Each metric consists of:

* The name of the metric, which will appear in reporting UI.&#x20;
* The dataset it should be applied to. This should be the exact same dataset that you plan on segmenting.&#x20;
* The aggregation to apply, either a count of the number of filtered events, or a sum of a particular attribute on those events.
* The related events dataset that should be aggregated over to calculate useful performance metrics. These are typically conversion-type events such as purchases or views of a particular bottom-of-funnel web page.&#x20;
* Optionally a filter can be applied to as well, such that the count/sum only applies to a subset of the events dataset.&#x20;

{% hint style="info" %}
**Metrics are defined on Event type datasets** that are related to other datasets. If you don't see an expected option when creating a metric, make sure your datasets' types and relationship are configured correctly. See [Dataset Core Concepts](../../datasets/core-concepts/) for more details.
{% endhint %}

**Important**: Metrics should be created before starting campaigns as they will only be measured for campaigns once they've been created, they will not be generated historically. While metrics can be added after an experiment starts, calculations will only begin from the day the metric is created (not retroactive).

### Understanding Performance Metrics

#### Normalized Values
When viewing performance metrics across different cohorts with varying sizes, Census provides "normalized" values to make comparisons more meaningful. A normalized value shows what the metric would be if each cohort represented 100% of the population. For example, if you have:

* Treatment A: 25% of users
* Treatment B: 25% of users
* Control: 50% of users

The normalized values would be:
* Treatment A: Raw result × 4
* Treatment B: Raw result × 4
* Control: Raw result × 2

This normalization makes it easier to compare the relative performance of cohorts regardless of their size differences.

#### Uplift Calculation
The uplift percentage shown in performance tracking represents the percent difference between a cohort's normalized value and the control group's normalized value. It is calculated as:

```
uplift = ((cohort_normalized_value - control_normalized_value) / control_normalized_value) × 100
```

## Activity Tab

The Activity tab provides two key pieces of information:
1. A chart showing how your segment size has changed over time
2. A history log of all changes made to the segment, including who made each change

This tab is particularly useful for monitoring segment health and auditing changes to segment definitions.

<figure><img src="../../.gitbook/assets/unnamed.png" alt=""><figcaption></figcaption></figure>

## Comparison Tab

The Comparison tab allows you to compare your segment against any other existing segment. This is particularly useful when you have many segments and want to understand overlap between audiences or verify that a new segment is sufficiently different from existing ones.

<figure><img src="../../.gitbook/assets/760-b937f5942ce3a9913c2afc4267cebcde96975ff5.gif" alt=""><figcaption></figcaption></figure>

## Additional Analysis Tools

### Warehouse Writeback

For the deepest level of analysis, you can take advantage of [Warehouse Writeback](../../syncs/sync-monitoring/warehouse-writeback.md), which logs all sync activity back to your data source. You can use this data to determine when users were added and removed from segments in each of the destinations your segment is synced to or the relative conversion performance of users across cohorts.&#x20;

To take advantage of Warehouse Writeback for your analysis, ensure it is enabled on your warehouse connection.
