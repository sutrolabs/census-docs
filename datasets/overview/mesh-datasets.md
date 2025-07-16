---
description: >-
  Learn how Mesh Datasets enable you to join, query, and activate data across
  multiple sources in Census Workbench — all within a single dataset.
---

# 🆕 Mesh Datasets

Census makes it it easy to connect or create Datasets from many different sources. Any SQL source can easily join data _within_ that source. But what about joining across sources? Now you can use Mesh Datasets to write SQL that spans datasets built on any SQL source together.

### Writing Mesh SQL&#x20;

To support querying across SQL sources, Census provides a virtual query engine that has access to a magic `datasets.*` schema. Every SQL dataset you've created in Census Workbench is automatically available as a virtual table in the schema. For example, if you have a dataset called VIP Users, you'll find that `datasets.vip_users` is now queryable when writing the SQL for your Mesh Dataset.

Mesh SQL is regular Postgres-compatible SQL syntax so any standard Postgres functions should work as expected. This is true even if your SQL sources are Snowflake, BigQuery, or some other service. Querying a Mesh Dataset primarily runs in Census's virtual query environment. The query engine automatically determines when a source-specific dataset needs to be executed and automatically pushed down to the appropriate source using the SQL defined in that referenced dataset.&#x20;

### Using Mesh SQL AI Assistant

Mesh Datasets also support using AI to generate SQL. Give your Mesh Dataset a description and then press the **Generate SQL** button. The LLM will use the metadata about all of your datasets to generate what it thinks is the most appropriate SQL.&#x20;

{% hint style="info" %}
LLMs are magic but they're not perfect! Census recommends using the generated SQL as a starting point for your Mesh Dataset rather than a perfect query every time. Make sure to review the logic and the results before you sync it to any destinations.
{% endhint %}

For more information on how we work with LLM providers, see our privacy docs on AI Integration & Data Privacy.

### Supported Sources

All SQL Sources including Snowflake, BigQuery, Databricks, Redshift, as well as [Census Store](../../misc/data-storage/census-store/) are supported and can be joined in Mesh Datasets.&#x20;

Streaming Sources such as Kafka and HTTP are not supported. Google Sheets, S3, and file Sources are also not supported. &#x20;
