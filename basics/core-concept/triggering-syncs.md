# Triggering & Scheduling

Running a sync manually is not that useful on its own. The real power of Census is having your syncs run automatically. Once you've got your sync up and running, you can configure your sync to run automatically in several ways:

* [Schedule](triggering-syncs.md#schedule) (including via [Cron](triggering-syncs.md#cron-custom-schedules))
* [dbt Cloud](triggering-syncs.md#dbt-cloud)
* After another sync with a [Sequence](triggering-syncs.md#sequences)
* [Programmatically via API](triggering-syncs.md#sync-trigger-api)
* With Orchestration: [Airflow](triggering-syncs.md#airflow), [Dagster](https://dagster.io/integrations/dagster-census), and [Prefect](https://prefecthq.github.io/prefect-census/)

## Schedule

Schedules let you specify a time and frequency that Census can use to run your sync automatically. You can choose options from weekly all the way to Continuous, which means Census checks your source roughly every minute for new changes.

![](../../.gitbook/assets/screely-1621265385900.png)

{% hint style="info" %}
To remove a schedule from a sync, click the edit icon and select **Manual** from the drop down list.
{% endhint %}

### Cron Custom Schedules

The last scheduling option is Cron. Cron lets you schedule syncs on arbitrary schedules such as every 3 hours, or only week days. Census accepts standard Cron definitions up to minute granularity (second-level granularity cron definitions are not supported). A Cron schedule is specified by a series of five values, separated by spaces. In order, the values are Minute-of-hour, hours-of-day, Days-of-month, Months-of-year, and Day-of-week. The timezone is UTC.

Here's a few examples of common Cron schedules:

* Once an hour, on the hour, every four hours: `0 */4 * * *`
* Hourly during weekdays: `0 * * * 1,2,3,4,5`
* Minutely on the 5th, 6th, and 7th hours of the day in UTC timezone:`0 5,6,7 * * *` , executes sync jobs at _9pm, 10pm and 11pm PST_ or _12am, 1am and 2am EST_

**Please note:** If including a range in your CRON schedule you'll want to make sure the values in the range are in a comma separated list.

**Example:**&#x20;

Hourly during weekdays should be: `0 * * * 1,2,3,4,5` instead of `0 * * * 1-5`

## dbt Cloud&#x20;

If you're using dbt Cloud to run your dbt project, you can configure Census to automatically run syncs whenever your models have been rebuilt. Simply select your dbt Cloud project's job to monitor and Census will automatically trigger a sync when it completes.

![](../../.gitbook/assets/screely-1641611574815.png)

{% hint style="info" %}
Using dbt Cloud to trigger syncs works great with [dbt Models](https://docs.getcensus.com/models/native-dbt-integration) but is not required. Both dbt integrations can be used independently.
{% endhint %}

To connect Census to your dbt Cloud, you'll first need a [dbt Cloud API](https://docs.getdbt.com/docs/dbt-cloud/dbt-cloud-api/service-tokens) key. We use this to subscribe to webhooks for each job you specify.&#x20;

* dbt strongly recommends you use a Service Account token, though User API keys with the correct permissions. Service Account tokens may only be created or modified by users with Account Admin (Enterprise plan) or Owner (Team plan) permissions.
* The Service Token requires at least the `developer` permission (for Enterprise) or a Developer License (for Team) in order to configure new webhooks. See [dbt Cloud docs](https://docs.getdbt.com/docs/deploy/webhooks#prerequisites) for more details.

With your token in hand, you can now connect dbt Cloud to your dbt project.

1. Visit the Settings page and select the Integrations tab\
   ![](../../.gitbook/assets/screely-1641611308263.png)\

2. Then copy your dbt Cloud API key, **Verify** your key is correct and has the proper permissions, and **Save** your settings.\


Now, you'll be able to use a dbt Cloud job to trigger syncs. Visit the **Configuration** tab of any of your syncs.

## Sequences

If your syncs have dependencies and you'd like to organize them to run in order, you can use a Sequence. A Sequence runs a dependent sync whenever its specified parent sync completes successfully. Sequences can be found on the sync configurations page:

<figure><img src="../../.gitbook/assets/CleanShot 2022-11-01 at 12.59.37@2x.png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Sequences do not currently support specifying multiple parent syncs. If you are interested in multi-parent functionality, please email [support@getcensus.com](mailto:support@getcensus.com).
{% endhint %}

## **Sync Trigger API**

Each sync can also be triggered via API. On the sync configuration page, you can access the trigger API endpoint for the sync.

![](../../.gitbook/assets/screely-1621265332761.png)

An empty HTTP POST call to this endpoint will trigger the sync (no need to provide any data in the body). You can use this API to automatically trigger Census syncs as part of your data pipeline, running syncs once the models they depend on have been rebuilt.

### `POST /syncs/[ID]/trigger`

{% tabs %}
{% tab title="Request" %}
```
curl -X POST https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/syncs/[SYNC_ID]/trigger
```
{% endtab %}

{% tab title="Response" %}
```
{
    "status": "success",
    "data": {
        "sync_run_id": 1234567890
    }
}
```
{% endtab %}
{% endtabs %}

| Response Property | Description                                                     |
| ----------------- | --------------------------------------------------------------- |
| status            | `success` or `error` indicating whether the sync was triggered. |
| data              | Present if successful. An object containing the `sync_run_id`   |
| message           | Present if error. Contains message describing the error.        |

### `GET /sync_runs/[ID]`

You can use the `sync_run_id` returned when successfully triggering a sync execution and get status on its progress or determine when it has completed.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/sync_runs/[SYNC_RUN_ID]
```
{% endtab %}

{% tab title="Response" %}
```
{
    "status": "success",
    "data": {
        "error_message": null,
        "records_failed": 15,
        "records_invalid": 5,
        "records_processed": 100,
        "records_updated": 80,
        "status": "completed"
    }
}
```
{% endtab %}
{% endtabs %}

| Response Property  | Description                                                                                                                                                                                                |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| status             | `success` if sync\_run was found                                                                                                                                                                           |
| data               | Present if successful. Contains the following properties:                                                                                                                                                  |
| status             | <ul><li><code>working</code> if the sync is currently executing</li><li><code>completed</code> if the sync finished successfully</li><li><code>failed</code> if the sync failed during execution</li></ul> |
| records\_processed | Number of new or updated records retrieved from the source                                                                                                                                                 |
| records\_updated   | Number of records successfully sent to the destination                                                                                                                                                     |
| records\_invalid   | Number of records skipped by Census because of data quality issues.                                                                                                                                        |
| records\_failed    | Number of records rejected by the destination.                                                                                                                                                             |

## Airflow

{% embed url="https://www.loom.com/share/3437c30c24fb44c09aa0d81f79cf99e6" %}

{% hint style="info" %}
Heads up: Unlike Airflow 2, Airflow 1 doesn't show any non-"core" providers (i.e. Census!) in the connections UI. If you're using Airflow 1, Census should be configured as an "HTTP" Conn Type, [as documented here](https://github.com/sutrolabs/airflow-provider-census#configuration-in-airflow-110).
{% endhint %}

Whether you're using [Astronomer](https://astronomer.io) or self-hosting your own instance, you can use Census's Airflow Provider to trigger and monitor Census syncs.

Visit the [Census Airflow Provider GitHub repository](https://github.com/sutrolabs/airflow-provider-census) for more details on how to use it for your project.

