# Bring your own GCS Bucket

{% hint style="info" %}
This feature is available to Census Paid Plans. Please contact your Census account representative for details before proceeding with these steps.
{% endhint %}

Buckets are used for 2 purposes

1. Temporary storage for warehouse unloads during sync runs
2. Record-level sync tracking for observability



If you bring your own GCS bucket:

1. It will only be used for warehouse unloads from BigQuery and select other warehouses. Please contact support for the full list, or if you'd like to use your GCS bucket for _every_ warehouse unload temporary storage.
2. It will be used as the record-level sync tracking storage for every sync run, regardless of source or destination.

{% hint style="info" %}
After following the steps below, you must provide your Census support representative with details. Please contact support via your established channels, or support@getcensus.com.\
\
Your Census rep will require

1. **GCP Project ID**
2. **GCS Bucket Name**
3. **GCP Service Account Email**
{% endhint %}



## Configuring a bucket for Sync Tracking

### 1. Create a GCS Service Account

Log into Google Cloud Console and navigate to IAM & Admin -> Service Accounts

<figure><img src="../../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

1. Click _Create Service Account_
2. Enter a Service Account Name
3. Keep the generated Service Account ID, generate a new one, or enter your own
4. **Copy the Service Account ID**
5. Configure the project permissions for the Service Account

<figure><img src="../../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>



### 2. Generate a Service Account Key

1. Log into Google Cloud Console and navigate to IAM & Admin -> Service Accounts
2. Click the name of your Service Account

<figure><img src="../../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

3. Open the Keys tab and click Add Key -> Create New Key

<figure><img src="../../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

4. Choose the key type "JSON" and click Create

<figure><img src="../../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

5. Save the generated `.json` file in a secure location.

<figure><img src="../../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

### 3. Create a GCS Bucket

1. Log into Google Cloud Console and navigate to your Project
2. Go to Cloud Storage -> Buckets and click Create

<figure><img src="../../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

3. Give your bucket a name
4. Configure the bucket settings
   1. Location: choose the same location setting as your BigQuery project
   2. Storage Class: Standard
   3. Check _Enforce Public Access Prevention_
   4. Access Control: Uniform
   5. Leave versioning, and encryption on defaults.
   6. Lifecycle Policy: Lifecycle rules should be enabled to:
      1. **Action**: Delete object
      2. **Object condition**: 14+ days since object was created `Name matches prefix 'sync-unloads/'`.
5. Once the bucket has been created, navigate to _Permissions_
6. Grant your Service Account the permissions
   1. Storage Object User
   2. Storage Object Creator

<figure><img src="../../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

## Configuring a bucket for temporary warehouse unloads from BigQuery

When creating your BigQuery connection

1. In Census, create a connection to BigQuery using the appropriate Project ID and Location.
2. Paste the contents of the Service Account Key JSON file (from above) into the _Service Account Key JSON (Optional)_ box.
3. Click _Connect_ and _Confirm_
   1.  Note: There is no need to copy and run the GCP Console commands

       provided in-app when following this setup guide. Please ignore them.

<figure><img src="../../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>
