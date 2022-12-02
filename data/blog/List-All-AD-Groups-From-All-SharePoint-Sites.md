---
date: '2021-02-01T08:10:31'
title: List all AD Groups that are invited into SharePoint
description: A Script to list all groups invited into SharePoint
tags: ['SharePoint', 'AD', 'Powershell']
summary: A Script to list all groups invited into SharePoint
authors: ['default']
---

So I was helping a friend of mine that had an issue she was faceing. The issue was that the company she was working for had alot of AD groups 1000+ Which needed to be replaced, these AD groups were invited as members in some SharePoint sites 1000+. The issue is when invited a AD group as a member of a SharePoint Site the group is added as a person and we can not distingush between a group and a person. So to solve this issue I create this script which will iterate through all Sites and check if any members of the site has the same GUID as the AD group. if so add it to a CSV.

## Requirements :

- Powershell 7

- Graph Module: https://learn.microsoft.com/en-us/powershell/microsoftgraph/installation?view=graph-powershell-1.0

- PnP Module: https://pnp.github.io/powershell/articles/installation.html

## Code for Downloading Image Column in List:

```
Import-Module Microsoft.Graph.Groups
Connect-Graph -Scopes "Group.Read.All", "Directory.Read.All"
$getAllADGroups = Get-MgGroup
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
