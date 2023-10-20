---
description: This page describes how to use Census with Google Ads.
---

# Google Ads

## 🏃‍♀️ Getting Started

Connecting to your Google Ads account is straightforward.

1. From the [Destinations](https://app.getcensus.com/destinations) page, click **New Destination** and select Google Ads from the menu.
2. Complete the OAuth flow. Make sure your are signed into a user account that has permissions to both view all of your accounts, as well as submit data to them (readonly accounts will not work).
3.  Select the Ads account you wish to use with Census. If you'd like to sync to multiple accounts, you will need to add each as its own destination.\


    <figure><img src="../../.gitbook/assets/Google Ads.png" alt=""><figcaption></figcaption></figure>

## 🗄 Supported Objects

<table data-header-hidden><thead><tr><th width="206"></th><th width="216" align="right"></th><th></th></tr></thead><tbody><tr><td><strong>Service</strong></td><td align="right"><strong>Object Name</strong></td><td></td></tr><tr><td><a href="https://docs.getcensus.com/destinations/google-ads/customer-match-audiences">Customer Match Lists (Audiences)</a></td><td align="right">Customer</td><td><a data-mention href="customer-match-audiences.md">customer-match-audiences.md</a></td></tr><tr><td><a href="https://docs.getcensus.com/destinations/google-ads/offline-conversions">Offline Conversions</a></td><td align="right">Click Conversion, <br>Call Conversion, <br>Conversion Adjustment, <br>Enhanced Conversion</td><td><a data-mention href="offline-conversions.md">offline-conversions.md</a></td></tr></tbody></table>

[Contact us](mailto:support@getcensus.com) if you're looking for additional Google Ads objects.

{% hint style="success" %}
Just a heads up: We use the new [Google Ads API](https://developers.google.com/google-ads/api/docs/start) as opposed to the older AdWords API.
{% endhint %}

## :warning:Common Issues

### Did my sync work? It says completed but it isn't showing the updated timestamp I expect.

The standard place where bulk files uploading update status doesn't actually update when using Census. Instead, you've gotta hover on a specific card.

Steps to get there:

1. Open your google ads account
2. Navigate to Tools & Settings > Audience Manager
3. Hover over the name of your desired audience in the list.
4. Expand the section labeled `Customers based on email, phone, and/or mailing address uploads`
5. Within that, you'll see a `Last upload` label.

![](<../../.gitbook/assets/Screen Shot 2021-11-16 at 10.34.57 AM.png>)

If that date isn't the same time as the most recent sync completed, please reach out via our in-app chat and we will investigate it with you.

## 🚑 Need help connecting to Google Ads?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
