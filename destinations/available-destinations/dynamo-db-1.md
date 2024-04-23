---
description: Use Census to sync data to a MongoDB table from any source we support.
---

# Mongo DB

## 🏃‍♀️ Getting Started

MongoDB is a popular NoSQL database known for its flexibility and scalability, using a document-oriented data model that stores data in JSON-like structures called BSON. With Census, you can sync data into MongoDB from any source we support.

To connect to MongoDB, Census needs to know the **Connection String** for your instance and the database you want to connect to.

#### For a Local MongoDB Installation

1. **Identify Your MongoDB Host and Port**: By default, MongoDB runs on port `27017`.&#x20;
2.  **Construct the Connection String**: The basic format of the connection string for a MongoDB server is:

    ```
    mongodb://user:pass@hostname:port/?retryWrites=true&w=majority
    ```

#### For MongoDB Atlas (Cloud Hosted)

1. **Log In to Your MongoDB Atlas Dashboard**: Access your cluster in the MongoDB Atlas dashboard.
2. **Navigate to the Connect Section**: Click on the "Connect" button associated with the cluster from which you want to retrieve the connection string.
3. **Choose Your Connection Method**: Select "Connect your application". This option provides you with the connection string.
4. **Copy the Connection String**: You will see a connection string provided by Atlas. Replace `<password>` with your database user's password, and adjust other parameters as necessary.

Now you're ready to set up your first sync to MongoDB!

### Table schemas

Because MongoDB tables have flexible schemas, Census treats every field you map from your source as a "custom field". Other than the key fields discussed above, Census won't know about your table's schema. Instead, you'll use Census's [Field Mapping](../../syncing-data/field-mapping/) feature to map fields from your source to your MongoDB table by explicitly specifying the destination table field name.

## 🚑 Need help connecting to MongoDB?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.
