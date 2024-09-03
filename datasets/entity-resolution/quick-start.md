# Quick Start

Entity Resolution helps you de-duplicate and associate records across your datasets.



#### Steps to Create Entity Resolution based Dataset

Step 1: Login to Census and Select `New Dataset` button on the Datasets tab

<figure><img src="../../.gitbook/assets/Screenshot 2024-08-30 at 11.46.42 AM.png" alt=""><figcaption></figcaption></figure>

Step 2: Fill in the Dataset name and choose "De-Duplication" as the transformation type.

<figure><img src="../../.gitbook/assets/Screenshot 2024-08-30 at 11.49.07 AM.png" alt=""><figcaption></figcaption></figure>

Step 3: Select Dataset(s) that you want to use as source datasets. These datasets have duplicate records.

<figure><img src="../../.gitbook/assets/Screenshot 2024-08-30 at 11.51.18 AM.png" alt=""><figcaption></figcaption></figure>

Step 4: Define criteria to identify duplicate records as [Match Rules](./#match-rules)

[Fuzzy Match](./#fuzzy-match) can help match similar items.

<figure><img src="../../.gitbook/assets/Screenshot 2024-08-30 at 12.12.34 PM.png" alt=""><figcaption></figcaption></figure>

Step 5: Define [Merge Rules](./#merge-rules) to identify winning record

<figure><img src="../../.gitbook/assets/Screenshot 2024-08-30 at 12.15.17 PM.png" alt=""><figcaption></figcaption></figure>

When no merge rules are defined or when merge rules fail to detect a winning record, census uses lower of the unique IDs to identify winning record.

Step 6: Optional: Override column values of the winning record

<figure><img src="../../.gitbook/assets/Screenshot 2024-08-30 at 1.44.37 PM.png" alt=""><figcaption></figcaption></figure>

Step 7: Review and confirm the configuration. Click Confirm and Census will start running Entity Resolution across your dataset.



Census creates an additional Lineage column on your resolved dataset to explore and debug the resolution.
