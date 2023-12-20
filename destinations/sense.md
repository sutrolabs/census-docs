---
description: This page describes how to use Census with Sense.
---

# Sense

Sense is smart talent engagement and communication platform that helps companies find and recruit. Census can send data to Sense to help you build better relationships with your candidates.

{% hint style="warning" %}
Sense's API is currently write only on a per record basis. This means that sending data to Sense will overwrite any existing data in Sense. As a result, Sense connector should only be used for initial data loading. For questions about this limitation, please reach out to you Sense Account Manager.
{% endhint %}

### 🏃‍♀️ Getting Started

To connect your Sense account to Census, you'll need a Client ID and Secret Key. Contact your Sense Account Manager to get access to these credentials.

* Navigate to the **Destinations** page in Census and click **New Destination**.
* Select **Sense** from the menu.
* Provide the Client ID and Secret, and click **Save**.
* You'll see your new Sense connection listed on the Destinations page.

### 🔀 Supported Objects, Keys and Behaviors

| **Object Name** | **Supported?** | **Sync Keys** | **Behaviors**    |
| --------------: | :------------: | ------------- | ---------------- |
|       Candidate |        ✅       | id            | Update or Create |
|         Company |        ✅       | id            | Update or Create |

Again, though the sync behavior is **Update or Create**, the functional result is that Census will **overwrite** any existing data associated with a given id currently in Sense with the data you send from Census. This is a limitation of Sense's API.

### 🚑 Need help connecting to Sense?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
