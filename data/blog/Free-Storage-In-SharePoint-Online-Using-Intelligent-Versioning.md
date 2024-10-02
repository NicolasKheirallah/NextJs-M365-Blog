---
date: '2024-09-18T13:14:22.412Z'  
title: How to Free Up Storage in SharePoint Online Using Intelligent Versioning and PowerShell  
description: A guide on freeing up storage in SharePoint Online using Intelligent Versioning and automated PowerShell cleanup.  
tags: ['SharePoint', 'SharePoint Premium']  
summary: A guide on how to use Intelligent Versioning in SharePoint Online and automate the cleanup of old document versions using PowerShell.  
authors: ['default']
---

# Introduction

## Freeing Storage in SharePoint Online Using Intelligent Versioning and PowerShell Automation

This is becoming more and more of an issue and is something I've gotten question about alot! As organizations increasingly adopt SharePoint Online for collaboration and document management, managing storage efficiently becomes a critical challenge. One significant contributor to storage consumption is SharePoint's **versioning feature**, which creates multiple versions of documents, leading to storage bloat over time.

So In this post, we’ll discuss how to **intelligently manage file versioning** in SharePoint Online and automate the cleanup of old versions using **PowerShell**. By the end, you’ll have a clear strategy for maintaining healthy storage and managing SharePoint's powerful versioning features effectively.

---

## **Understanding SharePoint Online Versioning**

**Versioning** in SharePoint Online allows users to save multiple copies of documents as they get revised. This is essential for tracking changes, restoring earlier versions, and enabling collaboration. However, if not managed properly, the version history of documents can accumulate rapidly, consuming valuable storage space.

By default, SharePoint retains **all versions** of a document. Over time, this can lead to excessive storage usage, increased costs, and slower performance. This is where **Intelligent Versioning** becomes a useful strategy.

---

## **What is Intelligent Versioning?**

**Intelligent Versioning** refers to a smart strategy that helps balance retaining valuable document history while **freeing up unnecessary storage**. Rather than keeping all document versions indefinitely, Intelligent Versioning helps ensure that only recent and important versions are retained, while older versions are deleted to conserve space.

This approach helps you optimize your SharePoint storage while preserving important data.

### **How Intelligent Versioning Works**

Intelligent Versioning introduces a feature called **automatic version thinning**, which gradually trims older document versions while preserving key timestamps. Here’s how it works:

- **First 30 Days**: All versions are kept.
- **From 30 to 180 Days**: Hourly or daily versions are stored.
- **Beyond 180 Days**: Weekly versions are kept indefinitely.

By using this automatic thinning approach, Microsoft reports that you can reduce version storage usage by up to **96%** in some cases, without compromising users’ ability to access important historical versions.

My personal experience, I've seen storage saved 30-60% from various clients! 

---

## **Benefits of Intelligent Versioning**

1. **Optimize Storage Costs**: By deleting outdated versions, you reduce storage consumption, keeping within limits and potentially lowering costs.
2. **Improve Performance**: With fewer document versions stored, searches and retrieval times are faster.
3. **Maintain Data Integrity**: Intelligent Versioning ensures you delete only unnecessary versions while keeping critical ones intact.

---

## **How to Enable Intelligent Versioning**

To enable Intelligent Versioning across your SharePoint Online tenant, use the following PowerShell command:

```powershell
# Connect to SharePoint Online
$adminSiteUrl = "https://<tenant>-admin.sharepoint.com"
Connect-SPOService -Url $adminSiteUrl

# Enable Intelligent versioning
Set-SPOTenant -EnableVersionExpirationSetting $true
```

PnP Powershell:
```powershell
# Install and Import PnP PowerShell module if not installed
# Install-Module -Name "PnP.PowerShell"

# Connect to SharePoint Online Admin Center
$adminSiteUrl = "https://<tenant>-admin.sharepoint.com"
Connect-PnPOnline -Url $adminSiteUrl -Interactive

# Enable Intelligent Versioning
Set-PnPTenant -EnableVersionExpirationSetting $true

```


