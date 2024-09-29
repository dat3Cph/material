---
title: Hotel API Test
description: Rest Assured, JUnit 5, and Hamcrest matchers to test all the finished endpoints.
layout: default
nav_order: 2
grand_parent: Rest API Test and Security
parent: Exercises
permalink: /rest-test-security/exercises/hotel-test/
---

# Part I: Testing the Hotel API

Our German developer team has developed the first version of an API for a hotel chain. It's not quite finished yet. Germans think in terms of quality. Hence, we've been tasked with adding integration tests to the project, so we can meet the usual standards. "Quadratisch praktisch gut," as they say:

1. Based on your code from last week (Hotel API), you should now add integration tests to the project. You should use Rest Assured, JUnit 5, and Hamcrest matchers to test all the finished endpoints.

![Bates hotel](./images/bates_hotel.jpg)

## Part II: Integration Testing of Database Functionality (DAO methods)

3. Ideally, it would have been best to start here with DAO-tests (think about why), but life doesn't always follow 'best practices'. Now we have to retroactively create tests for our DAO methods. Start with a couple and see how many you can achieve.

## Various hints and things worth considering

### Test Database

- Our application persists data in a Postgres database. It's not 'best practice' to conduct tests in a running production database, so we need to somehow run our integration tests on a different database, ensuring we don't corrupt the actual data. This is typically done in one of two ways:

   1. Either we create a database/schema (as it's called) in Postgres to run our tests in - and then we need to get our EntityManagerFactory to issue connections to the test database.
   2. Or, we run an entirely new Postgres database server in a separate Docker Container for our tests (on a new port). This way, we completely avoid mixing the test and development environments.

For the current semester, we choose to go with test-containers. We have [documented how you set up testcontainers](../../setup/testContainerSetup.md) in this description.
