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
Table Publications {
  PublicationID int [pk]
  Title varchar [not null]
  PublicationType varchar [not null]
  PublicationDate varchar [not null]
  Authors varchar [not null]
  ProjectID int [ref: > ResearchProjects.ProjectID, not null]
}
```

```
Table PublicationDetails {
  PublicationDetailID int [pk]
  PublicationVenue varchar [not null]
  DOI varchar [not null]
  PublicationID int [ref: > Publications.PublicationID, not null]
}
```

```
Table Authors {
  AuthorID int [pk]
  FirstName varchar [not null]
  LastName varchar [not null]
  Title varchar [not null]
}
```

```
Table Publications_Authors {
  PublicationAuthorID int [pk]
  PublicationID int [ref: > Publications.PublicationID, not null]
  AuthorID int [ref: > Authors.AuthorID, not null]
}
```

```
Table SupportServices {
  SupportServiceID int [pk]
  ServiceName varchar [not null]
  Description varchar [null]
  ContactInfo varchar [not null]
  Website varchar [null]
  CategoryService varchar [not null]
}
```

```
Table StudentResourceInteractions {
  InteractionID int [pk]
  InteractionDate varchar [not null]
  Details varchar [not null]
  StudentID int [ref: > Students.StudentID, not null]
  SupportServiceID int [ref: > SupportServices.SupportServiceID, not null]
}
```

```
Table TutoringSessions {
  SessionID int [pk]
  Subject varchar [not null]
  Date date [not null]
  Duration varchar [not null]
  Notes varchar [null]
  SupportServiceID int [ref: > SupportServices.SupportServiceID, not null]
  StudentID int [ref: > Students.StudentID, not null]
}
```

```
Table CounselingAppointments {
  AppointmentID int [pk]
  AppointmentType varchar [not null]
  Counselor varchar [not null]
  Date date [not null]
  Duration varchar [not null]
  Notes varchar [null]
  SupportServiceID int [ref: > SupportServices.SupportServiceID, not null]
  StudentID int [ref: > Students.StudentID, not null]
}
```

```
Table MentalHealthSupport {
  SupportID int [pk]
  SupportType varchar [not null]
  Topic varchar [not null]
  Date date [not null]
  Duration varchar [not null]
  Notes varchar [null]
  SupportServiceID int [ref: > SupportServices.SupportServiceID, not null]
  StudentID int [ref: > Students.StudentID, not null]
}
```

```
Table LibraryResources {
  LibraryResourceID int [pk]
  Title varchar [not null]
  Author varchar [not null]
  Publisher varchar [not null]
  PublicationDate date [not null]
  Description varchar [null]
  Type varchar [not null]
  Format varchar [not null]
  AccessLink varchar [null]
  Location varchar [null]
}
```

```
Table StudentOrganizations {
  OrganizationID int [pk]
  OrganizationName varchar [not null]
  Description varchar [null]
  DepartmentID int [ref: > Departments.DepartmentID, not null]
}
```

```
Table StudentMemberships {
  MembershipID int [pk]
  Role varchar [not null]
  StudentID int [ref: > Students.StudentID, not null]
  OrganizationID int [ref: > StudentOrganizations.OrganizationID, not null]
}
```

```
Table Clubs {
  ClubID int [pk]
  ClubFocus varchar [not null]
  MeetingFrequency varchar [not null]
  MeetingLocation varchar [not null]
  OrganizationID int [ref: > StudentOrganizations.OrganizationID, not null]
}
```

```
Table SportsTeams {
  SportsTeamID int [pk]
  Sport varchar [not null]
  Coach varchar [null]
  PracticeSchedule varchar [not null]
  OrganizationID int [ref: > StudentOrganizations.OrganizationID, not null]
}
```

```
Table Buildings {
  BuildingID int [pk]
  BuildingName varchar [not null]
  Address varchar [not null]
  Description varchar [null]
}
```

```
Table Facilities {
  FacilityID int [pk]
  FacilityType varchar [not null]
  Capacity varchar [not null]
  BuildingID int [ref: > Buildings.BuildingID, not null]
}
```

```
Table Classrooms {
  ClassroomID int [pk]
  RoomNumber varchar [not null]
  AccessibilityFeatures varchar [null]
}
```

```
Table Laboratories {
  LabID int [pk]
  LabName varchar [not null]
  Equipment varchar [not null]
  MaintenanceSchedule varchar [null]
}
```

```
Table Offices {
  OfficeID int [pk]
  RoomNumber varchar [not null]
  Occupant varchar [null]
}
```

```
Table CommonAreas {
  CommonAreaID int [pk]
  CommonAreaType varchar [not null]
  Amenities varchar [null]
}
```

```
Table Equipment {
  EquipmentID int [pk]
  EquipmentName varchar [not null]
  ModelNumber varchar [not null]
  SerialNumber varchar [not null]
  PurchaseDate varchar [not null]
  LabID int [ref: > Laboratories.LabID, not null]
}
```

```
Table RoomReservations {
  ReservationID int [pk]
  ReservationDate varchar [not null]
  StartTime varchar [not null]
  EndTime varchar [not null]
  ReservedBy varchar [not null]
  Purpose varchar [not null]
  FacilityID int [ref: > Facilities.FacilityID, not null]
  RequestedByUserID int [ref: > UserAccounts.UserID, not null]
}
```

```
Table UserAccounts {
  UserID int [pk]
  Username varchar [unique, not null]
  Password varchar [not null]
  Email varchar [unique, not null]
  StudentID int [ref: > Students.StudentID, null]
  DepartmentStaffID int [ref: > DepartmentStaff.StaffID, null]
}
```

```
Table UserRoles {
  UserRoleID int [pk]
  UserRoleName varchar [unique, not null]
}
```

```
Table UserRolesLink {
  UserRolesLinkID int [pk]
  UserID int [ref: > UserAccounts.UserID, not null]
  UserRoleID int [ref: > UserRoles.UserRoleID, not null]
}
```

```
Table FinancialAccounts {
  AccountID int [pk]
  AccountName varchar [unique, not null]
  AccountType varchar [not null]
}
```

```
Table TuitionFees {
  TuitionFeeID int [pk]
  AcademicYear varchar [not null]
  Amount float [not null]
  ProgramID int [ref: > Programs.ProgramID, not null]
}
```

```
Table Scholarships {
  ScholarshipID int [pk]
  ScholarshipName varchar [not null]
  Description varchar [null]
  FundingAccountID int [ref: > FinancialAccounts.AccountID, not null]
}
```

```
Table StudentFinancialAid {
  StudentFinancialAidID int [pk]
  AwardAmount float [not null]
  Semester varchar [not null]
  StudentID int [ref: > Students.StudentID, not null]
  ScholarshipID int [ref: > Scholarships.ScholarshipID, not null]
}
```

```
Table FinancialTransactions {
  TransactionID int [pk]
  TransactionDate datetime [not null]
  Amount float [not null]
  Description varchar [null]
  FromAccountID int [ref: > FinancialAccounts.AccountID, null]
  ToAccountID int [ref: > FinancialAccounts.AccountID, null]
  StudentID int [ref: > Students.StudentID, null]
  DepartmentStaffID int [ref: > DepartmentStaff.StaffID, null]
  ScholarshipID int [ref: > Scholarships.ScholarshipID, null]
}
```
