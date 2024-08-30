# Sync Tracking

Sync Tracking provides row-level observability into every sync run, along with the ability to&#x20;

* **Filter** to view invalid or rejected records
* **Search** for a particular record by its by primary identifier
* **Download** samples of the records

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

For each record, Census will display

* The primary identifier
* Its status (Invalid, Rejected, or Success)
* The error reason, if applicable
* The source record payload that was processed

This feature is available **live** while a sync is in progress and will continually update as each batch completes its processing.

{% hint style="info" %}
By default, Census will retain row-level logs and make them available to you for 14 days. To use your own bucket for storage and customize retention, see the [Observability Lake](observability-lake.md).
{% endhint %}



To use Sync Tracking, navigate to the [sync-history.md](sync-history.md "mention") page on the relevant sync. If a sync run falls within the 14-day retention period, a "View Records" button will be available. Click this button to open up the Sync Tracking modal and access detailed record information.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
