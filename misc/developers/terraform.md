# Terraform Provider

The Census Terraform Provider enables you to manage your Census infrastructure as code. You can programmatically create and configure workspaces, data sources, destinations, datasets, and syncs using Terraform's declarative configuration language.

## Overview

The Terraform Provider allows you to:
- **Manage Workspaces**: Create and configure Census workspaces for different teams or environments
- **Configure Data Sources**: Set up connections to your data warehouses (Snowflake, BigQuery, Postgres, Redshift, etc.)
- **Set Up Destinations**: Connect to business tools (Salesforce, HubSpot, Intercom, etc.)
- **Define Datasets**: Create SQL-based data transformations
- **Orchestrate Syncs**: Configure data flows between sources and destinations with field mappings and schedules

## Getting Started

### Installation

Add the Census provider to your Terraform configuration:

```hcl
terraform {
  required_providers {
    census = {
      source  = "sutrolabs/census"
      version = "~> 0.1.1"
    }
  }
}

provider "census" {
  personal_access_token = var.census_personal_token
  region                = "us"  # or "eu"
}
```

### Authentication

The provider uses **Personal Access Tokens** for authentication:

1. Go to Census Dashboard → Settings → Developer → Personal Access Tokens
2. Create a new token with workspace management permissions
3. Copy the token (starts with `census_pat_...`)
4. Configure the token in your Terraform variables

The provider automatically retrieves workspace-specific API keys when creating workspaces.

## Basic Usage

### Creating a Workspace

```hcl
resource "census_workspace" "data_team" {
  name                     = "Data Team Workspace"
  notification_emails      = ["data-alerts@company.com"]
  return_workspace_api_key = true
}
```

### Connecting a Data Source

```hcl
resource "census_source" "warehouse" {
  workspace_id = census_workspace.data_team.id
  name         = "Production Warehouse"
  type         = "snowflake"

  connection_config = {
    account   = "xy12345.us-east-1"
    database  = "ANALYTICS"
    warehouse = "COMPUTE_WH"
    role      = "CENSUS_ROLE"
    username  = "census_user"
    password  = var.snowflake_password
  }
}
```

### Configuring a Destination

```hcl
resource "census_destination" "crm" {
  workspace_id = census_workspace.data_team.id
  name         = "Production CRM"
  type         = "salesforce"

  connection_config = {
    username       = "census@company.com"
    password       = var.salesforce_password
    security_token = var.salesforce_token
    sandbox        = "false"
  }
}
```

### Creating a Sync

```hcl
resource "census_sync" "users_to_crm" {
  workspace_id = census_workspace.data_team.id
  label        = "Users to CRM"

  source_id      = census_source.warehouse.id
  destination_id = census_destination.crm.id

  source_attributes {
    connection_id = census_source.warehouse.id
    object {
      type         = "table"
      table_name   = "users"
      table_schema = "public"
    }
  }

  destination_attributes = {
    connection_id = census_destination.crm.id
    object        = "Contact"
  }

  operation = "upsert"
  sync_key  = ["email"]

  field_mappings {
    from      = "email"
    to        = "Email"
    operation = "direct"
  }

  field_mappings {
    from      = "first_name"
    to        = "FirstName"
    operation = "direct"
  }

  schedule {
    frequency = "daily"
    hour      = 8
    timezone  = "UTC"
  }
}
```

## Available Resources

- **census_workspace** - Manage Census workspaces
- **census_source** - Data warehouse connections (Snowflake, BigQuery, Postgres, Redshift, Databricks, etc.)
- **census_destination** - Business tool integrations (Salesforce, HubSpot, Intercom, Zendesk, etc.)
- **census_dataset** - SQL datasets for data transformation
- **census_sync** - Data syncs between sources and destinations

All resources have corresponding data sources for read-only operations.

## Features

### Multi-Region Support

The provider supports both US and EU Census instances:

```hcl
provider "census" {
  personal_access_token = var.census_personal_token
  region                = "eu"  # Use EU region
}
```

### Import Existing Resources

Import existing Census resources into Terraform state:

```bash
terraform import census_workspace.existing 12345
terraform import census_source.existing 67890
terraform import census_sync.existing 11111
```

### Staging Environment Support

Configure custom base URLs for testing against staging environments:

```hcl
provider "census" {
  personal_access_token = var.census_personal_token
  base_url              = "https://app.staging.getcensus.com/api/v1"
}
```

## Documentation & Examples

For detailed documentation and complete examples:

- **Provider Documentation**: [Terraform Registry](https://registry.terraform.io/providers/sutrolabs/census/latest/docs)
- **GitHub Repository**: [terraform-provider-census](https://github.com/sutrolabs/terraform-provider-census)
- **Complete Examples**: See the [examples directory](https://github.com/sutrolabs/terraform-provider-census/tree/main/examples) for working configurations

## Support

For questions or issues with the Terraform Provider:

- **GitHub Issues**: [Report issues](https://github.com/sutrolabs/terraform-provider-census/issues)
- **Census Support**: [support@getcensus.com](mailto:support@getcensus.com)
- **Census Documentation**: [docs.getcensus.com](https://docs.getcensus.com)

---

**Note**: The Census Terraform Provider is a community project designed to provide infrastructure-as-code integration with Census services.
