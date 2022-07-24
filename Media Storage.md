## Choose whether to store media in a folder on server or use a service like cloudinary

## Problem statement
Building applications where media files like images and videos need to be uploaded, a consideration for where best to store these files need to be made.

## Decision Matrix
|Criteria|Server|Cloudinary|
|---|---|---|
|Description|This is where files are stored in a folder on the same server as the application server|Cloudinary is an end-to-end image- and video-management solution for websites and mobile apps, covering everything from image and video uploads, storage, manipulations, optimizations to delivery.|
|Cost|No extra cost, but will have to increase server configuration as media volume increases|Free-tier is available and paid tier starts at $89/month|
|Recovery|Data is lost if anything happens to server|Implements a periodic auto-backup plan|
|Complexity|Simple to implement|Simple to implement|
|Feature:Manipulation (reshape, resize, etc)|These have to be coded as featured in the application code|Provided out of the box by the service|
|Feature: Delivery|Media is delivered based on server configuration and availability|Media are delivered using a CDN|
|Security|If the server gets hacked, the clients at risk for identity theft and further incidents of cybercrime. Hackers can also know the directory structure of media files since google index files, and go searching for files that can be used for illegal purposes|Better security|

## Decision

Both evaluated options __can handle the required scenarios__. We have decided to use Cloudinary due to the following merits:
* Reduce load time
* Improves performance
* Reduces bandwidth and infrastructure costs
* A given web server only has so much disk space, which means you now have to deal with the very real possibility of running out of disk space.
* Ability to quickly retrieve and store files there without taxing your web servers or database servers.

## Refereence
https://cloudinary.com/
