# Google Pub/Sub

Pub/Sub is Google's scalable messaging service that allows applications to send and receive messages between independent components. Census can act as a subscriber to a Pub/Sub topic, allowing you to sync messages from Pub/Sub to your destinations.

### Permissions

To read data from your Pub/Sub, Census will automatically generate a new service account. You'll need to grant the **roles/pubsub.editor** role to this service account on the GCP project ID where your Pub/Sub topic is located.

Census uses this role for the following actions:

* Create a subscription to selected topic(s)
* Consume messages from selected topic(s)
* Create an error topic ([Dead Letter Queue](https://aws.amazon.com/what-is/dead-letter-queue/)) and publish errors to the topic

## Create a Pub/Sub Connection

1. In Census, navigate to **Sources**.
2. Click **New Source** and select **Google Pub/Sub**.
3. Enter the GCP project ID where your Pub/Sub topic is located.
4. By default, Census will create a new service account to access your Pub/Sub. If you want to use an existing service account, you can provide the service account key JSON.
5. Click **Connect**.
6. If you did not provide an existing service account, Census will create a new service account and provide you with the service account email address. You will need to grant the **roles/pubsub.editor** role to this service account on the GCP project ID where your Pub/Sub topic is located.
7. Once you've granted the necessary permissions, click \*_Save_ to ensure Census can access your Pub/Sub.

You're now ready to define message schemas for your Pub/Sub topics.

## Define message schemas

Before you can use a Pub/Sub topic as the source for a sync, you must define the schema of the messages on the topic.

1. In Census, navigate to **Datasets**.
2. From the **Source** dropdown, select your Pub/Sub connection.
3. Census automatically pulls the list of topics from your project. You can also click **Refresh topics** to manually refresh the list.
4. Click on the name of the topic you want to define a schema for.
5. Select the format of the messages on your topic from the **Format** drop down. The only supported format is JSON.
6. Click **Import sample message** and enter a sample message. Your sample message should be a JSON object containing any top-level fields you want to use in your pipelines. Make sure the values of the fields in your sample message match the data type of the values in your actual messages.

{% hint style="warning" %}
Census stores message samples as part of the Dataset definition. Do not include customer PII or otherwise sensitive data in a sample message.
{% endhint %}

Click **Save Dataset**. Review the listed properties and types to ensure the sample message you provided was interpreted as intended.

## Need help connecting to Google Pub/Sub?

Contact the support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
