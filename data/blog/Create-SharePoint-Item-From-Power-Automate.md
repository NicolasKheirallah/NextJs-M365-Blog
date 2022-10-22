---
date: '2022-09-20T13:55:21'
title: Create SharePoint List item from PowerApps using Power Automate
description: A guide on how to List item from PowerApps using Power Automate
tags: ['SharePoint', 'Lists', 'PowerApps', 'PowerAutomate']
summary: A guide on how to List item from PowerApps using Power Automate
authors: ['default']
---

Another Query from an Client of mine that wondered how they could create an PowerApps to input Data to SharePoint list but didn't want the users to have any access to that list. So how do we do that ?

First off, we need an account to trigger the flow. Preferably a Service Acccount (or use your own account)

Secondly A SharePoint list!

So let's get started, I'm guessing you already know the basic of PowerApps:

1. Create an PowerApps

2. Add what kind of Input fields you have to use. Label them correctly to makew it easier to keep track!
   ![Image](/static/images/assets/PowerAppsCreateListItems/1.png)

3. Now we create a flow by pressing the flow icon on the left bar and then Create new flow
   ![Image](/static/images/assets/PowerAppsCreateListItems/2.png)

4. Create from Blank , you can also use finished templates if you like.
   ![Image](/static/images/assets/PowerAppsCreateListItems/3.png)
   ![Image](/static/images/assets/PowerAppsCreateListItems/4.png)

5. Press new step and then search for Create item
   ![Image](/static/images/assets/PowerAppsCreateListItems/5.png)

6. Select your SharePoint list and then choose "Ask in Powerapps" for each field you want to input
   ![Image](/static/images/assets/PowerAppsCreateListItems/6.png)

7. Press save And it should how up in PowerApps
   ![Image](/static/images/assets/PowerAppsCreateListItems/7.png)

8. Go to your button and press on select, and search for your Flow, Mine is called 'Powerapps -> Create item'.
   ![Image](/static/images/assets/PowerAppsCreateListItems/8.png)

9. Choose run and input your fields.
   ![Image](/static/images/assets/PowerAppsCreateListItems/9.png)

10. Save and now it will save it to the list! :-)
    ![Image](/static/images/assets/PowerAppsCreateListItems/10.png)

11. And this is how the SharePoint List looks like.
    ![Image](/static/images/assets/PowerAppsCreateListItems/11.png)

Remember to add a reset after inputting as well. This to clear the information for the user.
Also add a notification or screen to inform the user that it has been saved.
