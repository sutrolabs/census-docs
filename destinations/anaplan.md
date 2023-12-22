---
description: >-
  This page describes how to use Census to sync data from your warehouse to
  Anaplan.
---

# Anaplan

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Anaplan to Census and create your first sync.

### 1. Navigate to your Anaplan Model

From the URL, you will find the WorkspaceId and the ModelId. These will be needed to configure the connection from Census.

![Copy the WorkspaceId and the ModelId](<../.gitbook/assets/Anaplan URL.png>)

{% hint style="warning" %}
The Model Id needs to be the model to which you want to sync, both the Workspace ID and the Model ID should be 32 characters long
{% endhint %}

### 2. Configure the Anaplan Connection

Navigate to the connections tab in Census. Select Anaplan

You'll need to provide your username and password. After adding your credentials, paste your Anaplan Workspace and Model ID into Census. Finally, select which region your Anaplan instance is hosted in.

![Add a descriptive label and copy your credentials](<../.gitbook/assets/anaplan.png>)





### 3. Test the Connection

You have successfully configured and tested the connection, so you can now sync data into your financial models from your data source! :tada:

## 🗄️ Supported Objects and Behaviors

|        **Object** | **Supported?** | **Behaviors** |
| ----------------: | :------------: | :-----------: |
| **Import Action** |        ✅       | **Mirror**    |

{% hint style="info" %}
Import Actions must have the Source Type of File in order for Census to be able to sync to it. Look [here](https://help.anaplan.com/f19cdb3d-385a-4a27-aaa8-7422b240e8bc-Get-started-with-imports) for more details on how to configure this on the Anaplan side
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Anaplan.

## 🚑 Need help connecting to Anaplan?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
