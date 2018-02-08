---
layout: post
title: "Testing Pyramid"
description: ""
category:
tags: [junit, testing]
---

As developers, we want our unit tests to fail for a single reason.  When we're unable to achieve this, we spend countless hours or days fixing tests that failed by side-effect. Part of the reason this schism happens is that testing scenarios are written at the wrong level. Many developers and organizations suffer from this and are stuck in a trap of the 'traditional” testing model (inverted pyramid.)

In this model a team drives the majority of their tests through the UI; either using manual testing strategies and tools like Selenium as needed. Integration tests are represented in this model in the middle tier; though these tests aren't as prevalent. Last but not least, unit tests make an appearance at the bottom of the “traditional” pyramid.

<img src="/images/testing-triangle-1.svg?sanitize=true" width="400"/>

Let's assume we have a project comprised of three layers of code; a controller layer, service, and repository. For argument sake, let's say each layer has ten code paths and every code path talks to one another. In this example, if we were to write a unit for every condition we'd need 10³ tests to cover all scenarios. That's 1,000 tests to write and maintain.

<img src="/images/testing-triangle-2.svg?sanitize=true" width="400"/>

Introducing a single defect would result in one-hundred failing test. Making it difficult to determine more quickly what broke.

If instead each layer was tested independently the number of unit tests necessary for each layer's reduced to one-hundred. Leaving each layer having tests for specific units of work within its defined boundary.

<img src="/images/testing-triangle-3.svg?sanitize=true" width="400"/>

These tests don't cover the interaction between layer boundaries (i.e., controller → service and service → repository), for that, we need an integration test. These integration tests don't need to be elaborate or cover specific scenario's because those verifications have already been performed at a unit level.

<img src="/images/testing-triangle-4.svg?sanitize=true" width="400"/>

Introducing an end-to-end integration test ensures communication throughout the layers of code is appropriately handled. These types of tests are often referred to as smoke tests; a test or series of tests that is used to verify basic high-level functionality.

<img src="/images/testing-triangle-5.svg?sanitize=true" width="400"/>

As a result of writing specific tests the amount necessary to write (in this example) has been reduced from 1,000 down to 303. Whereas before when defects introduced, we'd have 100 failing tests, now we'd only have one.

<img src="/images/testing-triangle-6.svg?sanitize=true" width="400"/>

By writing tests to have a single focus you can begin to reduce the complexity and number of scenario's required. Effectively, you've turned your turning your testing pyramid right-side up.