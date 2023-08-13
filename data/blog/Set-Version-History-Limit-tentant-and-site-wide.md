---
date: '2023-08-02T07:20:22.217Z'
title: Set versioning limits at site and tenant
description: Set and manage your version history limit
tags: ['M365', SharePoint, 'Guide']
summary: Set and manage your version history limit
authors: ['default']
---

Hi!

If you're like me, you know how frustrating it can be to run out of storage space in SharePoint. It can happen quickly, especially if you're a small business with a limited number of licenses. One of the main culprits of this problem is version handling in SharePoint.

Basically, this means that every time you edit a file, a new version is created and the old one is kept. So, if you have a 1 GB PowerPoint presentation and you make 10 changes to it, you end up with 10 GB of data. And that's just for one file! The default limit in SharePoint is 500 versions per file, and until recently, the lowest you could set it was 100. That means you could still end up with 100 GB of data for a single file...

So here we're going to solve this , I'm going to show you how to lower the minimum number of versions Tentant-wide but also Site-wide to something more reasonable, and how to apply this setting across your whole tenant for all new libraries. Let's get started!

NOTE! This is still in Private Preview so it's not available for all!

## Requirements :

- Powershell 7
- SharePoint admin
- SPO Module: https://www.powershellgallery.com/packages/Microsoft.Online.SharePoint.PowerShell
  Or
- PnP Module: https://pnp.github.io/powershell/articles/installation.html

# Script

SPO:

```powershell
#Connects to Tentant
Connect-SPOService -Url "https://tenant-admin.sharepoint.com"

#This example sets Manual Version Storage Limits on all new document libraries at Tenant Level by limiting the number of major versions and the time (in days) versions are kept. Set EnableAutoExpirationVersionTrim as true for this.
Set-SPOTenant -EnableAutoExpirationVersionTrim $false -MajorVersionLimit 100 -ExpireVersionsAfterDays 30

```

PNP:

```powershell
# Connect to SharePoint Online using PNP
Connect-PnPOnline -Url "https://tenant-admin.sharepoint.com"
#This example sets Manual Version Storage Limits on all new document libraries at Tenant Level by limiting the number of major versions and the time (in days) versions are kept. Set EnableAutoExpirationVersionTrim as true for this.

Set-PnPTenant -EnableAutoExpirationVersionTrim $false -MajorVersionLimit 100 -ExpireVersionsAfterDays 30

```

Old lists Libraries need to be set to the default value

Site Level:

````powershell
# Connect to SharePoint Online
Connect-SPOService -Url "https://tenant-admin.sharepoint.com"

# Get all site collections
$siteCollections = Get-SPOSite

# Iterate through all your site collection
foreach ($site in $siteCollections) {
    # Get the root web of the site collection
    $siteWeb = Get-SPOWeb -Identity $site.Url

    # Set the versionhistory limit for all lists and libraries
    $siteWeb.Lists | ForEach-Object {
        $_.EnableVersioning = $true #Enabled Version History
        $_.MajorVersionLimit = 100  # 100 is the default limit in SharePoint, Replace 100 with your desired version limit if you want bigger or smaller
        $_.Update()
        Write-Host "Version history for site has been set:" $site.Url
    }

    ```
````
