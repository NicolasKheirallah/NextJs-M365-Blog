---
date: '2024-11-28T20:12:11.726Z'
title: Setting Default Content Type  in SharePoint Using Site Scripts and Power Automate
description: Learn how to use Site Scripts and Power Automate to dynamically assign content types to SharePoint lists or libraries with ease.
tags: ['SharePoint', 'Power Automate', 'Site Scripts', 'Automation']
summary: Learn how to automate content type assignments in SharePoint using Site Scripts and Power Automate.
authors: ['default']
---

So content types are important for maintaining structured content and ensuring consistent metadata across your libraries and lists. But in Site script it isn't possible to set a default content type. So by combining **Site Scripts** together woth **Power Automate**, we solve this by assigning content types to lists or libraries triggered by the site script!

This guide will walk you through how to use a Site Script to define content types and a Power Automate flow to assign those content types dynamically based on triggers.

---

### **Prerequisites**

1. **SharePoint Admin Access**:

   - You need permissions to configure Site Scripts and access to the SharePoint site where you will implement the solution.

2. **Power Automate Access**:

   - Ensure you have access to create flows in Power Automate.

3. **JSON Payload and Schema**:
   - Familiarity with JSON and understanding the structure of Site Scripts and Power Automate triggers.

---

### **Solution Architecture**

1. **Site Script**:

   - Define the content type and associate it with a specific SharePoint list or library.
   - Deploy the Site Script to SharePoint.

2. **Power Automate Flow**:

   - Triggered when a specific event occurs (e.g., site creation or a manual event).
   - Parse the Site Script JSON response and assign the content type dynamically to a list or library.

3. **Automated HTTP Request**:
   - Use Power Automate to send an HTTP request to SharePoint to finalize the assignment of the content type.

---

### **Step 1: Create and Deploy a Site Script**

A **Site Script** is a JSON file that defines the actions SharePoint should take when the script is applied. Below is an example of a Site Script that creates a custom content type.

#### Example Site Script JSON

```json
{
  "$schema": "schema.json",
  "actions": [
    {
      "verb": "addContentType",
      "name": "Project Document",
      "description": "A custom content type for project-related documents",
      "group": "Custom Content Types",
      "parentContentType": "0x0101", // Base content type (Document)
      "fields": [
        {
          "fieldName": "ProjectName",
          "displayName": "Project Name",
          "type": "Text",
          "required": true
        },
        {
          "fieldName": "ProjectStartDate",
          "displayName": "Project Start Date",
          "type": "DateTime",
          "required": false
        }
      ]
    },
    {
      "verb": "addSPList",
      "listName": "Project Documents",
      "templateType": 101, // Document Library
      "subactions": [
        {
          "verb": "addContentType",
          "contentTypeName": "Project Document"
        }
      ]
    },
    {
      "verb": "triggerFlow",
      "url": "https://prod-123.westus.logic.azure.com:443/workflows/abcd1234-trace5678", // Replace with your flow's HTTP trigger URL
      "name": "Notify Content Type Assignment",
      "parameters": {
        "contentTypeName": "Project Document",
        "siteUrl": "[webUrl]",
        "listName": "Project Documents"
      }
    }
  ],
  "bindata": {},
  "version": 1
}
```

#### Steps to Deploy

1. Save the above JSON as `ContentTypeSiteScript.json`.
2. Use **PowerShell** or the **SharePoint Admin Center** to deploy the script.

   **PowerShell Commands**:

   ```powershell
   Connect-SPOService -Url https://yourtenant-admin.sharepoint.com
   $siteScript = Get-Content -Path "ContentTypeSiteScript.json" -Raw
   Add-SPOSiteScript -Title "Project Document Script" -Content $siteScript
   ```

---

### **Step 2: Create the Power Automate Flow**

#### Overview of Flow Components

1. **Trigger**:

   - Start the flow manually or via an HTTP request when a site or list is created.

2. **Parse JSON**:

   - Parse the Site Script response to extract the `ContentTypeId`.

3. **Send HTTP Request**:
   - Use the `ContentTypeId` to dynamically assign the content type to a SharePoint list or library.

#### Steps to Build the Flow

##### 1. **Trigger the Flow**

- Use **"Manually trigger a flow"** or **"When an HTTP request is received"** as the trigger.
- Configure the trigger to accept input parameters if required.

##### 2. **Parse JSON**

