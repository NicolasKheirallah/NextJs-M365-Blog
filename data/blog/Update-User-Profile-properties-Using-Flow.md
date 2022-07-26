---
date: '2021-06-12T11:55:21'
title: Update User Profile Using Power Automate and Forms
description: Update User Profile Using Power Automate and Forms
tags: ['Forms', 'SharePoint', 'Power Automate']
summary: How to make it easy for users to update their user profiles!
authors: ['default']
---

1. Create a form under https://forms.office.com/Pages/DesignPageV2.aspx

2. Add the field or the fields you want to update in the form, Im going to update about me field

![Image](/static/images/assets/UpdateUserProfileFromFlow/2.png)

3. Save the form

4. Create a new flow under Power automate, this will be an automated flow
   https://make.powerautomate.com/

5. Select: "When a new response is submitted" as the trigger

6. Select your form
   ![Image](/static/images/assets/UpdateUserProfileFromFlow/3.png)

7. Add a new step and select: "Get Response Details"

8. Select your Form ID
   ![Image](/static/images/assets/UpdateUserProfileFromFlow/4.png)

9. Now add a new step and select: Send an HTTP request to SharePoint
   ![Image](/static/images/assets/UpdateUserProfileFromFlow/5.png)

## Single value Property

```
| Name         | Value                                                              |
| ------------ | ------------------------------------------------------------------ |
| Site Address | https://yourTenant.sharepoint.com/sites/yourSite                   |
| Method       | POST                                                               |
| Uri          | /\_api/SP.UserProfiles.PeopleManager/SetSingleValueProfileProperty |
| Headers      | Accept: application/json; odata=nometadata                         |
| Headers      | content-type: application/json; odata=nometadata                   |
| Body         |
```

```json
{
  "accountName": "i:0#.f|membership|UsersEmailFromForm",
  "propertyName": "AboutMe",
  "propertyValue": "YourFieldFromForms"
}
```

## Multi value Property

```
| Name         | Value                                                              |
| ------------ | ------------------------------------------------------------------ |
| Site Address | https://yourTenant.sharepoint.com/sites/yourSite                   |
| Method       | POST                                                               |
| Uri          | /\_api/SP.UserProfiles.PeopleManager/SetMultiValuedProfileProperty |
| Headers      | Accept: application/json; odata=nometadata                         |
| Headers      | content-type: application/json; odata=nometadata                   |
| Body         |                                                                    |
```

```json
{
  "accountName": "i:0#.f|membership|UsersEmailFromForm",
  "propertyName": "OnePiece",
  "propertyValue": ["Luffy", "Zoro", "Nami", "Usopp", "Robin"]
}
```

10. Tested my form:
    ![Image](/static/images/assets/UpdateUserProfileFromFlow/6.png)

11. And it's updated :smiley: :
    ![Image](/static/images/assets/UpdateUserProfileFromFlow/7.png)
