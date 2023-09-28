# Sync Alerts

Our goal is to keep all the data flowing smoothly, but sometimes things don't go as planned. When that happens, Census offers multiple ways to get alerted so you're always the first to know what's going on with your syncs. Read on to learn how to configure them.

Each Census sync has its own set of potential alerts and you can configure each of them to match your needs. There are two types of alerts available and both are turned on by default for each new sync:

1. **Sync Failures** - Alerts when a sync completely fails, usually because the source or destination connection is broken.
2. **Records Rejected or Invalid** - Alerts when a sync ran successfully but some of the records were invalid or rejected. In this case, you can configure the threshold that should generate alerts. By default, it's 75% of records, but that can be lowered all the way down to alert you if any record is invalid or rejected. [Learn more about invalid and rejected records](../core-concept/#understanding-sync-history).

{% hint style="info" %}
**Please note:** Census will send a Sync Failure or Rejected/Invalid Record alert upon the first sync run where the alerting conditions are met.&#x20;

To save your inbox, subsequent sync runs with the same failure or rejection % will not trigger additional alerts.&#x20;

Once your sync is back to running successfully or the number of rejected/invalid records has fallen below the specified threshold then new alerts will be sent if the alerting conditions are met again.&#x20;
{% endhint %}



To configure, visit to the **Alerts** tab in your Sync to configure which alerts are enabled per sync.

![](<../../.gitbook/assets/Screen Shot 2021-10-23 at 9.29.15 AM.png>)

### Configure your personal email subscriptions

By default, all members of your team will be subscribed to all emails. You can choose to personally opt out of certain emails, under **Settings** > **User Settings**.

![](<../../.gitbook/assets/Screen Shot 2021-10-23 at 9.45.37 AM.png>)

### Email subscriptions for aliases and mailing lists

You can also send sync alerts and weekly sync summaries to any non-user email address such as an email alias or mailing list. Simply go to **Census** > **Settings** and add the desired email address under **General Settings > Email Alerts and Weekly Summaries**.

### Slack alerts

You can send sync alerts to your selected channels via Slack's channel email feature. Every Slack channel has its own email address, and any emails sent to that address automatically appear as messages in that channel. This is a super easy way to configure alerting without having to give Census a lot of permissions to your organization's Slack.

1. In Slack, find the email address for the channel you want to send alerts to. To do this click the **channel name > Integrations**

![](../../.gitbook/assets/get\_slack\_channel\_email.png)

2. Once you have the email address, go to **Census** > **Settings** and paste that channel's email address under **General Settings** > **Slack Alerts**

![](<../../.gitbook/assets/Screenshot 2023-03-30 at 10.27.29 PM.png>)

:tada:That's it! Now your slack channel(s) will automatically post any alerts configured on all your syncs. (No weekly summaries will be sent to Slack channels.)
