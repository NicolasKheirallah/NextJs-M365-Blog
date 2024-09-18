Here’s the improved version of your post, incorporating the suggestions:

---

**date**: '2024-09-18T13:14:22.412Z'  
**title**: How to Free Up Storage in SharePoint Online Using Intelligent Versioning and PowerShell  
**description**: A guide on freeing up storage in SharePoint Online using Intelligent Versioning and automated PowerShell cleanup.  
**tags**: ['SharePoint', 'SharePoint Premium']  
**summary**: A guide on how to use Intelligent Versioning in SharePoint Online and automate the cleanup of old document versions using PowerShell.  
**authors**: ['default']

---

# Introduction

## Freeing Storage in SharePoint Online Using Intelligent Versioning and PowerShell Automation

As organizations increasingly adopt SharePoint Online for collaboration and document management, managing storage efficiently becomes a critical challenge. One significant contributor to storage consumption is SharePoint's **versioning feature**, which creates multiple versions of documents, leading to storage bloat over time.

In this post, we’ll discuss how to **intelligently manage file versioning** in SharePoint Online and automate the cleanup of old versions using **PowerShell**. By the end, you’ll have a clear strategy for maintaining healthy storage and managing SharePoint's powerful versioning features effectively.

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

Once enabled, this will apply Intelligent Versioning to all **new** files in SharePoint document libraries. You can verify this setting in the **Admin Center** under **Versioning Settings**.

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

---

## **How This Script Works**

1. **Connect to SharePoint Online**: The script first connects to your SharePoint Online tenant using the Admin Center URL.
2. **Retrieve All Site Collections**: It retrieves all site collections using the `Get-SPOSite` cmdlet.
3. **Set Retention Date**: The script calculates the retention date as 365 days before the current date.
4. **Create Batch Delete Job**: The `New-SPOSiteFileVersionBatchDeleteJob` cmdlet creates a batch job to delete versions older than the retention date.
5. **Error Handling**: If an error occurs, it logs the error and continues to the next site collection.

---

## **Best Practices for Intelligent Versioning and Cleanup**

1. **Define a Versioning Policy**: Decide how many versions you want to retain for different types of documents. This can be configured in library settings or using PowerShell (e.g., `-MajorVersionLimit X`).
2. **Automate Version Cleanup**: Use automation to regularly clean up old versions, minimizing the need for manual intervention.
3. **Monitor Storage Usage**: Regularly review storage reports from the SharePoint Admin Center to identify areas where storage is being consumed excessively.
4. **Combine with Retention Policies**: Protect critical files by applying **Retention Labels** or **Retention Policies** to ensure they are not deleted prematurely, especially for legal or compliance reasons.

---

## **Conclusion**

As your organization grows, efficiently managing SharePoint Online storage is crucial. **Intelligent Versioning** helps you retain the benefits of version control while optimizing storage and keeping costs under control. By using PowerShell to automate version cleanup, you can streamline the process, ensuring that unnecessary versions are deleted without impacting important data.

By combining automated scripts with best practices, you can maintain a high-performing SharePoint environment that meets your organization’s storage needs.
