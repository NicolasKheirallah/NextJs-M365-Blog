---
date: '2022-12-12T16:11:31'
title: How to open a Office document from link in desktop app
description: How to open a Office document from link in desktop app
tags: ['SharePoint', 'Office 365', 'Power Automate']
summary: A guide on how to open a Office document from link in desktop app
authors: ['default']
---

A quick blog post on a issue I helped a friend with today!

So a common issue is that you have links in Word/PowerPoint that you want to open in the desktop app and not in the web-app, and it's not always they will do that. Especially if it's document that are outside of SharePoint, so here is a tip on how to force an app to open in desktop.

So depending on your file type you need to add a prefix, this would be based on the application

```
| Application   | Value|
|:----: |:----: |
| MS Word| ms-word|
| MS PowerPoint | ms-powerpoint|
| MS Excel| ms-excel|
| MS Visio| ms-visio|
| MS Access | ms-access|
| MS Project| ms-project|
| MS Publisher| ms-publisher|
| MS InfoPath| ms-infopath|
```

```
| Commands| Value|
| :----: | :----: |
| View Document| ofv|
| Edit Document | ofe|
| New Document| nft|
```

Structure:

Application:Command|link

Example Open Word Document:

ms-word:ofv|u|https://yourlin/YourDocument.docx

More info can be found here:

https://learn.microsoft.com/en-us/office/client-developer/office-uri-schemes
