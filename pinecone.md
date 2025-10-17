# pinecone

### Getting Started

In this guide, we will show you how to connect to Census and create your first sync.

{% stepper %}
{% step %}
### Collect your Pinecone Credentials

Census needs the following information to create a Pinecone connection:

* API Key - instructions to create one can be found [here](https://docs.pinecone.io/guides/projects/manage-api-keys)
{% endstep %}

{% step %}
### Connect Pinecone in Census

* In Census, navigate to [Destinations](https://app.getcensus.com/destinations)
* Click the **New Destination** button
* Select **Pinecone** in the dropdown list
* Enter your credentials and click **Connect**

You're all set!
{% endstep %}
{% endstepper %}

{% hint style="info" %}
If you have any questions during setup, or have a use case that is not covered, please write us in-app or [send us an email](mailto:support@getcensus.com) via support@getcensus.com
{% endhint %}

## Supported Objects and Behaviors

Pinecone stores data within Indexes. Your Indexes in Pinecone can be used as objects to sync to from Census.

| **Object Name** | **Supported?** | **Sync Keys** | **Behaviors**                     |
| --------------- | -------------- | ------------- | --------------------------------- |
| Index           | ✅              | ID            | <p>Update or Create<br>Mirror</p> |

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Pinecone.

## Need help connecting to Pinecone?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com/) chat.
