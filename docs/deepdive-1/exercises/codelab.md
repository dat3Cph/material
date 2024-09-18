---
title: CodeLab
description: Deep Dive I CodeLab Exercise
layout: default
nav_order: 2
parent: Exercises
grand_parent: Java Deep Dive I
permalink: /deepdive-1/exercises/codelab/
---

# Deep Dive I CodeLab Exercise

Work in progress ....

This CodeLab exercise is designed to help you practice the concepts you have learned in the Java Deep Dive I module on day-1. You will be working on a series of tasks that involve Java Streams, Java Time API, and maybe Lambdas. We will also practice [pair programming](../../toolbox/sys/projectmanagement/pairprogramming.md) and collaboration using Github.

![Pair programming](./images/pairprogramming.gif)

## Exercise Overview

## Instructions

### 1. Team up (2 x 2)

1. Team up in pairs of 2
2. Find another pair to team up with
3. Create a team of 4 people in Moodle

### 2. Setup the development environment (one per team of 2 x 2)

1. One team member should fork [Flight data Repo](https://github.com/dat3Cph/flightapp) - a simple application that reads a CSV file with flight data and calculates the total flight time for each airline.]
2. Add all team members as collaborators to the forked repository
3. Protect the `main` branch and the `develop` branch from pushing directly to it. Only allow Pull Requests to merge into these branches.
4. Every team member should clone the forked repository to their local machine
5. Checkout the develop branch (each member)

### 4. Get aqainted with the code

1. Run the application (find the Main class in `FlightReader`) and see how it works
2. Look at the code and understand how it works. How does the duration of the flights get calculated and more? You might want to
know more about the [Lombok library](../../toolbox/java/deepdive/lombok.md) and how it is used in the code to simplify getters, setters, and more.
3. Look at the json file and discuss the structure of the data with your team
4. Make sure that the data in the json file correlates with the data printed in the console
5. Find the unit-test and run it.
6. See if you can understand the test and what it is testing. Could it be improved?

### 5. Identify tasks, break them down and assign to pair programmers as Issues in Github

Inspiration for first round tasks:

1. Add a new feature (e.g. calculate the **average flight time** for a specific airline. For example, calculate the average flight time for all flights operated by Lufthansa)
2. Add a new feature (e.g. calculate the **total flight time** for a specifc airline. For example, calculate the total flight time for all flights operated by Lufthansa)

### 6. Start working on the tasks (round 1)

1. Create a branch off the `develop` branch for each task
2. Work on the tasks in pairs

### 7. Pull request

1. Create a Pull Request to merge the task branch into the `develop` branch
2. Assign the Pull Request to the other pair for review

### 8. Review ([description of how to conduct code reviews using pull requests](../../toolbox/sys/projectmanagement/codereviews.md))

1. Review the Pull Request
2. Provide feedback
3. Merge the Pull Request and delete the branch

### 9. Repeat

1. Identify the next tasks (get inspiration from the list below)
2. Repeat steps 5-8 for the next tasks

## Inspiration for tasks

1. Add a new feature (make a list of flights that are operated between two specific airports. For example, all flights between Fukuoka and Haneda Airport)
2. Add a new feature (make a list of flights that leaves before a specific time in the day. For example, all flights that leave before 08:00)
3. Add a new feature (calculate the average flight time for each airline)
4. Add a new feature (make a list of all flights sorted by arrival time)
5. Add a new feature (calculate the total flight time for each airline)
6. Add a new feature (make a list of all flights sorted by duration)
7. Refactor the code where needed. Make sure that the code is clean and easy to read.
