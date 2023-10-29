---
date: '2023-10-29T20:59:22.412Z'
title: Designing an intelligent intranet with Viva in mind - Part 2
description: This is the second part of a guide on how you should design and architect your intelligent intranet, the do's and dont's and best practices.
tags: ['Viva', Viva Connections, 'SharePoint']
summary: This is will be multi-part a guide on how you should design and architect your intelligent intranet
authors: ['default']
---

# Introduction

So in previous post we went through the preparations, mindset needed as well as touching a bit about the underlying structure. So in this post we will dig deeper and go a bit more of logic, details and when to use different technologies!

# Clear Definitions - What is used where

One of the challenges that many organizations face is the lack of clarity and guidance on how to use different tools and platforms for communication and collaboration. This causes a lot confusion, frustration and inefficiency among users. To avoid this, the organization needs to create a clear definition of when to use SharePoint, Viva Engage and Teams, and how they complement each other. As these are powerful tools within the Microsoft 365 ecosystem, each with distinct use cases so knowing when to use each tool and how they complement each other is crucial for creating an efficient employee experience platform thats scalable and that can grow organically

So we will try overcome these challenges in this blog-post with examples to make clear understand how everything is designed together.

# What to use where:

SharePoint plays a pivotal role as the backbone of the employee experience platform, providing the infrastructure for collaboration and content management. It is the central repository for documents, data, and information, making it the cornerstone of the entire ecosystem. The success and effectiveness of the employee experience heavily depend on how SharePoint is architecturally designed and implemented from the start. This is also where usually see most of the with the implementation fail. The reasoning being those who are designing the architecture of the intranet/EXP don't have a clear understanding on how everything works together.

So when and for what do we use SharePoint ?

### Intranet

So, SharePoint Should be your intranet and the landing-page for the Intranet. My recommendation is to build it as a compliment to Viva Connection Home, This will make it easier for users to get the information with as few clicks as possible! As they can visit the intranet from Teams but also Thanks to Viva Connection Home they can relevant information for them quickly! So I always recommend to have it enabled both on Desktop and Mobile. And for Information that isn't Viva home or important links, they can go into to the intranet. The intranet should also be seen as the culture hub of organization, this is where the user will find everything that relevant for them but also who we are, what our goals are as well as getting information that's relevant for them.

I recommend also that the landing page of the intranet Is an Hub and is also the central part for the whole organization even if it's conglomerate or you have multiple companies within a tenant. As this will create culture but also create a less we against them.

[![Image](https://learn.microsoft.com/en-us/viva/media/connections/vc-vs-home-site-venn.png 'Homesite and Connections')](https://learn.microsoft.com/en-us/viva/connections/viva-connections-overview)

#### Viva Amplify

#### Viva Pulse

### Hubs

So a hub-site is a concept in SharePoint that can be a bit hard do grasp! and this is something I want to clear up, as this is one of the most important configurations that you do in designing your employee experience

A hub site is a type of SharePoint feature that connects and organizes other sites based on a common theme or purpose. For example, you can create a hub site for a department, a division, or a region. A hub site provides the following benefits:

- Shared navigation and branding: You can customize the navigation bar and the look and feel of the hub site and apply them to all the connected sites. This creates a consistent user experience and helps users navigate between related sites.
- Roll-up of content and search: You can aggregate news, events, documents, and other content from the connected sites and display them on the hub site. You can also search across all the connected sites from the hub site.
- A home destination for the hub: You can use the hub site as a landing page for your topic or area of interest. You can showcase important information, highlight key resources, and provide links to other hubs or sites.

Hub sites are flexible and dynamic. You can change the name, logo, navigation, or theme of a hub site at any time. You can also add or remove connected sites as your needs change. Hub sites are not hierarchical or nested; you can associate a site with only one hub site at a time, but you can change the association as needed.

So see hub-sites as the campfire which all other sites sit together around and share information! And is a key part of having intelligent and scalable intranet and employee experience!

[![Image](https://techcommunity.microsoft.com/t5/image/serverpage/image-id/205306i4E491AD65E4EB835/image-dimensions/2500?v=v2&px=-1 'Hubs')](https://learn.microsoft.com/en-us/sharepoint/information-architecture-modern-experience)

### Countries, Cities & Departments

This topic is something that I've seen most implementations fail at and how to create but also manage Countries, Cities & Departments!
The main issue is the choice of the wrong tooling but also lack of understanding on how information should flow and how user interact.

**Countries**:

So let's start with Countries, my recommendation for countries is just to have a regular communication site! This site is for local information, news and everything that's country specific with links to relevant information. This site will be a hub-site and all information from support functions that's related to this site will be connected to it, such as Cities and Areas! Pretty straight forward. These sites need to be local language as well as English!

**Cities and Areas**:
For Cities and Areas, the approach is a bit different! This should be created from Viva Engage, and now you're thinking why?
It's simple, you want to have the ability to communicate with each other but also you want people who aren't part of that city or area to be able communicate with you.

For example, imagine that someone from Sweden is coming to Paris in France for a visit to the office. They might want to know the office hours, the reception staff, and the local colleagues who work on similar projects. But they might also want to know some tips about the best places to visit, eat, and have fun in Paris.

These things can't be achieved by using teams, this needs Engage + SharePoint. Also other features such as storylines will create more of a community and bring everyone more closer.

But then you're wondering don't we need a SharePoint site ? Yes and you don't have to worry about creating one yourself! When you set up a Viva Engage community, you automatically get a SharePoint site along with other M365 Group features, such as an AD group and a mailbox.

So on this SharePoint Site we can customize add information of that office such as contact details, opening hours, news, and events but also who's new to the office! This site will be connected to the country hub!

**Departments**:
So Departments is kinda of a mix of countries and cities, so you want to create the department site via Viva Engage by doing a Community for that department, this is so you can communicate with within the department while also having the possibility to use more the features that Viva Engage offers that isn't included in teams such as Storylines.

So Viva Engage offers a lot better experience for communication that Teams!

The SharePoint site should serve as a hub-site for the department and all the relevant sites and sub-departments should be connected to this department. This way, the department can display news from all the connected sites, as well as events, important links and information, and the department's mission and objectives. It would also be nice to feature new members of the department in a news-feed. Of course, this can be tailored to the department's preferences.

The navigation should show information that is relevant for the users of the department to find what they mostly use!

## Teams

A common issue is to extend the use of teams outside of what it's designed for, and it's not something wrong with doing that but it's not scalable and lacking feature for example departments.

So when should you use Teams? Well you want to use teams to create a shared space for your team or for a project to collaborate, where you can chat, share files, schedule meetings, and more. Teams is ideal for ongoing collaboration and communication with a group of people who have a common goal or interest and have limited lifespan, and when the project is done, the file are transferred and the team is archived. Having to many teams will be hard for the user to navigate and finding the information for the organization will become harder!
