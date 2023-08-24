# School Exercise (JPQL)

### 1. Set up the data model as shown in the diagram below.

<img src="../images/school_eer_model.png" alt="School ERD" width="500"/>

### 2. Using JPQL find solutions to the following challenges:

**Part 1:**
1. Find all Students in the System with the first name Anders
2. Find (using JPQL) all Students in the system with the last name And 
3. Find (using JPQL) the total number of students, for a semester given the semester name as a parameter. 
4. Find (using JPQL) the total number of students that has a particular teacher. 
5. Find (using JPQL) the teacher who teaches the most semesters. 
6. Find the semester that has the fewest students

**Part 2:**
1. Create a StudentInfo class with the following properties: 
    - `fullName`
    - `studentId`
    - `thisSemesterName`
    - `thisSemesterDescription`
2. Add a public constructor that takes all the necessary arguments to initialize the properties.
3. Now create a method (using JPQL) with the following signature to return a list of all Students, encapsulated as StudentInfo.
    - `public StudentInfo getAllStudentInfo(int id)`