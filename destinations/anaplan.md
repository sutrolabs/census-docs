---
description: >-
  This page describes how to use Census to sync data from your warehouse to
  Anaplan.
---

# Anaplan

## Getting Started

In this guide, we will show you how to connect Anaplan to Census and create your first sync.

### 1. Locate your workspace and model ID

The Workspace ID can be found under `Administration` -> `Workspaces` within the Anaplan dashboard.

![Locate the workspace ID](<../.gitbook/assets/AnaplanWorkspaceID.png>)

Select the `Models` tab under the selected workspace and click on the desired model. This action will open the model details page.

![Select the model](<../.gitbook/assets/AnaplanModels.png>)

The model ID can be found on the model details page.

![Locate the model ID](<../.gitbook/assets/AnaplanModelID.png>)

{% hint style="warning" %}
The Model Id needs to be the model to which you want to sync, both the Workspace ID and the Model ID should be 32 characters long
{% endhint %}

### 2. Configure the Anaplan Connection

Navigate to the connections tab in Census. Select Anaplan

#### Authentication options

1. **User credentials**

   - You'll need to provide your
     - Username
     - Password
     - Anaplan Workspace ID
     - Model ID
     - Which region your Anaplan instance is hosted in.

The username and password will be the username and password used to authenticate to Anaplan

![Add a descriptive label and copy your credentials](<../.gitbook/assets/AnaplanUserCreds.png>)

2. **Self service OAuth**
  - You'll need to provide your
    - Client ID
    - Client secret
    - Anaplan Workspace ID
    - Model ID
    - Which region your Anaplan instance is hosted in

  ![Add a descriptive label and copy your credentials](<../.gitbook/assets/AnaplanSelfServiceOauth.png>)

  **Creating your client ID and secret**

  Navigate to `Administration` -> `Security` -> `OAuth Clients` and click the `New` button in the upper right.

  ![Create an oauth client](<../.gitbook/assets/AnaplanOauthClient.png>)

  Name the client, choose `Authorization code grant` as the type, and set the allowed callback URLs to include `https://app.getcensus.com/anaplan_callback`. Then, click `Create`.

  Clicking on the created OAuth client will provide access to the client ID and secret.

  ![Creates oauth client](<../.gitbook/assets/AnaplanOauthClientIDandSecret.png>)


### 3. Test the Connection

You have successfully configured and tested the connection, so you can now sync data into your financial models from your data source! :tada:

## ️ Supported Objects and Behaviors

|        **Object** | **Supported?** | **Behaviors** |
| ----------------: | :------------: |:-------------:|
| **Import Action** |        ✅       |  **Replace**  |

{% hint style="info" %}
Import Actions must have the Source Type of File in order for Census to be able to sync to it. Look [here](https://help.anaplan.com/import-basics-b9d40f84-d2c0-4003-84e3-47a8068da977) for more details on how to configure this on the Anaplan side
{% endhint %}

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Anaplan objects and/or behaviors.

## Need help connecting to Anaplan?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
