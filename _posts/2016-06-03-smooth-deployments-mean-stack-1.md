---
layout: post
title: Smooth Deployments - MEAN Stack - 1
date: 2016-06-03 04:59:17.000000000 +05:00
tags:
- Github
- Deployments
- Automation
status: in progress
type: post
published: false
author:
  login: mohuk
  email: mohammad.umair.k@gmail.com
  display_name: mohuk

  first_name: 'Mohammad Umair'
  last_name: 'Khan'
---
I have been posting about Angular JS a lot with my last post being more than a year ago. This time I wanted to talk something about servers and deployments. There is a lot of shady stuff people are putting into when it comes to deployments. From what I have seen, there has been manual copying, zipping of files. Smarter ones amongst those are writing a Windows Batch or Bash script to *rsync* code on to the servers. Configurations going hayware with **Cross Origin Resource Sharing** available to every freaking origin in the world. Sometimes there are deployment processes so bad that they are exposing their *private keys* and *secrects* as static files. Honestly, there is a fair bit of need to align everything up. So let's talk about deploying a standard NodeJS API + Angular JS SPA application to a linux server but we'd break this up in multiple posts with the first one being deploying your server and things to take care of.

### Prepping your API repository for deployment
Everything starts from ground zero which in our case is our repository.

# 1: package.json
Each NodeJS application has a `package.json` file which contains various metadata for the application. The important thing to understand from a deployment perspective is are the sections `dependencies` and `devDependencies`. `dependencies` are the packages which the application uses while executing its code e.g. `mongoose`, a package for object modeling with MongoDB. `devDependencies` are packages required only during development and are not part of the actual code e.g. `eslint`, a linting, styling tool for Javascript. We need to make sure our packages are in the correct sections because there is no need for `devDependencies` to be installed in a deployed application.

# 2: gitignore
Source control should always ignore a few things. We can set this up by populating our `.gitignore` file. Most importantly it should ignore folders which are populated by package managers which in our case is `node_modules`.

Second most important thing are the `private keys`, `certificates` and `configs`. These should never be made part of the source control. Imagine if your source control account is compromised, it would open all the doors to the servers.

Finally, ignores should contain editor generated folders e.g. `.idea` and log files.

You can find standard language specific `.gitignore` files online.

# 3: scripts
Standard deployment scripts should be ready. There can be completely separate post on the options we have for creating these scripts but it doesn't matter what you choose if it is there. Wiring it up with `npm scripts` has its own benefits.

### Creating a deploy key


