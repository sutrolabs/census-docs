# SaaS Datasets

Census allows you to create datasets directly from your CRM systems like HubSpot and Salesforce, making it easy to work with your business data alongside your warehouse data. This guide explains how SaaS Datasets work and how to get started.

## Overview

SaaS Datasets allow you to:
- Import any object from supported CRMs (including custom objects)
- Control which fields are imported for each object
- Automatically refresh data on your schedule (hourly, daily, or never)
- Use all Census features with your CRM data (AI columns, enrichments, deduplication)
- Create segments and syncs using your CRM data
- Query the data from your existing data warehouse using Census's Iceberg catalog

## How It Works

### Data Storage and Access

When you create a SaaS Dataset, Census imports your selected CRM objects into [Census Store](../../misc/data-storage/census-store/README.md), our managed storage solution. Here's what happens:

1. Your data is imported using your CRM's API credentials
2. The data is stored in Apache Iceberg format in Census Store
3. Census provides an Iceberg catalog that makes this data queryable from your data warehouse
4. Data is automatically refreshed based on your specified schedule

By default, data is stored in Census's secure infrastructure, but you can also [use your own storage infrastructure](../../misc/data-storage/census-store/README.md#using-an-alternative-object-storage-provider) for additional control.

### Querying Your Data

Because SaaS Datasets are stored in Apache Iceberg format, you can query them directly from your data warehouse using federated queries - meaning you don't need to copy the data into your warehouse first. This is sometimes called "Zero-Copy" or "Zero-ETL" access.

For example, if you're using Snowflake, you can query your SaaS Dataset tables just like any other table:
```sql
SELECT * FROM CENSUS_CATALOG.YOUR_WORKSPACE.HUBSPOT_CONTACTS;
```

See the [Census Store documentation](../../misc/data-storage/census-store/README.md#iceberg-catalog) for detailed instructions on setting up and using federated queries for your specific warehouse.

### Data Lifecycle

- Data is automatically refreshed based on your configured schedule
- When you delete a dataset, all associated data is permanently removed from storage
- You maintain full control over which objects and fields are imported

## Getting Started

To create your first SaaS Dataset:

1. Navigate to the `Datasets` tab in Census
2. Click `+ New Dataset` in the top-right corner
3. Select `Import Dataset from App`
4. Choose your CRM system (HubSpot or Salesforce)
5. Select the objects and fields you want to import
6. Configure your refresh schedule
7. Save your dataset

## Features and Capabilities

SaaS Datasets can be used with all Census features:

- Add [AI Columns](../ai-columns/README.md) for AI-powered data enrichment
- Apply [third-party enrichments](../enrichment/README.md)
- Perform [deduplication](../entity-resolution/README.md)
- Create [segments](../../audience-hub/README.md) for targeted marketing
- Build [syncs](../../syncs/core-concept/README.md) to other destinations

## Data Access Methods

Your SaaS Dataset data is accessible through:

1. Census UI - Browse and manage your datasets directly
2. Your Data Warehouse - Query the data using federated queries via the Census Iceberg catalog

## Best Practices

- Start with a subset of fields to optimize initial load times
- Set refresh schedules based on your data update frequency
- Monitor your API usage to stay within CRM limits
- Regularly review and clean up unused datasets

## Security and Compliance

- All data is encrypted at rest and in transit
- Access controls are managed through Census permissions
- Data storage follows Census's security and compliance standards
- Option to use your own storage infrastructure for additional control

For more details about data storage, security, and querying options, see our [Census Store documentation](../Census Store.md). 