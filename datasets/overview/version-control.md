# Version Control

Datasets provide version control tracking to give you a historical understanding of how your dataset definition has changed. You can view your Dataset versions under the **Activity** tab. You can track:

* The user made a change
* The time when the change was made
* The dataset information that was changed, such as:
  * Name change
  * Description change
  * Query change
  * Dataset Type change
  * Dataset Property Mappings delete, adds or change
  * Dataset Relationships delete, adds or change

<figure><img src="../../.gitbook/assets/image (7) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption></figcaption></figure>

Clicking the **Restore** button will restore the state of your Dataset query immediately prior to the selected change. This enables you to update your datasets with confidence, knowing you can always revert your changes if they accidentally break something downstream.

{% hint style="warning" %}
Note that restores will only affect the query value of the dataset. Names, descriptions, type etc will remain as they were before restoring.
{% endhint %}
