---
date: '2022-06-12T11:55:21'
title: Workaround for a Hanging issue related to OST Limit in Outlook
description: Quickfix for hanging outlook when dealing with large mailboxes!
tags: ['Outlook', 'Workaround']
summary: Quickfix for hanging outlook when dealing with large mailboxes
authors: ['default']
---

As a consultant, you recieve A LOT of email with alot of attachments, and sometimes you hit the upper limit of what Outlook can handle, and this is how you solve that

1. You need to be the admin for your computer

2. Press the Windows key or Search bar and type Regedit! Open this as an admin
   ![Image](/static/images/assets/FixOutlookHangingIssue/1.png)

3. Now Registry editor will open and you need to navigate to

`Computer\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\16.0\Outlook\PST`
![Image](/static/images/assets/FixOutlookHangingIssue/2.png)

4. Search for the key PST, right-click, and create two new variables.

```
Name: MaxLargeSize
Type: Dword(32-bit)
Value: 102400
(Max at 100GB)

Name: WarnLargeSize
Type: Dword(32-bit)
Value: 92160
(Warning at 90GB)
```

![Image](/static/images/assets/FixOutlookHangingIssue/3.png)

6. Create a key called OST

7. Under the key PST and create two new variables

```
Name: MaxLargeSize
Type: Dword(32-bit)
Value: 102400
(Max at 10GB)

Name: WarnLargeSize
Type: Dword(32-bit)
Value: 92160
(Warning at 90GB)
```

![Image](/static/images/assets/FixOutlookHangingIssue/4.png)
