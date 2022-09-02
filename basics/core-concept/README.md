# Creating Syncs

## 🔌 Sources and Destinations

Census at its core is about connecting and coordinating across your business's software stack. And so, one of the very first steps to using Census will be connecting your Data Warehouse Sources and Destination Services.&#x20;

### Data Warehouse Sources

Source data for all Census Syncs come from your Data Warehouse. Historically, a data warehouse was the end of the line, where data went to collect dust. But modern cloud data warehouses enable a huge variety of data sources and data size, as well as the flexibility to define how data should be aggregated, joined, and organized specifically for your business. It's this flexibility and scalability that make it the perfect data hub for your operations.

Census can use anything you grant access to in your data warehouse as a sync source, whether that is a table, a view, a SQL query, or a dbt model. We'll cover the process of building models in the next section.

{% hint style="info" %}
For instructions on connecting your specific data source, take a look at the Data Sources section on the left.&#x20;
{% endhint %}

#### Data Source Permissions and Read-only Access

Census provides a powerful and customizable sync engine on top of your data sources. To enable all of this without storing your customer data outside your infrastructure, we create a scratch or bookkeeping schema in your data warehouse that we use to cache sync states. This requires write permission to this schema and only this schema.&#x20;

If you don't have credentials with write access available, warehouses like Postgres and Redshift support connecting in Read-only mode. Read-only Mode lets you connect to a warehouse quickly with credentials that only have read access to a warehouse. This can get you started quickly but some of the features described below are not available.

{% hint style="warning" %}
At this time, read-only connections do not support incremental update syncs, or Mirror or Append sync behaviors.
{% endhint %}

#### Data source models and segments

Once you have your data source connected, you can also create models on top of your data source, or connect data modeling integrations like [dbt](../../models/native-dbt-integration.md) and [Looker](../../models/looker.md). Models are optional in Census, you can also sync data directly from a data source table or view, but models give you a simple way to create authoritative locations for the full set of all of your paying customers, invoices, or whatever other reusable data concept matters for your business. And once you've built your models, Census makes it easy to quickly select and sync [Segments](../../segments/getting-started.md) of your models as well. &#x20;

### Destination Services

Census helps you keep your data in sync across all the business apps you use to engage with your customers, from advertising and marketing, through sales, all the way to finance. The goal is to keep all of those apps in sync, powered by the exact same set of data.&#x20;

The process of connecting a service is a little different for each. Sometimes, it's as simple as an OAuth confirmation flow or a straightforward API key. Other times, a few more steps are required.

Once you've connected a source, we'll be able to access a set of objects that service makes available. Typically this is a Contact or a Company, but there are often others and in some cases, even custom defined objects are supported.\
\
All of the connection steps, the objects, and other details for each service are covered here in the docs. \
\
And don't forget, our library of connections grows every week! Keep an eye on our [integrations page](https://www.getcensus.com/integrations) for all of our available destinations and let us know if we're missing something you need!

## 🧮 Creating Syncs

The most important action in Census is defining Syncs. A Sync defines the rules of how data should be synced, from your selected source to your destination.&#x20;

Syncs are also what makes Census so unique. Unlike most integration tools that are event-based, Census works to keep your source and destination "in sync" (just like Dropbox or other cloud storage service). The benefit is that you don't have to worry about dropped events or backfills anymore. If you change your data in the model, Census just syncs it, easy as that!

### 🔀 Sync Behaviors

{% hint style="success" %}
All of our syncs are incremental, which means we only sync records that are new or have their data changed since the previous sync.
{% endhint %}

Sync Behaviors tell Census the types of change it should apply to your data when a sync finds a matching (or not) record in a source and a destination. We support a few different sync behaviors:

|                                  |                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Update or Create (aka Upsert)    | Update existing destination records when IDs match, otherwise create new ones if they're missing.                                                                                                                                                                                                                                                                               |
| Update Only                      | Update existing objects in the destination, don't create any new ones.                                                                                                                                                                                                                                                                                                          |
| Create Only                      | Create a new object if it doesn't exist in the destination.                                                                                                                                                                                                                                                                                                                     |
| Mirror                           | <p>Keep the destination in sync with the source.</p><ul><li>If a row is added or edited in the source, update the destination. </li><li>If a previously synced row no longer is in the source, remove the matching object from the destination. Note: some services such as Braze offer other actions as well. See specific connector documentation for more details.</li></ul> |
| Append Only                      | <p>Treat the destination as an append only log of data suitable for Event data. </p><p></p><p>Read more about <a href="https://docs.getcensus.com/basics/defining-source-data/events">sending event data</a>.</p>                                                                                                                                                               |
| Delete                           | ⚠️ Here be dragons! Delete syncs takes the list of provided IDs and deletes them from the destination. Be careful! Providing an incorrect set of IDs can result in data loss! Census recommends you backup data if you're concerned about accidentally deleting the wrong records.                                                                                              |

