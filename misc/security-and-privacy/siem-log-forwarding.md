---
description: >-
  Allow your Security Teams to Track Critical Data Flows are Being Modified in
  Census
---

# SIEM Log Forwarding

### Introduction

Census' Enterprise plan offers a robust SIEM (Security Information and Event Management) log forwarding feature, compatible with all major SIEM providers including Datadog, Splunk, Sumo, and Panther. This feature is designed to enhance your organization's security and compliance capabilities by forwarding detailed event logs.

### Requesting SIEM Log Forwarding Setup

To initiate the SIEM log forwarding setup, please reach out to our [support team](mailto:support@getcensus.com). During this process, you will need to provide an HTTP endpoint to which we will forward the events. We can support a variety of authentication mechanisms. Our team will guide you through the setup process to ensure seamless integration with your chosen SIEM system.

### Log Forwarding Schedule

Events are forwarded in batches every 15 minutes, ensuring timely updates without overwhelming your SIEM system.

### Log Format and Content

Logs are sent in JSON format. Each log includes the following properties:

* **ACTION:** The action that was performed by the user.
* **ACTOR\_EMAIL:** The email of the user performing the action, if applicable.
* **ACTOR\_ID:** The email of the user performing the action, if applicable.
* **COMMENT:** A description of the action.
* **ENTITY:** The entity related to the action.
* **UNIQUE\_ID:** A unique id for the event.
* **ORGANIZATION\_ID:** The actor's Census organization ID.
* **SOURCE\_IP:** The IP address associated with the actor.
* **TIMESTAMP:** When the action happened.

#### Supported Actions

Our system supports the following actions:

* `workspace_invite_sent`
* `success_change_password_request`
* `user_joined_organization`
* `user_workspace_role_updated`
* `user_claimed_workspace_invitation`
* `organization_invite_revoked`
* `success_silent_auth`
* `success_signup`
* `user_removed_from_workspace`
* `success_verification_email`
* `failed_sending_notification`
* `logout`
* `workspace_invite_revoked`
* `failed_login_(incorrect_password)`
* `success_change_password`
* `failed_exchange`
* `workspace_invite_role_changed`
* `success_exchange`
* `failed_login`
* `organization_invite_sent`
* `user_organization_role_updated`
* `failed_login_(invalid_email/username)`
* `failed_change_password_request`
* `warnings_during_login`
* `success_login`
* `user_removed_from_organization`
* `model_created`
* `model_updated`
* `model_deleted`
* `destination_created`
* `destination_deleted`

<br>
