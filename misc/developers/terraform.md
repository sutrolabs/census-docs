---
description: Use Terraform to manage Census resources as infrastructure as code
---

# Terraform Provider

The Census Terraform Provider allows you to manage Census resources programmatically using infrastructure as code (IaC). This enables you to version control, automate, and reproducibly deploy your Census configurations across different environments.

## Why use Terraform with Census?

* **Version Control** - Track changes to your Census configuration in Git alongside your other infrastructure code
* **Reproducibility** - Replicate configurations across development, staging, and production environments
* **Automation** - Integrate Census configuration into your CI/CD pipelines
* **Collaboration** - Review and approve infrastructure changes through standard pull request workflows
* **Multi-region Support** - Manage Census resources across US, EU, and AU regions

## Getting Started

### Installation

The Census Terraform Provider is available in the [Terraform Registry](https://registry.terraform.io/providers/sutrolabs/census/latest). Add it to your Terraform configuration:

```hcl
terraform {
  required_providers {
    census = {
      source  = "sutrolabs/census"
      version = "~> 0.2.0"
    }
  }
}

provider "census" {
  personal_access_token = var.census_personal_token
  region                = "us"  # or "eu", "au"
}
```

### Authentication

The provider requires a Census personal access token. You can generate one from your Census account settings. We recommend storing the token in an environment variable or using a secrets management system:

```bash
export CENSUS_PERSONAL_ACCESS_TOKEN="your-token-here"
```

The provider will automatically detect the `CENSUS_PERSONAL_ACCESS_TOKEN` environment variable.

### Basic Example

Here's a simple example of managing a Census workspace with Terraform:

```hcl
resource "census_workspace" "data_team" {
  name = "Data Team Workspace"
  notification_emails = ["data-alerts@company.com"]
  return_workspace_api_key = true
}

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

resource "census_sync" "users_to_crm" {
  workspace_id = census_workspace.data_team.id
  label        = "Users to CRM"

  source_attributes {
    connection_id = census_source.warehouse.id
    object {
      type         = "table"
      table_name   = "users"
      table_schema = "public"
    }
  }

  destination_attributes {
    connection_id = census_destination.crm.id
    object        = "Contact"
  }

  operation = "upsert"

  field_mapping {
    from                  = "email"
    to                    = "Email"
    is_primary_identifier = true
  }

  field_mapping {
    from = "first_name"
    to   = "FirstName"
  }

  run_mode {
    type = "triggered"
    triggers {
      schedule {
        frequency = "daily"
        hour      = 8
        minute    = 0
      }
    }
  }
}
```

## Available Resources

* **census_workspace** - Manage Census workspaces
* **census_source** - Data warehouse connections (Snowflake, BigQuery, Postgres, etc.)
* **census_destination** - Business tool integrations (Salesforce, HubSpot, etc.)
* **census_dataset** - SQL datasets for data transformation
* **census_sync** - Data syncs between sources and destinations

All resources have corresponding data sources for read-only operations.

## Resources & Documentation

* **Terraform Registry** - [registry.terraform.io/providers/sutrolabs/census](https://registry.terraform.io/providers/sutrolabs/census/latest) - Resource documentation, examples, and version history
* **GitHub Repository** - [sutrolabs/terraform-provider-census](https://github.com/sutrolabs/terraform-provider-census) - Source code and complete examples
* **Developer Documentation** - [developers.getcensus.com](https://developers.getcensus.com) - Full API reference
* **CHANGELOG** - [View changelog](https://github.com/sutrolabs/terraform-provider-census/blob/main/CHANGELOG.md) - Version history and changes

## Need help?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
