---
date: '2023-02-10T13:55:21'
title: How to Disable Viva Home Experience
description: A guide on how to Disable Viva Home Experience to go directly to intranet
tags: ['SharePoint', 'Viva', 'Viva Connections']
summary: A guide on how to Disable Viva Home Experience to go directly to intranet
authors: ['default']
---

## Intro

Microsoft has now released Viva home experience which provides employees with a centralized hub for the Viva resources and makes it easier for you get information quickly at a glance.
A con to this is that reaching your intranet is another click away, which can be hard to deploy and inform users that are used to reaching the intranet directly via teams without additional clicks.

So can we disable it?
Well yes! here's how:

## Requirements

- SharePoint admin
- Powershell 7

## Guide

1. Get SharePoint Management Shell installed: [SharePoint Management Shell](https://learn.microsoft.com/en-us/powershell/sharepoint/sharepoint-online/connect-sharepoint-online)

2. Connect to your SharePoint Admin Center:

```Powershell
Connect-SPOService -Url "https://<tenant>-admin.sharepoint.com" -ModernAuth
```

3. Run the command at below:

- "$true" will set your SharePoint site as Default landing page.
- "$false" will set Viva Home as the default landing

```Powershell
Set-SPOHomeSite -HomeSiteUrl <homesiteURL> -VivaConnectionsDefaultStart $true
```

---

date: '2023-10-14T13:55:21'
title: User Viva Home without setting an Homesite
description: A guide on how to setup Viva Home Without setting a homesite
tags: ['SharePoint', 'Viva', 'Viva Connections']
summary: A guide on how to setup Viva Home Without setting a homesite
authors: ['default']

---

## Intro

So I've gotten this question a couple of times so I decided to make a guide on how to set it up!
You might be wondering why would anyone just want Viva Home and not have their landing page in SharePoint?
Well there's several reasons you might want this, Your organisation might not have their intranet in SharePoint but in other systems but you still want to harness the power of Connections and Viva Home.

- You have an existing intranet system that is not based on SharePoint, but you still want to benefit from the features of Connections and Viva Home.
- You have frontline workers who need to access information quickly and easily, without having to navigate through SharePoint.
- You are aware of the upcoming redesign of Viva Home, which will include many of the functionalities that a Homesite provides, such as a news feed, links, user-defined links and more.

## Requirements

- SharePoint admin

## Guide

1.  Go to Microsoft admin:

https://admin.microsoft.com/#/featureexplorer

![Image](/static/images/assets/VivaHomeSetup/1.png)

2. Press Microsoft Viva
   ![Image](/static/images/assets/VivaHomeSetup/2.png)

3. Choose Connections
   ![Image](/static/images/assets/VivaHomeSetup/3.png)

4. Press Create and Manage Viva Connection Experiences, you can have more than one but you will need a premium license for multiple homesites.
   ![Image](/static/images/assets/VivaHomeSetup/4.png)

5. Press Create New
   ![Image](/static/images/assets/VivaHomeSetup/5.png)

6. Choose Create a Connection Experience, this will create one without a sharepoint site.
   ![Image](/static/images/assets/VivaHomeSetup/6.png)

7. Name it and give it a description
   ![Image](/static/images/assets/VivaHomeSetup/7.png)

8. Press Create
   ![Image](/static/images/assets/VivaHomeSetup/8.png)

9. It should show up, if you have a another Connection experience you can select the order.
   ![Image](/static/images/assets/VivaHomeSetup/9.png)

10. Now visit you connection app and you should have it .

![Image](/static/images/assets/VivaHomeSetup/10.png)
