---
description: Manage Census SQL models and syncs via YAML files in your Git repository.
---

# GitLink

## Overview

GitLink enables you to leverage best practices of production software development – like peer review and version control – when making changes to your Census workspace. This gives you:

- **Resources as Code**: Specify your Census SQL models and syncs in YAML configuration files.
- **Bi-directional Updates**: Make changes to Census via the Census UI, or by updating the YAML configuration files in your Git repository.
- **Git-Backed Change History:** View and rollback changes to Census resources not just within the Census UI, but also within Git.

Creating, editing, and deleting resources in the Census UI will all be represented as changes to your YAML configuration files stored in Git. All changes will be represented as commits to those files. When you create and edit the configuration files via commits and pull requests in a Git repository, Census will materialize your changes into your Census workspace.

<figure><img src="../../.gitbook/assets/screenshot.png" alt=""><figcaption><p>A sample YAML configuration file within Git that describes a Census SQL model.</p></figcaption></figure>

This will also enable a global History view of all resource changes across your entire Census workspace. You can isolate exactly when those changes went into effect, and the latest Git commit associated with that change.

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 3.40.20 PM.png" alt=""><figcaption><p>A sample set of changes within the new History view.</p></figcaption></figure>

{% hint style="warning" %}
GitLink is only accessible to Platform Plan accounts. If you would like to enable GitLink and are not on the Platform Plan, please contact us at [support@getcensus.com](mailto:support@getcensus.com).
{% endhint %}

## Setup

To set up GitLink:

1.  Go to **Settings -> Integrations.**

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 2.55.35 PM (1).png" alt=""><figcaption></figcaption></figure>

2.  Click **Setup.**

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 2.55.49 PM.png" alt=""><figcaption></figcaption></figure>

3.  You're now on the GitLink configuration page. Let's get set up by connecting to Git:

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 2.55.56 PM (1).png" alt=""><figcaption></figcaption></figure>

4.  Select the repositories you would like to use for version control:

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 2.56.15 PM.png" alt=""><figcaption></figcaption></figure>

5.  Once you select what repositories you want to be connected, it will redirect you back to the GitLink configuration page. Select the specific repository and branch name that you'd like to use for version control.

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 2.57.10 PM.png" alt=""><figcaption></figcaption></figure>

    Optionally, in addition to the repository and branch, you can select a directory where Census will read and write configuration files. Census will never edit any files outside of this path.

6.  Once the repository, branch, and directory are saved, click **Enable Git Sync**. You'll see a modal pop up. Here, you can specify whether to use Census as the basis for the first sync (thus overriding all Census configuration files within Git), or to import Git configurations into Census (thus overriding all models within Census). Click **Setup Git Sync** to continue.

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 3.02.22 PM.png" alt=""><figcaption></figcaption></figure>

7.  Click **Setup Git Sync** to continue. At this point, Census will be hard at work setting up GitLink, synchronizing the state of Census and Git. This should take a few minutes.

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 3.02.24 PM.png" alt=""><figcaption></figcaption></figure>

8.  Once the initial sync is done, GitLink will be set up!

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 3.02.29 PM.png" alt=""><figcaption></figcaption></figure>

## After Setup

Once GitLink is enabled, you can continue to use the Census UI as usual, with no changes to any workflows. Census will automatically commit all edits made within the UI to Git. Likewise, all changes within Git will automatically be synced to Census.

In addition, several new features will be available to users after the feature is enabled.

{% hint style="warning" %}
Please ensure that the directory structure within your repository matches the directory structure expected within Census at all times, for both models and syncs. For example, if models are configured to be written to `census/models/` in your Census settings, moving models to a different directory or subdirectory will delete the model from Census.
{% endhint %}

### YAML in your Git Repository

YAML files for each Census resource will be available in your Git repository. Below are sample model and sync configuration YAML files, with explanations of each parameter.

#### SQL Models

```yaml
model:users: ## Unchanging resource identifier for your SQL model
  name: Users ## Changeable UI label for your SQL model
  query: |- ## SQL to run against your data source
    select *
    from schema.users
  description: Accounts! ## Description of your SQL model
  connection: data_warehouse:snowflake-prod ## Resource identifier for your data source
```

#### Syncs

There are many more sync configuration parameters than model parameters, but there are reliable components that we'll discuss below.

To discover the exact YAML that might be necessary for your use case, we recommend creating a sample sync in the UI to your desired destination, or reaching out to [support@getcensus.com](mailto:support@getcensus.com).

{% hint style="info" %}
Available parameters for each sync are dependent on the destination. For example, in your sync to an [S3 bucket destination](../../destinations/s3.md), you might want to specify the file format (like CSV or Parquet), but this parameter is irrelevant to a sync to [Salesforce](../../destinations/salesforce.md).
{% endhint %}

```yaml
sync:hubspot-contact-sync: ## Unchanging resource identifier for your sync
  paused: false ## Option to pause the sync from its regular schedule, usually "false"
  label: Hubspot Contact Sync ## Changeable UI label for your sync

  # Sync operation behaviors, e.g. upsert, update, mirror
  behavior:
    operation: upsert

  # Scheduling options for your sync
  triggers:
    schedule:
      frequency: quarter_hourly
      minute: 0

  # Destination connection and object
  destination:
    connection_identifier: destination:hubspot-prod ## Resource identifier for your destination
    object_identifier: contact

  # Source connection and object (e.g. model, segment, table)
  source:
    type: model
    connection_identifier: data_warehouse:snowflake-prod ## Resource identifier for your data source
    object_identifier: model:users ## Resource identifier for your model / segment / entity

  # Mappings from your dataset's columns to the destination's fields
  mappings:
    - from:
        type: column
        data:
          column_name: ID
      to:
        field_name: USER_ID
      is_primary_identifier: true ## Census uses the identifier to look for matched records between source and destination
    - from:
        type: column
        data:
          column_name: LAST_LOGIN_DATE
      to:
        field_name: LAST_LOGIN

  # Alerting options and thresholds for your syncs
  operational_settings:
    alerts:
      failed_run_notifications:
        enabled: true
      failed_record_notifications:
        enabled: true
        threshold_percent: 75
```

