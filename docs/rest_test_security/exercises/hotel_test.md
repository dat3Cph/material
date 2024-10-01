---
title: Hotel API Test
description: Rest Assured, JUnit 5, and Hamcrest matchers to test all the finished endpoints.
layout: default
nav_order: 5
grand_parent: Rest API Test and Security
parent: Exercises
permalink: /rest-test-security/exercises/hotel-test/
---
# Codelab: Hotel API Test

## Part I: Integration Testing of Database Functionality (DAO methods)

Our German developer team has developed the first version of an API for a hotel chain. It's not quite finished yet. Germans think in terms of quality. Hence, we've been tasked with adding integration tests to the project, so we can meet the usual standards. "Quadratisch praktisch gut," as they say.

![Bates hotel](./images/bates_hotel.jpg)

Based on your code from last week (Hotel API), you should now add **integration tests** to the project.

Ideally, it would have been best to start here with DAO-tests (think about why), but life doesn't always follow 'best practices'. Now we have to retroactively create tests for our DAO methods. Start with a couple and see how many you can achieve.

## Part II: Testing the Hotel API

Next step is to test the **endpoints**. This is also an integration-test, but now you need to use Rest Assured, JUnit 5, and Hamcrest matchers to test all the finished endpoints. Also remember that testing endpoints require a running server, so you need to start the server (Jetty) before running the tests, and also closing it down after the tests are done.

## Various hints and things worth considering

### Test Database

- Our application persists data in a Postgres database. It's not 'best practice' to conduct tests in a running production database, so we need to somehow run our integration tests on a different database, ensuring we don't corrupt the actual data. This is typically done in one of two ways:

   1. Either we create a database/schema (as it's called) in Postgres to run our tests in - and then we need to get our EntityManagerFactory to issue connections to the test database. We did that on 2nd semester.
   2. Or, we run an entirely new Postgres database server in a separate Docker Container for our tests (on a new port). This way, we completely avoid mixing the test and development environments.

For the current semester, we choose to go with **test-containers**. This is a library that allows us to run a Docker container with a Postgres database for our tests. This way, we can ensure that our tests are run in a controlled environment, and we don't have to worry about corrupting the development database.

Our **HibernateConfig** file should be set up to use the test database when running tests. This can be done in one of two ways:

1. By setting `Hibernateconfig.setTest(true)` before creating the EntityManagerFactory. This is the easiest way to do it. But not the most elegant.
2. By using dependency injection to inject the EntityManagerFactory into the DAOs. This way, we can create a separate EntityManagerFactory for the tests and inject it into the DAOs. This will take some refactoring of your code, so maybe skip this for now.

### Startcode and code for inspiration

- In class we have been working on a project that is similar to this one. You can find the code here:

      https://github.com/jonbertelsen/dogs/tree/testHoldB

   You can clone a specific branch like this:

      git clone --branch testHoldB https://github.com/jonbertelsen/dogs

- In case your own hotel api is not up'n running, you can clone this one:

      https://github.com/jonbertelsen/hotel_api 

  and make it your own.

Viel Glück with the tests! 🍀
