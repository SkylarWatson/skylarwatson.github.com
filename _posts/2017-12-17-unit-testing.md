---
layout: post
title: "Testing Pyramid"
description: ""
category:
tags: [junit, testing]
---

Developers who find themselves unable to write a test that fails for a single reason may suffer from the “traditional” testing model (inverted pyramid.)

In this model a team drives the majority of their tests through the UI; either using manual testing strategies and/or through tools like, Selenium. Integration tests are also represented in the “traditional” testing model in the middle tier. Though these tests aren't as prevalent. Last but not least, unit tests make an appearance at the bottom of the “traditional” pyramid.

<img src="/images/testing-triangle-1.svg?sanitize=true" width="400"/>

Let's assume we have a project comprised of three layers of code; a controller layer, service, and repository. For argument sake, let's say each layer has ten code paths and every code path talks to one-another. In this example if we were to write a test for every condition we'd need 10³ tests to cover all scenarios. That's 1,000 tests to write and maintain.

<img src="/images/testing-triangle-2.svg?sanitize=true" width="400"/>

Introducing a single defect would result in an one-hundred failing tests. Making it difficult to determine quickly what broke.

If instead, each layer was tested independently the amount of unit tests necessary for each layer's reduced to one-hundred. Leaving each layer only having tests for specific units of work within its defined boundary.

<img src="/images/testing-triangle-3.svg?sanitize=true" width="400"/>

This doesn't cover the interaction between layer boundaries (i.e., controller → service and service → repository), for that an integration test is written. These integration tests don't need to be complex or cover specific scenario's because those verifications have already been performed at an unit level.

<img src="/images/testing-triangle-4.svg?sanitize=true" width="400"/>

Introducing an end-to-end integration test ensures communication throughout the layers of code's properly handled. These types of tests are often referred to as smoke tests; a test or series of test that are used to verify basic high-level functionality.

<img src="/images/testing-triangle-5.svg?sanitize=true" width="400"/>

As a result of writing specific tests the amount necessary to write (in this example) have been reduced from 1,000 down to 303. Whereas before when a defect was introduced we'd have 100 failing tests, now we'd only have one.

<img src="/images/testing-triangle-6.svg?sanitize=true" width="400"/>

By writing tests to have a single focus you can began to reduce the complexity and number of scenario's required. Effectively turning your testing pyramid right-side up.