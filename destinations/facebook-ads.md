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

    <figure><img src="../.gitbook/assets/Screenshot 2024-03-06 at 4.04.42 PM.png" alt="Facebook App UseCase Screen" width="563"><figcaption><p>New app usecase screen</p></figcaption></figure>

    * Then for Type select **Business**

    <figure><img src="../.gitbook/assets/Screenshot 2024-03-06 at 4.05.04 PM.png" alt="" width="563"><figcaption><p>New app type</p></figcaption></figure>

    * Then fill out the relevant details and press **Create App**

    <figure><img src="../.gitbook/assets/Screenshot 2024-03-06 at 4.05.22 PM.png" alt="" width="563"><figcaption><p>New app details</p></figcaption></figure>
2. Now you can generate a system user for the app. Go to your Business Manager and navigate to **Business Settings > Users > System Users**

Above your list of system users click **Add** to create a new System User

1. Provide a name and role. Census does **not** need an `Admin` role, `Employee` is sufficient.
2.  Once the system user is created click on **Add Assets** and add the Application you created in step one. Make sure to assign _full control_ of the app to the system user.



    <figure><img src="../.gitbook/assets/Screenshot 2024-03-06 at 4.08.15 PM.png" alt=""><figcaption><p>Assign your System User full control to your Application</p></figcaption></figure>
3.  You'll also need to assign your System User _full control_ over any Ad Accounts that own any Custom Audiences you'd like to sync data to.

    <figure><img src="../.gitbook/assets/Screenshot 2024-05-01 at 3.06.32 PM.png" alt=""><figcaption><p>Assign your System User full control to your Ad Accounts</p></figcaption></figure>
4. Now generate a token for the System User by pressing **Generate New Token.**
   * You will need to provide the following scope for Census to sync to your Facebook Conversions and Custom Audiences: `ads_management`
   *   Make sure to select `Never` for token expiration so you do not need to manually reauthorize your Census connection every 60 days.

       <figure><img src="../.gitbook/assets/Screenshot 2024-03-06 at 4.08.58 PM.png" alt="" width="563"><figcaption><p>Token Expiration &#x26; Scopes Page</p></figcaption></figure>
5. Once your token is generated be sure to save it in a safe place. This is the token you must provide to Census as a credential for your connection.

