---
description: Use Census to sync data to a DynamoDB table from any source we support.
---

# Amazon DynamoDB

## Getting Started

[Amazon DynamoDB](https://docs.aws.amazon.com/dynamodb/) is a fully managed NoSQL database service known for its performance and scalability. With Census, you can sync data into DynamoDB tables from any source we support.

To connect to DynamoDB, Census needs to know the **AWS Region** your instance is hosted in and the role to use to connect to it. Census uses AWS's recommended [Cross-account Role-based Access](https://aws.amazon.com/blogs/apn/securely-accessing-customer-aws-accounts-with-cross-account-iam-roles/) for authentication.

Creating an IAM Role with the necessary permissions requires a few steps in the AWS Console.

* Open your AWS Console in a separate tab and browse to the **IAM** service. Click **Roles** and **Create role**.
* When creating the role choose **AWS Account** for **Trusted Entity Type** and the **Another AWS Account** radio button. Use Census's Account ID `341876425553` as the **Account ID**.
* On a separate tab, create a custom policy
  * The policy should have the `dynamodb:ListTables` action.
  * The policy should include the following actions on the tables you want to give Census access to:

```
  "dynamodb:BatchGetItem",
  "dynamodb:BatchWriteItem",
  "dynamodb:PutItem",
  "dynamodb:DescribeTable",
  "dynamodb:DeleteItem",
  "dynamodb:UpdateItem"
```

* Save your new role.

When done, click on your role and copy its ARN. Now you can head back to Census to finish connecting to DynamoDB.

* Go to the [Destinations page](https://app.getcensus.com/destinations) in Census
* Select **New Destination** and choose **Amazon DynamoDB** from the menu
* Optionally, give your DynamoDB connection a unique name
* Paste in your **ARN** for the role you've created.
* Enter the **Region** where your DynamoDB instance is hosted (this can be found in the URL when you're signed into the AWS Management Console)
* Click **Connect** to finish connecting Census to DynamoDB

Now you're ready to set up your first sync to DynamoDB!

## Supported Objects and Behaviors <a href="#supported-objects-and-behaviors" id="supported-objects-and-behaviors"></a>

<table data-header-hidden><thead><tr><th width="168.6600566572238"></th><th width="137"></th><th width="154"></th><th></th></tr></thead><tbody><tr><td><strong>Object Name</strong></td><td><strong>Supported?</strong></td><td><strong>Sync Keys</strong></td><td><strong>Behaviors</strong></td></tr><tr><td>Table</td><td>✅</td><td>Partition Key</td><td>Update or Create, Mirror</td></tr></tbody></table>

DynamoDB is a NoSQL database and tables have flexible schemas and identifier approaches. That makes them a little quirky in Census. Here's a couple of things to keep in mind:

### Unique identifiers

DynamoDB tables can be configured to use either a single primary key or a composite key made up of two parts. Census supports both approaches, however requires a some data modeling first.

In your source data model, you'll need to provide two or three columns depending on the mode you're using.

If your table uses a single primary key, your source data will need to provide:

* The **Partition Key** - This is the unique identifier for each record in your table
* A **Composite Key** - This can be a duplicate of the **Partition Key** but does need to be a duplicate

If your table uses a composite key, your source data will need to provide:

* The **Partition Key** - This is the first part of the composite key
* The **Sort Key** - This is the second part of the composite key
* A **Composite Key** - A concatination of the **Partition Key** and **Sort Key**.

When you set up your sync, you'll select your **Composite Key** in your source data for the **Sync Key**. Then you'll need to map the **Partition Key** (and optionally **Sort Key**) to the appropriate keys in your DynamoDB table.

### Table schemas

Because DynamoDB tables have flexible schemas, Census treats every field you map from your source as a "custom field". Other than the key fields discussed above, Census won't know about your table's schema. Instead, you'll use Census's [Field Mapping](/broken/pages/-MV8ovxVCiy1fEjc0SO-#field-mappings) feature to map fields from your source to your DynamoDB table by explicitly specifying the destination table field name.

## Need help connecting to DynamoDB?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.
