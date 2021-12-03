# Alerts

Our goal is to keep all the data flowing smoothly, but sometimes things don't go as planned. When that happens, Census offers multiple ways to get alerted so you're always the first to know what's going on with your syncs. Read on to learn how to configure them.

### **Sync alerts**

Each Census sync has its own set of potential alerts and you can configure each of them to match your needs. There are two types of alerts available and both are turned on by default for each new sync:

1. **Sync Failures** - Alerts when a sync completely fails, usually because the source or destination connection is broken.
2. **Records Rejected or Invalid** - Alerts when a sync ran successfully but some of the records were invalid or rejected. In this case, you can configure the threshold that should generate alerts. By default, it's 75% of records, but that can be lowered all the way down to alert you if any record is invalid or rejected. [Learn more about invalid and rejected records](core-concept.md#understanding-sync-history).

To configure, visit to the **Alerts** tab in your Sync to configure which alerts are enabled per sync.

![](<../.gitbook/assets/Screen Shot 2021-10-23 at 9.29.15 AM.png>)

### Configure your personal email notifications

By default, all members of your team will receive all email notifications. You can choose to personally opt out of certain notifications, under **Settings** > **User Settings**.

![](<../.gitbook/assets/Screen Shot 2021-10-23 at 9.45.37 AM.png>)

### Send emails notifications to aliases and mailing lists

You can also send email notifications to any non-user email address such as an email alias or mailing list. Simply go to **Census** > **Settings** and add the desired email address under **Email notifications** > **Additional email addresses**

### Slack notifications

You can send Slack alerts to your selected channels via Slack's channel email feature. Every Slack channel has its own email address, and any emails sent to that address automatically appear as messages in that channel. This is a super easy way to configure notifications without having to give Census a lot of permissions to your organization's Slack.&#x20;

1. In Slack, find the email address for the channel you want to send notifications to. To do this click the **channel name > Integrations**

![](../.gitbook/assets/get\_slack\_channel\_email.png)

2\. Once you have the email address, go to **Census** > **Settings** and paste that channel's email address under **General** > **Slack Notifications**

![](<../.gitbook/assets/Screen Shot 2021-10-23 at 9.47.52 AM.png>)

:tada:That's it! Now your slack channel(s) will automatically post any alerts configured on all your syncs, as well as the weekly sync summary.&#x20;
