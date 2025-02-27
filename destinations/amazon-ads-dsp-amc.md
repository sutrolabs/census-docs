---
description: This page describes how to use Census with Amazon Ads DSP.
---

# Amazon Ads DSP (AMC)

Amazon Ads DSP is a demand-side platform that allows advertisers to programmatically buy display, video, and audio ads. Census can sync your customer data to Amazon Ads DSP to help you create and manage audiences for your ad campaigns.

## Getting Started

Connecting to your Amazon Ads account is straightforward.

1. From the [Destinations](https://app.getcensus.com/destinations) page, click **New Destination** and select Amazon Ads from the menu.
2. You'll first need to specify your desired **Region** by providing one of the following values:
   * North America: `www.amazon.com`
   * European Union: `eu.account.amazon.com`
   * Asian Pacific: `apac.account.amazon.com`
3. Complete the OAuth flow. Make sure your are signed into a user account that has permissions to both view all of your accounts, as well as submit data to them (read only accounts will not work).
4. Select the Ads account you wish to use with Census. If you'd like to sync to multiple accounts, you will need to add each as its own destination.

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

|  **Object Name** | **Supported?** | **Sync Keys**   | **Behaviors**    |
| ---------------: | :------------: | --------------- | ---------------- |
| Conversion Event |        ✅       | Event Unique ID | Send             |
|   Hashed Records |        ✅       | ID              | Update or Create |
|     DSP Audience |        ✅       | ID              | Update or Create |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/core-concept/#sync-behaviors) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Amazon Ads objects and/or behaviors.

### Conversion Events

Conversion Events are an [events.md](../syncs/structuring-data/events.md "mention") though they have some unique terminology and requirements. Visit [their documentation](https://advertising.amazon.com/API/docs/en-us/dsp-conversion-builder#tag/Conversion-Event-Data/operation/dspAmazonIngestConversionData) for more details.

Before you can sync conversion events, you need to first define them within the Amazon DSP Ui.

* Within Campaign Manager, select your desired **Advertiser**, then **Events manager**, then **Conversions** tab, and click Next under **Conversion API**.
* Once you've created your conversion, you'll need to copy the **Conversion Definition ID** to provide to Census.

Other than the Conversion Definition ID, you'll need a few more fields:

* Like other event syncs, Amazon requires an **Event Name** and a **Timestamp**.
* **Country Code** - Must be the two-letter country code described in [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes).
* **Match Key** - This is the user identifier of the user that triggered the event. Census currently only supports Email as a match key but will support additional options in the future. If you are going to provide Census with a pre-hashed value, it must follow this format:
  * Lowercase
  * Remove all non-alphanumeric characters \[a-zA-Z0-9] and \[.@-]
  * Remove any leading or trailing whitespace
  * Then apply SHA-256

There are also several optional fields available.

* **Currency Code** - This only applies to Off Amazon Purchase conversion definition type. This is the three letter currency code associated with the value of the event in [ISO-4217 format](https://en.wikipedia.org/wiki/ISO_4217#List_of_ISO_4217_currency_codes). If not provided, the currency setting on the conversion definition will be used.
* **Data Processing Options** - Currently, the only accepted value is `LIMITED_DATA_USE` which will cause Amazon to ignore this event. Typically, you can leave this field unmapped.
* **Units Sold** - This only applies to Off Amazon Purchase conversion definition type and represents the number of items purchased. If not provided on the conversion event, a default of 1 will be applied.
* **Value** - This has two modes depending on the conversion definition type.
  * For Off Amazon Purchase, this represents a monetary value. Must be a minimum of 0 and must not exceed 2 decimal points. If not provided, the static value provided on the conversion definition will be used.
  * For any other type, this represents a non-monetary value based on a scale of your choosing. Can be negative and must not exceed 2 decimal points. If not provided, the static value provided on the conversion definition will be used.

Census will send the Sync Key you specify as the unique identifier for your event sync to Amazon using the **Client Dedupe Id** property which allows Amazon to avoid capturing the same conversion event multiple times. In case of multiple events containing the same value, only the first will be kept.

### DSP Audiences

| **Advanced Configuration** |                               **Description**                               |
| -------------------------: | :-------------------------------------------------------------------------: |
|        Data Source Country | List of countries where user data in audience was collected for DMA support |

Amazon DSP Audiences are a pecular object in that they are actually two separate objects that are linked together through the use of a unique ID. Amazon DSP Audiences need to be managed in two phases:

1. First upload the PII about your audience members, where each record is identified by a unique ID you've assigned them. This is the Hashed Records (Part 1) object.
2. Wait for Amazon to process the data. Amazon's guidance is that this process can take up to 48hrs.
3. Then "assign" those records to an audience. This is the DSP Audience Members (Part 2) object.

This means using Amazon DSP Audiences requires at least two separate Census syncs. The first sync will upload the PII about your audience members and the second sync will assign those records to an audience. If you plan to create multiple audiences, we recommend that your Hashed Records sync uploads all of the records you plan to use in any of your audiences. Then you can create a separate DSP Audience Members sync for each audience you want to create.

Like Conversion Events, you can optionally provide pre-hashed values for your records. Amazon documents the requirements for this [here](https://advertising.amazon.com/help/GCCXMZYCK4RXWS6C). They are nearly identical to the requirements for Conversion Events, though notice that country and state identifiers are lower case if provided.

### Digital Markets Act (DMA)

Finally, to support upcoming Digital Markets Act (DMA) requirements, Amazon now accepts a Data Source Country field on the DSP Audience Members object. This field should be a comma separated list of two-letter country code using [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes) format. This list will be used by any segments created from this sync. This is required in order to create a new audience.

## Need help connecting to Amazon Ads DSP?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.
