---
description: This page describes how to use Census with Iterable.
---

# Iterable

{% hint style="info" %}
Please note that for larger syncs, it might take ~10 minutes for you to see the new data in Iterable's UI.
{% endhint %}

## 🏃‍♂️ Getting Started

### 1. Create a new Iterable API key

To connect Census to your Iterable, you'll need to provide Census with an API key so that we can talk to it directly. 

**A. Go to your Integration &gt; API keys page**

In the top right, click on your name, and select Account Settings

![](../.gitbook/assets/iterable_setup1.png)

**B. Create a new key for Census**

Click the Create New API key button in the top left.

![](../.gitbook/assets/iterable_setup2.png)

Select the "Standard" key type from the subsequent dropdown. 

![](../.gitbook/assets/iterable_setup3.png)

Copy the resulting key \(a string of 32 characters\) to add it to Census.

**C. Create a new Iterable connection in Census**

* Visit the Connections tab in Census
* Then select Iterable from the Add Service menu
* Finally, paste in the API Key you just created. You can customize the name of the connection if you plan to connect multiple instances of Iterable.

![](../.gitbook/assets/iterable_setup4.png)

Iterable will now appear as a new destination for Census syncs. 

### 2. Syncing data into Iterable

Once the service is added, you can sync users from your database into your Iterable audience \(and augment existing contacts with new product data\).

When creating a sync in Census, you can use _email_ or _userId_ as an identifier. 

![](../.gitbook/assets/iterable_setup5.png)

You can map data fields into your existing Iterable audience schema \(including into nested schemas\). You can also create new custom fields by clicking "+ Add Custom Field" when editing the mapping.

![](../.gitbook/assets/iterable_setup6.png)

{% hint style="info" %}
**Nested Objects in Iterable**

Iterable supports nested objects and fields on its User object. If you would like to send JSON, Arrays, or JSON Arrays to a field in Iterable, you may.

For most data warehouses, there are specific datatypes for these types of values. However, Amazon Redshift does not natively support JSON, so you will want to store this type of data as a string value. Provided that the values are valid JSON, Census will ensure that it is nested as expected when sending the data to Iterable. 

As an example, valid JSON for a field named "subscription" could have the following value:

```text
{
  "plan": "Premium",
  "products": [
      "unlimited_users",
      "24_hr_support_sla"
    ]
}
```

We recommend testing your JSON fields in Redshift by using Redshift's [IS\_VALID\_JSON](https://docs.amazonaws.cn/en_us/redshift/latest/dg/IS_VALID_JSON.html) and [IS\_VALID\_JSON\_ARRAY](https://docs.amazonaws.cn/en_us/redshift/latest/dg/IS_VALID_JSON_ARRAY.html) functions, especially before creating new fields in Iterable via Census's field mapper.
{% endhint %}

## 🗄 Supported Objects

| **Object Name** | **Supported?** | Identifiers |
| ---: | :---: | :--- |
| User | ✅ | User ID, Email |
| Event | ✅ | Event ID |

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Iterable.

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about what all of our sync behaviors on our [Core Concept page](../basics/core-concept.md#the-different-sync-behaviors).
{% endhint %}

| **Behaviors** | **Supported?** | **Objects?** |
| ---: | :---: | :---: |
| **Update or Create** | ✅ | User |
| **Update Only** | ✅ | User |
| **Append** | ✅ | Event |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync Behaviors for Iterable.

## 🚑 Need help connecting to Iterable?

Contact us via support@getcensus.com or start a conversion via the [in-app](https://app.getcensus.com) chat.

