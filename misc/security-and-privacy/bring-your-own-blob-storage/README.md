# Blob Storage

## 💽 How Census uses Blob Storage

All sources configured using the [Advanced Sync Engine](../../../sources/overview/#sync-engines) use Amazon S3 as temporary storage for the data that is unloaded from your warehouse before it is sent to the destination service or application. Additionally, we will use this storage to write files containing information about record-level sync tracking, enabling detailed tracking and debugging of syncs. &#x20;

By default, Census manages this storage on your behalf. This includes managing credentials with narrow permissions and short lifetimes, encrypting data in the bucket at rest and in transit, and automatically removing old data from the bucket once it is no longer in use. This approach is secure and is used by the vast majority of Census customers.

## Using your own Blob Storage

{% hint style="info" %}
This feature is available to Census Paid Plans. Please contact your Census account representative for details before proceeding with these steps.
{% endhint %}

If you prefer to manage your own bucket for legal or regulatory reasons, see the articles below

[bring-your-own-s3-bucket.md](bring-your-own-s3-bucket.md "mention")

[bring-your-own-gcs-bucket.md](bring-your-own-gcs-bucket.md "mention")

[bring-your-own-azure-bucket.md](bring-your-own-azure-bucket.md "mention")
