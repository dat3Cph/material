# Part III:  Expanding the Hotel API (team A)

It Thursday. First consider this: depending on how far you have gone during the previous and this week, you might need to catch up.

This exercise is building on top of these three exercises:

1. Thursday exercise week 1: [Exercise with Javalin and CRUD (Hotel Exercise)](../1_rest/Exercise_wed_thur.md)
2. [Hotel Exercise part 1: Rest Asssured](./Exercise_MonTue_HotelTest.md)
3. [Hotel Exercise part 2: Security](./Security_Wed_Thur_Security.md)

Luckily we have collected a "suggested" solution for all three exercises, so you can check them out, and learn from them. They are all in the same Repo on different branches:

| Step | Exercise /tutorial | Github Repo branch |
|------|--------------------|-------------|
|1. |[Building the Hotel API](../1_rest/Exercise_wed_thur.md) | [main](https://github.com/dat3Cph/hotel_exercise_rest/tree/main) |
|2. |[Testing a Rest API](../../setup/testContainerSetup.md) | [restassured](https://github.com/dat3Cph/hotel_exercise_rest/tree/restassured) |
|3. | [Securing Rest APIs](../../setup/securitySetup.md)| [security_jon](https://github.com/dat3Cph/hotel_exercise_rest/tree/security_jon)|

![Bates hotel](./images/bates_hotel.jpg)

## Thursday exercise

And now to this days exercise. The purpose is for you to get better acquainted with the architecture and code base.

Our German developer team has sent us some further requirements. So we need to develop the functionality of the Hotel API further:

Use the `security_jon` branch as a starting point - or better - use your own version of it. Then implement these requirements:

Requirements:

1. We would like add a room size in squaremeters for each room. Make sure that you implement this extension all the way through. From Entity, DTO, DAO, test etc.
2. We would like a new endpoint, so you can request all rooms within a given price range. For instance between 700 and 900.
3. The Rest Assured Tests for `HotelControllerTest` does not test for the `RouteRoles.MANAGER`. Please add a new user to the
the test who has that role, and test that you can
create a new hotel entity with that user.
4. The last bit is a little tricky. We would like
to add a Rest Assured test for the `UserController`. It would be great to have an automated test on the `login` and `register` methods. See if you can crack that nut. You have to be a litte creative. But give it a shot.

After this: see you all on Friday - and then have a great autumn holiday.