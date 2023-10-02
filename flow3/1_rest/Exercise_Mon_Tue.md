# Day 1 and 2 - Javalin
## Exercise with javalin and CRUD

1. Setup project with javalin
2. Create a new javalin server running on port 7007 that can handle the following routes representing a dog ressource:
   - GET /dogs // Returns all dogs from an in-memory collection of dogs (You decide the data structure)
   - GET /dog/{id} // Returns a specific dog based on the id
   - POST /dog // Creates a new dog
   - PUT /dog/{id} // Updates an existing dog
   - DELETE /dog/{id} // Deletes an existing dog
3. Setup the server so that all dog endpoints are under the path `/api/dogs`
4. Let the dogs live in a map in memory with the id as key and the dog as value.
5. Create a new class called `DogDTO.java` in a `src/main/java/dtos` folder with fields: `id`, `name`, `breed`, `gender`, `age`.
6. Create a new class called `DogController.java` in a `src/main/java/controllers` folder with the following methods:
   - getAllDogs()
   - getDogById()
   - createDog()
   - updateDog()
   - deleteDog()
7. Make sure that the server returns json for all endpoints.
8. Make sure to return 404 when a dog is not found.