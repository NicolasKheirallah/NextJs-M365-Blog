---
date: '2021-11-10T20:54:01.975Z'
title: Perform a Site swap from SharePoint Admin center
description: Performing a site swap for changing places for diffrent sites.
tags: ['SharePoint']
summary: Performing a site swap for changing places for diffrent sites.
authors: ['default']
---

So when working with Viva Connection you might have created a seperate Home site for development while your old one lives on until you're done. When you are done, you might wanna swap places so the new site get's the root URL. This is how you do it

1. Visit SharePoint Admin Center
   https://yourtenant-admin.sharepoint.com/_layouts/15/online/AdminHome.aspx#/home

2. Press Active sites
   ![Image](/static/images/assets/PerformSiteSwap/2.png)

3. Select Your root Site, "https://yourtenant.sharepoint.com/"

- Make sure it isn't a hub site.
- Make Sure there isn't any retention policies in place for those two sites for now
- Remove the site as a Home Site for now

![Image](/static/images/assets/PerformSiteSwap/3.png)

4. Add URL for your new site and press Save

   ![Image](/static/images/assets/PerformSiteSwap/4.png)

5. This can take a small while as something in the background will run.

6. When the site swap is done, I recommend that you reindex the site. Some webpart and search can be cause Issues first 24-48 hours
