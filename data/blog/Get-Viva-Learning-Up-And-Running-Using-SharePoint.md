---
date: '2022-09-29T21:51:21.726Z'
title: Get Viva Learning running using SharePoint
description: A guide on how to get Viva Learning running?
tags: ['Viva', 'Viva Learning', 'Teams', 'SharePoint']
summary: A guide on how to get Viva learning up and running, Common issues you can face and how to solve them
authors: ['default']
---

# Get Viva Learning running using SharePoint

Hi!

So I've got alot of questions from several of my clients about Viva and especially about how do we set it up.
So I'm planing to do a series on how to configure all Viva modules and in this post I'm gonna teach you how to set it up Viva learning as well as common issues that you can face.

Requirements

- Microsoft Teams admin (To add the )
- SharePoint admin
- Knowledge admin
- Azure AD Admin

You can of course use an global admin account if possible

- Microsoft 365 global admin

Prerequisite:

- SharePoint communication site
- New Setup policy group for the people in the Pilot.
- M365 group or Mail enabled security group for users in the pilot.

So we start of by vising the admin portal:
https://admin.microsoft.com/

## Sharepoint

My methodology is that we keep all the learning content in one of the same site! This is not a must but I find it easier to manage. You can always use any SharePoint site you want!

1. Create Communication Site called : Learning
   ![Image](/static/images/assets/GuideVivaLearning20220929/Picture2.png)

2. Give Everyone-except-External Read access (Optional)

## M365 Admin

From here we go to Settings and Choose Org Settings:
![Image](/static/images/assets/GuideVivaLearning20220929/Screenshot 2022-10-15 125322.png)

Scroll to the bottom and Choose Viva learning.
![Image](/static/images/assets/GuideVivaLearning20220929/Screenshot 2022-10-15 125400.png)

Viva Learning connects to SharePoint natively and uses a SharePoint List called "Learning App Content Repository" to determine where to find content. The SharePoint Content doesn't need to be stored on this site but is highly recommended.
![Image](/static/images/assets/GuideVivaLearning20220929/Screenshot 2022-10-15 125424.png)

This is usually pretty instant but can take upto 24 hours!

## Permission Groups

While in Admin we also need to create permission groups, these groups are needed to show the learning content in Viva learning.
For this we need one of two kinds of group:

- Mail-Enable Distrubtion group
  Or
- Microsoft 365 Group.

##Teams

For testing Viva Learning I recommend that you create a new Setup policy just for this:

1. Begin by visiting Teams admin: https://admin.teams.microsoft.com/
2. Select Teams apps and then Setup policy
   ![Image](/static/images/assets/GuideVivaLearning20220929/Picture4.png)
3. Press add and then name your Policy something proper: Viva Learning Pilot
4. Choose Add app uynder Installed apps and search Viva Learning, this will install it for everyone
   ![Image](/static/images/assets/GuideVivaLearning20220929/Picture5.png)
5. Go down to Pinned apps and Add Viva learning, this will make it visible for all
   ![Image](/static/images/assets/GuideVivaLearning20220929/Picture6.png)

## Adding content

Now we will add content to Viva learning. As this is a job that takes 24 hours to populate, you won't see the effect straight away. Adding content can be abit confusing, so we will break it down abit

Learning App Content Repository is used to tell the Viva Learning job where it should look for files.

- First off permission is set on folder level and not in the respository!

- You need to copy the URL from Share and not copy the URL. The URL from pressing Share needs to have /f/: s/ in it's URL.

1. First start of with going to the folder that you want to Share
   ![Image](/static/images/assets/GuideVivaLearning20220929/Screenshot 2022-10-16 145438.png)

2. Press Share And then Change type to "People in ... with the Link"
   ![Image](/static/images/assets/GuideVivaLearning20220929/Screenshot 2022-10-16 145450.png)

3. Set permission to Can view and then Apply!
   ![Image](/static/images/assets/GuideVivaLearning20220929/Screenshot 2022-10-16 145450.png)

4. Copy the URL
   ![Image](/static/images/assets/GuideVivaLearning20220929/Screenshot 2022-10-16 145517.png)

5. Now visit the List: Learning App Content Repository

6. New Item and Give it a Title and paste the URL.

![Image](/static/images/assets/GuideVivaLearning20220929/Picture1.png)
