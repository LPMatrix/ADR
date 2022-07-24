## Choose whether to store media in a folder on server or use a service like cloudinary

## Problem statement
Building applications where media files like images and videos need to be uploaded, a consideration for where best to store these files need to be made.

## Decision Matrix
|Criteria|Server|Cloudinary|
|---|---|---|
|Description|This is where files are stored in a folder on the same server as the application server|Cloudinary is an end-to-end image- and video-management solution for websites and mobile apps, covering everything from image and video uploads, storage, manipulations, optimizations to delivery.|
|Cost|No extra cost, but will have to increase server configuration as media volume increases|Free-tier is available and paid tier starts at $89/month|
|Recovery|--|--|
|Complexity|--|--|
|Features|--|--|
|Description|--|--|
|Description|--|--|

## Decision

Both evaluated options __can handle the required scenarios__. We have decided to use Cloudinary due to the following merits:
* Reduce load time
* Improves performance
* Reduces bandwidth and infrastructure costs

## Refereence
https://cloudinary.com/
