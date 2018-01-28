---
layout: default
---

# NPM Config registry setting

The amount of times I have cut and pasted this line... ugh. I'll include it so I don't have to search for it or use up precious resources of what's left in my brain.

## General format:

    npm config set registry=<registry url>

## NPM module in MyGet for GEMS:

    npm config set registry="https://www.myget.org/F/quartz/npm/"
    npm config set registry="https://www.myget.org/F/moist-package-feed/npm/"
    npm config set registry="https://www.myget.org/F/zircon/npm/"

## NPM Default - https://www.npmjs.com/package/angular:

    npm config set registry="https://registry.npmjs.org/"

## Working with private npm registry feeds

If a MyGet npm feed is marked as private, it will always require authentication. To setup authentication, run the following commands:

    npm adduser --registry=https://www.myget.org/F/zircon/npm/
    npm config set always-auth true 