---
description: Use Census to sync data to a DynamoDB table from any source we support.
---

# Amazon DynamoDB

## 🏃‍♀️ Getting Started

[Amazon DynamoDB](https://docs.aws.amazon.com/dynamodb/) is a fully managed NoSQL database service known for its performance and scalability. With Census, you can sync data into DynamoDB tables from any source we support.

In order to connect Census to your DynamoDB instance, you'll need to generate an access key for a user that has permission to write to your database:

* Open the [AWS Management Console](https://console.aws.amazon.com/)
* Navigate to the **IAM Dashboard**
* Go to the **Users** page
* Either create a new user or select an existing user with write access to your database
* Go to the **Security credentials** tab for that user
* Select **Create access key** and choose **Application running outside AWS** on the next screen
* Continue through the prompts to finish creating the key
* Copy your **Access Key** and **Secret Access Key** when prompted to do so (note these won't be shown to you again)

Once you've saved your access key credentials:

* Go to the [Destinations page](https://app.getcensus.com/destinations) in Census
* Select **New Destination** and choose **Amazon DynamoDB** from the menu
* Optionally, give your DynamoDB connection a unique name
* Paste in your **Access Key** and **Secret Key**
* Enter the **Region** where your DynamoDB instance is hosted (this can be found in the URL when you're signed into the AWS Management Console)
* Click **Connect** to finish connecting Census to DynamoDB

Now, head over to the Syncs page in Census to set up your first sync to DynamoDB!

## 🔀 Supported Objects and Behaviors <a href="#supported-objects-and-behaviors" id="supported-objects-and-behaviors"></a>

<table data-header-hidden><thead><tr><th width="168.6600566572238"></th><th width="137"></th><th width="154"></th><th></th></tr></thead><tbody><tr><td><strong>Object Name</strong></td><td><strong>Supported?</strong></td><td><strong>Sync Keys</strong></td><td><strong>Behaviors</strong></td></tr><tr><td>Table</td><td>✅</td><td>Partition Key</td><td>Update or Create, Mirror</td></tr></tbody></table>

{% hint style="info" %}
Because DynamoDB is a NoSQL database and tables have flexible schemas, Census treats every field you map from your source as a "custom field". In other words, we won't give you a fixed menu of destination field options to choose from when setting up your syncs—you'll need to tell Census the names of the fields you want to map to.
{% endhint %}

## 🚑 Need help connecting to DynamoDB?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.
