---
description: This page describes how to provide DMA consent to ad platforms via Census.
---

# Digital Markets Act (DMA) Consent for Ad Platforms

{% hint style="warning" %}
**If you are using Census to send audiences or conversion events to Google Ads, Google DV360, or Amazon Ads DSP, you’ll need to take the actions described on this page before March 2024 to avoid audience targeting from being affected.**
{% endhint %}

As you may be aware, many of the large advertising services are in the process of supporting the EU’s [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA). Census now supports syncing DMA-related properties to the following destinations:

* [Google Ads](dma-consent-for-ad-platforms.md#google-a-ds) (Audiences, Conversions)
* [Google Campaign Manager 360](dma-consent-for-ad-platforms.md#google-display-and-video-360) (Conversion Events)
* [Google Display & Video 360](dma-consent-for-ad-platforms.md#google-display-and-video-360) (Customer Match Audiences)
* [Amazon Ads DSP](dma-consent-for-ad-platforms.md#amazon-a-ds-dsp) (Audiences)

Google and Amazon have taken different approaches to supporting DMA metadata for their networks. Google asks you to provide consent information on a per-user basis, whereas Amazon requires you to indicate which region a particular audience’s data has been collected in to determine if the DMA applies. Below, we describe how to provide this information via Census.

## Google Ads

{% hint style="info" %}
If you’re using our one-click sync experience to send audiences to Google Ads, jump ahead to the [One-Click Audience Syncs](dma-consent-for-ad-platforms.md#one-click-audience-syncs-google-a-ds-only) section below.
{% endhint %}

When sending Audiences or Conversions to [Google Ads](../../destinations/google-ads/) (using our traditional sync experience) you will now see two optional fields: **Consent for ad personalization** and **Consent for ad user data**. You must provide both of these to assert the user data you are sending was collected in accordance with [Google’s EU User Consent Policy](https://www.google.com/about/company/user-consent-policy/).

<figure><img src="../../.gitbook/assets/CleanShot 2024-02-15 at 17.04.01@2x (1).png" alt=""><figcaption><p>Optional fields for providing consent to Google Ads.</p></figcaption></figure>

Google accepts the following values for both fields: `UNKNOWN`, `UNSPECIFIED`, `GRANTED`, `DENIED`. For more info, see [Google’s documentation](https://support.google.com/google-ads/answer/14310715).

There are two ways to populate these fields in Census:

1. Create two columns in your underlying data model to specify the appropriate values on a per-record basis

<figure><img src="../../.gitbook/assets/CleanShot 2024-02-26 at 12.09.00@2x (1).png" alt=""><figcaption><p>Specify consent via a column in your source data.</p></figcaption></figure>

2. Use the “Constant Value” feature in Census’s field mapper to provide the same value for all records in the audience (warning: only do this if you’re confident the same value will always apply to all members of your audience)

<figure><img src="../../.gitbook/assets/CleanShot 2024-02-26 at 12.07.26@2x.png" alt=""><figcaption><p>Provide a constant value in the field mapper.</p></figcaption></figure>

### One-Click Audience Syncs (Google Ads Only)

If you’re sending audiences to Google Ads using our [one-click audience sync](https://docs.getcensus.com/basics/audience-hub/syncing-segments#one-click-experience-for-a-d-platforms) experience, you’ll only need to provide consent status once for each underlying “person” dataset.

1. Go to the “Datasets” tab in Census.
2. Click on the “Person” dataset powering your one-click syncs. Look for the “Type” properties in the “Overview” tab and click “Edit”

<figure><img src="../../.gitbook/assets/image (80).png" alt=""><figcaption><p>Look for the "Type" properties in the "Overview" tab</p></figcaption></figure>

3. Add two additional mappings—1) **Google Ads Consent for Ad Personalization** and 2) **Google Ads Consent for Ad User Data**—and select the relevant fields in your source data. Acceptable values for these fields are: `UNKNOWN`, `UNSPECIFIED`, `GRANTED`, or `DENIED` (see [Google’s documentation](https://support.google.com/google-ads/answer/14310715) for more context).

<figure><img src="../../.gitbook/assets/image (82).png" alt=""><figcaption><p>Add additional mappings to your "Person" dataset</p></figcaption></figure>

4. Click “Save” in the bottom right to save your changes.
5. Repeat this process for any additional “Person” datasets powering one-click syncs.
6. That’s it! We’ll automatically ensure these fields get passed along to Google Ads.

## Google Campaign Manager 360

The process for providing DMA metadata to [Google CM360](../../destinations/google-campaign-manager-360.md) is nearly identical to Google Ads ([see above](dma-consent-for-ad-platforms.md#google-a-ds)). The only difference is that CM360 requires different values for consent status: `GRANTED` and `DENIED`. For more info, see [Google’s documentation](https://developers.google.com/doubleclick-advertisers/rest/v4/Conversion#FIELDS.ad_user_data_consent).

## Google Display & Video 360

Similarlly, the process for providing DMA metadata to [Google DV360](../../destinations/google-dv360.md) is also nearly identical. DV360's consent status values are `CONSENT_STATUS_UNSPECIFIED`, `CONSENT_STATUS_GRANTED`, `CONSENT_STATUS_DENIED`. For more info, see [Google’s documentation](https://developers.google.com/display-video/api/reference/rest/v3/firstAndThirdPartyAudiences#ContactInfoList.FIELDS.consent).

## Amazon Ads DSP

[Amazon Ads](../../destinations/amazon-ads-dsp-amc.md) has approached their DMA compliance by requiring a list of one or more country codes to be set on audiences defined in Amazon Ads DSP. These country codes indicate which countries the audience data was collected in. If the list includes any in-scope EU country, it will be subject to the regulation and potential restrictions will be applied (Amazon has not yet clarified what those are). Note that any audiences without **Data Source Country** information provided will be assumed to be in scope for DMA by default.

When syncing to Amazon Ads DSP Audiences with Census, you can now provide the list of countries where the included users’ data was collected. This list will be used whenever Census creates a new audience (it will not modify existing audiences).

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-25 at 9.05.36 PM.png" alt=""><figcaption><p>Provide a list of country codes to Amazon.</p></figcaption></figure>

## Have Questions?

If you have any questions or need assistance, contact our support team.