### Automatic YAML Spec Versions

The YAML spec for GitLink-backed resources is versioned. Currently, the spec version is `0.x`. Version updates will automatically upgrade your repository with new feature support, until `1.x`. We do not anticipate changes to any core model and sync components (like the `mappings` or `operational_settings` sync configuration blocks).

YAML specs will be upgraded to enable support for new resources, and match support for model and sync configuration options. After `1.x`, you will have migration windows announced at least 2 weeks in advance, with the ability to choose exactly when upgrades occur.

### History View

Census provides a History View of all changes applied from Census to Git, and from Git to Census. To find the History View:

1.  Navigate to the **Integrations** page and click **View History**.

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 4.53.43 PM (1) (1) (1) (1) (1) (1) (2) (2) (1) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

2.  You can see a full list of all changes, including the latest commit from the changes that were applied, the number of changes (and failures), and when the changes were applied.

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 3.40.20 PM (1).png" alt=""><figcaption></figcaption></figure>

3.  You can always ask Census to perform a reconciliation between the Census UI and your git repository by clicking the **Force Reconciliation** button. Use this in the rare cases where the git repository's APIs and webhook functionality are not performing as expected.

### Linked Git Configuration

Every resource within Census that is backed by version control will have a link to the YAML configuration file for that specific resource, and for the latest commit that introduced a change. You can find the link within the Census UI, for example within the Models page:

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 4.59.37 PM.png" alt=""><figcaption></figcaption></figure>

## GitHub&#x20;

GitLink offers some additional functionality when connected to GitHub repositories by automatically adding YAML configuration checks. If you are using GitHub's branch protection features, you may also need to make some changes to allow GItLink to operate smoothly.

### Automated Continuous Integration Tests

When using GitHub as your GitLink repository, Census will run Continuous Integration (CI) tests on every pull request. These tests will specify exactly which changes will occur, as well as whether there are any errors in any YAML configuration.

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-17 at 3.29.10 AM.png" alt="" width="563"><figcaption></figcaption></figure>

### Working with Branch Protection

Because GitLink keeps the state of Census and Git synchronized, Census must write to Git on each resource save. This may conflict with certain branches that have branch protection (i.e. `main`). To fix this, you can add the **Census Git** app to the list of actors that bypass required pull request approvals once you install the app during the [#setup](gitlink.md#setup "mention") flow.

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 5.02.53 PM.png" alt=""><figcaption></figcaption></figure>

## Troubleshooting

There are a few strict requirements in order to use GitLink:

- The governed GitLink directory (by default, `census/models/*.yml`) must be entirely empty, or populated only by configuration files that Census can read. As such, if you have `.txt` files, `README.md` files, or other files that are not YAML-deserializable and correspond to a known resource configuration by Census, GitLink will not work.
- Each SQL model and sync configuration should be in its own file.

## Sync Attributes Guide

Please refer to this section on the different parameters and their values a sync configuration could take up

- `paused` - (Type: Boolean) Indicates whether the current sync is in a paused state. Setting this to false will prevent the sync from running in its cadence.

- `label` - (Type: String) Name of the sync.

- `template_sync_identifier` - (Optional, Type: String) Resource Identifier of the sync from which the current sync was created from

- `behavior` - (Type: Object) Describe the sync behavior to Census

  - `operation` - (Type: String) Indicate to Census how to deal with records that match (don't match) between the sync's source and destination. Possible values are <span style="color:red">upsert</span>, <span style="color:red">update</span>, <span style="color:red">create</span>, <span style="color:red">mirror</span>, <span style="color:red">append</span> or <span style="color:red">delete</span>

  - `append_properties`

    - `backfill_records`

    - `high_water_mark`

      - `column_name`

  - `mirror_properties`

    - `strategy`

- `mapping_configuration`

  - `sync_all_source_columns`

    - `enabled`

    - `mode`

  - `name_normalization`

  - `order_by`

- `triggers`

  - `schedule`

    - `frequency`

    - `day`

    - `hour`

    - `minute`

    - `cron_expression`

  - `on_other_sync_success`

  - `dbt_cloud`

    - `project_id`

    - `job_id`

- `enable_sync_logs`

- `service_slice_size`

- `destination`

  - `connection_identifier`

  - `object_identifier`

  - `lead_union_default_object`

  - `file_settings`

    - `file_format`

    - `delimiter`

    - `include_header`

- `source`

  - `type`

  - `connection_identifier`

  - `object_identifier`

  - `table_catalog`

  - `table_schema`

  - `table_name`

- `mappings`

  - `from`

    - `type`

    - `data`

  - `to`

    - `field_name`

    - `lookup_object`

      - `object_identifier`

      - `field_to_match_by`

  - `field_type`

  - `follow_source_type`

  - `array_field`

  - `is_primary_identifier`

  - `upsert_mapping`

  - `truncate`

  - `generate_field`

  - `preseve_values`

  - `operation`

- `advanced_configuration`

- `operational_settings`

  - `alerts`

    - `failed_run_notifications`

      - `enabled`

    - `failed_record_notifications`

      - `enabled`

      - `threshold_percent`
