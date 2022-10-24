---
date: '2022-06-12T11:55:21'
title: Workaround for Hanging issue related to OST Limit in Outlook
description: Quickfix for hanging outlook when dealing with large mailboxes!
tags: ['Outlook', 'Workaround']
summary: Quickfix for hanging outlook when dealing with large mailboxes
authors: ['default']
---

Another Query from an Client of mine that wondered how they could create an PowerApps to input Data to SharePoint list but didn't want the users to have any access to that list. So how do we do that ?

First off, we need an account to trigger the flow. Preferably a Service Acccount (or use your own account)

Secondly A SharePoint list!

So let's get started, I'm guessing you already know the basic of PowerApps:

1. You need to be admin for you computer

2. Press the Windows key or Search bar and type Regedit! Open this as an admin
   ![Image](/static/images/assets/FixOutlookHangingIssue/1.png)

3. Now Registery editor will open and you need to navigate to

`Computer\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\16.0\Outlook\PST`
![Image](/static/images/assets/FixOutlookHangingIssue/2.png)

4. Search for the key PST, right cklick and create two new varibales.

```
Name: MaxLargeSize
Type: Dword(32-bit)
Value: 102400
(Max at 100gb)

Name: WarnLargeSize
Type: Dword(32-bit)
Value: 92160
(Warning at 90gb)
```

![Image](/static/images/assets/FixOutlookHangingIssue/3.png)

6. Create a key called OST

7. Under the key PST and create two new varibales

```
Name: MaxLargeSize
Type: Dword(32-bit)
Value: 102400
(Max at 10gb)

Name: WarnLargeSize
Type: Dword(32-bit)
Value: 92160
(Warning at 90gb)
```

![Image](/static/images/assets/FixOutlookHangingIssue/4.png)
