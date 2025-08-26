---
description: Monitor and optimize match rates across all your ad platforms in Audience Hub
---

# Audience Match Rates

<figure><img src="../../.gitbook/assets/match rates 2.png" alt=""><figcaption><p>Matched audience size and match rate for an audience in Google Ads.</p></figcaption></figure>

When you send audiences to ad platforms like Facebook and Google Ads, the platforms attempt to match as many of your audience members as possible to their own users. The more users they're able to match, the greater your reach when running campaigns against those audiences.

The success of this process is often represented via two numbers: **matched audience size** and **match rate**_._ When using our [one-click experience](../syncing-segments.md#one-click-experience-for-a-d-platforms) to send audiences to ad platforms, Census reports both.

{% hint style="info" %}
Some ad platforms take 24-48 hours to process audience uploads, so these numbers may lag slightly.
{% endhint %}

## Matched Audience Size

This is the total size of an audience in the ad platform after accounting for invalid and unmatched records:

<figure><img src="https://lh7-us.googleusercontent.com/ILe8lQzEbZjDbgDTxdEiKt1Qx26jsU_ar1A3X4HYK2GUS7yytasg8F3RQ_hrOQqtiAnc-yOOaCzlge1LaiFlvWb9wtd-uzcNIpLfIf6nlpgZNC9yPWrf4NuLY_hABPyrdGYn_qK-Np4JGrn6VC5AarY" alt=""><figcaption><p>Matched audience size = original segment size - invalid records - unmatched records</p></figcaption></figure>

The original segment size is the total number of members in an audience as reported in Audience Hub:

<figure><img src="https://lh7-us.googleusercontent.com/Z_b6wlipQZl0BZhpyw61haGdghxW9JHXNZLiOaucYZ8gWC51oeTM6NdV6SmetL_Upz03gbKi_kcKiL7BVRwSn4t4qCC2DfRJOG9dBM3ZmhUfrsJ-8Bm_xhgBOct_kWofzjy68U3ntcUMFLFcIqzFTWE" alt="" width="375"><figcaption><p>Original audience size reported in Census.</p></figcaption></figure>

Obviously, this number has a big impact on the final matched audience size, but volume isn’t everything—data quality matters too.

Records can be invalid in different ways. One of the most common is that data isn’t normalized and/or hashed properly. Each ad platform has different requirements for how data should be formatted before being sent. For example, TikTok requires you to remove all periods before the @ in an email address, whereas Facebook doesn’t.

Fortunately, Census handles this normalization automatically if you provide us with unhashed identifiers. (If you give us hashed data, we can’t tell whether it was normalized correctly prior to being hashed.)

Once the data is normalized, it’s often required to be hashed as well. If you haven’t given us hashed data for a field that requires hashing, we’ll do it automatically behind the scenes so you don’t have to worry about it.

If the ad platform still can’t match a properly normalized and hashed record to one of their users (using their black box methods) then that person will be omitted from the final audience, thus reducing the matched audience size. This might happen because the identifiers provided were either wrong or insufficient to uniquely identify someone, or because that person is actually not a user of that platform.

Subtracting both the invalid and unmatched records from the original segment size yields the matched audience size reported in Census. We get this number directly from the ad platforms.

## Match Rate

Once we’ve got the matched audience size, computing the match rate is straightforward—it’s simply the matched audience size divided by the total number of audience members uploaded to the platform (i.e. the original segment size in Census):

<figure><img src="https://lh7-us.googleusercontent.com/tTu838F4wozoVuLVHO4QLIaR2Ya2KOHmgN_k3PH3CH-6Je_jWWEvCq9YUVvKra7XmLqUXo93RYKDXI-Hoev5wmQnIh9S0FoxHXepP4uOApb0GhC_blRkMq1blqNW_ndoTNoj2lspkuLxIOuDTms-Udc" alt=""><figcaption><p>Match rate = matched audience size / original segment size</p></figcaption></figure>

Some ad platforms report their own match rate and it may differ from what you see in Census. If that’s the case, it’s probably because they’re computing it based on the number of records that were successfully uploaded to their platform, whereas Census counts all records in your original audience.

In this case, ignoring invalid records decreases the size of the denominator (i.e. original segment size) in the formula above, thus increasing the match rate. We think it’s better to include those invalid records in the calculation, because otherwise you may not know there’s a problem that’s directly impacting the size of your matched audience!

## Need Help?

If you have questions or feedback on how we can improve this feature, please contact our support team via our in-app chat.
