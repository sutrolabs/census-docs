---
description: >-
  Census Enrichment makes it easy to enrich your dataset with third-party data
  and sync them to any business apps. The outcome also materializes in your data
  warehouse.
---

# Enrichment Columns

Census connects with any generic HTTP service using [HTTP Request Enrichments.](http-request-enrichments.md)

### Challenges with Enrichments CRM-based Enrichments

Enriching first party data, in your data warehouse or CRM systems, with third party data (e.g. company size, address, etc) is challenging for a number of reasons:

* Running enrichments directly on CRM eats up your API quota
* CRM based enrichments are not easily accessible across other business apps like marketing tools or outreach tools
* A single enrichment provider is not sufficient because no single solution has all the correct data
* You still have to dance around combining first party data, third party data, and manual edits to make these enrichments useful for personalized campaigns

Historically, an enrichment flow includes hitting an API directly on top of a CRM tool, storing it in the CRM tool, sending it to your warehouse, run sql to combine the company or person data, then sync this data back to CRM or marketing automation destinations.  Along the way, this leads to race conditions, duplicated records and unnecessary enrichment cost.

**Census Enrichment simplifies this entire workflow. With just a few clicks, you can enrich your warehouse (and CRM) data, combine it seamlessly with your existing datasets, and sync enriched insights to any business app—all in minutes.**

### Setup Enrichments

To set up enrichments, you can follow our [quick start guide](/broken/pages/cGEIVfMl9G8ejPK7gPYP).&#x20;

Once your enrichment is configured, Census will start querying your enrichment service and populating results.

You can immediately start using the new enrichment-powered attributes on your datasets within Census Segments and Syncs. Note that you'll see an indication in syncs and segments if the enrichment is still actively running but data will be backfilled in future sync runs if enrichment data is not immediately available at sync time.

{% hint style="info" %}
Enrichments is currently supported on Snowflake, Redshift, BigQuery, Databricks, and Postgres with more warehouses coming soon!
{% endhint %}



### Warehouse Writeback

The outcome of Enrichment Columns materializes in your data warehouse under Census Schema. Census Datasets join your enriched columns with your first party data to help you visualize, explore and sync to any destination.

### Need help with data enrichment?

Having issues with Enrichments or have feedback for us? [Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
