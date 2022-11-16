---
date: '2022-10-16T20:54:01.975Z'
title: Open documents in desktop mode by default in SharePoint and Teams
description: A small guide on how to open files in desktop mode by default
tags: ['Teams', 'SharePoint']
summary: A small guide on how to open files in desktop mode by default
authors: ['default']
---

Sometimes you want to open in desktop instead of Web version of Word,Powerpoint, Excel etc and here's how you do it

## Single site

```
# Site Collection URL
$siteUrl = "https://<tenant>.sharepoint.com/<siteurl>"

# SharePoint Feature ID: Open in Client
$featureId = "8a4b8de2-6fd8-41e9-923c-c7c3c00f8295"

Connect-PnPOnline -Url $siteUrl -Interactive

# Get Feature from SharePoint site
$activateFeature = Get-PnPFeature -Scope "Web" -Identity $featureId

# Check if feature found or not
if($enableFeature.DefinitionId -eq $null) {
    Write-host "Activating Feature ($featureId)..."
    Enable-PnPFeature -Scope Site -Identity $FeatureId
    Write-host -f Green "Feature ($featureId) has been activated Successfully!"
}
else {
    Write-host "Feature ($featureId) is already enabled on this site!"
}

```

## All Sites

```

$Connection =  Connect-PnPOnline -Url "https://yourtenant-admin.sharepoint.com/" -Interactive

#Get All Site collections - Exclude Non-user sites
$SiteCollections = Get-PnPTenantSite | Where -Property Template -NotIn ("SRCHCEN#0", "REDIRECTSITE#0", "SPSMSITEHOST#0", "APPCATALOG#0", "POINTPUBLISHINGHUB#0", "EDISC#0", "STS#-1")

#Loop through each site collection
ForEach($Site in $SiteCollections)
{
    # SharePoint Feature ID: Open in Client
    $featureId = "8a4b8de2-6fd8-41e9-923c-c7c3c00f8295"

    Connect-PnPOnline -Url  $Site.URL -Interactive
    Write-host  Connected to site $Site.URL
    # Get Feature from SharePoint site
    $activateFeature = Get-PnPFeature -Scope "Web" -Identity $featureId
    # Check if feature found or not

    if($enableFeature.DefinitionId -eq $null) {
    Write-host "Activating Feature ($featureId)..."

    Enable-PnPFeature -Scope Site -Identity $FeatureId
    Write-host -f Green "Feature ($featureId) has been activated Successfully!"
}
else {
    Write-host "Feature $featureId is already enabled on this site!"
 }
}
```

## Teams

This is user specific,

1. Press the three dots and then settings:

   ![Image](/static/images/assets/OpenInDesktopDefault/1.png)

2. Go down to files:

   ![Image](/static/images/assets/OpenInDesktopDefault/3.png)

3. Choose Desktop App:

   ![Image](/static/images/assets/OpenInDesktopDefault/2.png)
