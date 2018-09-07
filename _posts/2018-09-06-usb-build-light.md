---
layout: post
title: "Build Visibility and Remote Teams"
description: ""
category:
tags: [CI]
---

Working in a global team presents a lot of challenges around co-location with regards to build status visibility. When working remote, you don't always have the luxury of hardware like strobe lights. Or even co-workers alerting you when an incident transpires. The Virtual Team Survey Report cites the pace of decision making as one of the most significant challenges faced by global teams. Being able to react to a build issue quickly starts by understanding a problem has occurred.

On a coaching engagement where the majority of my team was remote I had the opportunity to meet my team members physically. During one of these visits, I shared with a developer the value of visualizing build status. This conversation was heading in the direction of what I thought to be a dead end; as he was the only member working from his location.

As I was de-boarding from my weekly taxi home, I received a text message from the excited developer about a personal USB notifier he found online called [Blink(1)](https://blink1.thingm.com/). This device is programmable and contains a LED light on both sides. Without hesitation, the developer purchased the USB and began developing a tool to integrate with his teams' continuous integration server.

By experimenting with Blink(1), the team realized they didn't need co-location to utilize a build notification tool. The group became more responsive to builds when an issue arose. They even used Blink(1) to alert them of quality gate concerns from SonarQube after check-in. Overall, the team found their collaboration increased by having a visible light as a symbol for an opportunity to communicate.

If you're interested in using Blink(1) in your projects, I've created a Java wrapper called [Blinky](https://github.com/SkylarWatson/blinky) on GitHub. Blinky doesn't currently have support for Windows.