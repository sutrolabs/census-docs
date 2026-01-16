---
description: This page describes how to use Census with Google Sheets.
---

# Google Sheets

Google Sheets is a Google's cloud-based spreadsheet that allows you to create, edit, and collaborate with others in real-time. It's a great tool for storing and sharing data, and with Census, you can sync data from your data warehouse directly into Google Sheets.

## Getting Started

In this guide, we will show you how to connect Google Sheets to Census.

### 1. Create a Google Sheets connection

Our Google Sheets destination behaves a little differently than other Census destinations. Instead of going through an OAuth connection flow, we provide you a Google Identity address you use to share the correct Google Sheets docs. This lets you be very specific about which Google Sheets you give Census access to.

* In Census, navigate to [Destinations](https://app.getcensus.com/destinations)
* Click the New Destination button
* Select **Google Sheets** in the menu

Your new Google Sheets connection will include a Google Identity email. This is the email address you'll use to grant Census access to your target Google Sheet. Click the copy button (<img src="../.gitbook/assets/copy-solid.svg" alt="" data-size="line">) to save it to your clipboard, will use it in a minute.

### 2. Share your target Google Sheet

Now head to the Google Sheet you'd like to sync to. If you don't have one in mind, you can [create a new one](https://sheets.new). Either way, make sure your target Google Sheet has an empty tab inside it that Census can sync to, as the contents of which ever tab you select will be replaced by Census.

To give Census access to your Google Sheet, press the Share button and then add paste the Google Identity email from Census into the share dialog and confirm.

![](../.gitbook/assets/screely-1622879521880.png)

## :question:Is It Possible to Enforce A Sort Order?

Unfortunately, no. Census can not guarantee a preserved order from your model, even if your model has an `ORDER BY` statement. When we unload the records, we just use a normal SELECT, so the records can come back in any order.\
\
We recommend treating the Google Sheet that is receiving data as the "raw data" and doing any necessary transformations, like ordering, in a separate sheet within the file.\
\
The `IMPORTRANGE` function in Google Sheets can be a great solution for this use case - you can find the documentation and best practices [here](https://support.google.com/docs/answer/3093340).

## :question:My sync failed because it was too big?

Syncs to Google Sheets as a destination are limited to 5M updated _cells_ to ensure the reliability of the syncs\_.\_ A cell corresponds to a column-to-field mapping so if your source data for the sync has 100 rows and the sync uses 4 columns, that will end up being 400 cells that are updated.

If Census determines a sync will update over 5M cells the sync will fail with the following error: `Sheets prohibits updates of over 5M cells. Please try modifying your source data to limit the total cell count.`

This is a runtime error and will not be caught at the time of Sync creation.

## Supported Sync Behaviors

| **Object Name** | **Supported?** | **Behaviors** |
| :-------------: | :------------: | ------------- |
|    Sheet Tabs   |        ✅       | Replace       |

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](/broken/pages/-MV8ovxVCiy1fEjc0SO-#the-different-sync-behaviors).
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Google Sheets.

## Need help connecting to Google Sheets?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
