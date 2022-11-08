---
date: '2022-04-05T16:11:31'
title: How to Set permissions for a SharePoint list
description: A guide on how to set permissions for a SharePoint list
tags: ['SharePoint', 'Lists', 'Power Automate']
summary: A guide on how to Set permissions for a SharePoint list
authors: ['default']
---

I got question the other day on how to remove permissions on a SharePoint List item using Power Automate so here is a quick guide:

1. Create an Automated Flow

2. When an item is created:

![Image](/static/images/assets/BreakInheritence/1.png)

3. Send Http Request to SharePoint (Break List Item Inheritance)

```
| Name        | Value                                                                                                                           |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------- |
| *Site Address |https://YOURURL.sharepoint.com/sites/yourSite                                                                                                                 |
| *Method   | POST                                                                                                                     |
| *Uri | _api/web/lists/getByTitle(ListUrl)/items/getById(FileID)/breakroleinheritance(copyRoleAssignments=false,clearSubscopes=true) |
```

![Image](/static/images/assets/BreakInheritence/2.png)

4. Get User Profile(V2):

The user that not allowed to see this UPN/Mail
![Image](/static/images/assets/BreakInheritence/3.png)

5. Send Http Request to SharePoint (Remove User from List item)

```
| Name        | Value                                                                                                                           |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------- |
| *Site Address |https://YOURURL.sharepoint.com/sites/yourSite                                                                                                                 |
| *Method   | POST                                                                                                                     |
| *Uri | _api/web/lists/getbytitle(ListUrl)/items(FileID)/roleassignments/removeroleassignment(principalid='userID',roleDefId=1073741827) |
```

![Image](/static/images/assets/BreakInheritence/4.png)

5. Visit the list item and you can see the inheritence being broken

![Image](/static/images/assets/BreakInheritence/5.png)

Whole Flow:

![Image](/static/images/assets/BreakInheritence/6.png)
