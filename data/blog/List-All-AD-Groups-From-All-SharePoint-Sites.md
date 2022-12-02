---
date: '2021-02-01T08:10:31'
title: List all AD Groups that are invited into SharePoint
description: A Script to list all groups invited into SharePoint
tags: ['SharePoint', 'AD', 'Powershell']
summary: A Script to list all groups invited into SharePoint
authors: ['default']
---

So I was helping a friend of mind that had an issue with not knowing which AD groups are invited into SharePoint, as these groups are seen as persons when invited directly into SharePoint own permissions groups. So I helped them out with creating a script that checks all the sites if they contain any AD group.

Requirements:
Powershell 7
Graph Module: https://learn.microsoft.com/en-us/powershell/microsoftgraph/installation?view=graph-powershell-1.0
PnP Module: https://pnp.github.io/powershell/articles/installation.html

Code for Downloading Image Column in List:

```
Import-Module Microsoft.Graph.Groups
Connect-Graph -Scopes "Group.Read.All", "Directory.Read.All"
$getAllADGroups = Get-MgGroup
Export-Csv '.\getAllSitesWithADGroup.csv'
Connect-PnPOnline -Url "https://-admin.sharepoint.com/" -Interactive

#Get All Site collections data and export to CSV
$getAllSites = Get-PnPTenantSite
$Addr = @()
foreach ($site in $getAllSites.Url) {

    #Connect to PnP Online
    Connect-PnPOnline -Url $site -Interactive
    #sharepoint online pnp powershell get group members
    $getAllMembers = Get-PnPGroup | Get-PnPGroupMember

    $getAllADGroups.Id | ForEach-Object {
        if ($getAllMembers.LoginName -match $_) {
            $newrow = [PSCustomObject] @{
                "SiteURL"    = $site;
                "Group Title"    = $getAllMembers.Title;
                "AD GroupID" = $_;
            }
            $Addr += $newrow

            Write-Host "AD group found contains in $site ad group id [$_]"
        }
    }
    $Addr | Export-CSV '.\getAllSitesWithADGroup.csv' -Force

}
```
