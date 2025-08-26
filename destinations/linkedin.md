---
description: This page describes how to use Census with LinkedIn.
---

# LinkedIn

## Getting Started

In this guide, we will show you how to connect LinkedIn to Census.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your LinkedIn account (associated with your ads) ready, including the username and password.
* Have your data source properly configured within Census. See our docs for [supported data sources](broken-reference) for further information.

### Step 1: Connect LinkedIn

* Once you are in Census, navigate to [Destinations](https://app.getcensus.com/destinations)
* Click the **New Destination** button

![Select LinkedIn in the dropdown list](<../.gitbook/assets/LinkedIn Connection Button.png>)

![Click Confirm](<../.gitbook/assets/Confirm Census Connecting.png>)

* You'll be taken to a LinkedIn OAuth screen

![Sign in with Email/Phone and Password](<../.gitbook/assets/LinkedIn Username and Password Oauth.png>)

* You'll be taken back to Census where you need to select the Ads Account you want to sync data into

![If you have multiple, select the one of interest from the drop down](<../.gitbook/assets/Choose LI Account.png>)

### Step 2: Create a Model

Now navigate to the [Model section of our Dashboard](https://app.getcensus.com/models).​‌

Here you will have to write SQL queries to select the data you want to send to LinkedIn. Here are some ideas of data you should select‌.

* Current customers to advertise near renewal period
* Target Companies / Users in your Ideal Customer Profile (ICP)
* Competitors to exclude from advertising

## Supported Objects and Sync Behaviors

Census currently supports syncing to the following LinkedIn objects.

|  **Object Name** |    **Supported?**    | **Sync Keys**                                                                                  | **Behaviors**                     |
| ---------------: | :------------------: | ---------------------------------------------------------------------------------------------- | --------------------------------- |
|     Company List |           ✅          | Company Email Domain, Company Name, Company Page URL, Company Website Domain, Organization Urn | <p>Update or Create<br>Mirror</p> |
|        User List |           ✅          | Email (unhashed, SHA256/512 hashed), Google Advertising Id, Apple Advertising Id               | <p>Update or Create<br>Mirror</p> |
| Conversion Event | :white\_check\_mark: |                                                                                                | Send                              |

Census currently supports syncing to the Company List and User List LinkedIn objects through audience matching (based on [this documentation](https://docs.microsoft.com/en-us/linkedin/marketing/integrations/matched-audiences/matched-audiences)). The more information provided, the match rate will improve.

{% hint style="warning" %}
It is required to provide a DMP Segment Id for both Company List and User List
{% endhint %}

Contact the support team if you want Census to support more objects for LinkedIn.

## Need help connecting to LinkedIn?

Contact the support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
