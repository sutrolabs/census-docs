---
description: Manage Census SQL models and syncs via YAML files in your Git repository.
---

# GitLink

GitLink enables you to leverage best practices of production software development – like peer review and version control – when making changes to your Census workspace. This gives you:

* **Resources as Code**: Specify your Census SQL models and syncs in YAML configuration files.
* **Bi-directional Updates**: Make changes to Census via the Census UI, or by updating the YAML configuration files in your Git repository.
* **Git-Backed Change History:** View and rollback changes to Census resources not just within the Census UI, but also within Git.

Creating, editing, and deleting resources in the Census UI will all be represented as changes to your YAML configuration files stored in Git. All changes will be represented as commits to those files. When you create and edit the configuration files via commits and pull requests in a Git repository, Census will materialize your changes into your Census workspace.

Please visit our full developer documentation at [**developers.getcensus.com/gitlink/guide**](https://developers.getcensus.com/gitlink/guide) for more.

You can also view this [video](https://www.loom.com/share/53e5a08688e246c2a36c5e915b659a0d?sid=b50a009c-7a93-4c67-89a7-b20d2248d38f) for a step by step guide on setting up GitLink in minutes.

{% hint style="info" %}
The GitLink feature is currently in private beta. If you are interested please reach out to your Census representative or the Census Support team at support@getcensus.com
{% endhint %}