Once enabled, this will apply Intelligent Versioning to all **new** files in SharePoint document libraries. You can verify this setting in the **Admin Center** under **Versioning Settings**.

   ![Image](/static/images/assets/EnableAndCleanStorage/1.png)

---

## **Automating Version Cleanup Using PowerShell**

While Intelligent Versioning applies to new documents, **older files** require manual intervention. Managing versions manually across multiple sites can be a tedious task. Fortunately, PowerShell allows you to automate the process.

Using the `New-SPOSiteFileVersionBatchDeleteJob` cmdlet, you can create batch deletion jobs to remove document versions older than a specified date.

### **Prerequisites**:

- SharePoint Online Administrator permissions.
- [SharePoint Online Management Shell](https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-online/connect-sharepoint-online?view=sharepoint-ps) installed.

---

### **PowerShell Script: Automating Version Cleanup**

Here’s a PowerShell script that retrieves all site collections in your SharePoint Online tenant and creates a batch delete job for document versions older than 365 days:

```powershell
# Connect to SharePoint Online
$adminSiteUrl = "https://<tenant>-admin.sharepoint.com"
Connect-SPOService -Url $adminSiteUrl

# Get all site collections
$siteCollections = Get-SPOSite -Limit All

# Loop through each site collection
foreach ($site in $siteCollections) {
    Write-Host "Processing site: $($site.Url)"

    # Create a batch delete job for versions older than 365 days
    try {
New-SPOSiteFileVersionBatchDeleteJob -Identity $site.Url -DeleteBeforeDays 365 -confirm:$false 
        Write-Host "Batch delete job created for site: $($site.Url)"
    }
    catch {
        Write-Host "Error creating batch delete job for site: $($site.Url)"
        Write-Host $_.Exception.Message
    }
}

# Disconnect from SharePoint Online
Disconnect-SPOService
```

