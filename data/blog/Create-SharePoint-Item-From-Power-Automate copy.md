---
date: '2022-04-10T16:51:31'
title: Create File with Special Characthers in Power Automate
description: A guide on how to create File with Special Characthers in Power Automate
tags: ['SharePoint', 'Document Library', 'PowerAutomate']
summary: A guide on how to create File with Special Characthers in Power Automate
authors: ['default']
---

So a common problem with Creating new files in Power Automate is that you can't use Special Characters, which can be abit annoying! But there is an work around for this and this is to use Http Request connector for SharePoint!

This is how:

1. Create Your flow

2. Search for the Connector Send an HTTP request to SharePoint

3. Add these Values:

| Site Adress  | Your Site                                                                            |
| ------------ | ------------------------------------------------------------------------------------ |
| Method       | Post                                                                                 |
| URI          | \_api/web/lists/getByTitle('YourLibrary')/getitembyid(ItemID)/validateUpdateListItem |
| Header       |
| accept       | application/json; odata=verbose                                                      |
| content-type | application/json; odata=verbose                                                      |
| Body         |

```json
{
  "formValues": [
    {
      "__metadata": { "type": "SP.ListItemFormUpdateValue" },
      "FieldName": "FileLeafRef",
      "FieldValue": "@{outputs('FileName')}"
    }
  ],
  "bNewDocumentUpdate": true,
  "checkInComment": "Updated Filename" //This is optional
}
```

It should look something like this

![Image](/static/images/assets/CreateSpecialCharatechersFile/1.png)

This will allow you to create files with Special Characters
