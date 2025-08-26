---
description: This page describes how to use Census with Iterable.
---

# Iterable

Iterable is a growth marketing platform that enables brands to create, execute, and optimize campaigns to power world-class customer engagement across email, push, SMS, in-app, and more with unparalleled data flexibility.

{% hint style="info" %}
Please note that for larger syncs, it might take \~10 minutes for you to see the new data in Iterable's UI.
{% endhint %}

## Getting Started

The first step is to create a new API key in Iterable. API keys are created within an Iterable Project so ensure you're in the project you want to connect to Census.

1. Within your Iterable project, click the **Integration** option in the top menu and select **API keys**.
2. We recommend you create a new API key for Census. Click **+ New API Key** in the top right.
3. Select the "Server-side" key type from the subsequent dropdown.
4. Copy the resulting key (a string of 32 characters).

You'll also need to know your Iterable region. This is not currently displayed in the UI, but should be visibile in the URL when you're logged into Iterable.

Back in Census, navigate to the Destinations page and click **Add Destination**. Select Iterable from the list of destinations. Provide your API Key and select your region. Finally click **Save**.

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

| **Object Name** | **Supported?** | **Sync Keys**  | **Behaviors**                 |
| --------------: | :------------: | -------------- | ----------------------------- |
|            User |        ✅       | User ID, Email | Update or Create, Update Only |
|           Event |        ✅       | Event ID       | Send                          |
|         Catalog |        ✅       | Key            | Update or Create, Mirror      |
|     Static List |        ✅       | User ID, Email | Mirror                        |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

Contact our support team if you want Census to support more Iterable objects and/or behaviors

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

We recommend testing your JSON fields in Redshift by using Redshift's [`IS_VALID_JSON`](https://docs.amazonaws.cn/en_us/redshift/latest/dg/IS_VALID_JSON.html) and [`IS_VALID_JSON_ARRAY`](https://docs.amazonaws.cn/en_us/redshift/latest/dg/IS_VALID_JSON_ARRAY.html) functions, especially before creating new fields in Iterable via Census's field mapper.

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

## Need help connecting to Iterable?

Contact our support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
