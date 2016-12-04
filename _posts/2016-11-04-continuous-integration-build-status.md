---
layout: post
title: "Continuous Integration Build Status"
description: ""
category:
tags: [CI]
---
I'm writing this entry to expand on issues of failing builds and responsibilities that team members should consider owning. The following definition may be useful for those who aren't familiar with the term Continuous Integration.

_“Continuous Integration (CI) is a development practice that requires developers to integrate code into a shared repository several times a day. Each check-in is then verified by an automated build, allowing teams to detect problems early.”_

_“By integrating regularly, you can detect errors quickly, and locate them more easily.”_

<a href="https://www.thoughtworks.com/continuous-integration">https://www.thoughtworks.com/continuous-integration</a>

I'd encourage everyone to check the status of their build server before pushing/promoting into version control. If the latest build that ran on CI failed, is it okay to promote your changes on top of the failing change-set? Of course there may be no process preventing us from doing so. But by continuously promoting during build failures, we begin to lose track of what problems exist in our systems. The build failures may originally present themselves as unrelated environmental issues and over time turn into a series of code, environment, or even configuration problems – effectively leaving us with little value from having our CI server.

We can have higher confidence in our systems if we all stop immediately and fix the build as soon as it fails. Fixing the failed build should be a shared responsibility among the team, regardless of who last pushed/promoted of why the last build failed.

It helps to have a visual indicator in the team area for build failures. I've seen this done different ways: having a build radiator opened in a browser tab, build radiator on a team monitor, or even having a strobe light that turns on while the build is failing.