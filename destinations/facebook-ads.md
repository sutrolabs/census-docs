---
description: >-
  This page describes how to use Census with Facebook Ads (Audiences and
  Conversions).
---

# Facebook Ads


In this guide, we will show you how to connect Facebook Ads to Census and create your first sync.

## 🏃‍♀️ Getting Started

Facebook Ads support two separate authentication mechanisms: OAuth and System User. We recommend using System User for the most reliable connection long term as it does not require re-authentication every 60 days.

### Using a System User (Recommended)

The steps to create a [Facebook System User](https://www.facebook.com/business/help/327596604689624?id=2190812977867143) are more complex than using OAuth, but it's the most reliable way to connect to Facebook Ads, especially if you intend to use the connection long term.

A regular system user is recommended over an admin system user. You can use an existing system user or create a new one with the following steps:

1.  To generate a system user token, you'll first need an application. If you don't have one already, you can create one with the following steps:

    * Open your Business Manager
    * Navigate to **Business Settings > Accounts > Apps**
    * Click **Add** and then **Create New App ID**
    * For use case select **Other**

    <figure><img src="../.gitbook/assets/FB App UseCase.png" alt="Facebook App UseCase Screen" width="375"><figcaption><p>New app usecase screen</p></figcaption></figure>

    * Then for Type select **Business**

    <figure><img src="../.gitbook/assets/FB New App Type.png" alt="" width="375"><figcaption><p>New app type</p></figcaption></figure>

    * Then fill out the relevant details and press **Create App**

    <figure><img src="../.gitbook/assets/FB New App Details.png" alt="" width="375"><figcaption><p>New app details</p></figcaption></figure>
2.  Now you can generate a system user for the app. Go to your Business Manager and navigate to **Business Settings > Users > System Users**
    <figure><img src="../.gitbook/assets/Screenshot 2023-05-18 at 8.23.16 AM.png" alt="" width="375"><figcaption><p>Business Manager Navigation Panel</p></figcaption></figure>
3. Above your list of system users click **Add** to create a new System User
4. Provide a name and role. Census does **not** need an `Admin` role, `Employee` is sufficient.
5. Once the system user is created click on **Add Assets** and assign the relevant Product Catalogs that you want Census to sync to. Make sure to assign _full control_ of the catalog to the system user.
6. Now generate a token for the System User by pressing **Generate New Token**, select the relevant app you created earlier, select the relevant scopes, and then press **Generate Token**
   * You will need to provide _at least_ the `business_management` and `catalog_management` scopes for Census to sync to your product catalogs
   *   Make sure to select `Never` for token expiration so you do not need to manually reauthorize your Census connection every 60 days.



       <figure><img src="../.gitbook/assets/Screenshot 2023-05-18 at 8.33.35 AM.png" alt="" width="375"><figcaption><p>Token Expiration &#x26; Scopes Page</p></figcaption></figure>
7. Once your token is generated be sure to save it in a safe place. This is the token you must provide to Census as a credential for your connection.

### Using an Existing System User

If you already have a system user you can use it by simply generating a new token with the correct permissions. Census needs the `business_management` and `catalog_management` scopes. Also be sure to assign the catalog asset to your system user so Census can sync to it.

### Using OAuth

If you'd like to use OAuth, connecting to Facebook Ads is as simple as clicking the "Connect" button and following the prompts. Census will guide you through the process of authenticating with Facebook and selecting the ad accounts you'd like to sync data from.

The downside of this method is that authentication will expire every 60 days and require re-authentication. We recommend using a System User for the most reliable connection long term.


### Setting Up Connection

You are now ready to set up a connection. Head to the Census Destinations page and press **New Destination**. From the list, select Facebook Ads.

Select the authentication method you prefer and provide your token or complete the OAuth flow. Once you hit save, you can use your destination to create new syncs.


## 🗄 Supported Objects

|                                                                           **Object Name** | **Supported** | **Identifiers**                                                                                           |**Behaviors** |
| ----------------------------------------------------------------------------------------: | :------------: | --------------------------------------------------------------------------------------------------------- | :------------: |
|                                                                                  Audience |        ✅       | [External ID](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/external-id/) | Update or Create, Mirror |
| Conversions ([CAPI](https://developers.facebook.com/docs/marketing-api/conversions-api/)) |        ✅       | Any unique ID                                                                                             | Append |


Census supports [custom fields on Conversions](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data#custom-properties), simply Create New Field when creating a Conversions sync.

Update or Create will add or update users to the audience, but will never remove users. Mirror will also remove users that have been removed from the source.\
\
Note: If you're reusing an existing Facebook Audience, Census will not remove any users already added to that audience through other means. Census only removes users that it created initially.

{% hint style="info" %}
Learn more about our sync behaviors on our [Core Concept page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

## Audiences

### 1. Collect the Facebook Audience ID

The first step is finding the audience you'd like to sync data into. You can do that by visiting the [Audiences section of Facebook's Ads Manager](https://business.facebook.com/adsmanager/audiences). Make a note of the ID (name will work too) of the audience you want to sync to from Census.

If you'd like to use a new Facebook Audience with Census, go ahead and create it now. Facebook Audiences makes it a bit confusing to create a new empty audience for Census. You'll need to create a new Customer List Custom Audience and then upload a CSV with the columns that you'll be using.

### 2. Create a SQL Model from your source data

The results of the View, Table, or Census Model should contain a row per user. Each row will have three or more columns:

1. A unique identifier for the user, Facebook calls this the External ID. This is usually a unique ID from your application database, but could be email as well if that also uniquely identifies each row.
2. A column indicating what Facebook Audience the user should be synced to (can be the audience name or audience ID).
3. Any other identifying fields that Facebook can use to match your audience. Facebook requires these fields to be formatted in a certain way. For example, email must be lower-case. You can read more about each of the formatting requirements in the[ Facebook Documentation](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#hash).

Example Facebook Audience Model:

```sql
SELECT
    user_id,
    LOWER(email_address) AS email,
    'active users audience' AS fb_audience
FROM user_activity_table;
```

### 3. Create a sync

Now that your data is prepared and in the correct format, we're ready to start syncing users to Facebook.

#### **A. Select your model from above as a data source and Facebook Audiences as a destination.**

![](../.gitbook/assets/fb\_setup1.png)

#### **B. Choose the appropriate sync behavior**

Update or Create will add or update users to the audience, but will never remove users. Mirror will also remove users that have disappeared from the source. Note: If you're reusing an existing Facebook Audience, Census will not remove any users already added to that audience through other means. Census only removes users that it created initially.

![](../.gitbook/assets/fb\_setup2.png)

#### **C. Select an external identifier to match rows uniquely in Facebook**

This should be the user id or other external ID you selected when you created the model.

![](../.gitbook/assets/fb\_setup3.png)

#### **D. Associate users with the Audience**

Let Census know which column should be used to assign users to their audience. Select the Audience's ID or Name to correspond to the type of identifier you're providing with your model.

![](../.gitbook/assets/fb\_setup4.png)

#### **E. Map the remaining identifying fields**

You can then map any user identifying fields that are present in your source data (e.g. phone number, email, first name, last name, etc).

## Conversions

Send web events directly to Facebook from your warehouse, exactly as if they were pixel events using the Facebook Conversions API.

### 1. Choose or create a conversion event in Facebook, Collect the Pixel ID

To view all your Facebook Ads accounts' Pixel IDs go to the [Events Manager](https://www.facebook.com/business/help/898185560232180): [https://business.facebook.com/events\_manager2/list/](https://business.facebook.com/events\_manager2/list/).

Be sure to select the specific ads account you want to work on. You can switch ad accounts in the navigation bar on the left side of the screen.

In the events manager, you can view all your ad account's pixels and existing events. If a custom event doesn't exist already, Census will create it for you.

### 2. Create a sync

In your SQL model, dbt model, or table -- ensure that you have all required fields for your conversion sync, and any user identifiers so that Facebook can perform ad attribution. Facebook Conversion syncs require the following fields:

#### A. Event ID

Census requires the model to have a column that stores a unique identifier for each row so that Census never sends any duplicate records. We'll call this unique identifier column "Event ID". If you have an identifier that you are already passing via your pixel on the website for online versions of this conversion event, use this identifier. Some common examples include `user_id`, `lead_id`, and `order_id`.

#### B. Minimum Event Parameters

The Facebook Conversions API requires 4 fields for every event:

* Pixel ID - see above to find.
* [Action Source](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event#action-source) - This field allows you to specify where your conversions occurred. It accepts one of the following values: "email", "website", "phone\_call", "chat", "physical\_store", "system\_generated", and "other".
* [Event Name](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event#event-name) - A Facebook pixel [Standard Event](https://developers.facebook.com/docs/facebook-pixel/implementation/conversion-tracking#standard-events) or [Custom Event](https://developers.facebook.com/docs/facebook-pixel/implementation/conversion-tracking#custom-events) name.
* [Event Time](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event#event-time) - can be up to 7 days before you send an event to Facebook. This date must be sent in GMT timezone.

#### C. Customer Information Parameters

Facebook attributes conversions back to ad campaigns by identifying the users that saw or interacted with ad content. To do so, they accept the following user identifiers and will attempt to match each conversion to a facebook user. **Sending more identifiers will improve match rates**.

For a more complete description of each identifier, please see [Facebook's API documentation](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters). When Facebook requires a field's value to be hashed, you may choose to use a pre-hashed value (if you have one), or for Census to perform the hashing for you.

* Email
* Phone
* Gender
* Date of Birth
* Last Name
* First Name
* City
* State
* Zip
* Country
* External ID
* Client IP address
* Client user agent
* Click ID
* Browser ID
* Subscription ID
* Facebook Login ID
* Lead ID

#### Putting it all together...

Your final sync configuration will look like the following!

![](<../.gitbook/assets/screely-1626208532062 (1).png>)

### Sample Data Requirements

| event\_id | pixel\_id  | action\_source | timestamp               | event\_name   | email           | other customer information parameters                                                                                 |
| --------- | ---------- | -------------- | ----------------------- | ------------- | --------------- | --------------------------------------------------------------------------------------------------------------------- |
| 1234      | 1000294785 | website        | 2022-01-01 00:00:00+000 | sample\_event | test@domain.com | [Like the ones listed above](https://docs.getcensus.com/destinations/facebook-ads#c.-customer-information-parameters) |


#### Data Normalization

Facebook Audiences and Conversions are a bit unique from other services. We do not upload the data you provide directly. Instead, it's "matched" to Facebook's audience. To do this, both sides "hash" their data so users can be compared without revealing the actual personally identifiable information.

Census automatically takes care of this hashing step for you.

**However, all values provided to Census must be lowercase**. You can use this standard SQL function `LOWER()`that works across all data warehouses.

Additionally, there is specific behavior for certain fields in Facebook, check out [this link](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) to their docs, but you also need to remove white spaces on certain Customer Information parameters. For example:

* City changing from 'San Antonio' => 'sanantonio' using `replace( ,' ','')`
* Date of birth changing from '1983-12-24' => '19831224' using `replace( ,'-','')`

Please [contact us](mailto:support@getcensus.com) if there are additional Facebook Ads objects you'd like us to support.

## 🆘 Common Errors

Sometimes error messages can be a little cryptic. Here's some Facebook errors that pop up on occasion and what they mean.

#### Authentication errors when syncing Custom Audiences:

{% code overflow="wrap" %}
```
Custom Audience terms have not been accepted: Accept the Custom Audience terms at [url] to create or edit an audience with an uploaded customer list.
```
{% endcode %}

In order to get around this error, the user that does the authentication to Census should be the same user that accepts the policy updates. For example, you may have a "Business" account on Facebook, but to authenticate to Census you might use personal Facebook accounts that are "attached" to the business account.  The corresponding personal account would need to accept the policy. \
\
If you are unsure if your team has already accepted the terms and conditions, you can make a GET call to see if your account has signed the terms and conditions.\
\
The API call is: \
`GET act_<AD_ACCOUNT_ID>?fields=tos_accepted` \
\
A sample response would be something like this:&#x20;

```
{
  "tos_accepted": {
    "custom_audience_tos": 1 // this means the terms were signed
  },
  "id": "act_<AD_ACCOUNT>"
}
```

## 🚑 Need help connecting to Facebook?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
