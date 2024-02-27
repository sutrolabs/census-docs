---
description: This page describes how to use Census with Gainsight.
---

# Gainsight

Gainsight is a customer success platform that helps businesses grow faster by reducing churn, increasing upsell, and driving customer advocacy. Census can sync your customer data to Gainsight provide the full context of your customer data to your customer success team.

## 🏃‍♀️ Getting started

This guide shows you how to use Census to connect your Gainsight account to your data warehouse and create your first sync.

1. Within Gainsight, open the **Sidebar** and click on **Administration** > **Integrations** > **Connectors 2.0**
2. Click on the **Create Connection** button in the top right, then select the Gainsight API.
   - Do not select the GS Bulk API, select the Gainsight API
   - Gainsight only allows a single API key to be created per organization. You can reuse this key if you've already created one.

![](<../.gitbook/assets/Screen Shot 2021-11-19 at 8.28.18 PM.png>)

3. The Access Key is initially empty. Dismiss the dialog and then select **Edit Connection** from the three-dot menu on the new Gainsight API card.
4. Copy the Access Key.

![](<../.gitbook/assets/Gainsight Credentials.png>)

5. Back within Census, go to the [Destinations](https://app.getcensus.com/destinations) page in Census and click **New Destination**.
6. Select **Gainsight** from the menu.

7. Paste the Access Key into the **Access Key** field and the domain for your Gainsight account into the **Domain** field (exclude the `https://` and any path after the domain). Hit save and you're done!

You should now be ready to sync your data to Gainsight.

## 🗄 Supported Objects and Behaviors

|     **Object Name** | **Supported?** | **Sync Keys**                                                                       | **Behaviors** |
| ------------------: | :------------: | ----------------------------------------------------------------------------------- | :------------: |
|              Person |        ✅       | Email                                                                               | Update or Create |
|             Company |        ✅       | Name                                                                                | Update or Create, Update Only |
|      Company Person |        ✅       | UniqueId for Census. Company Name and Person Email are required                     | Update or Create |
| Relationship Person |        ✅       | UniqueId for Census. Company Name, Person Email, and Relationship Name are required | Update or Create |
|       Custom Object |        ✅       | Available Update Keys that are not a lookup                                         | Update or Create, Update Only |

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Gainsight.

#### Custom Objects Quirks

The Custom Object must be configured like below for Census to be able to edit it. You can access this on your Administration > Customer Data > Data Management path on the lefthand sidebar.

![](<../.gitbook/assets/Screen Shot 2022-02-01 at 6.47.18 PM.png>)

## 🚑 Need help connecting to Gainsight?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
