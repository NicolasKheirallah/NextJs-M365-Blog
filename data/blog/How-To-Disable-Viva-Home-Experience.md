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
