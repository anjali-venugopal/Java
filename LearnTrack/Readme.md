# LearnTrack

A console-based **Student & Course Management System** built with Core Java. Admins can manage students, courses, and enrollments through a menu-driven terminal interface. All data is stored in memory using `ArrayList`.

**Repository:** [github.com/anjali-venugopal/Java](https://github.com/anjali-venugopal/Java)

## Features

- Add, view, search, update, and deactivate students
- Add, view, and activate/deactivate courses
- Enroll students in courses and track enrollment status
- Graceful error handling for invalid input and missing records

## Project Structure

```
src/com/airtribe/learntrack/
├── Main.java
├── entity/         Student, Course, Enrollment
├── repository/     In-memory data storage (ArrayList)
├── service/        Business logic
├── exception/      Custom checked exceptions
├── util/           IdGenerator, InputValidator
├── constants/      MenuOptions, AppConstants
└── enums/          EnrollmentStatus, CourseStatus
```

## Class Diagram

```mermaid
classDiagram
    direction TB

    class Main {
        +main(String[] args)
        -run()
    }

  class Student {
        -int id
        -String firstName
        -String lastName
        -String email
        -String batch
        -boolean active
        +getDisplayName() String
    }

    class Course {
        -int id
        -String courseName
        -String description
        -int durationInWeeks
        -CourseStatus status
        +isActive() boolean
    }

    class Enrollment {
        -int id
        -int studentId
        -int courseId
        -LocalDate enrollmentDate
        -EnrollmentStatus status
    }

    class EnrollmentStatus {
        <<enumeration>>
        ACTIVE
        COMPLETED
        CANCELLED
    }

    class CourseStatus {
        <<enumeration>>
        ACTIVE
        INACTIVE
    }

    class StudentRepository {
        -ArrayList students
        +save(Student)
        +findById(int) Student
        +findAll() List
    }

    class CourseRepository {
        -ArrayList courses
        +save(Course)
        +findById(int) Course
        +findAll() List
    }

    class EnrollmentRepository {
        -ArrayList enrollments
        +save(Enrollment)
        +findById(int) Enrollment
        +findByStudentId(int) List
        +findAll() List
    }

    class StudentService {
        -StudentRepository studentRepository
        +addStudent()
        +listStudents()
        +findStudentById(int)
        +updateStudent()
        +deactivateStudent()
    }

    class CourseService {
        -CourseRepository courseRepository
        +addCourse()
        +listCourses()
        +findCourseById(int)
        +setCourseActiveStatus()
    }

    class EnrollmentService {
        -EnrollmentRepository enrollmentRepository
        -StudentRepository studentRepository
        -CourseRepository courseRepository
        +enrollStudent()
        +getEnrollmentsForStudent()
        +markEnrollmentCompleted()
        +markEnrollmentCancelled()
    }

    class IdGenerator {
        <<utility>>
        -static int studentIdCounter
        -static int courseIdCounter
        -static int enrollmentIdCounter
        +getNextStudentId() int
        +getNextCourseId() int
        +getNextEnrollmentId() int
    }

    class InputValidator {
        <<utility>>
        +requireNonEmpty()
        +parsePositiveInt()
    }

    class EntityNotFoundException {
        <<exception>>
    }

    class InvalidInputException {
        <<exception>>
    }

    class MenuOptions {
        <<constants>>
    }

    class AppConstants {
        <<constants>>
    }

    Exception <|-- EntityNotFoundException
    Exception <|-- InvalidInputException

    Course --> CourseStatus : uses
    Enrollment --> EnrollmentStatus : uses

    StudentRepository --> Student : stores
    CourseRepository --> Course : stores
    EnrollmentRepository --> Enrollment : stores

    StudentService --> StudentRepository : uses
    StudentService --> IdGenerator : uses
    CourseService --> CourseRepository : uses
    CourseService --> IdGenerator : uses
    EnrollmentService --> EnrollmentRepository : uses
    EnrollmentService --> StudentRepository : uses
    EnrollmentService --> CourseRepository : uses
    EnrollmentService --> IdGenerator : uses

    Main --> StudentService : uses
    Main --> CourseService : uses
    Main --> EnrollmentService : uses
    Main --> MenuOptions : uses
    Main --> AppConstants : uses
    Main --> InputValidator : uses
    Main ..> EntityNotFoundException : catches
    Main ..> InvalidInputException : catches
```

## Prerequisites

- JDK 17 or higher ([setup guide](docs/Setup_Instructions.md))

## How to Compile and Run

**IntelliJ IDEA:** Open the project, set JDK 17+, and run `com.airtribe.learntrack.Main`.

**Terminal** (from project root):

```bash
javac -d out -sourcepath src src/com/airtribe/learntrack/Main.java
java -cp out com.airtribe.learntrack.Main
```

## Documentation

| File | Description |
|------|-------------|
| [docs/Setup_Instructions.md](docs/Setup_Instructions.md) | JDK installation and Hello World |
| [docs/JVM_Basics.md](docs/JVM_Basics.md) | JDK, JRE, JVM, and bytecode |
| [docs/Design_Notes.md](docs/Design_Notes.md) | Design decisions and architecture |

## Submission

| Item | Details |
|------|---------|
| **GitHub repository** | [https://github.com/anjali-venugopal/Java](https://github.com/anjali-venugopal/Java) |
| **Visibility** | Repository must be **public** |
| **Pull request** | Submit a PR from this repository to the cohort template repository as instructed by your mentor |

## Author

**Anjali Venugopal** — Airtribe Java Fundamentals
