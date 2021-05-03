---
description: This page describes how to use Census with Netsuite.
---

# Netsuite

## 🏃‍♀️ Getting Started

{% embed url="https://www.youtube.com/watch?v=ITZzrwtCf7M" %}

In addition to may other destinations, Census can sync your data warehouse data into Netsuite objects such as Customer, Invoice, and more. In this article, we'll walk you through the process of setting up a new Netsuite connection in Census.

### 0. Prerequisites

You'll need a Census account as well as a NetSuite account with the Administrator role. This process involves several steps - please set aside 15-30 minutes to complete it. Netsuite configuration can be complex, so if you have any questions please reach out to support@getcensus.com and we'll help you tailor these instructions to your needs.

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
2. Navigate to the tab **SuiteCloud &gt; Manage Authentication**
3. Make sure **Token Based Authentication is checked**
4. Save

![](../.gitbook/assets/netsuite_step3.png)

### 3. Create a Token Role

The Administrator user you're using with Netsuite and Census also needs "Token Role".

1. Global search to **page: New Role**
2. Name the role: **Census**
3. Check **WEB SERVICES ONLY ROLE**
4. Check **DO NOT RESTRICT EMPLOYEE FIELDS**
5. For multi-subsidiary Netsuite users**,** check **ALL** under **ACCESSIBLE SUBSIDIARIES**
6. Under **Permissions &gt; Setup**, add the following permissions:
   * User Access Token: **Full**
   * Access Token Management: **Full**
   * SOAP Web Services: **Full**

![](../.gitbook/assets/netsuite_step4.png)

7. Under  **Permissions &gt; Lists**, Give your Role the appropriate permissions for the Netsuite objects you'll be updating. For example, to update Customers, you'll want to give this role the Lists &gt; Customers \(Full\) permission. \(See screenshot below\)

![](../.gitbook/assets/netsuite_step5.png)

8. Under  **Permissions &gt; Setup**, Give your Role the appropriate permissions for the Netsuite Custom Fields you'll need access to. For example, to if you're syncing Customers \(an Entity\), you'll want to give this role the Custom Entity Fields \(Full\) permission. If your syncing a Transaction \(i.e. Cash Sales\), give this role access to Custom Body Fields and Custom Column Fields \(Full\) permissions. \(See screenshot below\)

![](../.gitbook/assets/image-2021-05-03-at-4.42.55-pm.jpg)



### 4. Add Token Management Permissions

1. Global search to **page: Employees**
2. Edit the employee record of the Admin user you will be using Census with.
3. Navigate to **Access &gt; Roles** and add the Token Role you just created above.

![](../.gitbook/assets/netsuite_step6.png)

### 5. Create Access Tokens

1. Global search to **page: Access Tokens**
2. Click **New Access Token**
3. Select the application and role we created above, then press Save
4. Copy and paste the new Token ID and Token Secret to your password manager or file. We'll use it below.

![](../.gitbook/assets/netsuite_step7.png)

### **6. One more thing: Netsuite Account ID**

The last bit of information you’ll need is your Netsuite Account ID:

1. Global search to **page: Company Information.** 
2. Your **ACCOUNT ID** will be found on that page. Copy and paste it as well.

### 7. Finally, Configure Your Census Connection

1. Now in Census, add a new Service Connection.

![](../.gitbook/assets/netsuite_step8.png)

1. Paste the Account ID of your Netsuite Account, as well as the Consumer Key, Consumer Secret, Token ID and Token Secret created above.

![](https://paper-attachments.dropbox.com/s_ACE57C63B405EBF6B9657B58E87579C023CBACD5A7F5017A55D85276839F3265_1608658256016_Screen+Shot+2020-12-22+at+11.17.39+AM.png)

1. Click Save Connection, and click Test to double check your connection information.

You're ready to start using Census to load data from your warehouse to Netsuite! If you have any trouble with these steps, please don't hesitate to reach out to: support@getcensus.com and we'll help get this setup.

## 🏎 Sync Speed

Netsuite's API speed and rate limitation are complex and are tied to the plan you are on but you can expect a speed of ~500 records sync / minute on their base plan,

| **Service** | **Records sync / Minute** |
| :--- | :--- |
| Netsuite | 500 |

{% hint style="info" %}
Please note that you can contact your Customer Success Manager at Netsuite to increase your [Netsuite account API concurrency](https://nlcorp.app.netsuite.com/core/media/media.nl?id=127925362&c=NLCORP&h=8742ad8b887aa6881f85&_xt=.pdf) to increase the records sync speed.
{% endhint %}

## 🗄️ Supported Objects

This is is the current list of [Netsuite objects](https://www.netsuite.com/portal/developers/resources/suitetalk-documentation.shtml) supported by our connector. There are many more and we add them on a case by case basis. If you need a different type of object, please contact us to let us know which object do you need, and we will be happy to support it.

| **Object Name** | **Supported?** |
| ---: | :---: |
| Account | ✅ |
| Contact | ✅ |
| Currency | ✅ |
| Customer | ✅ |
| Customer Status | ✅ |
| Employee | ✅ |
| Invoice | ✅ |
| Subsidiary | ✅ |

{% hint style="info" %}
Please note that Netsuite doesn't support the [creation of fields](../basics/core-concept.md#field-creation) via Census and currently we don't support [add all fields ](../basics/core-concept.md#add-all-fields)feature for Netsuite
{% endhint %}

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concept page](../basics/core-concept.md#the-different-sync-behaviors).
{% endhint %}

| **Behaviors** | **Supported?** | **Objects?** |
| ---: | :---: | :---: |
| **Update or Create** | ✅ | All |
| **Update Only** | ✅ | All |

🔋[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync Behaviors for this destination

## 🚑 Need help connecting to Netsuite?

Contact us via support@getcensus.com or start a conversion via the [in-app](https://app.getcensus.com) chat.



