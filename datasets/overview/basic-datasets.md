# Basic Datasets

Basic datasets are the foundation of Census's data activation capabilities. They allow you to leverage your existing data warehouse infrastructure to power your business operations by connecting your warehouse data directly to your business applications.

{% hint style="info" %}
Need a hand getting a handle on your data warehouse? Contact our support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat to let us know what questions we can help with!
{% endhint %}

## Getting Started

To create a new basic dataset:

1. Navigate to the Datasets section in Census
2. Click "New Dataset" and select "Basic Dataset"
3. Choose your connection
4. Select one of the following options:
   * **Select a table** - Choose a specific table or view directly from your data warehouse
   * **SQL** - Write a custom SQL query to define your dataset with more flexibility
5. Test your dataset to ensure it returns the expected data
6. Save and use your dataset in syncs

## Connecting to Your Data Warehouse

Census provides multiple ways to define and access data in your warehouse:

### Direct Table and View Access

The simplest way to get started with Census is to use the "Select a table" option to access existing tables and views in your data warehouse. Census can directly access these objects, making it easy to sync data that's already well-structured and ready for use.

### Custom SQL Queries

When you need more flexibility, Census allows you to use the "SQL" option to define custom SQL queries directly in the platform. This approach is ideal when you need to:

* Join multiple tables together
* Apply complex transformations
* Filter data to include only what's relevant for a specific destination
* Create aggregations or calculations

```sql
-- Example: Creating a customer 360 view with SQL
SELECT 
  c.customer_id,
  c.email,
  c.name,
  c.created_at,
  SUM(o.amount) as lifetime_value,
  COUNT(o.order_id) as order_count,
  MAX(o.created_at) as last_order_date
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id
GROUP BY 1, 2, 3, 4
```

### Python Transformations

For even more advanced use cases, Census supports Python transformations that let you apply complex business logic, machine learning models, or data processing that goes beyond what SQL can easily accomplish.

```python
# Example: Python transformation for customer segmentation
def transform(df):
    # Calculate recency, frequency, monetary value
    df['recency'] = (datetime.now() - df['last_order_date']).dt.days
    
    # Apply segmentation logic
    conditions = [
        (df['lifetime_value'] > 1000) & (df['recency'] < 30),
        (df['lifetime_value'] > 500) & (df['recency'] < 60),
        (df['lifetime_value'] > 0)
    ]
    choices = ['VIP', 'Regular', 'Occasional']
    df['segment'] = np.select(conditions, choices, default='Inactive')
    
    return df
```

## Integration with Data Transformation Tools

Census seamlessly integrates with popular data transformation tools, allowing you to leverage your existing data modeling investments.

### dbt Integration

Census's [native dbt integration](external-dataset-repositories/dbt-integration.md) allows you to directly access your dbt models without having to redefine them in Census. This ensures consistency between your analytics models and operational data, creating a single source of truth.

Benefits of the dbt integration:

* Automatically discover and use dbt models
* Maintain consistent business logic across analytics and operations
* Leverage dbt's testing and documentation capabilities
* Sync data as soon as dbt models are refreshed

### Looker Integration

The [Looker integration](external-dataset-repositories/looker-integration.md) allows you to use your Looker Explores and Looks as datasets in Census. This is particularly valuable for organizations that have invested heavily in Looker as their business intelligence platform.

Benefits of the Looker integration:

* Reuse existing business logic defined in LookML
* Maintain consistent definitions between reporting and operational systems
* Leverage Looker's governance and access controls

### Sigma Integration

For teams using Sigma as their analytics platform, Census's [Sigma integration](external-dataset-repositories/sigma-integration.md) allows you to use Sigma workbooks as datasets. This enables business users who are building in Sigma to directly activate their insights without requiring data team intervention.

Benefits of the Sigma integration:

* Empower business users to create operational datasets
* Maintain consistency between analytics and operations
* Leverage Sigma's visual modeling capabilities

## Best Practices for Basic Datasets

Getting the most out of your basic datasets requires some thoughtful planning. Here are some tips we've gathered from working with hundreds of data teams:

* **Use incremental syncs** whenever possible to reduce load on your warehouse and speed up sync times
* **Add appropriate filters** to your queries to limit the data being processed to just what you need
* **Create indexes** on frequently queried columns in your warehouse to improve query performance
* **Consider materialized views** for complex queries that are used frequently to reduce computation time
* **Add clear descriptions** to your datasets to help business users understand what data is available
* **Set up appropriate access controls** in your warehouse to maintain data security
* **Use version control** to track changes to your dataset definitions and make it easy to roll back if needed
* **Validate data types** and formats before syncing to avoid errors in destination systems
* **Create test syncs** to validate new datasets before using them in production workflows
