---
date: '2021-01-11T07:20:18.207Z'
title: How to set Office template using SharePoint
description: Set and manage your organization default template
tags: ['M365', SharePoint, 'Guide']
summary: How to set Office template using SharePoint
authors: ['default']
---

Hi!

So I got asked by a client of mine that just went through a merger how they could add their organizational office templates to Word, so I decided to create a script that easily handles that so the just needs to upload their documents:

This script should be just plug and play, just fill in your information and run :)

```powershell
$adminUPN=""
$orgName=""
$userCredential = Get-Credential -UserName $adminUPN -Message "Type the password."
Connect-PnPOnline -Url "https://$orgName-admin.sharepoint.com" -Credential $userCredential
New-PnPSite -Type TeamSite -Title "Assets" -Owner $adminUPN -alias "Assets"
$siteUrl = Get-PnPTenantSite | ? Title -eq "Assets"
Connect-PnPOnline $siteUrl.url -Credentials
$CreateTemplateDoc = New-PnPList -Title "Templates" -Template DocumentLibrary -OnQuickLaunch
$GetTemplateDoc = Get-PnPList -Identity "Templates"
Add-PnPFolder -Name  "Organisation images" -Folder $GetTemplateDoc.Title
Add-PnPFolder -Name "Office Templates" -Folder $GetTemplateDoc.Title
Set-PnPList -Identity $GetTemplateDoc.Title -BreakRoleInheritance
$everyoneExceptExternal = Get-PnPUser| ? Title -eq "Everyone except external users"
Set-PnPListPermission -Identity $GetTemplateDoc.Title -User $everyoneExceptExternal.LoginName -AddRole 'read'
$docUrl ="https://$orgName.sharepoint.com" +  $GetTemplateDoc.RootFolder.ServerRelativeUrl + "/officetemplates"
$imgUrl ="https://$orgName.sharepoint.com" +  $GetTemplateDoc.RootFolder.ServerRelativeUrl + "/Organisationimages"

#Because PnPorgnasationlibrary isn't as flexible...
Connect-SPOService "https://$orgName-admin.sharepoint.com" -Credential $userCredential
Set-SPOOrgAssetsLibrary -LibraryUrl  $docurl -CdnType Private -OrgAssetType OfficeTemplateLibrary
Set-SPOOrgAssetsLibrary -LibraryUrl  $imgUrl -CdnType Private -OrgAssetType ImageDocumentLibrary
```

So, a bit of explaining about the PS code:

I'm using a mix of PnP and SPO as some feature available for one but not the other. As we are just running this script once that shouldn't be a problem :)

So what are we doing?

```powershell
New-PnPSite -Type TeamSite -Title "Assets" -Owner $adminUPN -alias "Assets"
```

We are creating a new site called assets as this site will use used for all company assets, both office templates to photos etc. Reason for this is that it's better to have everything centralized as it becomes easier to manage for both the end user and the admin.

Here we are getting the site URL so we can use it to connect to it

```powershell
$siteUrl = Get-PnPTenantSite | ? Title -eq "Assets"
```

As we need some place to store our templates, I'm creating a document library called Template, this is optional. You can use "Document" if you want :)

I also create folders for the different kind of assets, as we both want to store Office template as well as organizational images.

After creating this I'm breaking the inheritance to the site and adding "**Everyone except external users**"

Why? because usually you just want communication to have access to this site, but we still need everyone else accessing the files. :)

```powershell
$CreateTemplateDoc = New-PnPList -Title "Templates" -Template DocumentLibrary -OnQuickLaunch
$GetTemplateDoc = Get-PnPList -Identity "Templates"
Add-PnPFolder -Name  "Organisation images" -Folder $GetTemplateDoc.Title
Add-PnPFolder -Name "Office Templates" -Folder $GetTemplateDoc.Title
Set-PnPList -Identity $GetTemplateDoc.Title -BreakRoleInheritance
$everyoneExceptExternal = Get-PnPUser| ? Title -eq "Everyone except external users"
Set-PnPListPermission -Identity $GetTemplateDoc.Title -User $everyoneExceptExternal.LoginName -AddRole 'read'
```

![Assets lib](/static/images/assets/assets.png)

So what now?

We connect using Connect-SPOService as PnP doesn't support setting different OrgAssetType and we set the one for the images and one for the office templates.

```powershell
#Because PnPorgnasationlibrary isn't as flexible...
Connect-SPOService "https://$orgName-admin.sharepoint.com" -Credential $userCredential
Set-SPOOrgAssetsLibrary -LibraryUrl  $docurl -CdnType Private -OrgAssetType OfficeTemplateLibrary
Set-SPOOrgAssetsLibrary -LibraryUrl  $imgUrl -CdnType Private -OrgAssetType ImageDocumentLibrary
```

And we are done :D

Source:
https://docs.microsoft.com/en-us/sharepoint/organization-assets-library
