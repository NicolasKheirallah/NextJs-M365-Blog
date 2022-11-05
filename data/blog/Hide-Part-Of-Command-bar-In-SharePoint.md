---
date: '2022-08-22T17:53:23.432Z'
title: Hide part of the command bar in SharePoint Lists and Libraries
description: A guide on how to hide part of the command bar in SharePoint Lists and Libraries
tags: ['SharePoint', 'Lists']
summary: A guide on how to hide part of the command bar in SharePoint Lists and Libraries
authors: ['default']
---

So a client of mine wanted the ability for users to hide the ability part of the command bar on certain lists for various reasons, as the organization didn't want them, users, to use it on that list!

They wanted to:

- Hide the ability to create new folders
- Comment
- Export

So how did we do it? Well, we used us the "view-command bar-formatting":

You can find a lot more from here:

https://learn.microsoft.com/en-us/sharepoint/dev/declarative-customization/view-commandbar-formatting

This made it easy for us to hide any of the options of the command bar that we didn't want. So this is how we did it:

1. Navigate to the site and the list that you want to modify

2. Select View and then Format Current view.

   ![Image](/static/images/assets/CommandBarFormatJson/1.png)

3. Choose Advance mode and then paste the JSON below:

   ![Image](/static/images/assets/CommandBarFormatJson/2.png)

4. Paste the JSON inside of the Format View editor:

```JSON
{
  "commandBarProps": {
    "commands": [
      {
        "key": "newFolder",
        "hide": true
      },
      {
        "key": "comment",
        "hide": true
      },
      {
        "key": "export",
        "hide": true
      }
    ]
  }
}
```

![Image](/static/images/assets/CommandBarFormatJson/4.png)

5. Press Preview to see if it worked and then press save if it fills your requirements.
   ![Image](/static/images/assets/CommandBarFormatJson/5.png)
