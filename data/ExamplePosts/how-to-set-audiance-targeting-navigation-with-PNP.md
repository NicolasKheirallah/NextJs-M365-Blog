---
date: '2020-06-13T10:02:01.975Z'
title: Settings Navigation Audiance with PNP
description: A new navigation items with audiance targeting using PNP
tags: ['Teams', 'SharePoint']
summary: A new navigation items with audiance targeting using PNP
authors: ['default']
---

```
$siteURL = Read - Host "Enter site url"
try {
    Connect - PnPOnline - Url $siteURL - Credentials(Get - Credential)
    #Get Hub Navigation and Its Sub Menu
    $topNavsMenu = Get - PnPNavigationNode - Location TopNavigationBar | Select Title, Url, Id
    foreach($topNav in $topNavsMenu) {
        Write - Host "Top Navigaion : "
        $topNav.Title
        $node = Get - PnPNavigationNode - Id $topNav.Id
        $childMenus = $node.Children | Select Title, Url, Id
        if ($childMenus - ne $null) {
            foreach($childMenus in $node.Children) {
                Write - Host "SubNavigation : "
                $childMenus.Title
                $subNodeMenus = Get - PnPNavigationNode - Id $childMenus.Id
                $subchilds = $subNodeMenus.Children | Select Title, Url, Id
                if ($subchilds - ne $null) {
                    foreach($childMenus in $subchilds) {
                        Write - Host $childMenus.Title
                    }
                }
            }
        }
    }
} catch {}

```
