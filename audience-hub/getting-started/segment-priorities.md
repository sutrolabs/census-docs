# Segment Priorities

Marketing to a large audience can be a challenging task, especially when you have hundreds of different segments that overlap in different ways. Often, marketing teams want to ensure that users only appear in a single segment at any given time. This is where segment priorities come in.

Segment priorities allow you to define the relative priorities of segments, so that users only appear in the highest priority segment they could be a member of. Priorities set an order of segments from highest to lowest. When a user “falls off” the end of a segment, they go into the next highest priority segment they could be a member of.

## Setting up Priorities

1. First ensure you have more than 1 segment on an entity
2. Navigate to Audience Hub and then Priorities
3. Click "New Priority List"&#x20;
4. Give it a name and select the parent entity
5. Now choose the segments that will be part of the priority list
6. These can be reordered, with the higher in priority the higher in the list

<figure><img src="../../.gitbook/assets/CleanShot 2023-07-25 at 02.49.01@2x.png" alt=""><figcaption></figcaption></figure>

In the example above if a user is in the Soccer Players Segment then they will be categorized as so.  If not then they will be checked against the next segment, Cyclists. Again if they don't fall into this segment then they will continue down the list until they fit into a segment or no segment.  \
\
To avoid conflicting priorities a segment can only be a part of a single priority list.&#x20;
