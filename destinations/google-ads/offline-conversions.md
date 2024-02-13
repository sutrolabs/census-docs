---
description: Optimize your ad spend to find your best leads and customers.
---

# Offline Conversions

{% embed url="https://www.youtube.com/watch?v=4zjoFp0fkNU" %}

## Connect your Google Ads Account

Follow the [set-up instructions here!](https://docs.getcensus.com/destinations/google-ads)

## 🔄 Supported Objects & Behaviors

|                       |                  |                          |
| --------------------- | ---------------- | ------------------------ |
| **Object**            | **Behaviors**    | **Identifier**           |
| Click Conversion      | Update or Create | Click ID, WBRAID, GBRAID |
| Call Conversion       | Update or Create | Caller ID                |
| Enhanced Conversion   | Update or Create | Order ID                 |
| Conversion Adjustment | Append           |                          |

[Contact us](mailto:support@getcensus.com) if you're looking for additional Sync Behaviors!

{% hint style="info" %}
Learn more about our sync behaviors on our [Core Concept page](../../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

## Sync Offline Click and Call Conversions with Census

### 1. Create or find your custom conversion event in Google Ads

Google Ads has extensive documentation on [creating offline conversion events](https://support.google.com/google-ads/answer/7012522?hl=en-GB). The main steps are:

1. Create a new conversion action.
2. Select the data source for this conversion action as **Import**.
3. Select **Other data sources or CRMs**.
4. Select **Track conversions from clicks** or **Track conversions from calls**.
5. Enter a name for the conversion action that you're creating. Hold onto this name exactly as entered -- spelling and capitalization will be important when syncing these conversions via Census!
6. Choose your [counting option](https://support.google.com/google-ads/answer/3438531?hl=en-GB) for the conversion action, either **One conversion** or **Every conversion**. Many offline conversions occur only once (e.g. "Reached onboarding milestone X"). In this case, select the counting option **One conversion** to protect yourself from accidentally syncing duplicate conversions.
7. Complete the set-up for this conversion event, selecting your desired conversion window (we recommend using the maximum 90-days) and ads attribution model.

{% hint style="danger" %}
**Important**: After creating a new conversion action, Google recommends waiting 6 hours before syncing conversions for that conversion action. If you sync conversions during the first 6 hours, it can take two days for those conversions to appear on your reports.
{% endhint %}

### 2. Create your Census Model for the Conversion Action

Navigate to the [Models](https://app.getcensus.com/models) page.​

Here you can write SQL queries that contain the conversion action you want to send to Google Ads.

Google Ads Offline Click and Call Conversions require a specific set of properties. We'll want a model that has the following three required fields:

* One of: the **Google Click ID** (also often known as the `gclid`), **WBRAID**, or **GBRAID** value.
* The **Conversion Name**, spelled exactly as it is found in Google Ads
* The **Conversion Timestamp**, with timezone specified -- either using your warehouse's "timestamp with timezone" datatype, or hard-coded in a string (e.g. '2021-03-04 09:23:57+0000').

Optional properties include:

* Order ID, a unique reference in your systems for this conversion action
* Conversion Value, positive non-zero decimal values accepted (e.g. 1.00 USD = 1.00)
* Currency Code, the[ ISO 4217 3-character currency code](https://developers.google.com/adwords/api/docs/appendix/codes-formats#expandable-18) (e.g. 'USD')
* External Attribution Credit and Model, calculated outside Google Ads

Once you have created your model, click save.

### 3. Create your Sync

Now head to the [Sync page](https://app.getcensus.com/syncs) and click the **Add Sync** button

In the "**What data do you want to sync?"** section

* For the **Connection**, select the data warehouse you connected in the Prerequisites Step 2
* For the **Source,** select the model you created in step 2 of this section

Next up is the **"Where do you want to sync data to?"** section

* Pick **Google Ads** as the Connection
* For Object, pick **Click Conversion** or **Call Conversion**

For the "**How should changes to the source be synced?"** section

* **Append** will be selected by default
* Pick the right mapping key, the **Google Click ID** in your model

Finally, select the fields you want to update in the Mapper in the **"Which Fields should be updated?"** section. Here simply map the fields from your model to the properties of the Click or Call Conversion.

The end result should look something like this:

![](../../.gitbook/assets/screely-1631098088943.png)

Click the **Next** button to see the final preview which will have a recap of what will happen when you start the sync.

### 4. Confirm the conversions are now in Google Ads

It may take around 3 hours for synced offline conversions to show up in your Google Ads account. When they do, they'll appear in reporting on these conversion actions. To learn more about reporting on these conversions, you may wish to visit [this Google Ads help article](https://support.google.com/google-ads/answer/6270625).

## Sync Enhanced Conversions with Census

Google Ads also supports conversion tracking on the web if you only know your prospect or customer's email or phone number, using ["Enhanced Conversions"](https://support.google.com/google-ads/answer/13261987). These conversions can be used in place of, or as a supplement to, Click Conversions.

Essentially, Google will compare the person's email or phone number to its database of Google users and ad clicks, and give credit for the Conversion to an ad campaign when it finds a match.

### 1. Create or find your custom conversion event in Google Ads

Setting up a conversion in Google Ads is [exactly the same as traditional Click Conversions](https://support.google.com/google-ads/answer/13261987). However, Enhanced Conversions require slightly different data points so that Google can match a person to your conversion, and avoid duplication if you also track this conversion using other methods.

### 2. Create your Census Model for the Conversion Action

Navigate to the [Models](https://app.getcensus.com/models) page.​

Here you can write SQL queries that contain the conversion action you want to send to Google Ads, plus the data Google needs to track the conversion via the Enhanced Conversion mechanism.

Google Enhanced Conversions require a specific set of properties.

#### A. Minimum Conversion Parameters

We'll want a model that has the following three required fields:

* The **Order ID**
  * If you are tracking the conversion solely as an Enhanced Conversion, any unique ID will do
  * If you are supplementing existing conversion tracking, use the same Order ID that you're already sending to Google Ads
* The **Conversion Name**, spelled exactly as it is found in Google Ads
* The **Conversion Timestamp**, \_\_ with timezone specified -- either using your warehouse's "timestamp with timezone" datatype, or hard-coded in a string (e.g. '2021-03-04 09:23:57+0000').



#### B. User Identifiers

You also **must** supply user identifier parameters so that Google can match this conversion to its records of users and ad click.

You may choose to use a pre-hashed value (if you have one), or for Census to perform the hashing for you:

* **Email**, normalized with the following transformations:
  * Remove leading/trailing whitespaces.
  * Convert the text to lowercase.
  * Remove all periods (.) that precede the domain name in gmail.com and googlemail.com email addresses.
* **Phone Number**, formatted to the [E164 standard](https://en.wikipedia.org/wiki/E.164).

#### C. Optional Parameters

* **Conversion Value**, positive non-zero decimal values accepted (e.g. 1.00 USD = 1.00)
* **Currency Code**, the[ ISO 4217 3-character currency code](https://developers.google.com/adwords/api/docs/appendix/codes-formats#expandable-18) (e.g. 'USD')

Once you have created your model, click **save**.

### 3. Create your Sync

Now head to the [Sync page](https://app.getcensus.com/syncs) and click the **Add Sync** button

In the "**What data do you want to sync?"** section, select the model you created in step 2 of this section, or an existing table that contains this data.

Next up is the **"Where do you want to sync data to?"** section

* Pick **Google Ads** as the Connection
* For Object, pick **Enhanced Conversion**

Finally, select the fields you want to update in the Mapper in the **"Set Up Field Mappings"** section. Here simply map the fields from your model to the properties of the Enhanced Conversion.

The end result should look something like this:

<figure><img src="../../.gitbook/assets/screely-1695656460930.png" alt=""><figcaption></figcaption></figure>

Click the **Next** button to see the final preview which will have a recap of what will happen when you start the sync.

### 4. Confirm the conversions are now in Google Ads

It may take around 3 hours for synced offline conversions to show up in your Google Ads account. When they do, they'll appear in reporting on these conversion actions. To learn more about reporting on these conversions, you may wish to visit [this Google Ads help article](https://support.google.com/google-ads/answer/6270625).

## Conversion Adjustments

Once a conversion has already been reported to Google Ads, you can [adjust the conversion](https://support.google.com/google-ads/answer/7686447) at a later point in time using Census.

A conversion adjustment requires exactly one of the following sets of properties in order to identify which conversion to adjust.

* **Order ID** or
* **Google Click ID (GCLID) and exact conversion date time**

### Digital Markets Act (DMA)

When syncing Conversions to Google Ads, you can include consent information to ensure compatibility with [Google's EU User Consent Policy](https://www.google.com/about/company/user-consent-policy/). Google Ads objects now support two additional fields: `Consent for ad user data` and `Consent for ad personalization`, which can be set to one of the following values: `UNKNOWN`, `UNSPECIFIED`, `GRANTED`, `DENIED`. See Google's [documentation](https://support.google.com/google-ads/answer/14310715) for more information on the behavior of different options.