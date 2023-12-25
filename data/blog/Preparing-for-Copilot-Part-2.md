---
date: '2023-12-25T00:54:01.975Z'
title: Preparing for Copilot - Part two - Prep work!
description: We will go through what needed organizational when planning to start with copilot!
tags: ['SharePoint', 'Copilot']
summary: A blog series on what needed do to get started Copilot
authors: ['default']
---

# Introduction

In the previous post we went though what the organization needs to think about and prepare on a organizational level such as who are the stakeholders, defining the Use-cases with some examples of what different departments can benefit from using Copilot! This is to give an idea of what it can be used for an what you can use to calculate ROI on!

The plan for this post is to get a bit more technical about what kind of prep work that is needed from you in Microsoft 365 to increase the success rate but also getting the right information, because Copilot works best if it has good data and it can't figure out what's good data and not. So that's up to you and your organization to do, and this is something that really needs to be pushed from above and down!

And this is what I'm going to deeper in this post!

## Identify your sources

So, Copilot gathers its data from a variety of sources, including your own data sources and public sources. This means that you have some control over the data that Copilot can access. However, it's important to ensure that the data is accurate, relevant, and up-to-date. It's also important to make sure that the data is classified appropriately and that only authorized users have access to it. So to mitigate these concerns, it's important to identify which data Copilot is using and to control who has access to that data. This can be done by checking the permissions to the information such as Sites, files etc and to grant access to specific users or groups.

As Copilot makes extensive use of the Graph API to access data from Interal sources, including SharePoint, Teams, and OneDrive. This means that Copilot has access to the same information as the user who is logged in. This can be a powerful feature, but it also raises privacy concerns.

![Image](/static/images/assets/getstartedwithcopilot/copilot-diagram-final.png)

Here's some examples of the different data sources that copilot uses out of the box:

- Microsoft Graph: This is a unified API that connects to data from various Microsoft 365 services, such as Outlook, Teams, SharePoint, OneDrive, and more. M365 copilot uses Microsoft Graph to access the user's calendar, email, contacts, files, chats, and other information that can help the user manage their tasks and projects.

- Bing Search: M365 copilot uses Bing Search to find relevant information and resources for the user's queries ny querying web pages, images, videos, news, and other online content.

- Azure Cognitive Services: This is a collection of AI-powered services that enable M365 copilot to perform natural language processing, speech recognition, computer vision, and other cognitive tasks. M365 copilot uses Azure Cognitive Services to analyze the user's voice, text, images, and videos, and provide relevant feedback and suggestions.

- Leveraging Plugins: Plugins are a key enabler for connecting Copilot to external data. They provide live access to external services without the need for pre-indexing data. This means that Copilot can retrieve the latest information and respond to your prompts in real time:

  - OpenAI Plugins: Access external APIs and data using a simple YAML file interface.

  - Microsoft Teams Message Extensions: Integrate Copilot with third-party applications and services within Teams.

  - Power Platform Connectors: Leverage Power Platform data and automation capabilities.

Plugins allow Copilot to retrieve real-time data as needed to respond to your prompts, enhancing its ability to provide accurate and up-to-date information. They also enable Copilot to take direct actions through plugins, such as updating records or triggering workflows.

## Don't be afraid of deleting data

A issue i've seen in a lot of companies is that they are hesitate to delete or remove data, fearing that they might need it in the future. This approach is not only counterproductive but also poses potential security and compliance risks.

A data cleanup strategy is essential for ensuring data integrity, minimizing storage costs, and enhancing data accessibility. It involves identifying, classifying, and managing data throughout its lifecycle, from creation to deletion. A well-defined data lifecycle management policy outlines the retention periods for different types of data, ensuring that only relevant information is retained while unnecessary data is purged.

Regular data cleanup exercises are essential for maintaining a healthy system and to keep cost down. One effective approach is to implement annual cleanup weeks, during which users are encouraged to review and delete old documents that are no longer relevant or required. This practice not only reduces storage clutter but also promotes data ownership and accountability among users.

Another crucial aspect of data cleanup is identifying and archiving inactive sites or teams. Sites or teams that have been dormant for two years or more should be flagged for review. If the owner is still within the organization, they should be contacted to confirm their continued use of the site or team. In cases where the owner is no longer with the organization, the members should be notified. If no response is received, the site or team should be locked and archived for future reference. There's a couple of ways of doing this, I usually use Power Automate and build som logic around it but you will be able in the future use the access review feature in SharePoint Premium! This is what I would recommend to use in the future!

But in essence data cleanup is not just about deleting old data; it's also about organizing and structuring existing information. By implementing clear data naming conventions, consistent file formats, and metadata tagging, the organizations can make their data more searchable and accessible both for the user but also for Copilot, which enhances productivity and collaboration.

## Permissions are important!

## Retention Policy and Sensitivity Labels!
