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

3.  You can always ask Census to perform a reconciliation between the Census UI and your git repository by clicking the **Force Reconcile** button. Use this in the rare cases where the git repository's APIs and webhook functionality are not performing as expected.

### Linked Git Configuration

Every resource within Census that is backed by version control will have a link to the YAML configuration file for that specific resource, and for the latest commit that introduced a change. You can find the link within the Census UI, for example within the Models page:

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 4.59.37 PM.png" alt=""><figcaption></figcaption></figure>

## GitHub&#x20;

GitLink offers some additional functionality when connected to GitHub repositories by automatically adding YAML configuration checks. If you are using GitHub's branch protection features, you may also need to make some changes to allow GItLink to operate smoothly.

### Automated Continuous Integration Tests

When using GitHub as your GitLink repository, Census will run Continuous Integration (CI) tests on every pull request. These tests will specify exactly which changes will occur, as well as whether there are any errors in any YAML configuration.

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-17 at 3.29.10 AM.png" alt="" width="563"><figcaption></figcaption></figure>

## Working with Branch Protection

Because GitLink keeps the state of Census and Git synchronized, Census must write to Git on initial setup and when resources are updated. This may conflict with certain branches that have branch protection (i.e. `main`). To enable GitLink to write to Git, you'll need to bypass pull/merge requests (and sometimes status checks) for the protected branch. 

### GitHub

1. Navigate to your GitHub repo's branch protection settings, and click Edit for the branch connected to GitLink.

