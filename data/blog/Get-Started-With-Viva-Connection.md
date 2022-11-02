---
date: '2022-10-01T11:43:00'
title: Get Started with Viva Connections
description: A guide on how to get started with Viva connections
tags: ['Viva', 'Viva Connections', 'Teams', 'SharePoint']
summary:
authors: ['default']
---

So this is a step to step guide for getting started with Viva Connections

Requirements

- Microsoft Teams admin (To add Viva Connection)
- SharePoint admin
- SharePoint Home Site
- Communication Site (Recommend using root site)

Optional:

- Custom name for your Intranet
- Custom icons in PNG, 192X192 and 32x32 in size

Recommendation:

I strongly recommend that you redesign your Home site and modernize it if it hasn't been done in a while. Don't be afraid to take help from your communication department, as they are usually the one who owns the landing site.

You can make use of Lookbook to get insperation

Guide:

1. Vising your SharePoint Admin center.
   ![Image](/static/images/assets/SetUpVivaConnections/8.png)

2. Select Active sites and copy the URL off the Site you want to use as a Home site
   ![Image](/static/images/assets/SetUpVivaConnections/9.png)

3. Press settings and then select Home Site.
   ![Image](/static/images/assets/SetUpVivaConnections/10.png)

4. Paste the URL and wait for the confirmation that the URL can be used. Confirm this.
   Note: You need the https://
   ![Image](/static/images/assets/SetUpVivaConnections/11.png)

5. Now visit Teams Admin center
   ![Image](/static/images/assets/SetUpVivaConnections/1.png)

6. Go down to Teams apps
   ![Image](/static/images/assets/SetUpVivaConnections/2.png)

7. Choose manage apps and search after Viva Connection
   ![Image](/static/images/assets/SetUpVivaConnections/3.png)

8. Select the Viva connection App and select Allow.

9. You can now customize this, You can change name, description, icon, color etc.
   ![Image](/static/images/assets/SetUpVivaConnections/4.png)

10. Now press Setup policy, choose global if you want to push it to all users.
    ![Image](/static/images/assets/SetUpVivaConnections/6.png)

11. Press on add app under Installed apps and search for your app, do the same under pinned apps.
    ![Image](/static/images/assets/SetUpVivaConnections/7.png)

12. Press Save

Now all users show have gotten the app pushed out, it can take upto 24h to show up. But usually straight away on Teams on the web.

![Image](/static/images/assets/SetUpVivaConnections/12.png)

Common issue:

- Q: If app does install?
  - A: Check that there isn't a permission policy in place that prevents the app of showing up, the app needs to be included in the custom permission policy