More advanced version with options:
```powershell
# Check if SharePoint Online Management Shell is installed 
$module = Get-Module -ListAvailable -Name "Microsoft.Online.SharePoint.PowerShell"

if (-not $module) {
    Write-Host "Downloading and installing the SharePoint Online Management Shell module..."
    Install-Module -Name "Microsoft.Online.SharePoint.PowerShell" -Force -AllowClobber
}

# Import the SharePoint Online Management Shell module
Import-Module "Microsoft.Online.SharePoint.PowerShell" -UseWindowsPowerShell

# Function to make input case-insensitive
function Get-InsensitiveInput($prompt) {
    return (Read-Host $prompt).ToLower()
}

# Prompt for Intelligent Versioning enablement
$intelligentVersionEnable = Get-InsensitiveInput "Do you want to enable Intelligent Versioning? (y/n)"

if ($intelligentVersionEnable -eq "y") {
    $tenantName = Read-Host "Enter your SharePoint tenant name (e.g., 'mytenant' for 'https://mytenant-admin.sharepoint.com')"
    $adminSiteUrl = "https://$tenantName-admin.sharepoint.com"
    Connect-SPOService -Url $adminSiteUrl

    # Enable Intelligent Versioning
    Set-SPOTenant -EnableVersionExpiration $true

    # Prompt for deletion mode
    $deletionMode = Get-InsensitiveInput "Do you want to run the Delete mode? (yes/no)"

    if ($deletionMode -eq "yes") {
        # Prompt for deletion type: days or versions
        $deletionModeType = Get-InsensitiveInput "Do you want to delete by 'days' or 'versions'? Enter your choice."

        # Check for valid input for deletion type
        if ($deletionModeType -ne "days" -and $deletionModeType -ne "versions") {
            Write-Host "Invalid option. Please run the script again and choose either 'days' or 'versions'."
            exit
        }

        # Prompt for additional input based on the deletion mode
        if ($deletionModeType -eq "days") {
            $deleteBeforeDays = Read-Host "Enter the number of days to keep file versions (e.g., 365 for one year)"
        }
        elseif ($deletionModeType -eq "versions") {
            $versionsToKeep = Read-Host "Enter the number of versions to keep (e.g., 5 for the last 5 versions)"
        }
    }

    # Get all site collections
    $siteCollections = Get-SPOSite -Limit All

    # Loop through each site collection
    foreach ($site in $siteCollections) {
        Write-Host "Processing site: $($site.Url)"

        try {
            # Enable AutoExpirationVersionTrim for each site
            Set-SPOSite -Identity $site.Url -EnableAutoExpirationVersionTrim $true -Confirm:$false

            # Perform batch delete operation if deletion mode is 'yes'
            if ($deletionMode -eq "yes") {
                # Create batch delete job based on the deletion mode type
                if ($deletionModeType -eq "days") {
                    New-SPOSiteFileVersionBatchDeleteJob -Identity $site.Url -DeleteBeforeDays $deleteBeforeDays -Confirm:$false
                    Write-Host "Batch delete job created for site: $($site.Url) for file versions older than $deleteBeforeDays days."
                }
                elseif ($deletionModeType -eq "versions") {
                    New-SPOSiteFileVersionBatchDeleteJob -Identity $site.Url -MajorVersionLimit $versionsToKeep -Confirm:$false
                    Write-Host "Batch delete job created for site: $($site.Url), keeping only the last $versionsToKeep versions."
                }
            }
            else {
                Write-Host "Deletion mode not enabled for site: $($site.Url)."
            }
        }
        catch {
            Write-Host "Error processing site: $($site.Url)"
            Write-Host $_.Exception.Message
        }
    }

    # Disconnect from SharePoint Online
    Disconnect-SPOService
}
elseif ($intelligentVersionEnable -eq "n") {
    Write-Host "Intelligent Versioning not enabled. Exiting script."
    exit
}
else {
    Write-Host "Invalid input. Please run the script again and enter 'y' or 'n'."
    exit
}


```

---

## **How This Script Works**

1. **Connect to SharePoint Online**: The script first connects to your SharePoint Online tenant using the Admin Center URL.
2. **Retrieve All Site Collections**: It retrieves all site collections using the `Get-SPOSite` cmdlet.
3. **Set Retention Date**: The script calculates the retention date as 365 days before the current date.
4. **Create Batch Delete Job**: The `New-SPOSiteFileVersionBatchDeleteJob` cmdlet creates a batch job to delete versions older than the retention date.
5. **Error Handling**: If an error occurs, it logs the error and continues to the next site collection.

---

## **Best Practices for Intelligent Versioning and Cleanup**

1. **Define a Versioning Policy**: Decide how many versions you want to retain for different types of documents. This can be configured in library settings or using PowerShell (e.g., `-MajorVersionLimit X`). My Recommendation is to set it to automatic!
2. **Automate Version Cleanup**: Use automation to regularly clean up old versions, minimizing the need for manual intervention.
3. **Monitor Storage Usage**: Regularly review storage reports from the SharePoint Admin Center to identify areas where storage is being consumed excessively. Make sure that the owners clean up old files and make use of Archive and backup function for data that isn't used daily!
4. **Combine with Retention Policies**: Protect critical files by applying **Retention Labels** or **Retention Policies** to ensure they are not deleted prematurely, especially for legal or compliance reasons.

---

## **Conclusion**

As your organization grows, efficiently managing SharePoint Online storage is crucial. **Intelligent Versioning** helps you retain the benefits of version control while optimizing storage and keeping costs under control. By using PowerShell to automate version cleanup, you can streamline the process, ensuring that unnecessary versions are deleted without impacting important data.

By combining automated scripts with best practices, you can maintain a high-performing SharePoint environment that meets your organization’s storage needs.
