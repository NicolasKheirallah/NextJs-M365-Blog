---
date: '2023-10-03T11:14:22.442Z'
title: Get better insight of how users interact with your intranet using Clarity.
description: Make full use of Microsoft Clarity to see how your users interact with your intranet and continuously improve it
tags: ['SharePoint', 'Viva Connections']
summary: A guide on how to optimize your intranet using Microsft Clarity
authors: ['default']
---

# Introduction

Microsoft Clarity is one of my favorite tools to use when implementing a new intranet, as this gives you an overview of how to intranet is being used and gives you the option to optimize your intranet and improve user experience based on how the users interact.

So Clarity, we can track how users interact with your intranet pages, identify common issues and pain points, and discover new insights by using heatmaps and user interactions to enhance our content and design.

# Getting Started

1. Sign up for a free account at clarity.microsoft.com. You will need a Microsoft account to sign up.

![Image](/static/images/assets/Clarity/1.png)

2. Create a new project and enter your website name and URL. You can also choose to enable or disable features such as heatmaps, session recordings, and insights.
   ![Image](/static/images/assets/Clarity/2.png)
   ![Image](/static/images/assets/Clarity/3.png)

3. Press get "tracking code" and copy the tracking code that is generated for your project and paste it into a text file for now.
   ![Image](/static/images/assets/Clarity/7.png)

4. Download joaoferreira module for Clarity: https://github.com/joaoferreira/microsoftclarity/tree/main/sharepoint/solution
   The file should be called "Clarity.sppkg"

5. Go to your SharePoint Admin and go into the Appcatalog, You might need to create one if you have not.
   ![Image](/static/images/assets/Clarity/4.png)
   ![Image](/static/images/assets/Clarity/5.png)

6. Upload the SPPKG file and install it. Make sure it's installed as a tenant wide extension

7. Press tenant wide Extensions and press open:
   ![Image](/static/images/assets/Clarity/6.png)
8. Add your ClarityID here, it should be on

Example:

```
{"clarityID":"eiw3c7oiy1"}
```

8. Wait for some data to be collected by Microsoft Clarity. It may take up to 24 hours for the data to appear on your dashboard.
   ![Image](/static/images/assets/Clarity/8.png)
9. Explore the different reports and features that Microsoft Clarity offers such as:

- Heatmaps: Heatmaps will show you where users click, scroll, and move their mouse on your intranet pages. You can use this data to understand what users are looking for, what they find engaging, and what they ignore or miss. You can also compare different segments of users, such as by device, location, or role, to see how their behavior differs.
  ![Image](/static/images/assets/Clarity/13.png)

-Recordings: Recordings let you watch how users navigate your intranet, from the moment they enter to the moment they leave. You can see how users interact with your navigation, search, forms, and other elements on your intranet. You can also filter recordings by various criteria, such as page views, time spent, errors, or feedback.

![Image](/static/images/assets/Clarity/12.png)

- Identify and fix issues with metrics and reports: Clarity provides you with various metrics and reports that help you measure the performance and usability of your intranet. You can see how many users visit your intranet, how long they stay, how often they return, and how satisfied they are. You can also see how many errors, rage clicks, dead clicks, or excessive scrolling occur on your intranet pages, and which pages have the most issues.
  ![Image](/static/images/assets/Clarity/11.png)

- Test and optimize your intranet with experiments. Experiments allow you to test different versions of your intranet pages and see which one performs better. You can create experiments based on various goals, such as clicks, conversions, engagement, or satisfaction. You can also use Clarity's insights to inform your experiments and make data-driven decisions.
