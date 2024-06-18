---
description: Use Census directly with dbt through the native dbt integration.
---

# DBT Integration

Census supports connecting to an existing dbt project hosted in GitHub or GitLab, which allows you keep all your source code & transforms in a single repository while leveraging Census' functionality. Census is designed to work hand-in-hand with dbt Cloud or any other dbt runner.

## Setting it up

Here are the instructions for connecting a dbt project:

1. **Connect to your repository** in GitHub or GitLab. If you’d prefer to use a different service, please let us know!
2. **Select the branch** you’d like Census to use. Census will refresh the project on a regular basis and detect any changes to your models. You can force a refresh at any point from the models' page.
3. **Specify the database and schema parameters** used when compiling models. These values should be the same values you use in the `profiles.yml` file for your production dbt runs. You may need to ensure that your Census data warehouse connection has read access to intermediate tables produced by your dbt run.
4. **Customize optional parameters**:
   1. _The Census model selector._ Any model exposed to Census becomes available as a source for syncing your data to external tools. By default, Census looks for models with the `census` tag but you can customize the filter. Example selectors:
      * All models with a tag: `tag:census`
      * All models in a directory: `path/to/models`
      * All models: `*`
      * For more information on selector syntax, see [dbt’s Model Selector Syntax](https://docs.getdbt.com/reference/model-selection-syntax/).
   2. _Target Profile Name._ Provide Census with your production profile's name if this value is used as a variable in a custom `generate_schema_name` macro or other location. Otherwise, leave this value as `default`.
   3. _Environment Variables_. Use the Environment Variable editor to specify the values that Census should use when compiling your dbt models.

Once you’ve configured your project repository, Census will analyze your project and display the models you’ve made available. You’re now ready to start using these models as part of Census syncs!

## Managing dbt versions

Census currently supports the following dbt versions: `1.4`, `1.5`, `1.6`, `1.7`, and `1.8`. We announce new version support in our [changelog](https://whatsnew.getcensus.com/), and we aim to add support for a new dbt version no more than four weeks after its release by dbt labs.

To determine your dbt version, Census uses the [`require-dbt-version`](https://docs.getdbt.com/reference/project-configs/require-dbt-version) field (if specified) in your project's `dbt_project.yml`. We recommend you pin your dbt project to the minor version range as dbt recommends. For example, the following configuration would ping your project to version 1.6:

```yaml
require-dbt-version: ">=1.6.0,<1.7.0"
```

A few additional notes:

* If this field is not specified, a default version of `1.4` will be used. After Jan 15, 2024, the latest available version will be used.
* We do not recommend you specify a single patch-level dbt version (for example: `require-dbt-version: 1.6.0`) as this can cause your project to break when newer versions are adopted.
* If Census does not support a version the matches the conditions in `require-dbt-version` field, the project will not compile successfully.
* If Census supports multiple dbt versions that match the requirements, the latest version supported by Census will be used.

Alternatively, you can configure your dbt project in Census to use a specific dbt version (note that this version must be within the supported version range defined in your `dbt_project.yml` if one is specified). You can set this by selecting a specific version in the **dbt Version** dropdown menu with in your dbt project's configuration in Census.

<figure><img src="../.gitbook/assets/dbt Version (1).png" alt=""><figcaption></figcaption></figure>

Note that setting an version override may cause issues if the Census configured value falls behind your project configuration. We recommend you provide the support values using `require-dbt-version` instead.

Census ignores the optional `version` and `config-version` fields in `dbt_project.yml`.

## Unsupported features

Our dbt integration is designed to pair nicely with your existing dbt runner, whether dbt Cloud or self-hosted. We do this by using the `dbt compile` command rather than the typical `dbt run` and then make use of the compiled output only.

As a result, there's several dbt features that Census does not make use of. These include:

* Materialization directives. Census doesn’t currently materialize your tables back to your data warehouse. Census will however use materialized tables by your dbt runner to speed up the execution
* Pre and post hooks
* Non-public packages
* Census does not currently support dbt regions other than `North America multi-tenant`. dbt regions described in [documentation here](https://docs.getdbt.com/docs/cloud/about-cloud/regions-ip-addresses).

{% hint style="info" %}
Census does not currently support dbt regions other than `North America multi-tenant.`Further information about dbt regions in [documentation here](https://docs.getdbt.com/docs/cloud/about-cloud/regions-ip-addresses).
{% endhint %}

## dbt Continuous Integration (CI) Checks in GitHub

For dbt models used in Census syncs, Census can check whether you are going to drop, rename, or move a model that will end up breaking an active sync in your account. When a Pull Request (or commit to a Pull Request) is created, dbt CI Checks will help ensure that your dbt development never unexpectedly breaks downstream Census syncs.

### Installing CI Checks in GitHub

To enable these CI checks, navigate to your dbt integration in Census and click "Enable CI/CD Tests in GitHub". Note that Census will require the `checks:read` permission to install.

![You can find dbt Checks in a new section of your dbt integration, under "Automatic tests in dbt".](<../.gitbook/assets/Screen Shot 2022-08-10 at 3.43.09 PM.png>)

Once you enable CI checks, Census will automatically run a sample check on a PR. You can then view the PR to see the results of the check.

![](<../.gitbook/assets/Screen Shot 2022-08-10 at 4.38.56 PM.png>)

If any tests do not pass, you can click **Details** to view more information about the results. You'll see a report of any broken models and their dependent syncs, with links to investigate these syncs further in Census.

![A detailed view of the test failures.](<../.gitbook/assets/Screen Shot 2022-08-10 at 4.39.19 PM.png>)

## Coordinating with dbt Cloud

If you're using dbt Cloud to run your dbt project, our integration goes even further. You can configure Census to automatically run syncs whenever your models have been rebuilt. See our documentation on [connecting and configuring dbt Cloud](../basics/core-concept/triggering-syncs.md#dbt-cloud-integration).

## Required data warehouse permissions

Census doesn't necessarily require the same permissions your dbt project needs because Census only runs the models you've exposed to Census during set up. Census only requires read access to your selected models and any of their materialized dependencies. That means you can use dbt's materialize configuration flag to create permissions boundaries. Once materialized dependencies are generated by dbt runner, Census will reference the materialized results when accessing your models.
