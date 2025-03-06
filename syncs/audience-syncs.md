# Audience Syncs

Audience Syncs makes managing your segments across all your destinations a snap. When a destination supports Audience Sync behavior, Census can automatically create and manage the segment/audience/list in the destination, adding and removing members to keep it in sync, and automatically create any missing user profiles if necessary. It can be used with any dataset as a source but works best with [Segments created in Audience Hub](../../audience-hub/getting-started/).

Audience Syncs are an advanced version of a typical Census sync. They providing three additional capabilities:

1. **Audience Creation** - When creating the sync, you can select an existing audience in the destination, or create a new one automatically.
2. **Profile Creation As Needed** - If the destination requires a separate profile be created for each user before they can be added to the audience or list, Census will automatically create the missing profile first.
3. **Record Removal** - Configure what happens when a record leaves your source data set.

Audience Sync destinations all have one thing in common, they support the concept of creating a fixed list of members (in nearly all cases, members of these lists are either individual users or companies). These destinations might refer to this as a custom audience, a CRM list, a cohort or something else. Census takes care of making these lists dynamic by adding, and optionally removing records from these lists every time the sync is run.

### Selecting a Target Audience

Destinations that support audience syncs will allow you to select the specific audience or list you'd like to sync into. You can also provide Census with a new audience name and Census will automatically create the segment for you. You can also select a column from the data itself and Census will use that value in the data to either create a new audience or update an existing one.

<figure><img src="../../.gitbook/assets/Artboard Copy.png" alt=""><figcaption></figcaption></figure>

#### Census-created Audience Tracking

Note that some services do not provide the ability to list existing audiences (for example, Braze Cohorts and Amazon Ads Audiences). In these cases, Census will keep track of audiences it has created and will attempt to not create duplicates, though duplication will happen if the same account is used across multiple Census organizations. A side effect of this is that Test Syncing is not available for these destinations.

### When Records Leave the Source Data

You can optionally define what happens when a record leaves your source data set. You have two options in most cases:

* **Remove Record From Audience** - When the record disappears, also remove it from the destination audience. If the destination represents members with a standalone profile record, this will not be deleted, just removed from the audience.
* **Do Nothing** - Simply stop updating. This is useful if your audience has a separate automatic expiration configured where stale members are removed automatically.

<figure><img src="../../.gitbook/assets/Artboard Copy 2.png" alt=""><figcaption></figcaption></figure>

The rest of the sync configuration is identical to any other typical sync and the fields that you map will be passed to the destination. For more information see [Syncs in Core Concepts](./).
