# Observability Lake

Observability Lake allows you to store a comprehensive history of your sync data in your own cloud storage environment, providing extended retention and flexibility beyond the default 14-day period.

You receive:

* **Customizable Retention**: Extend your data retention beyond the default 14 days to meet your business needs.
* **Bring Your Own Bucket (BYOB)**: Use your own Amazon S3, Google Cloud Storage, or Azure Blob Storage to store sync data, giving you full control over your storage environment.
* **Full Historical Access**: Keep a complete record of all sync activities for auditing, compliance, and long-term analysis.

## How to Set Up Observability Lake

To set up Observability Lake, follow the steps in our [Bring Your Own Bucket documentation](https://docs.getcensus.com/misc/security-and-privacy/bring-your-own-blob-storage).

Once you configure your own bucket, **Census will automatically use it as storage for all sync run logging going forward.**

By using Observability Lake, you gain the flexibility to manage your sync data retention according to your specific requirements, ensuring you have the historical data needed for comprehensive analysis and compliance.

## Sync Tracking in Observability Lake

Sync Tracking takes advantage of Observability Lake to store sync your data for a customized retention period. It also allows access query logs directly enabling more complex analysis and monitoring of Census syncs. See the [Sync Tracking documentation](sync-tracking.md) for details on the Sync Tracking data schema.
