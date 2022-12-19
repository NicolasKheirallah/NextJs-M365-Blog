---
date: '2022-11-24T11:43:00'
title: How to enable sensitivity labels on PDF using Adobe
description: A guide on how natively enable Sensitivity labels on PDFs
tags: ['Sensitivity Labels', 'SharePoint', 'PDF', 'Adobe']
summary: A guide on how natively enable sensetivity labels on PDFs
authors: ['default']
---

So in this guide we will enable native sensetivity labels in adobe acrobat!

Requirements:

- Admin on local computer
- Adobe Acrobat (atleast version 22.001.20142)
- Windows 10 or 11 machine
- Sensitivity labels setup (ofc?)

https://helpx.adobe.com/uk/enterprise/kb/mpip-support-acrobat.html

1. First press the search box or  Windows key + r and run Regedit:

2. Navigate to :

> Computer\HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Policies\Adobe\Adobe Acrobat\DC\FeatureLockDown

Change the value of variable:

> bMIPCheckPolicyOnDocSave = 1

> bMIPLabelling to 1

3. Now navigate to:

> Computer\HKEY_CURRENT_USER\SOFTWARE\Adobe\Adobe Acrobat\DC\MicrosoftAIP

Change the value of variable:

> bShowDMB value to 1

4. Now close Regedit and restart Adobe Acrobat

5. Choose your PDF file and then

File → Protect PDF → Select a Microsoft Sensitivity Label

6. Login and you should have all your labels available

Sidenote:

- Remember to remove any additional plugins
- Password encrypted PDFs aren't supported
- PDF/A isn't supported either, usually a goverment requirement.
