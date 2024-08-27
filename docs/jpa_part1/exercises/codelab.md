---
title: CodeLab
description: JPA part 1 CodeLab Exercise
layout: default
nav_order: 2
parent: Exercises
grand_parent: JPA Part 1
permalink: /jpa-part-1/exercises/codelab/
---

# JPA part I - CodeLab Exercise

This CodeLab exercise is designed to help you practice the concepts you have learned in the JPA 1 module on day 1. You will be working on a series of tasks that involve Java Persistence API, with Entities and DAOs. We will also practice [pair programming](../../toolbox/sys/projectmanagement/pairprogramming.md) and collaboration using Github.

![Pair programming](../../deepdive-1/exercises/images/pairprogramming.gif)

## Exercise Overview

## Instructions

### 1. Team up (2 x 2)

1. Team up in pairs of 2
2. Find another pair to team up with
3. Create a team of 4 people in Moodle

### 2. Setup the development environment (one per team of 2 x 2)

1. One team member should create a new github repository and make everybody else collaborators on the repo.
2. Then create a new maven project with a [Hibernate Config file](https://github.com/HartmannDemoCode/jpademo/blob/main/src/main/java/dk/cphbusiness/persistence/HibernateConfig.java) and the appropriate [pom.xml](https://github.com/HartmannDemoCode/jpademo/blob/main/pom.xml) dependencies for using with JPA.
3. Create a new branch: `develop` and Protect the `main` branch and the `develop` branch from pushing directly to it. Only allow Pull Requests to merge into these branches.
4. Every team member should clone the new repository to their local machine
5. Checkout the develop branch (each member)

### 3. Connecting to the database

1. Each member should create a database in your docker environment with postgres called `jpademo`.
2. Set up the HibernateConfig file to connect to the database.
3. Create a new Entity class called `Person` with the following fields:
   - id (int)
   - name (String)
   - age (int)
4. Create a new DAO class called `PersonDAO` with the following methods:

- `createPerson(Person person)`

5. Create a new Main class and test that you can add a new person to your database.

### 4. The assignment

You are going to create a new student management system. We need to be able to persist data about students and their courses.
We need to have information about each student such as their name, phone number, email, address, status, date of birth, date of enrollment and whatever you think is relevant. We also need to have information about the courses they are taking such as the name of the course, the teacher, the semester, the classroom, the time of the course and whatever you think is relevant.
Since we have not yet learned how to create relationships/references between entities, you can choose to just store the id of the courses in the student entity for now (we will learn how to do it the right way in JPA week 2).

### 5. Identify tasks, break them down and assign to pair programmers as Issues in Github

The following tasks are suggestions for the first round of tasks. You can add more tasks as you go along.

1. Create new student
2. Create new course
3. Update student information
4. Update course information
5. Delete student
6. Delete course
7. List all students
8. List all courses
9. List all courses for a specific student
10. List all students for a specific course (use streams and filters for this one)
11. Come up with more tasks as you go along ...

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

1. Identify the next tasks
2. Repeat steps 5-8 for the next tasks
