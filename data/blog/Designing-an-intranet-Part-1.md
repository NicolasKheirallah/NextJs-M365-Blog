---
date: '2023-09-27T02:59:22.412Z'
title: Designing an intelligent intranet with Viva Connection in mind - Part 1
description: This is will be multi-part a guide on how you should design and architect your intelligent intranet, the do's and dont's and best pratices.
tags: ['Viva Connection', 'SharePoint']
summary: What is the best practice when using Viva goals
authors: ['default']
---

# Part 1 Where to begin

## Introduction

As a SharePoint Architect and consultant with nearly 10 years of experience in creating and designing over 80 intranets for various clients.

Main goal if this blogpost, Is to teach what is required for a successfull implementation of a new Intranet,
What the best practices for intranet design and what it entails, because I have seen many cases where the intranet solutions are not well-designed, scalable, or maintainable, and that lead to increased costs for upkeep and support.

So see these posts as a handbook on how to approach things.

## Getting started

There are a few things that are needed to succeed when building your Intranet, The way you want to drive this kind of project is to have a a flexible and iterative approach. As such a project no matter the size of the company does not have to be developed for a year before being released but you can release it in phases and make continuous improvements based on user feedback and engagement. This way, you can create an Intranet that grows and improves organically, meeting the needs and expectations of your users.

This DOES mean that you need to have a strategy, coordination, and execution .

As the Intranet is the campfire that connects employees within an organization and facilitates communication, collaboration, and information sharing. You want your users to come here, get the information that they need with as few clicks as possible, and not be a dreaded process to do so! We want to get rid of the old stigma that the Intranet is something you don't have to visit. This is where Viva connection comes into play.

## What's needed to succeed

To succeed when building an Intranet, these are a few things that are needed:

- A clear vision and strategy: The Intranet should align with the organization's goals, values, and culture. It should also have a well-defined purpose, scope, and target audience. The Intranet should be designed with the employee experience in mind, the information presented to the user should be relevant for them as this is the needs and expectations of the users.

- A dedicated team and stakeholders: The Intranet project should have a strong and committed team that includes representatives from different departments, roles, and levels of the organization. My preferred method of building a team for designing and building a teams

- A user-centric approach: The Intranet should be built with the users in mind. The team should conduct user research, surveys, interviews, and testing to understand the user's needs, preferences, and behaviors. The team should also involve the users in the design, development, and evaluation of the Intranet, and solicit their feedback and suggestions regularly. The Intranet should be user-friendly, intuitive, and accessible to all users.

- A robust technology platform: The Intranet should be built on a reliable, secure, and scalable technology platform that can support the functionality, performance, and growth of the Intranet. The platform should also be compatible with the existing systems and applications of the organization, and allow for easy integration and customization. The platform should also enable the team to update and maintain the Intranet easily and efficiently.

- A continuous improvement process: The Intranet should not be seen as a one-time project, but as an ongoing process that requires constant monitoring, evaluation, and improvement. The team should measure the usage, impact, and satisfaction of the Intranet, and identify the strengths, weaknesses, opportunities, and threats of the Intranet. The team should also implement changes and enhancements based on the data, feedback, and best practices of the Intranet.

A modern and intelligent intranet isn't owned by IT anymore but owned by large part by the whole organization and each part owns its own space.

## Stakeholders

An intranet project in SharePoint requires a clear definition of the roles and responsibilities of the different stakeholders involved. A stakeholder team should consist of representatives from the key departments that will use and benefit from the intranet. Ideally, these representatives should be the heads of their respective departments, but if that is not feasible, other members of the departments can also participate. The stakeholder team should have the necessary skills, resources, and authority to manage the project effectively. The stakeholder team should also have a clear leader who can provide direction, guidance, and support throughout the project lifecycle. Some of the departments that should be included in the stakeholder team are:

- HR: to provide input on employee engagement, policies, benefits, training and other requirements.
- Communication: to provide input on branding, content, design, and user feedback.
- IT: to provide input on technical requirements, security, integration, and maintenance.
- CISO: to provide input on compliance, risk management, and data protection.

## Ownership

As intranet in SharePoint is not a single entity, but a collection of sites, hubs, and pages that are owned and managed by various departments and teams. Each department or team has its own hub site, which serves as the main entry point and navigation hub for its content and services. The hub site owner is responsible for creating, maintaining, and governing the hub site and its associated sites.

In addition to the hub site owners, there is also a need for a service owner for SharePoint and Viva Connections. The service owner is responsible for overseeing the overall strategy, design, and governance of the intranet platform. The service owner works with the hub site owners to ensure that the intranet meets the needs and expectations of the organization and its users. The service owner also coordinates the communication, training, and support for the intranet platform.

For example, the communication department may own the landing page and the country pages of the intranet. The landing page is the first page that users see when they access the intranet, and it provides an overview of the organization's vision, values, news, and events. The country pages are sub-sites that provide localized information and resources for each country or region where the organization operates. The communication department is responsible for creating and updating these pages, as well as ensuring that they are consistent with the organization's brand and identity.

The HR department may own an HR hub site, which contains information and services related to human resources, such as employee handbook, policies, benefits, payroll, performance management, learning and development, etc. The HR department is responsible for creating and updating these pages, as well as ensuring that they comply with the legal and regulatory requirements of each country or region.

## Users in mind

One of the key aspects of intranet design is understanding what users really value as well as requiring a deep understanding of what users really need, and how to deliver information that is relevant, accessible, and convenient for them. This is something I've seen forgotten when designing intranets.
This is something that makes Viva Connections such a great tool! It allows users to access the intranet with minimal clicks and provides a comprehensive overview using Viva Home, especially on the go.

Another thing that users appreciate is having clear guidance on the purpose and use of different tools. For instance, in my case, SharePoint is for working and sharing information such as news, documents, and information in general, while Viva Engage is for community and culture especially erasing the boundaries of sharing data. So a department should have a Viva Engage community where they can chat and share information, as well as use the associated SharePoint site for news and so on. Teams are for project collaborations and personal chats.

## Underlaying structure - The Base of an intelligent intranet

The structure of an Intranet is a crucial factor that determines its effectiveness and usability. In my daily work, I see a lot of confusion and inconsistency in how to plan and implement an Intranet, how to use hub sites to create a coherent and logical hierarchy, and how to optimize them to enhance the information flow and user satisfaction. This leads to a lot of problems, as the Intranet should be able to adapt and evolve with the organization's needs, growth, and goals, without requiring major overhauls in the future. The structure is like the foundation of a house, and if it is not done well, it will collapse.

Hubsites are a powerful way to organize SharePoint sites based on the information context, rather than the site structure. For instance, we can create a hub for HR and connect all the sites that are related to HR, such as policies, benefits, training, etc. This way, we can enable the HR team to manage their own hub navigation and have more options, without depending on IT. We can also use the hub features to display context-specific content, such as news from all the HR sites, or to perform searches within the HR scope. However, I have noticed that many users are not familiar with or do not use this connection, and miss out on its benefits.

One way to visualize the structure is to think of the European Union and its member states. The European Union is the Intranet, and the member states are the hubs, the sites are the countries within each member state. Just as a country within a member state shares some common culture with the other countries in that state, a site connected to a hub shares some common navigation, branding and search settings with the other sites in that hub. However, each site also has its own content, permissions and features that are specific to its purpose and audience.

``![Image](/static/images/assets/DesigningAnIntranet/EOrR55NX0AAXO4M.png 'Source: Microsoft')
