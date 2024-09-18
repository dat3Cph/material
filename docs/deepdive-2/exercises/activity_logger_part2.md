---
title: Activity Logger part 2
description: Java Deep Dive II Exercise DTO and JSON
layout: default
nav_order: 9
has_children: false
grand_parent: Java Deep Dive II
parent: Exercises
permalink: /deepdive-2/exercises/activity-logger-part-2/
---

# Activity Logger Exercise Part 2

This is the Friday exercise for Java Deep Dive II. The exercise is a continuation of the exercise from Tuesday. Your task is to persist the data from the external APIs in a database.

- The first part of the exercise can be found [here](./activity_logger_part1.md)
- In case you haven't completed the first part, you can find a solution [here](https://github.com/jonbertelsen/activitylogger) that you can use as a starting point.

Just to recap. The json from the WeatherInfo API looks like this:

```json
{
    "LocationName": "Roskilde",
    "CurrentData": {
        "temperature": 13.4,
        "skyText": "Hovedsageligt klar",
        "humidity": "",
        "windText": "13.7 m/s"
    }
}
```

The json from the CityInfo API looks like this (we have removed a lot of attributes to make things simpler):

```json
[
{
    "id": "12337669-dbab-6b98-e053-d480220a5a3f",
    "primærtnavn": "Roskilde",
    "href": "https://api.dataforsyningen.dk/steder/12337669-dbab-6b98-e053-d480220a5a3f",
    "visueltcenter": [
        12.08713962,
        55.63659446
    ]
}
]
```

Also, the `ActivityDTO`, that includes all data should look something like this:

```java
public class ActivityDTO {
    private LocalDate exerciseDate;
    private Activity exerciseType;
    private LocalTime timeOfDay;
    private double duration;  // In hours, for example
    private double distance;  // In kilometers or miles
    private String comment;
    private CityInfoDTO cityInfo;
    private WeatherInfoDTO weatherInfo;
}
```

## The exercise

1. Create a database with JPA and persist the data from the external APIs in the database. You should probably create the entities for `Activity`, `CityInfo` and `WeatherInfo`. Remember to add the Entities to the HibernateConfig file. Think about the relationships between Activity, CityInfo, and WeatherInfo when designing your entities. Consider using one-to-many or one-to-one relationships as needed, and ensure you annotate them properly with JPA annotations like @OneToMany, @ManyToOne, etc.
2. You should create a ActivityDAO class that can persist the data in the database. Send in the DTO's and let the DAO class persist the data. You might want to return DTO's with the ID's from the database when creating new entries.
3. Create an `ActivityService` that can call the DAO class and persist the data in the database.
4. Perform number of requests to the APIs and persist the data in the database. You can use the `ActivityService` to do this.
5. Add a getAll method to the DAO class that can return all activities from the database. Use the Jackson ObjectMapper to convert your DTOs to JSON. For example, you can use objectMapper.writeValueAsString(dto) to convert an object into a JSON string.

## Extra

1. Create integrations tests for the DAO class as needed.
