---
description: This page describes how to configure Google BigQuery as a Census destination.
---

# Google BigQuery

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Census to Google BigQuery as a destination.

{% hint style="info" %}
If you are configuring Google BigQuery as a source (to query data from BigQuery to sync elsewhere), that process is documented separately here: [Google BigQuery as a Source](../sources/google-bigquery.md)
{% endhint %}

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Google Cloud account and project ready.
* Have access within the Google Cloud project to configure IAM role grants.

### Step 1: Add Destination

* Click _+ New Destination_ and enter your Google Cloud Project ID.
* Optionally, name the connection.

<figure><img src="../.gitbook/assets/Screenshot 2023-07-21 at 8.50.07 AM (1).png" alt=""><figcaption></figcaption></figure>

### Step 2: Grant Permissions to the Census Service Account

Census creates a dedicated Google Cloud Service Account for each BigQuery destination. After the previous step, this account was created. To load data into BigQuery, the account needs the appropriate permissions.

<figure><img src="../.gitbook/assets/Screenshot 2023-07-21 at 8.55.40 AM.png" alt=""><figcaption></figcaption></figure>

Click the _Activate Cloud Shell_ (near top right) icon in Google Cloud and execute the following commands.

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

* Replace `cs-sandbox-12345` with your Project ID.
* Replace `census-12345abcd1234512345abcdabcd@sutrolabs-giza-production.iam.gserviceaccount.com` with the service account provided in the Census UI.

```
gcloud projects add-iam-policy-binding cs-sandbox-123456 \
  --member serviceAccount:census-12345abcd1234512345abcdabcd@sutrolabs-giza-production.iam.gserviceaccount.com \
  --role roles/bigquery.dataOwner

  gcloud projects add-iam-policy-binding cs-sandbox-123456 \
  --member serviceAccount:census-12345abcd1234512345abcdabcd@sutrolabs-giza-production.iam.gserviceaccount.com \
  --role roles/bigquery.jobUser
```

### Step 3: Test and Finish

With permissions configured, return to Census and proceed. Census will test the connection.

**🎉 Congratulations! You've configured a connection to BigQuery!**

<figure><img src="../.gitbook/assets/Screenshot 2023-07-21 at 9.10.06 AM.png" alt=""><figcaption></figcaption></figure>

## 🚑 Need help connecting to Google BigQuery?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.
