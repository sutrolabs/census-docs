# Overview

## What is a Sync?

A Sync is the core operation in Census that defines how data should flow from your selected source to your destination. Syncs are what make Census unique - unlike most integration tools that are event-based, Census works to keep your source and destination "in sync" (similar to how Dropbox or other cloud storage services work). This means you don't have to worry about dropped events or backfills. If you change your data in the source, Census automatically syncs it to your destination.

## Creating Syncs

To create a sync, you'll need to define:

1. A **source** - Where your data is coming from (Basic Dataset, Streaming Dataset, SaaS Dataset, CSV Dataset, or direct warehouse access)
2. A **destination** - Where your data is going (CRM, marketing platform, etc.)
3. A **sync behavior** - How Census should handle the data (update, create, mirror, etc.)
4. **Sync keys** - How to match records between source and destination
5. **Field mappings** - Which fields to sync and how they map between systems

### 🔀 Sync Behaviors

{% hint style="success" %}
All of our syncs are incremental, which means we only sync records that are new or have their data changed since the previous sync.
{% endhint %}

Sync Behaviors tell Census the types of change it should apply to your data when a sync finds a matching (or not) record in a source and a destination. We support a few different sync behaviors:

|                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Update or Create (aka Upsert) | Update existing destination records when IDs match, otherwise create new ones if they're missing.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Update Only                   | Update existing objects in the destination, don't create any new ones.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Create Only                   | Create a new object if it doesn't exist in the destination.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Mirror                        | <p>Keep the destination in sync with the source.</p><ul><li>If a row is added or edited in the source, update the destination.</li><li>If a previously synced row no longer is in the source, remove the matching object from the destination. Note: some services such as Braze offer other actions as well. See specific connector documentation for more details.</li><li>Mirror syncs identify changes by comparing against the data they have already sent -- not the data that might or might not already exist in the destination. This means that the first sync will be an upsert for all records, and the second and following syncs will account for changes from the source data.</li></ul> |
| Append Only                   | <p>Treat the destination as an append only log of data suitable for Event data.</p><p>Read more about <a href="https://docs.getcensus.com/basics/defining-source-data/events">sending event data</a>.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Delete                        | <p>Delete syncs takes the list of provided IDs and deletes them from the destination.<br><br>Be careful! Providing an incorrect set of IDs can result in data loss! Census recommends you backup data if you're concerned about accidentally deleting the wrong records.</p>                                                                                                                                                                                                                                                                                                                                                                                                                            |

{% hint style="warning" %}
Please note that some of these behaviors are only available for certain destinations. Visit our individual integration pages to view what's supported.
{% endhint %}

### 🔎 Sync Keys

Sync Keys let Census know how to associate data in the source with the destination. Both the source and destination need to provide a single, unique per record, identifying field. Census uses the identifiers to look for matches. When a match is found, or not found, it then can use your selected Sync Behavior to decide what to do.

For example, if Census sees your source and destination both have records with the identifier ABCD1234, it knows that it should update that record with data from the source when you've got an Update Only, Update or Create, or Mirror Sync Behavior configured.

### 🖇 Field Mappings

Once you've defined _how_ data is related between your source and destination, the next step is to let Census know _what_ properties should be updated. The field mapping step lets you specify how fields should be mapped from your source model to the destination object's fields. You can automatically add all matching fields, but even if names don't match, you can also provide the matching manually. If you remove fields from your mapping, Census will just stop updating those fields. We will not delete the values.

#### **Using templates to transform source data**

Sometimes the data in your source systems isn't in quite the format or style that the destination expects. If you need to transform records from the source before sending them to the destination, you can use a **Templated Field.**

Census supports templated fields using the Liquid template language. As a basic example, this Liquid template lets you combine a customer's city and country into a single piece of text:

```liquid
{{ record['city'] }}, {{ record['country'] }}
```

To give you an idea of the capabilities available, here are a few more examples:

* `Customer` → Sends just the word "Customer" to the destination field
* `Last updated at {{ "now" | date: "%Y-%m-%d %H:%M" }}` → Prepends a timestamp with some initial text
* `{{ record['first_name'] | rstrip }}` → Removes trailing whitespace from a customer's name

You can read all about the Liquid template system provided by Census here:

{% content-ref url="../structuring-data/liquid-templates.md" %}
[liquid-templates.md](../structuring-data/liquid-templates.md)
{% endcontent-ref %}

{% hint style="info" %}
Templated fields have a few limitations:

