---
description: >-
  In this guide, you’ll learn the necessary steps to complete sync-a-swag. Each
  step has a companion video to assist you.
---

# Sync-a-swag

Census sends custom fields (contact info, swag preferences) from a data warehouse to a marketing automation platform to automatically send swag to your doorstep. This is a hands-on, simple way to understand the functionality and benefits of Census.

{% embed url="https://youtu.be/S_J6ExHAA5Y" %}

## 🏃‍♀️ Getting Started

### Prerequisites

Have your Census account ready. If you need one, [**create a Free Trial Census account**](https://app.getcensus.com) now.

{% embed url="https://youtu.be/dbUQ3sG_-Ao" %}

## Open the sync-a-swag feature

Navigate to the [**Census quickstart page**](https://app.getcensus.com/quickstart) and click **enter info** under the **sync some sweet Census swag to yourself** option. This will automatically create a source and destination for your sync.

{% embed url="https://youtu.be/YbpxSVZ4O9c" %}

Next, you’ll see Census’s modeling feature where you can write SQL to create a model (see below) from the source we set up for you.

## Create a model

Follow these steps to **create a model** called Sync-a-Swag Entry Form:

1. Update the **string property values** with your **contact info** and **swag preferences**.
   * _Example: Change Email to your desired email address:_ [_peterpan@neverland.com_](mailto:peterpan@neverland.com)_._
   * Tip: Each **property** is a **string** **value**. Don’t forget to include the **apostrophes** **(' ')** **for** **each**                **value**.

![](<../.gitbook/assets/sync-a-swag step 2.gif>)

2\. Click **preview** to verify that your SQL query works properly and includes the correct information.

3\. Click **save model**.

{% embed url="https://youtu.be/lNh-CfjxIJQ" %}

## Create a sync

Next, **create a sync** to send the Sync-a-Swag Entry Form model from the Redshift data warehouse to the marketing automation platform.

Update the following sections on the **sync page**:

1. Click **syncs** on the navigation menu on the left hand side of your screen. Next, click **add** **sync** on the top right of your screen. These steps allow you to start a new sync.
2. Choose the data that you want to sync.
   * **Select the warehouse and modeled data you want to sync:**
     * **Connection:** Redshift - tf-redshift-demo-cluster
     * **Source:** Sync-a-Swag Entry Form.

![](<../.gitbook/assets/sync-a-swag step 3.gif>)

3\. Choose where you want to sync data to.

* **Select the warehouse and modeled data you want to sync:**
  * **Connection:** Sync-a-Swag
  * **Object:** Sync Your Address Here (US only)

4\. Indicate how sources and destination records are matched.

* Syncs require you to **match the source and destination with a unique identifier.**
  * On the left-hand side, **select ‘email’ as the identifier** for the “Sync-a-Swag Entry Form”.

![](<../.gitbook/assets/sync-a-swag step 3.1.gif>)

5: (No action needed, just FYI) Select which properties should be updated.

6\. Scroll to the bottom of the page and click **next**.

7\. On the confirm details page click **run** **sync now?** and then click **create**  **sync**.

8\. You’ll see a quick confirmation that your sync was successful. 🎉

{% embed url="https://youtu.be/KJqE5d1IRak" %}

## **🚑** Need help with Sync-a-Swag?

[Contact us](https://mail.google.com/mail/u/0/?fs=1\&tf=cm\&source=mailto\&to=support@getcensus.com) via support@getcensus.com or start a conversation with us via the[ in-app](https://app.getcensus.com) chat.
