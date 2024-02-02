---
description: This page describes how to use Census with Iterable.
---

# Iterable

{% hint style="info" %}
Please note that for larger syncs, it might take \~10 minutes for you to see the new data in Iterable's UI.
{% endhint %}

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Iterable to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Iterable account ready.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Azure Synapse](../sources/azure-synapse.md)
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Elasticsearch](https://docs.getcensus.com/sources/elasticsearch)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [MySQL](https://docs.getcensus.com/sources/mysql)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Rockset](https://docs.getcensus.com/sources/rockset)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)
  * [SQL Server](https://docs.getcensus.com/sources/sql-server)

### 1. Create a new Iterable API key

To connect Census to your Iterable, you'll need to provide Census with an API key so that we can talk to it directly.

**A. Go to your Integration > API keys page**

In the top right, click on your name, and select Account Settings

![](../.gitbook/assets/iterable\_setup1.png)

**B. Create a new key for Census**

Click the Create New API key button in the top right.

![](<../.gitbook/assets/image (8).png>)

Select the "Server-side" key type from the subsequent dropdown.

![](<../.gitbook/assets/image (1) (1) (1) (1).png>)

Copy the resulting key (a string of 32 characters) to add it to Census.

![](<../.gitbook/assets/image (17).png>)

**C. Create a new Iterable connection in Census**

* Visit the Destinations tab in Census
* Click New Destination and select Iterable from the menu
* Finally, paste in the API Key you just created. You can customize the name of the connection if you plan to connect multiple instances of Iterable.

![](../.gitbook/assets/iterable\_setup4.png)

Iterable will now appear as a new destination for Census syncs.

### 2. Syncing data into Iterable

Once the service is added, you can sync users from your database into your Iterable audience (and augment existing contacts with new product data).

When creating a sync in Census, you can use _email_ or _userId_ as an identifier.

![](../.gitbook/assets/iterable\_setup5.png)

You can map data fields into your existing Iterable audience schema (including into nested schemas). You can also create new custom fields by clicking "+ Add Custom Field" when editing the mapping.

![](../.gitbook/assets/iterable\_setup6.png)

## 🗄 Supported Objects

| **Object Name** | **Supported?** | **Sync Keys**  |
| --------------: | :------------: | -------------- |
|            User |        ✅       | User ID, Email |
|           Event |        ✅       | Event ID       |
|         Catalog |        ✅       | Key            |
|     Static List |        ✅       | User ID, Email |

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Iterable.

### Handling Nested Objects

Iterable supports nested objects and fields on its User object. If you would like to send JSON, Arrays, or JSON Arrays to a field in Iterable, you may.

For most data warehouses, there are specific datatypes for these types of values. However, Amazon Redshift does not natively support JSON, so you will want to store this type of data as a string value. Provided that the values are valid JSON, Census will ensure that it is nested as expected when sending the data to Iterable.

As an example, valid JSON for a field named "subscription" could have the following value:

```
{
  "plan": "Premium",
  "products": [
      "unlimited_users",
      "24_hr_support_sla"
    ]
}
```

We recommend testing your JSON fields in Redshift by using Redshift's [`IS_VALID_JSON`](https://docs.amazonaws.cn/en\_us/redshift/latest/dg/IS\_VALID\_JSON.html) and [`IS_VALID_JSON_ARRAY`](https://docs.amazonaws.cn/en\_us/redshift/latest/dg/IS\_VALID\_JSON\_ARRAY.html) functions, especially before creating new fields in Iterable via Census's field mapper.

### Syncing to GeoLocation Fields

Iterable has a field data type called [GeoLocation](https://support.iterable.com/hc/en-us/articles/208183076-Field-Data-Types#geo-location) that stores a latitude and longitude in an object. To create or sync to an existing Iterable GeoLocation field with Census there are a couple of requirements.

* The destination field name must use the suffix `_geo_location` . **NOTE:** The suffix is case sensitive
* The geo\_location object data can only contain two fields, `lat` and `lon`
  * **Example**: `{ "lat": 31, "lon": -14 }`
  * For more information on using structured data within Census please visit our [Structured Data](https://docs.getcensus.com/basics/defining-source-data/structured-data) documentation.

### Syncing to Catalogs

Iterable Catalogs let you create custom objects within Iterable that can be associated with users. Here's a few tips when using Catalogs to make sure your sync is successful.

* Census will rely on the schema you've defined inside Iterable. We don't currently allow you to create fields from Census.
* We strongly recommend that you specify the type of each catalog field through the Iterable UI before using Census to sync items. Untyped fields are not searchable by collections. And any catalog item uploaded _before_ a field is typed will not have searchable by that field. If we see an untyped field in Census, we will send string values to that field because we don't know what type it should be.
* In practice, even if a field is typed, Iterable will accept and update field values of different types. For instance, if the `age` field is typed as a Long, but we send a value of "25", Iterable will accept and update records to use the string "25" as age.
* Iterable can take a while to process new Catalog items. In some cases, we see Iterable take as long as 20 minutes before the record appears.

### **Invalid Email Rejections**

When syncing to the User object Iterable may reject some records with the message `Invalid Email`. This is thrown for in the following cases

* **Invalid Email Formatting:** When an email address is not properly formatted. For more information about the formatting guide used by Iterable please refer to Iterable's documentation [linked here](https://support.iterable.com/hc/en-us/articles/209082806-Email-Validation-in-Iterable).
* **Forgotten/Deleted Emails**: Iterable will also send reject a record with Invalid Email when a user has been previously forgotten or deleted. For more information regarding this functionality in Iterable please refer to the Iterable documentation [linked here](https://support.iterable.com/hc/en-us/articles/360029174171-Responding-to-GDPR-Requests-#right-to-be-forgotten-requests).

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about what all of our sync behaviors on our [Core Concept page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** |      **Objects**     |
| -------------------: | :------------: | :------------------: |
| **Update or Create** |        ✅       |     User, Catalog    |
|      **Update Only** |        ✅       |         User         |
|           **Append** |        ✅       |         Event        |
|           **Mirror** |        ✅       | Catalog, Static List |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync Behaviors for Iterable.

## 🚑 Need help connecting to Iterable?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
