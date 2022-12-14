---
date: '2022-12-13T11:51:21.726Z'
title: Update your old SPFX project to latest SPFX version
description: Upgrade your older SPFX 1.10 and older spfx project to 1.16.1
tags: ['Power Automate', 'SharePoint', 'Lists']
summary: A guide on how to upgrade your older SPFX 1.10 and older spfx project to 1.16.1 abd newer
authors: ['default']
---

So I've needed to do this a couple of time so here's my step by step in upgrade from a SPFX superold project to the latest SPFX version.
This is a living post and a reminder to myself on how to do it, so it will be updated time to time when i find new things to do add :)

Here is my tips common things I need to do!:

1. Download and install Ncu, This can be used to check if you have the latest packages, as most probably needs to be updated

https://www.npmjs.com/package/npm-check-updates

2. Remove TSlint file, This file isn't needed anymore and can be deleted.

3. Update tsconfig, make sure that the compiler uses rush-stack-compiler-4.5, move any duplicate dev dependenices such as rush-stack-compiler-\*:

- npm install -D @microsoft/rush-stack-compiler-4.5

Add tsconfig:

- "extends": "./node_modules/@microsoft/rush-stack-compiler-4.5/includes/tsconfig-web.json",
  ![Image](/static/images/assets/UpgradeSPFXProject/1.png)

4. Remove @microsoft/sp-webpart-workbench, this Isn't supported by SPFX newer than 12.1:

5. Use react 17.0.2

   ![Image](/static/images/assets/UpgradeSPFXProject/2.png)

6. If using MS-graph, update client code to import MSGraphClientV3

```Javascript
import { MSGraphClientV3 } from '@microsoft/sp-http';

    this.props.context.msGraphClientFactory
      .getClient('3')
      .then((client: MSGraphClientV3) => { //do your stuff
      })
```

7. Use npm dedupe to remove duplicates

8. You can use make use of CLI for m365 to make a full report of what you need to do:

https://pnp.github.io/cli-microsoft365/cmd/spfx/project/project-upgrade/
