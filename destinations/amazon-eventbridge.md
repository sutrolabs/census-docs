# Amazon EventBridge

## 🏃‍♀️ Getting Started

This guide will walk through connecting Census to an Amazon EventBridge instance as a data destination.

EventBridge is an Event Stream style destination. Census will send changes in the source data as a series of events that can then be consumed by a number of destinations, typically other applications or microservices in your infrastructure.

### Connecting and Authentication

To connect to EventBridge, Census needs to know the **AWS Region** your instance is hosted in and the role to use to connect to it. Census uses AWS's recommended [Cross-account Role-based Access](https://aws.amazon.com/blogs/apn/securely-accessing-customer-aws-accounts-with-cross-account-iam-roles/) for authentication.

Creating an IAM Role with the necessary permissions requires a few steps in the AWS Console.

* Open your AWS Console in a separate tab and browse to the **IAM** service. Click **Roles** and **Create role**.
* When creating the role choose **AWS Account** for **Trusted Entity Type** and the **Another AWS Account** radio button.
* Provide Census's AWS Account ID: `341876425553`.
* Select the policy
  * For services that write to EventBridge, [AWS recommends](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-use-identity-based.html#eb-events-iam-roles) the `AmazonEventBridgeFullAccess` and this is the only pre-made policy offering the necessary permissions.
  * You can also use any custom policy that includes the `events:PutEvents` and `events:ListEventBuses` actions.
* Save your new role.

When done, click on your role and copy its ARN. Go back to the tab where you're editing the Census EventBridge destination and enter the **Role ARN**. Click **Connect**. Confirm the connection test is successful and you're ready to go.

### (Optional) Configure Global Endpoint

You can provide an optional Endpoint ID if you are using [EventBridge's Global Endpoint](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-global-endpoints.html) mechanism in order to make your EventBridge instance region-fault tolerant.

The [Endpoint ID](https://docs.aws.amazon.com/eventbridge/latest/APIReference/API\_Endpoint.html#eventbridge-Type-Endpoint-EndpointId) is the URL subdomain of your global endpoint. For example, if the URL for your Endpoint is `https://abcde.veo.endpoints.event.amazonaws.com`, then the EndpointId is `abcde.veo`.

## 🔀 Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

| **Object Name** | **Supported?** | **Sync Keys** | **Behaviors**                  |
| --------------: | :------------: | ------------- | ------------------------------ |
|           Event |        ✅       | Event ID      | Send, Update or Create, Mirror |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](broken-reference) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Amazon Eventbridge objects and/or behaviors.

### Event Properties and Formatting

Events in EventBridge are JSON object with a default set of properties, as well as a `details` sub object. You can use Census to set the values of of the default properties, and then add any additional properties you like.

* **Sync Key / Event ID** - This field is used to identify unique records but is not by default sent to EventBridge. If you'd like to send it, explicitly include it as an additional custom mapping.
* **Detail Type** - This is functionally the event name, and Detail Types of the same type should have the same **Detail** structure.
* **Source** - Identifies the source that generated the event
* **Event Bus Name** - The target event bus name. If you're using a global endpoint with a custom bus, you must enter the name, not the ARN, of the event bus.

**Optional System Fields**

* **Resources** (Array) - Amazon Web Services resources, identified by Amazon Resource Name (ARN), which the event primarily concerns or is targeted at.
* **Time** - The timestamp of the event. If no time stamp is # provided, the time stamp of the PutEvents call is used.
* **Trace Header** (Object) - An X-Ray trace header, which is an http header (X-Amzn-Trace-Id) that contains the trace-id associated with the event

**Custom Properties**

Any other property mappings you include will be included in the **Detail** nested object. Census will also automatically include an **Operation** property indicating whether the record change was **added**, **updated**, or **removed**. You may modify the names of the operations Census uses in the advanced configuration.

You can also override the shape of the **Detail** object by providing an override Census by providing a JSON template using [mustache syntax](https://mustache.github.io/mustache.5.html).

## 🚑 Need Help Connecting to EventBridge?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.
