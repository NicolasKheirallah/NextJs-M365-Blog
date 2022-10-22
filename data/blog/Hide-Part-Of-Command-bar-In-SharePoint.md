---
date: '2022-08-22T17:53:23.432Z'
title: Hide part of command bar in SharePoint Lists and Libraries
description: A guide on how to hide part of command bar in SharePoint Lists and Libraries
tags: ['SharePoint', 'Lists']
summary: A guide on how to hide part of command bar in SharePoint Lists and Libraries
authors: ['default']
---

So a client of mine wanted the ability for users to hide the ability part of the commandbar on certain list for various reason, as the organisaton didn't want them to users to use it on that list!

They wanted to:

- Hide ability to create new folders
- Comment
- Export

So how did we do it ? Well we used us of the "view-commandbar-formatting":

You can find alot more from here:

https://learn.microsoft.com/en-us/sharepoint/dev/declarative-customization/view-commandbar-formatting

This made it easy for us to hide the any of the option of the commandbar that we didn't want. So this is how we did it:

1. Navigate to the site and the list that you want to modify

2. Select View and then Format Current view.

   ![Image](/static/images/assets/CommandBarFormatJson/1.png)

3. Choose Advance mode and then paste the Json below:

   ![Image](/static/images/assets/CommandBarFormatJson/2.png)

4. Paste the Json inside of the Format View editor:

```json
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
