# Academic-Institution-Database-Design
Academic Institution Database, Database Design, Schema

# Introduction and Overview of the database design
My database meets the needs of storing and managing a large amount of data for a famous university in Vietnam.

The university offers undergraduate and graduate programs across numerous departments.
Each department houses a faculty body comprising professors, lecturers, and teaching assistants.
These faculty members conduct a variety of courses, each of which has a set of learning outcomes, a syllabus, and a grading scheme.
Students can enroll in multiple courses per semester and are evaluated based on their performance in assignments, quizzes, exams, and projects.

In addition to teaching, faculty members are actively engaged in research.
They lead research projects, sometimes funded by external grants, and produce publications such as journal articles, conference papers, and books.

The university offers resources such as tutoring services, career counseling, and mental health support.
The university tracks student interactions with these resources to better understand and meet their needs.

The university library offers a vast collection of books, journals, and digital resources, all of which are cataloged and available for students and faculty.

Students can participate in student organizations, clubs and sports teams at the university.

The university's facilities include multiple buildings, classrooms, laboratories, offices, and common areas.

The university manages finances including tuition, scholarships for students and payroll for faculty and staff.
The university keeps detailed records of all financial transactions.

# The Entity Relationship Diagram (ERD)
![Entity Relationship Diagram Image](Academic_Institution_Diagram.png)

## The link to a diagram:
### https://dbdiagram.io/d/669905b58b4bb5230eb34266

# Detail Entites Diagram
### The database consists of 45 separate entities to meet the university's database system needs.

```
Table Students {
  StudentID int [pk]
  FirstName varchar [not null]
  LastName varchar [not null]
  DateOfBirth date [not null]
  Email varchar [unique, not null]
  PhoneNumber varchar [not null]
  NationalID varchar [unique, not null]
  CurrentAddress varchar [not null]
  PermanentAddress varchar [not null]
  ProgramID int [ref: > Programs.ProgramID, not null]
}
```

```
Table Faculties {
  FacultyID int [pk]
  FacultyName varchar [not null]
}
```

```
Table Departments {
  DepartmentID int [pk]
  DepartmentName varchar [not null]
  FacultyID int [ref: > Faculties.FacultyID, not null]
}
```

```
Table DepartmentStaff {
  StaffID int [pk]
  FirstName varchar [not null]
  LastName varchar [not null]
  Email varchar [unique, not null]
  PhoneNumber varchar [not null]
  Title varchar [not null]
  PaySalary float [not null]
  PayFrequency varchar [not null]
  DepartmentID int [ref: > Departments.DepartmentID, not null]
}
```

```
Table Programs {
  ProgramID int [pk]
  ProgramName varchar [not null]
  Degree varchar [not null]
  DepartmentID int [ref: > Departments.DepartmentID, not null]
}
```

```
Table Courses {
  CourseID int [pk]
  CourseName varchar [not null]
  Description varchar [null]
  Credits varchar [not null]
  ProgramID int [ref: > Programs.ProgramID, not null]
  LearningOutcomesID int [ref: > LearningOutcomes.LearningOutcomesID, not null]
}
```

```
Table CourseMaterials {
  MaterialID int [pk]
  MaterialType varchar [not null]
  Description varchar [null]
  FilePath varchar [not null]
  CourseID int [ref: > Courses.CourseID, not null]
}
```

```
Table LearningOutcomes {
  LearningOutcomesID int [pk]
  Description varchar [null]
  CourseID int [ref: > Courses.CourseID, not null]
}
```

```
Table CourseOfferings {
  CourseOfferingID int [pk]
  Semester varchar [not null]
  Year year [not null]
  CourseID int [ref: > Courses.CourseID, not null]
  ProgramID int [ref: > Programs.ProgramID, not null]
}
```

```
Table Enrollments {
  EnrollmentID int [pk]
  StudentID int [ref: > Students.StudentID, not null]
  CourseID int [ref: > Courses.CourseID, not null]
  Semester varchar [not null]
  Year year [not null]
}
```

```
Table Evaluations {
  EvaluationID int [pk]
  EvaluationType varchar [not null]
  Weight float [not null]
  Score float [not null]
  EnrollmentID int [ref: > Enrollments.EnrollmentID, not null]
}
```

```
Table EvaluationDetails {
  EvaluationDetailID int [pk]
  DueDate date [not null]
  Rubric varchar [not null]
  EvaluationID int [ref: > Evaluations.EvaluationID, not null]
}
```

```
Table Transcripts {
  TranscriptID int [pk]
  Grade float [not null]
  StudentID int [ref: > Students.StudentID, not null]
  EnrollmentID int [ref: > Enrollments.EnrollmentID, not null]
}
```

```
Table Grants {
  GrantID int [pk]
  GrantingAgency varchar [not null]
  Amount float [not null]
  StartDate datetime [not null]
  EndDate datetime [not null]
}
```

```
Table ResearchProjects {
  ProjectID int [pk]
  ProjectTitle varchar [not null]
  Description varchar [null]
  DepartmentID int [ref: > Departments.DepartmentID, not null]
  GrantID int [ref: > Grants.GrantID, not null]
}
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```