{% hint style="info" %}
To validate that your System User Token is set up correctly and has the necessary scopes you can input your access token in the link below.\
\
[https://developers.facebook.com/tools/debug/accesstoken](https://developers.facebook.com/tools/debug/accesstoken)
{% endhint %}

<figure><img src="../.gitbook/assets/Screenshot 2024-03-08 at 2.54.09 PM.png" alt=""><figcaption><p>Correct scopes shown for Access Token in debugger</p></figcaption></figure>

### Using an Existing System User

If you already have a system user you can use it by simply generating a new token with the correct permissions. Be sure to assign the asset for your Application to your System User with full control. Census needs the `ads_management` scope.

### Using OAuth

If you'd like to use OAuth, connecting to Facebook Ads is as simple as clicking the "Connect" button and following the prompts. Census will guide you through the process of authenticating with Facebook and selecting the ad accounts you'd like to sync data from.

The downside of this method is that authentication will expire every 60 days and require re-authentication. We recommend using a System User for the most reliable connection long term.

### Setting Up Connection

You are now ready to set up a connection. Head to the Census Destinations page and press **New Destination**. From the list, select Facebook Ads.

Select the authentication method you prefer and provide your token or complete the OAuth flow. Once you hit save, you can use your destination to create new syncs.

If you are setting up a connection with a System User Token when you input your Ad Account ID manually you will want to prepend the string `act_` to your Ad Account ID. When connecting through Oauth this is automatically prepended, but will need to be done manually if using a System User Token.&#x20;

**Example:** `act_123456789`

## 🗄 Supported Objects and Behaviors

|                                                                           **Object Name** | **Supported** | **Identifiers**                                                                                                  |      **Behaviors**       |
|------------------------------------------------------------------------------------------:| :-----------: |------------------------------------------------------------------------------------------------------------------|:------------------------:|
|                                                                           Custom Audience |       ✅       | [External ID](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/external-id/), Email | Update or Create, Mirror |
| Conversions ([CAPI](https://developers.facebook.com/docs/marketing-api/conversions-api/)) |       ✅       | Any unique ID                                                                                                    |           Send           |

{% hint style="info" %}
Learn more about our sync behaviors on our [Core Concept page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

### Data Normalization

Facebook Audiences and Conversions, like many other ads destinations, don't upload raw data but instead send hashed information for "matching" to protect user PII.

Census automatically takes care of this hashing step for you.

**However, all values provided to Census must be lowercase**. You can use this standard SQL function `LOWER()`that works across all data warehouses.

```sql
SELECT
    user_id,
    LOWER(email_address) AS email,
    'active users audience' AS fb_audience
FROM user_activity_table;
```

Additionally, certain fields require removing whitespaces and punctuation. For example:

* City changing from 'San Antonio' => 'sanantonio' using `replace( ,' ','')`
* Date of birth changing from '1983-12-24' => '19831224' using `replace( ,'-','')`

See the [Facebook documentation](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) for more information on the specific requirements for each field. And please [contact us](mailto:support@getcensus.com) if you have any issues with this normalization.

### Audiences

Audiences provide a way to group users together for targeting in Facebook Ads. This is useful for creating custom audiences for ad targeting, lookalike audiences, and more.

Here's a few things to keep in mind when syncing to Facebook Audiences:

* You can reuse existing audiences or have Census create new ones.
* **Update or Create** will add or update users to the audience, but will never remove users. **Mirror** will also remove users that have disappeared from the source. Note: If you're reusing an existing Facebook Audience, Census will not remove any users already added to that audience through other means. Census only removes users that it created initially.

### Conversions

Send web events directly to Facebook from your warehouse, exactly as if they were pixel events using the Facebook Conversions API.

When sending conversions, you'll need to do a bit more work to ensure that the data is in the right format for Facebook. Here's a quick guide to get you started:

#### 1. Choose or create a conversion event in Facebook, Collect the Pixel ID

To view all your Facebook Ads accounts' Pixel IDs go to the [Events Manager](https://www.facebook.com/business/help/898185560232180): [https://business.facebook.com/events\_manager2/list/](https://business.facebook.com/events\_manager2/list/).

Be sure to select the specific ads account you want to work on. You can switch ad accounts in the navigation bar on the left side of the screen.

In the events manager, you can view all your ad account's pixels and existing events. If a custom event doesn't exist already, Census will create it for you.

#### 2. Event ID

Census requires source data to have a column that stores a unique identifier for each row so that Census never sends any duplicate records. We call this unique identifier column "Event ID". If you have an identifier that you are already passing via your pixel on the website for online versions of this conversion event, use this identifier. Some common examples include `user_id`, `lead_id`, and `order_id`.

#### 3. Minimum Event Parameters

The Facebook Conversions API requires 4 fields for every event:

* Pixel ID - Covered above.
* [Action Source](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event#action-source) - This field allows you to specify where your conversions occurred. It accepts one of the following values: "email", "website", "phone\_call", "chat", "physical\_store", "system\_generated", and "other".
* [Event Name](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event#event-name) - A Facebook pixel [Standard Event](https://developers.facebook.com/docs/facebook-pixel/implementation/conversion-tracking#standard-events) or [Custom Event](https://developers.facebook.com/docs/facebook-pixel/implementation/conversion-tracking#custom-events) name.
* [Event Time](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event#event-time) - can be up to 7 days before you send an event to Facebook. This date must be sent in GMT timezone.

#### 4. Customer Information Parameters

Facebook attributes conversions back to ad campaigns by identifying the users that saw or interacted with ad content. To do so, they accept the following user identifiers and will attempt to match each conversion to a facebook user. **Sending more identifiers will improve match rates**.

Census also supports [custom fields on Conversions](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data#custom-properties), simply Create New Field when creating a Conversions sync.

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

#### Sample Data Requirements

| event\_id | pixel\_id  | action\_source | timestamp               | event\_name   | email           | other customer information parameters                                                                                 |
| --------- | ---------- | -------------- | ----------------------- | ------------- | --------------- | --------------------------------------------------------------------------------------------------------------------- |
| 1234      | 1000294785 | website        | 2022-01-01 00:00:00+000 | sample\_event | test@domain.com | [Like the ones listed above](https://docs.getcensus.com/destinations/facebook-ads#c.-customer-information-parameters) |

## 🆘 Common Errors

Sometimes error messages can be a little cryptic. Here's some Facebook errors that pop up on occasion and what they mean.

#### Authentication errors when syncing Custom Audiences:

{% code overflow="wrap" %}
```
Custom Audience terms have not been accepted: Accept the Custom Audience terms at [url] to create or edit an audience with an uploaded customer list.
```
{% endcode %}

In order to get around this error, the user that does the authentication to Census should be the same user that accepts the policy updates. For example, you may have a "Business" account on Facebook, but to authenticate to Census you might use personal Facebook accounts that are "attached" to the business account. The corresponding personal account would need to accept the policy.

Facebook may require this to be completed when creating new audiences even if already accepted previously on the account.\
\
If you are unsure if your team has already accepted the terms and conditions, you can make a GET call to see if your account has signed the terms and conditions.\
\
The API call is:\
`GET act_<AD_ACCOUNT_ID>?fields=tos_accepted`\
\
A sample response would be something like this:

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