- Add the **Parse JSON** action to handle the response from the Site Script.

**Schema Example**:

```json
{
  "type": "object",
  "properties": {
    "contentTypeName": {
      "type": "string"
    },
    "siteUrl": {
      "type": "string",
      "format": "uri"
    },
    "listName": {
      "type": "string"
    }
  }
}
```

##### 3. **Initialize Variable**

- Add the **Initialize variable** action to store the `ContentTypeId`.

**Configuration**:

- **Name**: `ContentTypeId`
- **Type**: String
- **Value**: Select `contentType > Id` from the parsed JSON.

##### 4. **Send an HTTP Request to SharePoint**

Use the **"Send an HTTP request to SharePoint"** action to assign the content type to a list.

**Configuration**:

- **Site Address**: The SharePoint site URL.
- **Method**: POST
- **URI**:
  ```
  /_api/web/lists/getbytitle('Project Documents')/contenttypes/addavailablecontenttype
  ```
- **Headers**:
  ```json
  {
    "Accept": "application/json;odata=verbose",
    "Content-Type": "application/json"
  }
  ```
- **Body**:
  ```json
  {
    "contentTypeId": "@{variables('ContentTypeId')}"
  }
  ```

---

### **Step 4: Add the `Send an HTTP Request to SharePoint` Action**

In this step, the flow uses an HTTP request to set the **Unique Content Type Order** for the folder or document library to ensure the content type is applied correctly.

#### **Configuration for the HTTP Request**

1. **Add the Action**:

   - In Power Automate, add a new action after parsing the `ContentTypeId` or initializing the variable.

2. **Action**: **Send an HTTP Request to SharePoint**

3. **Configure Parameters**:

   - **Site Address**: Use the dynamic content that corresponds to the site URL (e.g., `Body SiteUrl`).
   - **Method**: `POST`
   - **URI**:
     ```plaintext
     _api/web/lists/getbytitle('<Body DisplayName>')/RootFolder
     ```
     - Replace `<Body DisplayName>` with the dynamic content referencing the name of the list or library.

4. **Headers**:
   Add the following headers:

   - **Accept**: `application/json;odata=verbose`
   - **Content-Type**: `application/json;odata=verbose`
   - **If-Match**: `*`
   - **X-HTTP-Method**: `MERGE`

5. **Body**:
   Use the following JSON structure in the **Body** section:
   ```json
   {
     "_metadata": { "type": "SP.Folder" },
     "UniqueContentTypeOrder": {
       "_metadata": { "type": "Collection(SP.ContentTypeId)" },
       "results": [{ "StringValue": "@{variables('ContentTypeId')}" }]
     }
   }
   ```

---

### **Explanation of Each Parameter**

- **Site Address**: Specifies the SharePoint site where the list or library is located.
- **URI**: Points to the `RootFolder` of the specified list or library.
- **Headers**:
  - `Accept`: Indicates the response format expected from the API.
  - `Content-Type`: Specifies the format of the request payload.
  - `If-Match`: Ensures the HTTP request only updates existing resources.
  - `X-HTTP-Method`: Sets the request to `MERGE` mode, updating the specified resource without overwriting it entirely.
- **Body**:
  - `_metadata`: Defines the folder or list object type in SharePoint.
  - `UniqueContentTypeOrder`: Specifies the unique content type order for the list or library, ensuring the newly created content type is applied.
  - `StringValue`: Uses the `ContentTypeId` extracted earlier in the flow.

---

![Image](/static/images/assets/setContenttypeUsingFlow/Screenshot2024-07-28-1.png)
![Image](/static/images/assets/setContenttypeUsingFlow/Screenshot2024-07-28-2.png)

### **Step 5: Test the Flow**

1. **Deploy the Flow**:

   - Ensure the flow is saved and ready for testing.

2. **Trigger the Flow**:

   - Trigger the flow manually or via the Site Script.

3. **Monitor Flow Execution**:

   - Check the flow's run history in Power Automate to ensure the HTTP request was successful.

4. **Validate in SharePoint**:
   - Go to the target SharePoint site.
   - Open the list or library to confirm that the content type has been applied and is set as unique.

---

### **Conclusion**

By combining the power of **Site Scripts** and **Power Automate**, you can create a seamless, automated workflow for setting content types in SharePoint. This solves one of the missing features in Site scripts!

If you have any questions or need help implementing this solution, feel free to contact me!

```

```
