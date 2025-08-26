---
description: This page describes how to use Census with Google Datastore.
---

# Google Datastore

## Getting Started

1. Click **New Destination**.
2. Select **Google Datastore** from the menu.
3. When prompted, enter the following credentials:

* **Project ID** Can be found in the Google Cloud Console by clicking the project drop down next to the search bar.

<figure><img src="../.gitbook/assets/image (1) (3).png" alt=""><figcaption><p>Get your Project ID from the Google Cloud Console</p></figcaption></figure>

4. Click `Connect`, a Google service account ID will be displayed. Copy this value.
5. Navigate to the [Google Cloud IAM Console](https://console.cloud.google.com/iam-admin/iam). Click the `+ GRANT ACCESS` button. When prompted enter the following information

* **New principals** Paste the Google service account ID copied in the previous step.
* **Select a role** Choose the `Cloud Datastore User` role

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption><p>New principals will be the value copied in step 4.</p></figcaption></figure>

###

### Supported Sync Behaviors

|    **Behaviors** | **Supported?** |
| ---------------: | :------------: |
| Update or Create |        ✅       |

### Need help connecting to Google Datastore?

Contact the support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
