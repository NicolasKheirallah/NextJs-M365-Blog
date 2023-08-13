---
date: '2023-06-01T13:14:22.412Z'
title: Attach Images from Microsoft Forms into a SharePoint List item.
description: a guide on how to attach items to SharePoint list items from Forms
tags: ['SharePoint', 'Power Automate', 'Forms']
summary: a guide on how to attach items to SharePoint list items from Forms
authors: ['default']
---

# Introduction

So a friend asked me the other day how she could build a simple contact-form where she could upload image attachment and then save it all to a SharePoint list. So I thought I might as well create a blogpost about it! :)

## Lets get started:

1. First visit forms:
   https://forms.office.com/Pages/DesignPageV2.aspx?prevsubpage=design

2. Press new form and create your form:

3. Add an upload file:

![Image](/static/images/assets/attachFilesFromForm/1.png)

4. Press Collect Responses and Copy the link

![Image](/static/images/assets/attachFilesFromForm/2.png)

5. Visit power Automate and choose Automated Cloud flow, we want this because we want to trigger each time a new form is submitted

6. Choose these:

![Image](/static/images/assets/attachFilesFromForm/4.png)

7. Now save and do a test run! Submit an response.  
   This is because we want get the Json from the compose as well as the path for the file

![Image](/static/images/assets/attachFilesFromForm/5.5.png)

8. Now check previous run and copy the JSON from the previous run.

![Image](/static/images/assets/attachFilesFromForm/6.png)

9. Edit the flow and add Parse Json select Outputs as source and press generate from Sample and paste in the json from previous run that you just copied:

![Image](/static/images/assets/attachFilesFromForm/19.png)

10. Now go into your onedrive copy the path

Here you need to choose choose the Path for your form, it should be under:

/Documents/Apps/Microsoft%20Forms

11. Now select SharePoint Connector and choose Send an HTTP Request to SharePoint, select the Sharepoint site:

```
| Name         | Value                                                              |
| ------------ | ------------------------------------------------------------------ |
| Site Address | https://yourTenant.sharepoint.com/sites/yourSite                   |
| Method       | POST                                                               |
| Uri          | _api/web/lists/getbytitle('My Personal information')/items|
| Headers      | Accept: application/json; odata=nometadata                         |
| Headers      | content-type: application/json; odata=nometadata                   |
| Body         |                                                                    |
```

```json
{
  "__metadata": {
    "type": "SP.Data.LogoUniverseListItem"
  },
  "Title": "Power Automate",
  "ProfileImage": "{\"type\":\"thumbnail\",\"fileName\":\"@{items('Apply_to_each')['name']}\",\"fieldName\":\"ImageColumnName\",\"serverUrl\":\"https://avarante-my.sharepoint.com\",\"serverRelativeUrl\":\"/personal/admin_avarante_onmicrosoft_com/Documents/Apps/Microsoft%20Forms/Personal%20Information%20Form/Question/@{items('Apply_to_each')['name']}\"}"
}
```

The flow should look something like this

![Image](/static/images/assets/attachFilesFromForm/9.png)

And that should do it:

![Image](/static/images/assets/attachFilesFromForm/8.png)
