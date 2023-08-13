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

10. Now select onedrive connector and choose: Get file content using path from Path.

Here you need to choose choose the Path for your form, it should be under:

/Apps/Microsoft Forms/

Here you select previous uploaded file.
Now remove file name and add name from Json instead

This will get the path of the attachment and the file name

Now select SharePoint Connector and choose add attachment, select the new SharePoint List item you have created:

The flow should look something like this

![Image](/static/images/assets/attachFilesFromForm/5.png)

And that should do it:

![Image](/static/images/assets/attachFilesFromForm/8.png)
