# External Dataset Repositories

Census seamlessly integrates with popular data transformation tools, allowing you to leverage your existing data modeling investments.

### dbt Integration

Census's [native dbt integration](dbt-integration.md) allows you to directly access your dbt models without having to redefine them in Census. This ensures consistency between your analytics models and operational data, creating a single source of truth.

Benefits of the dbt integration:

* Automatically discover and use dbt models
* Maintain consistent business logic across analytics and operations
* Leverage dbt's testing and documentation capabilities
* Sync data as soon as dbt models are refreshed

### Looker Integration

The [Looker integration](looker-integration.md) allows you to use your Looker Explores and Looks as datasets in Census. This is particularly valuable for organizations that have invested heavily in Looker as their business intelligence platform.

Benefits of the Looker integration:

* Reuse existing business logic defined in LookML
* Maintain consistent definitions between reporting and operational systems
* Leverage Looker's governance and access controls

### Sigma Integration

For teams using Sigma as their analytics platform, Census's [Sigma integration](sigma-integration.md) allows you to use Sigma workbooks as datasets. This enables business users who are building in Sigma to directly activate their insights without requiring data team intervention.

Benefits of the Sigma integration:

* Empower business users to create operational datasets
* Maintain consistency between analytics and operations
* Leverage Sigma's visual modeling capabilities
