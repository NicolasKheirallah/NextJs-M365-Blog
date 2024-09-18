---
date: '2024-09-18T13:14:22.412Z'
title: Free Storage In SharePoint Online Using Intelligent-Versioning.
description: A guide on Free Stroage In SharePoint Online Using Intelligent-Versioning
tags: ['SharePoint', 'SharePoint Premium']
summary: a guide on how to attach items to SharePoint list items from Forms
authors: ['default']
---

# Introduction

### Freeing Storage in SharePoint Online Using Intelligent Versioning and PowerShell Automation

As organizations increasingly adopt SharePoint Online for collaboration and document management, storage can become a significant challenge. SharePoint Online's versioning feature, while powerful, can contribute to storage bloat as multiple versions of documents accumulate over time. Fortunately, you can manage and clean up these old versions intelligently to free up valuable storage space, ensuring optimal performance without losing critical data.

In this post, we will discuss how to intelligently manage file versioning in SharePoint Online and automate the cleanup of versions older than 365 days using PowerShell. By the end, you'll have a clear strategy for maintaining healthy storage and managing SharePoint's powerful versioning features effectively.

#### **Understanding SharePoint Online Versioning**

Versioning in SharePoint Online allows users to keep multiple copies (or versions) of documents as they are revised. This feature is essential for tracking changes, reverting to previous versions, and maintaining collaboration. However, over time, these versions can pile up, especially for frequently modified documents.

By default, SharePoint Online retains all versions of a document. If not managed properly, version history can consume a significant amount of storage space, leading to increased costs and slower performance. This is where **Intelligent Versioning** comes in.

#### **What is Intelligent Versioning?**

**Intelligent Versioning** refers to a strategy where you let SharePOINT maintain a balance between keeping valuable document history and freeing up unnecessary storage. The idea is to retain the most recent versions of a document but delete older versions that are no longer relevant. This approach helps in optimizing your SharePoint storage without sacrificing critical data.

#### Key Aspects of Intelligent Versioning:

Automatic Version Thinning: Microsoft provides an "Automatic" mode where an algorithm gradually trims older versions as they age while keeping key timestamps. This helps users retain access to a wide range of versions without wasting storage. For example:

All versions are kept for the first 30 days.
From 30-180 days, hourly or daily versions are stored.
After 180 days, weekly versions are stored indefinitely.
This automatic thinning results in a dramatic reduction in storage usage—up to 96% in certain cases—without impacting the user experience of retrieving critical file versions.

#### **Benefits of Intelligent Versioning:**

1. **Optimize Storage Costs**: With intelligent versioning, you can delete outdated versions and reduce storage consumption, helping you stay within storage limits and potentially lowering costs.
2. **Improve Performance**: Fewer document versions mean faster search and retrieval times.
3. **Maintain Data Integrity**: By setting intelligent versioning policies, you ensure that you only delete unnecessary versions while keeping the relevant ones intact.

---

Enable Intelligent Verisoning

```powershell
# Connect to SharePoint Online
# Requires you to be connected to SharePoint Online as an administrator
$adminSiteUrl = "https://tenant-admin.sharepoint.com"
Connect-SPOService -Url $adminSiteUrl
# Enable Intelligent versioning
Set-SPOTenant -EnableVersionExpirationSetting $true

```

This will enable verisoning for all new files!
You can double check that it's enabled in Admin center!

![Image](/static/images/assets/EnableAndCleanStorage/1.png)

### **Automating Version Cleanup Using PowerShell**

For older files, intelligent versioning doesn't apply until the files are modified. Managing file versions manually across multiple sites can be a time-consuming task. Fortunately, PowerShell automation can streamline this process. Using the `New-SPOSiteFileVersionBatchDeleteJob` cmdlet, you can automate the removal of document versions older than a specified date by scheduling batch deletion jobs, making version management more efficient.

Here's how you can set up a PowerShell script to automatically clean up document versions older than X days.

#### **Pre-requisites**:

- SharePoint Online Administrator permissions.
- [SharePoint Online Management Shell](https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-online/connect-sharepoint-online?view=sharepoint-ps) installed on your local machine.

---

### **PowerShell Script: Automating Version Cleanup in SharePoint Online**

The following script retrieves all site collections in your SharePoint Online tenant and creates a batch delete job for file versions older than 365 days:

```powershell
# Connect to SharePoint Online
# Requires you to be connected to SharePoint Online as an administrator
$adminSiteUrl = "https://tenant-admin.sharepoint.com"
Connect-SPOService -Url $adminSiteUrl

# Get all site collections
$siteCollections = Get-SPOSite -Limit All

# Loop through each site collection
foreach ($site in $siteCollections) {
    Write-Host "Processing site: $($site.Url)"

    # Create a date variable for 365 days ago
    $olderThanDate = (Get-Date).AddDays(-365)

    # Create a batch delete job for versions older than 365 days
    try {
        New-SPOSiteFileVersionBatchDeleteJob -Identity $site.Url -DeleteBeforeDays $olderThanDate

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

### **How This Script Works:**

1. **Connect to SharePoint Online**: The script first connects to your SharePoint Online tenant using the SharePoint Online Admin Center URL.
2. **Retrieve All Site Collections**: Using the `Get-SPOSite` cmdlet, the script fetches all site collections in the tenant.
3. **Set Retention Date**: For each site collection, it calculates the retention date as 365 days before the current date.
4. **Create Batch Delete Job**: The `New-SPOSiteFileVersionBatchDeleteJob` cmdlet is used to create a batch job that deletes all file versions older than the specified date (365 days ago in this case).
5. **Error Handling**: If an error occurs while creating the delete job, it is logged, ensuring the script continues processing other site collections.

---

### **Best Practices for Intelligent Versioning and Cleanup**

1. **Define a Versioning Policy**: Decide how many versions of a document you need to retain. You can set this in the document library settings in SharePoint Online and using the script, -MajorVersionLimit X -MajorWithMinorVersionsLimit X
2. **Automate Version Cleanup**: Let SharePoint Decide when to automate the deletion of old versions regularly.
3. **Monitor Storage Usage**: Keep an eye on your SharePoint Online storage usage. You can view storage reports from the SharePoint Admin Center to see where storage is being consumed.
4. **Combine with Retention Policies**: If certain files or versions need to be kept for legal or compliance reasons, make sure they’re protected with retention labels or policies in Microsoft Purview.

---

### **Conclusion**

Managing SharePoint Online storage efficiently is crucial, especially as your organization grows. Intelligent versioning allows you to maintain the benefits of version control while keeping storage costs in check. With the help of PowerShell automation, you can streamline the cleanup process, ensuring that only necessary document versions are retained.

By implementing a combination of automated cleanup scripts and smart versioning policies, you can optimize your SharePoint storage and maintain a clutter-free, high-performing environment for your users.
