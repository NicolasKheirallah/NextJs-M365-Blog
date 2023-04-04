---
date: '2023-04-01T16:11:31'
title: How to Delete Empty Folders After Applying Retention Policy in SharePoint
description: A guide on how to Delete Empty Folders After Applying Retention Policy in SharePoint
tags: ['SharePoint', 'Microsoft Purview']
summary: A guide on how to Delete Empty Folders After Applying Retention Policy in SharePoint
authors: ['default']
---

If you are using retention policies in SharePoint to manage the lifecycle of your documents, you may have noticed that empty folders are not deleted automatically when the files inside them are removed by the policy. This can create clutter and confusion for your users, who may see empty folders that no longer serve any purpose. In this blog post, we will explain why this happens and how you can solve this problem by using a Power Automate flow.

## Why are empty folders not deleted by retention policies?

Retention policies in SharePoint work at the file level, not at the folder level. This means that when you apply a retention policy to a document library or a folder, only the files within that scope will be affected by the retention settings. The folders themselves are not considered as content by the retention policy, and therefore they are not deleted when their contents are removed.

![Image](/static/images/assets/RetentionPolicyFolders/Screenshot_1.png)

## So How can you delete empty folders after applying retention policy?

One way to delete empty folders after applying retention policy is to use a Power Automate flow that runs after the retention period has been furfilled and checks for empty folders in your document libraries. The flow can then delete those folders.

To create such a flow, you will need to use the SharePoint connector and the Recurrence trigger in Power Automate. The basic steps are:

- Create a new flow and add a Automatic trigger trigger. This will be triggered from when the retention policy has hit it's end.
  ![Image](/static/images/assets/RetentionPolicyFolders/Screenshot_2.png)

- Add a Get files (properties only) action from the SharePoint connector. Specify the site address and library name from the trigger, here you should get the URLs.

- Add a Condition action to check if there are any files inside each folder. You can use length(body('Get*files*(properties_only)\_2')?['value']) as the expression for the condition, and compare it with 0.
- If the condition is true (the folder is empty), add a Delete file action from the SharePoint connector. Specify the same site address as before, and use File identifier from the first Get files action as the file identifier. This will delete the empty folder.
- If the condition is false (the folder is not empty) do nothing.

You can customize this flow according to your requirements and preferences.
