---
description: This page describes how to add Google Sheets as a source to Census.
---

# Google Sheets

Census lets you select a Google Sheet to treat as a source for your syncs.

In order to sync data from a Google Sheet, Census creates a special service account email address for each Google Sheets connection. You can then "share" your Google sheet with that unique Census email, just like you'd share your sheet with anyone.

This will walk you through creating a new Google Sheets source.

### Create a Google Sheets connection

First, you'll need to create a connection to your Google Sheets account.

1. In Census, go to **Sources** or click [here to go to the app](https://app.getcensus.com/sources).
2. Click **New Source** and select **Google Sheets**.

![](<../.gitbook/assets/image (18).png>)

3\. **If you're already signed in with Google single sign-on** - A new service account email will automatically be created for Google Sheets. Scroll down to the bottom of your list of data sources if you can't see it.

4\. **If you're not already signed in with Google**, you will need to authorize your Google account. Once you've done that, a new service account email will automatically be created for Google Sheets. Scroll down to the bottom of your list of data sources if you can't see it.

5\. Give your Google sheets connection a unique name by clicking **Edit** and adding a label

![Name your Google Sheets source by clicking Edit](../.gitbook/assets/name\_google\_sheets\_source.png)

### Connect a Google Sheet

We will now use this service account email to "share" the Google sheet you want to connect to Census.

1. Go over to your Google Sheets account
2. Select the sheet you wish to connect to Census
3. In Census, copy the service account email generated for Google Sheets

![](<../.gitbook/assets/image (12).png>)

4\. Back in your Google Sheet, click **Share** in the top right corner

5\. Paste the Census service account email to share that google sheet with Census

![](<../.gitbook/assets/image (14).png>)

6\. Confirm you do want to share and you're done! You can now use that sheet create a sync using that connection.

### Create a sync

You can now go on to create a sync from your Google Sheet to a destination app.

1. In Census, click on **Syncs** in the left menu
2. Click on **Add Sync**
3. Under connection select the name of your Google Sheets connection
4. **Important:** If this is your first time connecting a Google Sheet, it won't show up under the 'Spreadsheets' dropdown. You will need to click **Refresh** in order to load the Google Sheets that you shared with this connection (from the previous section).
5. Once you've refreshed and loaded the Spreadsheets, you can select the Spreadsheet and Sheet tab you wish to sync from.

![You have to click Refresh to load a newly shared Spreadsheet](../.gitbook/assets/refresh\_google\_sheets.png)

For more detailed instructions on how to configure your sync, please read the docs page for the destination app you want to sync data to.

## Notes

* You cannot create SQL Models on Google Sheets data
* Be sure that all line breaks are removed from the header row

## Need help connecting to Google Sheets?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
