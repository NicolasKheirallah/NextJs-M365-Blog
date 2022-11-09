---
date: '2022-11-09T08:10:31'
title: Create a download button using for items and coloumns
description: A guide on create a download button using for library using Column formatting json
tags: ['SharePoint', 'Lists', 'column-formatting']
summary: A guide on create a download button using for library using Column formatting json
authors: ['default']
---

A short blog post on how to create a download button for files.

Select column -> column settings -> format this column -> Advanced mode
![Image](/static/images/assets/createDownloadButton.png)

Code for Downloading field from library:
Optional:
Create a additional field, this will be used

```
{
  "$schema": "https://developer.microsoft.com/json-schemas/sp/v2/column-formatting.schema.json",
  "elmType": "a",
  "txtContent": "Download",
  "style": {
    "background-color": "gray",
    "text-decoration": "none",
    "color": "white",
    "font-size": "14px",
    "padding-left": "5px"
  },
  "attributes": {
    "target": "_blank",
    "href": "=@currentWeb+'/_layouts/15/download.aspx?sourceurl='+[$FileRef]"
  }
}
```

Code for Downloading Image Column in List:

```
{
  "$schema": "https://developer.microsoft.com/json-schemas/sp/v2/column-formatting.schema.json",
  "elmType": "button",
  "style": {
    "border-radius": "5px",
    "margin": "5px 0px",
    "padding": "0px"
  },
  "attributes": {
    "class": "ms-bgColor-themePrimary"
  },
  "children": [
    {
      "elmType": "a",
      "txtContent": "Download",
      "style": {
        "text-decoration": "none",
        "padding": "10px 0px",
        "width": "100%"
      },
      "attributes": {
        "href": "=@currentWeb + '/_layouts/15/download.aspx?sourceurl=' + @currentField.serverRelativeUrl",
        "target": "_blank",
        "class": "ms-fontColor-white"
      }
    }
  ]
}
```