* Templated fields operate on one record at a time. If you need to bring multiple records together, take a look at [Datasets](../datasets/overview/), which allow you to use SQL to prepare your source data for syncing, or at the Census [Audience Hub](../audience-hub/), which includes a powerful point-and-click [visual segment builder](../audience-hub/getting-started/#using-the-visual-builder) and [calculated fields](../audience-hub/data-preparation-1/#calculated-fields).
* Not all sources support templates yet; we are always adding support for new sources!
{% endhint %}

#### Conditional field mappings

Where available, Census supports two types of conditional field mappings:

* **Don't Sync Null Values** - By default, Census will sync any Null values from the source to the destination. On some connections, you can disable sending any Null values. When disabled, the particular Null value for the property is ignored, but the rest of the recode is synced. Note that the the destinations may handle Null values differently. For example, Salesforce will convert Null values to empty strings, and Braze will delete the property completely when a Null value is synced.

![Also Sync Null Values in the source field editor](../.gitbook/assets/conditional_field_mapping_dont_sync_nulls.png)

* **Set If Empty** - By default, Census will sync any values from the source to the destination, even if the destination already has a value. On some connections, you can set a property to only sync if the destination property is empty. This is useful if you want to set a default value for a property, but not overwrite any existing values.

![Set only if destination field is empty](../.gitbook/assets/conditional_field_mapping_set_if_empty.png)

#### Creating new fields on your destination object

For some destinations, such as Braze, Customer.io or Iterable (see full list below), you can create new fields directly from the Census app. This means the next time a sync runs, Census will create new properties or attributes for that object in the destination. This is useful if you want to automatically create new fields based on the columns in your source data.

Simply select **"Sync All Properties"** when setting up a sync.

![Simply select "Sync All Properties"](../.gitbook/assets/sync_all_fields.png)

{% hint style="info" %}
The following destinations currently support automatically adding new properties:

Braze, Custom API, Customer.io, Google Cloud Storage, Google Sheets, Iterable, Klaviyo, Mixpanel, S3, Salesforce Marketing Cloud, Segment, SFTP, Slack, Vitally, Webhook
{% endhint %}

## Running Syncs

Once syncs are created, you'll probably want to run them! That's where the real magic happens. There's a few things you should know about running and maintaining syncs though including how frequently they should run and what sync history tells you about the health of your sync.

### ⏱ Schedules and API

You can happily run a sync manually, but that's not all that useful on its own. The real power of Census is having your syncs run automatically. Once you've got your sync up and running, you can configure your sync to run automatically in three ways:

* [Schedules](triggering-syncs.md#schedule) including with Cron
* [Programmatically via API or Orchestration tool](triggering-syncs.md)
* [Automatically with dbt Cloud](../basics/core-concept/broken-reference/)

Pick the sync execution trigger that makes for your connection and Census will keep the data flowing to your schedule.

### Sync History

You can dive deeper into why syncs failed, or what records were invalid from the source, or rejected by the destination, under the **Sync History** tab.

**Failed Syncs**\
Hover over the status label to see a detailed error.

![](../.gitbook/assets/census_sync_history_failed_sync.png)

**Invalid or rejected records**\
Click the number of invalid or rejected records to see a sample (up to 100), and the reason why they were invalid or rejected.

**What is the difference between Invalid and Rejected records?**

* **Invalid** records are flagged and filtered by Census _prior_ to syncing to your destination. Census will check the source data for records with NULL identifiers and duplicates.
* **Rejected** records are records that were sent to the destination, but the destination did not accept them. The sample of rejected records will provide the specified reasons received from the destination.

![](../.gitbook/assets/census_sync_invalid_rejected_records.png)

![Output of invalid records diagnostic log](../.gitbook/assets/census_invalid_records.png)

## 🔌 Sources and Destinations

To create a sync, you'll need to connect both a source and a destination.

### Data Sources

Census supports a variety of data sources for your syncs:

* **Basic Datasets** - Connect directly to your data warehouse tables, views, or custom SQL queries
* **Streaming Datasets** - Process real-time events from Kafka, Confluent Cloud, and other streaming sources
* **SaaS Datasets** - Use data directly from your CRM systems like Salesforce or HubSpot
* **CSV Datasets** - Upload and use CSV files for quick testing or one-time syncs
* **Direct Warehouse Access** - Sync directly from warehouse tables without creating a dataset

This flexibility allows you to use the right data source for each use case, whether you need batch processing, real-time streaming, or direct access to your SaaS applications.

{% hint style="info" %}
For instructions on connecting your specific data source, take a look at the Data Sources section on the left.
{% endhint %}

#### Data Source Permissions and Read-only Access

Census provides a powerful and customizable Advanced Sync Engine on top of your data sources. To enable all of this without storing your customer data outside your infrastructure, we create a scratch or bookkeeping schema in your data warehouse that we use to cache sync states. This requires write permission to this schema and only this schema. This schema will not be selectable as a source within the Census sync configuration UI.

If you don't have credentials with write access available, you can connect to your warehouse using our Basic Sync Engine which instead stores this state outside the warehouse.

Either option may be right for you, read more about the differences between [Basic and Advanced Sync Engines](https://docs.getcensus.com/sources/overview#sync-engines).

#### Datasets and segments

Datasets in Census provide a flexible way to organize and prepare your data for syncing. You can create datasets from various sources:

* **Basic Datasets** from your data warehouse using SQL or table selection
* **Streaming Datasets** for real-time data activation
* **SaaS Datasets** from your connected business applications
* **CSV Datasets** for simple file uploads

You can also connect dataset integrations like [dbt](../datasets/overview/external-dataset-repositories/dbt-integration.md), [Looker](../datasets/overview/external-dataset-repositories/looker-integration.md), or [Sigma](../datasets/overview/external-dataset-repositories/sigma-integration.md).

Datasets are optional in Census—you can also sync data directly from a data source table or view—but datasets give you a simple way to create authoritative locations for the full set of all of your paying customers, invoices, or whatever other reusable data concept matters for your business. And once you've built your datasets, Census makes it easy to quickly select and sync [Segments](../audience-hub/getting-started/) as well.

### Destination Services

Census helps you keep your data in sync across all the business apps you use to engage with your customers, from advertising and marketing, through sales, all the way to finance. The goal is to keep all of those apps in sync, powered by the exact same set of data.

The process of connecting a service is a little different for each. Sometimes, it's as simple as an OAuth confirmation flow or a straightforward API key. Other times, a few more steps are required.

Once you've connected a source, we'll be able to access a set of objects that service makes available. Typically this is a Contact or a Company, but there are often others and in some cases, even custom defined objects are supported.

All of the connection steps, the objects, and other details for each service are covered here in the docs.

And don't forget, our library of connections grows every week! Keep an eye on our [integrations page](https://www.getcensus.com/integrations) for all of our available destinations and let us know if we're missing something you need!

## Need Help?

That's it! Now you've got everything you need to know to get the most out of Census syncs, but don't worry, you can still get into the nitty gritty on individual data sources or destinations. And we're always here to help. If you have any questions, just let us know!
