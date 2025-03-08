---
description: This page describes how to use Census with NetSuite.
---

# NetSuite

## Getting Started

In this guide, we will show you how to connect NetSuite to Census and create your first sync.

{% embed url="https://www.youtube.com/watch?v=ITZzrwtCf7M" %}

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your NetSuite account ready, with the Administrator role.

{% hint style="warning" %}
This process involves several steps - please set aside 15-30 minutes to complete it. NetSuite configuration can be complex, so if you have any questions please [contact us](mailto:support@getcensus.com) via support@getcensus.com and we'll help you tailor these instructions to your needs.
{% endhint %}

* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Azure Synapse](../sources/available-sources/azure-synapse.md)
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Elasticsearch](https://docs.getcensus.com/sources/elasticsearch)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [MySQL](https://docs.getcensus.com/sources/mysql)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)
  * [SQL Server](https://docs.getcensus.com/sources/sql-server)

### 1. Create an Integration Record for Census

1. Visit the integrations page or use the global search to look for and navigate to: **page: Manage Integrations**

![](../.gitbook/assets/netsuite_step1.png)

1. Create a new integration with the follow properties:
   * Give it a name that you'll recognize, such as **Census**
   * **Check** TOKEN-BASED AUTHENTICATION
   * Leave OAuth 2.0 AUTHORIZATION CODE GRANT **unchecked**
   * Leave TBA: AUTHORIZATION FLOW **unchecked**
   * Set State to **Enabled**
2. Click Save when finished.
3. Copy and paste the **CONSUMER KEY / CLIENT ID** and **CONSUMER SECRET / CLIENT SECRET** to a password manager. You'll need those later to paste into Census.

![](../.gitbook/assets/netsuite_step2.png)

### 2. Enable Token Based Authentication

1. Global search to **page: Enable Features**
2. Navigate to the tab **SuiteCloud > Manage Authentication**
3. Make sure **Token Based Authentication is checked**
4. Save

![](../.gitbook/assets/netsuite_step3.png)

### 3. Create a Token Role

The Administrator user you're using with NetSuite and Census also needs "Token Role".

1. Global search to **page: New Role**
2. Name the role: **Census**
3. Check **WEB SERVICES ONLY ROLE**
4. Check **DO NOT RESTRICT EMPLOYEE FIELDS**
5. For multi-subsidiary NetSuite users\*\*,\*\* check **ALL** under **ACCESSIBLE SUBSIDIARIES**
6. Under **Permissions > Setup**, add the following permissions:
   * Access Token Management: **Full**
   * Custom Body Fields: **Full**
   * Custom Column Fields: **Full**
   * Custom Entity Fields: **Full**
   * Custom Fields: **Full**
   * Custom Item Fields: **Full**
   * SOAP Web Services: **Full**
   * REST Web Services: **Full**
   * User Access Token: **Full**

![](<../.gitbook/assets/netsuite_step4 (1).png>)

![](<../.gitbook/assets/Image 2021-05-03 at 4.42.55 PM.jpg>)

7\. Under **Permissions > Lists**, Give your Role the appropriate permissions for the NetSuite objects you'll be updating. For example, to update Customers, you'll want to give this role the Lists > Customers (Full) permission.

![](../.gitbook/assets/netsuite_step5.png)

### 4. Add Token Management Permissions

1. Global search to **page: Employees**
2. Edit the employee record of the Admin user you will be using Census with.
3. Navigate to **Access > Roles** and add the Token Role you just created above.

![](../.gitbook/assets/netsuite_step6.png)

### 5. Create Access Tokens

1. Global search to **page: Access Tokens**
2. Click **New Access Token**
3. Select the application and role we created above, then press Save
4. Copy and paste the new Token ID and Token Secret to your password manager or file. We'll use it below.

![](../.gitbook/assets/netsuite_step7.png)

> **Note:** Netsuite permission changes to a role or user **do not occur immediately**. These changes typically take anywhere from a few minutes to a few hours, and they can even take up to 24 hours to go into effect. If you are confident that you have given Census the correct permissions above and experience an error setting up the connection, we recommend waiting for these changes to go into effect before testing the connection again.

### **6. One more thing:** NetSuite **Account ID**

The last bit of information you’ll need is your NetSuite Account ID:

1. Global search to **page: Company Information.**
2. Your **ACCOUNT ID** will be found on that page. Copy and paste it as well.

### 7. Finally, Configure Your Census Connection

1. Now in Census, add a new Destination.

![](../.gitbook/assets/netsuite_step8.png)

1. Paste the Account ID of your NetSuite Account, as well as the Consumer Key, Consumer Secret, Token ID and Token Secret created above.

![](https://paper-attachments.dropbox.com/s_ACE57C63B405EBF6B9657B58E87579C023CBACD5A7F5017A55D85276839F3265_1608658256016_Screen+Shot+2020-12-22+at+11.17.39+AM.png)

1. Click Save Connection, and click Test to double check your connection information.

You're ready to start using Census to load data from your warehouse to NetSuite! If you have any trouble with these steps, please don't hesitate to reach out to: support@getcensus.com and we'll help get this setup.

>

## Sync Speed

NetSuite's API speed and rate limitation are complex and are tied to the plan you are on but you can expect a speed of \~500 records sync / minute on their base plan,

| **Service** | **Records sync / Minute** |
| ----------- | ------------------------- |
| NetSuite    | 500                       |

{% hint style="info" %}
Please note that you can contact your Customer Success Manager at NetSuite to increase your NetSuite[ account API concurrency](https://nlcorp.app.netsuite.com/core/media/media.nl?id=127925362\&c=NLCORP\&h=8742ad8b887aa6881f85&_xt=.pdf) to increase the records sync speed.
{% endhint %}

## ️ Supported Objects

This is is the current list of NetSuite[ objects](https://www.netsuite.com/portal/developers/resources/suitetalk-documentation.shtml) supported by our destination. There are many more and we add them on a case by case basis. If you need a different type of object, please contact us to let us know which object do you need, and we will be happy to support it.

|           **Object Name** | **Supported?** |
| ------------------------: | :------------: |
|                   Account |        ✅       |
|           Billing Account |        ✅       |
|                 Cash Sale |        ✅       |
|                     Class |        ✅       |
|                   Contact |        ✅       |
|               Credit Memo |        ✅       |
|                  Currency |        ✅       |
|                  Customer |        ✅       |
|          Customer Deposit |        ✅       |
|          Customer Payment |        ✅       |
|           Customer Refund |        ✅       |
|           Customer Status |        ✅       |
|             Custom Record |        ✅       |
|                Department |        ✅       |
|                  Employee |        ✅       |
|                   Invoice |        ✅       |
|            Inventory Item |        ✅       |
|      Inventory Adjustment |        ✅       |
|          Item Fulfillment |        ✅       |
|              Item Receipt |        ✅       |
|             Journal Entry |        ✅       |
|                  Location |        ✅       |
|         Other Charge Item |        ✅       |
|                   Partner |        ✅       |
|            Purchase Order |        ✅       |
|               Sales Order |        ✅       |
|              Subscription |        ✅       |
| Subscription Change Order |        ✅       |
|                Subsidiary |        ✅       |
|                    Vendor |        ✅       |
|               Vendor Bill |        ✅       |

{% hint style="info" %}
Please note that NetSuite doesn't support the [creation of fields](../syncs/core-concept/#field-creation) via Census and currently we don't support [add all fields ](../syncs/core-concept/#add-all-fields)feature for NetSuite
{% endhint %}

## Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

|        **Behaviors** | **Supported?** | **Objects** |
| -------------------: | :------------: | :---------: |
| **Update or Create** |        ✅       |     All     |
|      **Update Only** |        ✅       |     All     |
|      **Create Only** |        ✅       |     All     |

:mailbox: [Contact us](mailto:support@getcensus.com) if you want Census to support more Sync Behaviors for this destination

## ❓Netsuite Quirks

Netsuite is one of our most complex destinations, and some objects have behavior that is not explained in the Netsuite docs. Here are some known quirks to be aware of:

#### Customer Payment

* The `Account` field cannot be set on record creation; it can only be set on record update
* In order to change a Customer Payment status to "Deposited", you must send a record update that both sets the `Undep Funds` (short for "undeposted funds") field to `false`, and sets the `Account` field to the bank account into which the funds were deposited.

**Invoice**

* If you're syncing to the Item List on the Invoice object your Item List data will need to be formatted in a JSON array like the following example.`[{"amount": 2.5, "item": {"internalId": "13"}, "quantity": 1}]` .
* For more information on the Invoice schema please visit [Netsuite's Schema Browser](https://www.netsuite.com/help/helpcenter/en_US/srbrowser/Browser2016_1/schema/record/invoice.html)

**Using TranId as a Sync Key**

* In order to sync to the `TranId` field, Allowed Override will need to be checked for the Document Numbers of the object.
* Example: Setup > Company > Auto-Generated Numbers > Document Numbers > Journal
* For more information on Auto Generated Numbers please visit the [Netsuite Help Center](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/bridgehead_4340435273.html)

For more information on all Netsuite Objects and their fields please visit [Netsuite's Schema Browser](https://www.netsuite.com/help/helpcenter/en_US/srbrowser/Browser2016_1/schema/record/account.html)

## Need help connecting to NetSuite?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