{% hint style="warning" %}
Please note that some of these behaviors are only available for certain destinations. Visit our individual integration pages to view what's supported.
{% endhint %}

### 🔎 Matching Identifiers

Matching Identifiers let Census know how to associate data in the source with the destination. Both the source and destination need to provide a single, unique per record, identifying field. Census uses the identifiers to look for matches. When a match is found, or not found, it then can use your selected Sync Behavior to decide what to do. \
\
For example, if Census sees your source and destination both have records with the identifier ABCD1234, it knows that it should update that record with data from the source when you've got an Update Only, Update or Create, or Mirror Sync Behavior configured. &#x20;

### 🖇 Field Mappings

Once you've defined _how_ data is related between your source and destination, the next step is to let Census know _what_ properties should be updated. The field mapping step lets you specify how fields should be mapped from your source model to the destination object's fields. You can automatically add all matching fields, but even if names don't match, you can also provide the matching manually. If you remove fields from your mapping, Census will just stop updating those fields. We will not delete the values.

#### Creating new fields on your destination object

For some destinations, such as Braze, Customer.io or Iterable (see full list below), you can create new fields directly from the Census app. This means the next time a sync runs, Census will create new properties or attributes for that object in the destination. This is useful if you want to automatically create new fields based on the columns in your source data.

Simply select **"Sync All Properties"** when setting up a sync.

![Simply select "Sync All Properties"](../../.gitbook/assets/sync\_all\_fields.png)

{% hint style="info" %}
The following destinations currently support automatically adding new properties:&#x20;

Braze, Custom API, Customer.io, Google Cloud Storage, Google Sheets, Iterable, Klaviyo, Mixpanel, S3, Salesforce Marketing Cloud, Segment, SFTP, Slack, Vitally, Webhook
{% endhint %}

## Running Syncs&#x20;

Once syncs are created, you'll probably want to run them! That's where the real magic happens. There's a few things you should know about running and maintaining syncs though including how frequently they should run and what sync history tells you about the health of your sync.

### ⏱ Schedules and API

You can happily run a sync manually, but that's not all that useful on its own. The real power of Census is having your syncs run automatically. Once you've got your sync up and running, you can configure your sync to run automatically in three ways:

* [Schedules](triggering-syncs.md#schedule) including with Cron
* [Programmatically via API or Orchestration tool](triggering-syncs.md)
* [Automatically with dbt Cloud](../../models/native-dbt-integration.md#integrating-with-dbt-cloud)

Pick the sync execution trigger that makes for your connection and Census will keep the data flowing to your schedule.

### Understanding Sync history

You can dive deeper into why syncs failed, or what records were invalid from the source, or rejected by the destination, under the **Sync History** tab.

**Failed Syncs**\
****Hover over the status label to see a detailed error.

![](../../.gitbook/assets/census\_sync\_history\_failed\_sync.png)

**Invalid or rejected records**\
****Click the number of invalid or rejected records to see a sample (up to 100), and the reason why they were invalid or rejected.

**What is the difference between Invalid and Rejected records?**

* **Invalid** records are flagged and filtered by Census _prior_ to syncing to your destination. Census will check the source data for records with NULL identifiers and duplicates.
* **Rejected** records are records that were sent to the destination, but the destination did not accept them. The sample of rejected records will provide the specified reasons received from the destination.

![](../../.gitbook/assets/census\_sync\_invalid\_rejected\_records.png)

![Output of invalid records diagnostic log](../../.gitbook/assets/census\_invalid\_records.png)

## Wrapping things up

That's it! Now you've got everything you need to know to get the most out of Census, but don't worry, you can still get into the nitty gritty on individual data warehouses or service destinations. And we're always here to help. If you have any questions, just let us know!
