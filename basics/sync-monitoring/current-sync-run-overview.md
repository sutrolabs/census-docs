# Current Sync Run Overview

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

Within a given sync configuration, Census exposes many data points of information on the current or most recent sync run.

#### Sync Run Metadata

* **Status**: The current status of the sync run. This can be "Working", "Completed", "Failed", or "Canceled".
* **Start Time**: The time the sync run started.
* **Estimated Time Remaining**: If running, the estimated time remaining for the sync run.
* **Total Duration**: If completed, the total duration of the sync run.

#### Source Record Counts

* **Total Source Records**: The total number of records in the source.
* **Changed Source Records**: The number of records that have changed since the last sync run.
* **Invalid Source Records**: The number of records that are invalid in the source.

#### Destination Record Counts

* **Successfully Synced Records**: The number of records that were successfully synced to the destination.
* **Rejected Records**: The number of records that were rejected during the sync run.
