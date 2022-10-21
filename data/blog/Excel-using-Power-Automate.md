---
date: '2022-10-21T21:51:21.726Z'
title: How to automatically extract list items and add them to an Excel using Power Automate
description: A guide on how to use power automate to fill an excel
tags: ['Power Automate', 'SharePoint', 'Lists']
summary: A guide on how to use power automate to fill an excel
authors: ['default']
---

1. A simple Power Automate job I did for a client who wanted all the list created wthin a month emailed to her as an Excel, So this is how I did it:
   First visit Power Automate:

   https://make.powerautomate.com/

2. Press Create

3. Choose Scheduled cloud flow
   ![Image](/static/images/assets/ExcelusingPowerAutomate/0.png)

4. Choose when the script will run, I choose once a month.

![Image](/static/images/assets/ExcelusingPowerAutomate/2.png)

4. Create two variables:
   Name: FirstofPreviousMonth
   Type: String:
   `addDays(startOfMonth(addDays(startOfMonth(utcNow()),-1)),1)`

Name: LastofPreviousMonth
Type: String:
`addDays(startOfMonth(utcNow()),-1)`

![Image](/static/images/assets/ExcelusingPowerAutomate/3.png)

5.  Create a new connector - SharePoint Get List items

![Image](/static/images/assets/ExcelusingPowerAutomate/4.png)

Site: YourSite
List: yourlist
Filter query:  
`ParkingDate ge'@{variables('FirstOfLastMonth')}' and ParkingDate le '@{variables('LastOfLastMonth')}'`

6. Search after "Create HTML Table":

From: Value from SharePoint Get List items

_Header_: Header for excel
_Value_: The value from the sharepoint list

![Image](/static/images/assets/ExcelusingPowerAutomate/5.png)

7. Search after the Sharepoint Connector and choose Create file:
   _Site Adress_: Choose where you want to save your file
   _Folder Path_: What is the path for the file
   _File Name_: Filename + .xls
   _File Output_: Output from Create HTML Table

![Image](/static/images/assets/ExcelusingPowerAutomate/6.png)