![settings branches](https://github.com/sutrolabs/census-docs/assets/8723127/becd6685-b64f-4e9f-b039-761ec7fc61d1)

2. Add the **Census Git** app to the list of actors that bypass required pull request approvals once you install the app during the [#setup](gitlink.md#setup "mention") flow.

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 5.02.53 PM.png" alt=""><figcaption></figcaption></figure>

3. Uncheck the "Require status checks to pass before merging" setting.

![status checks setting](https://github.com/sutrolabs/census-docs/assets/8723127/9602306e-0a5b-4ed2-aa1f-b9fcf6956aee)

To read more about protected branches, see the official GitHub documentation at https://docs.github.com/articles/about-protected-branches

### GitLab

For instructions to bypass merge requests, follow GitLab's instructions at https://docs.gitlab.com/ee/user/project/protected_branches.html#allow-everyone-to-push-directly-to-a-protected-branch

### Bitbucket

For instructions to bypass pull requests, follow BitBucket's instructions at https://confluence.atlassian.com/bitbucketserver/using-branch-permissions-776639807.html

## Troubleshooting

There are a few strict requirements in order to use GitLink:

- The governed GitLink directory (by default, `census/models/*.yml`) must be entirely empty, or populated only by configuration files that Census can read. As such, if you have `.txt` files, `README.md` files, or other files that are not YAML-deserializable and correspond to a known resource configuration by Census, GitLink will not work.
- Each SQL model and sync configuration should be in its own file.

## Sync Attributes Guide

Please refer to this section on the different parameters and their values a sync configuration could take up

- `paused` - (Type: Boolean) Indicates whether the sync is self-operating. Setting this to false will prevent the sync from running automatically based on given schedule or triggers.

- `label` - (Type: String) A short human readable description.

- `template_sync_identifier` - (Optional, Type: String) Resource identifier used as a template when initially creating this one. This property is used for attribution and has no effect on the sync's configuration.

- `behavior` - (Type: Object) Group of parameters that governs how the sync behaves.

  - `operation` - (Type: String) How to deal with records that match (and that don't match) between the source and destination. Possible values are `upsert`, `update`, `create`, `mirror`, `append` or `delete`.

  - `append_properties` - (Type: Object) Parameters for append only syncs (only applies if the `append` option was selected for sync operation).

    - `backfill_records` - (Type: Boolean) Indicate during append sync setup whether records in the source should be backfilled in the destination or just new records moving forward.

    - `high_water_mark` - (Optional, Type: Object) The column (almost always a timestamp) that should be used when identifying new records in an append sync. Including this will use timestamps to determine new records instead of the default Census diff engine (using primary keys).

      - `column_name` - (Type: String) Column name to use as the high water mark key.

  - `mirror_properties` - (Optional, Type: Object) Properties when the mirror sync behavior is provided. Only required when mirror behavior is used and ignored otherwise.

    - `strategy` - (Type: String) How the sync should maintain the mirror between the source and destination. Possible values are `sync_updates_and_deletes` or `sync_updates_and_nulls`.

- `mapping_configuration` - (Optional, Type: Object) Parameters for how Census should handle the mappings of the sync.

  - `sync_all_source_columns` - (Optional, Type: Object) Indicate whether all source columns should be sent to the destination.

    - `enabled` - (Type: Boolean) Denote if sync all source columns is active for this sync.

    - `mode` - (Type: String) How are existing values in destination handled. Possible values are `add_only` or `add_and_delete`.

  - `name_normalization` - (Optional, Type: String) Indicate how the sync would map the source column names to their corresponding destination field names. Possibles values are `match_source_names`, `start_case`, `lower_case`, `upper_case`, `camel_case`, `snake_case` or `ensure_uniqueness`.

  - `order_by` - (Optional, Type: String) Indicate how the mappings between source and destination are ordered. Possible values are `alphabetical_column_name` or `mapping_order`.

- `triggers` - (Type: Object) Upstream triggers that would trigger the current sync to run.

  - `schedule` - (Type: Object) Schedule of the sync.

    - `frequency` - (Type: String) Frequency of the sync trigger. Possible values are `never`, `expression`, `continuous`, `hourly`, `daily`, `weekly` or `quarter_hourly`.

    - `day` - (Optional, Type: String) Week of the day description of the sync schedule. Required if `frequency` is `weekly`. Possible values are `Monday`, `Tuesday`, `Wednesday`, `Thursday`, `Friday`, `Saturday` or `Sunday`.

    - `hour` - (Optional, Type: Integer) Hour description of the sync schedule. Required if `frequency` is `weekly`, `hourly` or `daily`. Possible values are `0` - `23`.

    - `minute` - (Optional, Type: Integer) Minute description of the sync. Required if `frequency` is `weekly`, `hourly` or `daily`. Possible values are `0`-`59`.

    - `cron_expression` - (Type: String) Cron expression for the sync's frequency. Ensure that for `frequency` above, the `expression` option is specified. Please refer to the Census [documentation](/basics/core-concept/triggering-syncs.md#cron-custom-schedules) on what CRON expressions we support.

  - `on_other_sync_success` - (Optional, Type: String) Resource identifier of the sync that would trigger the current sync. The trigger would only be fired if the former sync succeeds.

  - `dbt_cloud` - (Optional, Type: Object) dbt cloud specifications for job that would trigger the current sync. A dbt cloud API key needs to be installed in your Census organization for this to operate correctly.

    - `project_id` - (Type: String) Project ID for the dbt cloud project.

    - `job_id` - (Type: String) dbt job ID within the project triggering current sync.

- `enable_sync_logs` - (Optional, Type: Boolean) Indicate whether the warehouse writeback feature is enabled for this sync.

- `service_slice_size` - (Optional, Type: Integer) Denote the size of the data chunks in which data will be uploaded to the destination. Possible values are `1` - `100,000`.

- `destination` - (Type: Object) The destination to which the sync will upload the data.

  - `connection_identifier` - (Type: String) Resource identifier of the sync destination.

  - `object_identifier` - (Type: String) Object identifier of the sync destination object to which the records are uploaded. Please refer to the Management API documentation on [Destination Objects](api/destination-objects.md) to find object identifiers for a given destination.

  - `lead_union_default_object` - (Type: String) Whether to upload records as a 'Lead or Contact' or 'Lead or Account' object. Only applicable if the current sync has a Salesforce destination. Possible values are `converted` (Lead or Contact) or `lead` (Lead or Account).

  - `file_settings` - (Optional, Type: Object) File settings of the sync destination.

    - `file_format` - (Type: String) File format of the sync destination. Possible values are `CSV`, `TSV`, `JSON`, `NDJSON` or `Parquet`.

    - `delimiter` - (Optional, Type: String) String character that delineates the records in destination.

    - `include_header` - (Optional, Type: Boolean) Indicate if the header row of the destination file should be transferred as a record.

- `source` - (Type: Object) The data source from which records are extracted.

  - `type` - (Type: String) Type of the data source. Possible values are `table`, `segment`, `entity`, `model` or `cohort`.

  - `connection_identifier` - (Type: String) Resource identifier of the source connection.

  - `object_identifier` - (Type: String) Resource identifier of the sync source object. Required if the source type is a `entity`, `model` or `segment`.

  - `table_catalog` - (Type: String) Sync source table catalog name. Required if the source type is a `table`.

  - `table_schema` - (Type: String) Sync source table schema name. Required if the source type is a `table`.

  - `table_name` - (Type: String) Sync source table name. Required if the source type is a `table`.

- `mappings` - (Type: Array)

  - `from` - (Type: Object) The data being mapped from the source.

    - `type` - (Type: String) Type of source data. Possible values are `column`, `constant`, `reference`, `compound` or `segment-membership`.

    - `data` - (Optional, Type: Object) Parameters of the data in the source object.

      Use **one** of the following groups of fields

      1. **Static Expressions** - Constant value to use for the mapping.

         - `basic_type` - (Type: String) Data type of the constant. Possible values are `Text` or `Number`.

         - `value` - (Type: String) Value of the constant.

      2. **Source Column** - Column in the source to be used for the mapping.

         - `column_name` - (Type: String) Name of the source column.

      3. **Compound Upsert Keys**

         - `subexpressions` - (Type: Array) Array of expression objects. Each element should be either a `static expression` or `source column` object (defined above).

      4. **Related Entity Expressions**

         - `object_identifier` - (Type: String) Resource Identifier of source entity.

         - `referenced_column_name` - (Type: String) Column name within entity.

         - `referenced_object_identifier` - (Type: String) Identifier for object within entity.

  - `to` - (Type: Object) Mapping properties in the destination.

    - `field_name` - (Type: String) Name of the mapped column in the destination.

    - `lookup_object` - (Optional, Type: Object) Object properties of the destination.

      - `object_identifier` - (Type: String) Identifier for the destination object.

      - `field_to_match_by` - (Type: String) Field on the object to match a record with.

  - `field_type` - (Optional, Type: String) Data type of the mapping.

  - `follow_source_type` - (Optional, Type: Boolean) Indicate if destination should conform the mapping to the same type as the source.

  - `array_field` - (Optional, Type: Boolean) Indicate if the current field is of type `array`.

  - `is_primary_identifier` - (Optional, Type: Boolean) Indicate if the mapping is the primary identifier for the records between the source & destination.

  - `generate_field` - (Optional, Type: Boolean) Indicate to Census if the mapping is a user-generated field.

  - `preserve_values` - (Optional, Type: Boolean) Indicate if mapping should overwrite existing values in the destination.

  - `operation` - (Optional, Type: String) Array operation indicating how array fields should be updated in the destination. Only applies if `array_field` is set to `true`. Possible values are `overwrite` or `merge`.

- `advanced_configuration` - (Optional, Type: Object) Any advanced configuration that a sync requires, particularly for notification syncs.

- `operational_settings` - (Type: Object) Other operational settings.

  - `alerts` - (Optional, Type: Object) Alerting configuration for the sync.

    - `failed_run_notifications` - (Optional, Type: Object) Notification settings for sync failures.

      - `enabled` - (Optional, Type: Boolean) Indicate if notification is sent on run fails.

    - `failed_record_notifications` - (Optional, Type: Object) Notification settings for when individual records fail in the sync run.

      - `enabled` - (Optional, Type: Boolean) Enable notifications on record failures.

      - `threshold_percent` - (Optional, Type: Integer) The percentage of records that need to fail to send a record failing notification. Possible values are `0` - `100`.
