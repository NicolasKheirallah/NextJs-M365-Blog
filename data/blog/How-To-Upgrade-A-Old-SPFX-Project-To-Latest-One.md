---
date: '2022-12-13T11:51:21.726Z'
title: Update your old SPFX project to latest SPFX version
description: Upgrade your older SPFX 1.10 and older spfx project to 1.15 or newer
tags: ['Dev', 'SharePoint', 'SPFX']
summary: A guide on how to upgrade your older SPFX 1.10 and older spfx project  1.15 or newer
authors: ['default']
---

So I've needed to do this a couple of time so here's my step by step in upgrade from a SPFX superold project to the latest SPFX version.
This is a living post and a reminder to myself on how to do it, so it will be updated time to time when i find new things to do add :)

# How to Upgrade Your SPFX Project to the Latest Version

If you're working with SharePoint Framework (SPFX) projects, you might have encountered some challenges when trying to upgrade your project to the latest version of SPFX. Maybe you're not sure which packages need to be updated, how to deal with deprecated features, or how to fix any errors that might arise.

Don't worry, I've got you covered. In this blog post, I'll share with you my step-by-step guide on how to upgrade your SPFX project from a super old version to the latest one. This is a living post and a reminder to myself on how to do it, so I'll update it from time to time when I find new things to add.

## Step 1: Check Your Current SPFX Version

Before you start upgrading your project, you need to know which version of SPFX you're currently using. To do that, open your project folder and look for a file called package.json. This file contains information about your project dependencies and versions.

In the package.json file, look for a line that says `"@microsoft/sp-core-library": "x.x.x"`. The x.x.x part is your current SPFX version. For example, if it says `"@microsoft/sp-core-library": "1.4.1"`, then you're using SPFX 1.4.1.

You can also use the command `npm list @microsoft/sp-core-library` in your terminal or command prompt to check your current SPFX version.

## Step 2: Install NCU

NCU stands for npm-check-updates. It's a tool that helps you check if you have the latest versions of your npm packages and update them easily. You can install NCU globally by running this command:

`npm install -g npm-check-updates`

Once NCU is installed, you can use it to check for outdated packages in your project by running this command:

`ncu`

This will show you a list of packages that have newer versions available and what versions they are.

## Step 3: Update Your Packages

To update all your packages to their latest versions, run this command:

`ncu -u`

This will update your package.json file with the new versions of your packages.

Alternatively, you can update only specific packages by specifying their names after the ncu command. For example:

`ncu -u @microsoft/sp-webpart-base @microsoft/sp-build-web`

This will update only these two packages and leave the rest unchanged.

After updating your package.json file, run this command to install the new versions of your packages:

`npm install`

This will download and install the updated packages in your node_modules folder.

## Step 4: Remove TSLint File

TSLint is a tool that checks your TypeScript code for style and quality issues. However, TSLint has been deprecated since 2019 and replaced by ESLint as the recommended linter for TypeScript projects.

Therefore, if you have a TSLint file in your project (usually called tslint.json), you can delete it as it's no longer needed or supported by SPFX.

## Step 5: Update TSConfig File

TSConfig is a file that configures how TypeScript compiles your code into JavaScript. It's usually called tsconfig.json and located in the root folder of your project.

To make sure that TypeScript uses the correct compiler options for SPFX projects, you need to update some settings in this file.

First, look for a line that says `"extends": "./node_modules/@microsoft/rush-stack-compiler-x.x/includes/tsconfig-web.json"`. The x.x part is the version of rush-stack-compiler that TypeScript uses. You need
to change this line according
to
the following table:

| Current rush-stack-compiler | New rush-stack-compiler |
| --------------------------- | ----------------------- |
| 2.x                         | 3.x                     |
| 3.x                         | 4.x                     |

For example,
if
you have `"extends": "./node_modules/@microsoft/rush-stack-compiler-2.7/includes/tsconfig-web.json"`, change it
to
`"extends": "./node_modules/@microsoft/rush-stack-compiler-3.9/includes/tsconfig-web.json"`.

Next,
look
for any duplicate dev dependencies in
your package.json file,
such as rush-stack-compiler-\*,
and move them
to
the devDependencies section.
For example,

# How to Upgrade Your SPFx Project to React 17

React 17 is the latest version of the popular JavaScript library for building user interfaces. It comes with some new features and improvements, such as better support for concurrent mode, automatic JSX transform, and native event delegation. If you are using React in your SharePoint Framework (SPFx) project, you might want to upgrade to React 17 to take advantage of these benefits.

However, upgrading to React 17 is not as simple as changing a version number in your package.json file. There are some steps you need to follow to ensure a smooth transition and avoid breaking changes. In this blog post, we will guide you through these steps and show you how to upgrade your SPFx project to React 17.

## Step 1: Use SPFx Version 1.13 or Higher

The first step is to make sure that you are using SPFx version 1.13 or higher. This is because SPFx 1.13 introduced support for React 17 and TypeScript 4.x, which are required for upgrading your project. I personally always recommend using the latest one

To check your SPFx version, run the following command in your project folder:

# Using latest Graph module: If using MS-graph, update client code to import MSGraphClientV3

Microsoft Graph is a powerful API that connects multiple services and devices across Microsoft 365, Windows, and Enterprise Mobility + Security . It enables developers to build intelligent apps that interact with millions of users and access rich, people-centric data and insights.

One of the benefits of using Microsoft Graph is that it provides a unified endpoint, https://graph.microsoft.com, for accessing data and services from various Microsoft cloud sources. However, this also means that developers need to keep up with the changes and updates in the API versions and features.

Recently, Microsoft announced a new version of the Microsoft Graph REST API: v3.0. This version introduces some breaking changes and new capabilities that affect how developers use MS-graph in their applications.

One of the breaking changes is that MS-graph no longer supports importing MSGraphClient from @microsoft/sp-http package. Instead, developers need to import MSGraphClientV3 from @microsoft/sp-graph-client package. This change ensures that developers can use the latest features and improvements in MS-graph v3.0.

If you are using MS-graph in your client code, you need to update your import statement as follows:

```Javascript
import { MSGraphClientV3 } from '@microsoft/sp-http';

    this.props.context.msGraphClientFactory
      .getClient('3')
      .then((client: MSGraphClientV3) => { //do your stuff
      })
```

# Remove duplicate Packages:

Use npm dedupe to remove duplicates

You can use make use of CLI for m365 to make a full report of what you need to do:

https://pnp.github.io/cli-microsoft365/cmd/spfx/project/project-upgrade/

# Remove Workbench

Remove @microsoft/sp-webpart-workbench, this Isn't supported by SPFX newer than 12.1
