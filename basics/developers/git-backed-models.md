---
description: >-
  See and make changes to Census SQL models via YAML files in your Git
  repositories.
---

# Git-backed Models

{% hint style="warning" %}
Git-backed Models is only accessible to Platform Plan accounts. If you would like to enable version control and are not on the Platform Plan, please contact us at [support@getcensus.com](mailto:support@getcensus.com).
{% endhint %}

Git-backed Models enables you to leverage best practices of production software development – like peer review and version control – when making changes to your Census workspace. This gives you:

* **Resources as Code**: Specify your Census SQL models in YAML configuration files.
* **Bi-directional Updates**: Make changes to Census via the Census UI, or by updating the YAML configuration files in your Git repository.
* **Git-Backed Change History:** View and rollback changes to Census SQL models not just within the Census UI, but also within Git.

Creating, editing, and deleting SQL Models in the Census UI will back them up into a git repository as YAML configuration files. All changes will be represented as commits to those files.&#x20;

<figure><img src="https://lh6.googleusercontent.com/5rHaynRLBu56UJevrOaLiD0NQ7RP-2N4zNc1L_7CjSkXjizHm1TfRL1tBGom1EswZVk0uOCIJoM5hw-Ze8fehOdtSyfO-jdwIunGx5irBZDyyhhTVCAswvq7eJ2ZhJdayHM2ZgSpAishwlicN1BwvII" alt=""><figcaption><p>A sample YAML configuration file within Git that describes a Census SQL model.</p></figcaption></figure>

When you create and edit the configuration files via commits and pull requests in a git repository, Census will materialize your changes into your Census workspace.&#x20;

<figure><img src="https://lh3.googleusercontent.com/0B2EWmcpZFfv9oX1PbRJwOqFTS7O4s-phb26iz4BUMj21cCL09htzoDTnQHV7wvI6ecD3yqOfEkMDToS0oejFJTW5RPc0vrBhesV37watjyLUPFVF0hkwvATYeGtKda4CTAeZlE1tw-j-Dd8frmQWgc" alt=""><figcaption><p>Changes will also show their source (Census or Git). And don't worry, we still think YAML is great! Woohoo!</p></figcaption></figure>

This will also enable a global History view of all SQL Model changes across your entire Census workspace. You can isolate exactly when those changes went into effect, and the latest Git commit associated with that change.

<figure><img src="https://lh3.googleusercontent.com/-AI0eDkUq-Fi1-HsPHeZq4SIqNxB0WUZ_Fxys1DRXuJ3cjBlJxplezz2nLg289tBQfnyEZqbKw8nWi6M5CBFleDQJyGVnL7AGHRxBTwNS37TLhK7d79hyIjLoESz_MatzGLnPlL99S0PoZMfToYQR_c" alt=""><figcaption><p>A sample set of changes within the new History view.</p></figcaption></figure>



## Setup

To set up Git-backed Models:

1.  Go to **Settings -> Integrations.**

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 2.55.35 PM (1).png" alt=""><figcaption></figcaption></figure>
2.  Click **Setup.**

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 2.55.49 PM.png" alt=""><figcaption></figcaption></figure>
3.  You're now on the Git-backed Models configuration page. Let's get set up by connecting to Git:&#x20;

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 2.55.56 PM (1).png" alt=""><figcaption></figcaption></figure>
4.  Select the repositories you would like to use for version control:

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 2.56.15 PM.png" alt=""><figcaption></figcaption></figure>
5.  Once you select what repositories you want to be connected, it will redirect you back to the Git-backed Models configuration page. Select the specific repository and branch name that you'd like to use for version control.

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 2.57.10 PM.png" alt=""><figcaption></figcaption></figure>

    Optionally, in addition to the repository and branch, you can select a directory where Census will read and write configuration files. Census will never edit any files outside of this path.
6.  Once the repository, branch, and directory are saved, click **Enable Git Sync**. You'll see a modal pop up. Here, you can specify whether to use Census as the basis for the first sync (thus overriding all Census configuration files within Git), or to import Git configurations into Census (thus overriding all models within Census). Click **Setup Git Sync** to continue.

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 3.02.22 PM.png" alt=""><figcaption></figcaption></figure>
7.  Click **Setup Git Sync** to continue. At this point, Census will be hard at work setting up Git-backed Models, synchronizing the state of Census and Git. This should take a few minutes.

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 3.02.24 PM.png" alt=""><figcaption></figcaption></figure>
8.  Once the initial sync is done, Git-backed Models will be set up!

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 3.02.29 PM.png" alt=""><figcaption></figcaption></figure>



## After Setup

Once Git-backed Models is enabled, users can continue to use Census as usual, with no changes to any workflows. Census will automatically commit all edits made within the UI to Git, without requiring any additional effort from users. Likewise, all changes within Git will automatically be synced to Census.

In addition, several new features will be available to users after the feature is enabled.

### History View

Census provides a History View of all changes applied from Census to Git, and from Git to Census. To find the History View:

1.  Navigate to the **Integrations** page and click **View History**.

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 4.53.43 PM (2).png" alt=""><figcaption></figcaption></figure>
2.  You can see a full list of all changes, including the latest commit from the changes that were applied, the number of changes (and failures), and when the changes were applied.

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 3.40.20 PM.png" alt=""><figcaption></figcaption></figure>

### Linked Git Configuration

Every resource within Census that is backed by version control will have a link to the YAML configuration file for that specific resource, and for the latest commit that introduced a change. You can find the link within the Census UI, for example within the Models page:

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 4.59.37 PM.png" alt=""><figcaption></figcaption></figure>



## Troubleshooting

There are currently several limitations to the setup and usage of Git-backed Models:

*   Census must have direct write-access to the specified branch and repository. This may conflict with certain branches that have branch protection (i.e. `main`). To fix this, you can add the **Census Git** app to the list of actors that bypass required pull request approvals once you install the app during the [#setup](git-backed-models.md#setup "mention") flow.

    <figure><img src="../../.gitbook/assets/Screenshot 2023-03-03 at 5.02.53 PM.png" alt=""><figcaption></figcaption></figure>
* The installation directory of SQL models (by default, `census/models/*.sql`) must be entirely empty, or populated only by configuration files that Census can read. As such, if you have `.txt` files, `README.md` files, or other files that are not YAML-deserializable and correspond to a known resource configuration by Census, Git-backed Models will not work.
* For optimal performance, each SQL model should be in its own file.
