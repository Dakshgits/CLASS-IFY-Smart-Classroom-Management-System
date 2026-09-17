# CLASS-IFY — Smart Classroom Management System

### *Intellect | Functionality | Youth*

A modern full-stack **Smart Classroom Management System (SCMS)** designed to digitize and simplify essential academic and classroom operations such as attendance, notices, assignments, resources, events, analytics, and student-faculty communication.

Built as a final-year BCA project for **SIH1625 — Smart Classroom Management Software for Enhanced Learning Environments**.

---

## 📌 Project Overview

Traditional classroom management often depends on manual attendance registers, scattered announcements, spreadsheets, messaging groups, and disconnected academic records. These approaches can be time-consuming, difficult to maintain, and vulnerable to errors or proxy attendance.

**CLASS-IFY** provides a centralized web-based platform where students and faculty can manage important classroom activities through a single system.

The system focuses on:

* Secure authentication and role-based access
* Time-bound QR attendance
* GPS-based attendance verification
* Academic notices and assignments
* Resource/library management
* Events and scheduling
* Attendance and performance analytics
* Automated academic notifications
* Online quizzes and learning activities

The system is designed using the **MERN stack** and follows a modular architecture so additional functionality can be introduced later without redesigning the complete application.

---

# 🎯 Problem Statement

The project is based on **SIH1625 — Smart Classroom Management Software for Enhanced Learning Environments**.

Educational institutions often face problems such as:

* Manual and time-consuming attendance processes
* Proxy attendance
* Scattered notices and academic information
* Difficulty tracking assignments and deadlines
* Lack of centralized resource management
* Difficulty monitoring attendance and academic performance
* Lack of timely reminders for students
* Separate systems or platforms for different classroom activities

CLASS-IFY addresses these problems by bringing the major classroom-management workflows into one centralized application.

---

# 💡 Proposed Solution

CLASS-IFY uses a role-based web application where students and faculty access different functionalities according to their roles.

### Student

Students can:

* Register and securely log in
* View their dashboard
* Mark attendance using a time-bound QR code
* Verify classroom presence using GPS
* View attendance percentage
* View notices and announcements
* Access assignments and academic resources
* View upcoming events and schedules
* Track academic performance
* Participate in quizzes

### Faculty

Faculty can:

* Securely log in
* Manage classroom sessions
* Generate time-limited QR codes for attendance
* Monitor attendance records
* Manually manage attendance when required
* Post notices and announcements
* Create and manage assignments
* Manage academic resources
* Manage events
* View attendance and performance analytics
* Create/manage quizzes

---

# ⭐ Key Features

## 1. 🔐 JWT Authentication & Role-Based Access

The application uses **JWT (JSON Web Token) authentication** for secure user sessions.

### Authentication Flow

```text
User
  ↓
Login / Registration
  ↓
Credentials Validation
  ↓
Password Verification
  ↓
JWT Generation
  ↓
Secure Authentication Cookie
  ↓
Authenticated Request
  ↓
JWT Verification Middleware
  ↓
Role Authorization
  ↓
Protected Resource
```

### Security Features

* JWT-based authentication
* Password hashing using `bcryptjs`
* HTTP-only cookies for authentication tokens
* Protected routes
* Role-based access control
* Separate permissions for students and faculty
* Backend authorization middleware

This prevents users from accessing functionality that does not belong to their assigned role.

---

# 2. 📱 QR Code + GPS Attendance System

Attendance is one of the core features of CLASS-IFY.

Instead of relying on a static QR code, the system uses a **time-bound/expiring QR code** generated for a particular classroom session.

The architecture specifies rolling QR tokens that refresh periodically and GPS validation using the **Haversine distance calculation**.

### Attendance Flow

```text
Faculty Starts Class
        ↓
Attendance Session Created
        ↓
Temporary QR Code Generated
        ↓
QR Displayed in Classroom
        ↓
Student Scans QR
        ↓
QR Token Validation
        ↓
Expiry Check
        ↓
Student Authentication Check
        ↓
Browser GPS Permission
        ↓
GPS Coordinates Obtained
        ↓
Distance From Classroom Calculated
        ↓
Location Validation
        ↓
Attendance Marked
```

### QR Security

Each QR attendance session contains a temporary token associated with the classroom/session.

The backend verifies:

* Whether the QR token is valid
* Whether the token has expired
* Whether the attendance session is active
* Whether the student is authenticated
* Whether the student has already marked attendance

This makes simply sharing an old QR code ineffective after its validity period.

### GPS Verification

After scanning the QR code, the student's browser requests location permission through the **Geolocation API**.

The student's coordinates are compared with the classroom's configured coordinates.

The system calculates the distance using the **Haversine formula**.

```text
Student GPS Coordinates
          +
Classroom GPS Coordinates
          ↓
   Haversine Calculation
          ↓
    Distance Check
          ↓
 Within Allowed Radius?
      ↙          ↘
    YES           NO
     ↓             ↓
Attendance      Rejected
  Marked
```

GPS therefore acts as an additional verification layer rather than relying only on the QR code.

> **Note:** GPS accuracy can vary depending on the device, browser, network, and indoor environment. Therefore, the system should use a configurable location radius and provide a faculty/manual fallback when verification cannot be completed.

---

# 3. 📊 Attendance Management

Faculty can manage attendance sessions and records for their classes.

Students can view:

* Subject-wise attendance
* Attendance history
* Attendance percentage
* Present/absent records
* Attendance trends

Attendance records can be associated with:

* Student
* Subject
* Faculty
* Date
* Attendance session
* Timestamp
* Verification status

---

# 4. 📚 Resource & Library Management

The system provides centralized management of academic resources.

Faculty/authorized users can manage available resources while students can view availability and request resources where applicable.

### Example Resources

* Books
* Study material
* Classroom resources
* Teaching aids

The system maintains information such as:

* Resource name
* Category
* Total quantity
* Available quantity
* Issue status
* Request information
* Due date

MongoDB transactions can be used for operations where maintaining resource availability consistently is important.

---

# 5. 📢 Notice & Academic Feed

CLASS-IFY provides a centralized academic feed instead of relying on multiple messaging groups.

Faculty can publish:

* Notices
* Announcements
* Lecture resources
* Important academic information
* Assignment-related updates

Students can access relevant information from their dashboard.

---

# 6. 📝 Assignment Management

Faculty can create and manage assignments.

An assignment can contain:

* Title
* Description
* Subject
* Instructions
* Submission deadline
* Supporting files/resources

Students can view assignments and their deadlines from their dashboard.

The system can maintain submission-related information so academic activities remain organized in one place.

---

# 7. 📅 Events & Scheduling

CLASS-IFY provides an event section for academic and institutional activities.

Faculty can create events containing:

* Event title
* Description
* Date
* Start time
* End time
* Location
* Additional information

Students can view upcoming events through the centralized event section.

---

# 8. 📈 Performance & Analytics Dashboard

The analytics module provides visual representations of academic information.

Possible dashboard data includes:

* Attendance percentage
* Attendance trends
* Assignment records
* Quiz performance
* Academic progress

Charts can be implemented using **Recharts or Chart.js**.

### Example Dashboard

```text
              STUDENT DASHBOARD
                     │
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
  Attendance     Assignments    Performance
       │             │             │
       ↓             ↓             ↓
   Percentage      Deadlines      Charts
       │             │             │
       └─────────────┼─────────────┘
                     ↓
              Academic Overview
```

---

# 9. 🔔 Automated Alerts & Notifications

The system can provide automated reminders for important academic activities.

Examples include:

* Low attendance notifications
* Assignment deadline reminders
* Important notices
* Upcoming academic activities

Scheduled background tasks can be handled using **Node-Cron**, while email notifications can be implemented using **Nodemailer**.

The architecture specifies automated checks for attendance thresholds and approaching deadlines.

---

# 10. 🧠 Quiz Zone

CLASS-IFY includes a basic online quiz module for student engagement and academic assessment.

Faculty can create subject-based questions.

Students can:

* Start quizzes
* Answer MCQs
* Submit responses
* View their scores
* Track quiz performance

Quiz information can be stored in MongoDB through a dedicated question-bank structure.

---

# 🏗️ System Architecture

CLASS-IFY follows a three-layer architecture.

```text
┌───────────────────────────────────────┐
│              FRONTEND                 │
│                                       │
│ React + Vite + Tailwind CSS           │
│ React Router + Context/Redux          │
│ QR Scanner + Geolocation API          │
└──────────────────┬────────────────────┘
                   │
                   │ HTTP / REST API
                   │
┌──────────────────▼────────────────────┐
│              BACKEND                  │
│                                       │
│ Node.js + Express.js                  │
│ JWT Authentication                    │
│ RBAC Middleware                       │
│ Attendance Validation                 │
│ QR Token Validation                   │
│ GPS / Haversine Verification          │
│ Business Logic                        │
└──────────────────┬────────────────────┘
                   │
                   │ Mongoose
                   │
┌──────────────────▼────────────────────┐
│              DATABASE                 │
│                                       │
│ MongoDB / MongoDB Atlas               │
│                                       │
│ Users                                 │
│ Attendance Sessions                   │
│ Attendance Records                    │
│ Courses                               │
│ Assignments                           │
│ Notices                               │
│ Resources                             │
│ Events                                │
│ Quizzes                               │
│ Notifications                         │
└───────────────────────────────────────┘
```

---

# 🛠️ Technology Stack

## Frontend

| Technology                  | Purpose                       |
| --------------------------- | ----------------------------- |
| React.js                    | Frontend application          |
| Vite                        | Development/build tooling     |
| React Router DOM            | Client-side routing           |
| Tailwind CSS                | Styling and responsive UI     |
| Context API / Redux Toolkit | State management              |
| Framer Motion               | UI animations                 |
| html5-qrcode                | QR code scanning              |
| Geolocation API             | Student location verification |
| Recharts / Chart.js         | Analytics dashboards          |
| Lucide React                | UI icons                      |

The architecture also identifies `html5-qrcode` and the browser Geolocation API for QR attendance implementation.

## Backend

| Technology     | Purpose                     |
| -------------- | --------------------------- |
| Node.js        | Server runtime              |
| Express.js     | Backend framework           |
| REST API       | Client-server communication |
| JSON Web Token | Authentication              |
| bcryptjs       | Password hashing            |
| cookie-parser  | Cookie handling             |
| Node-Cron      | Scheduled tasks             |
| Nodemailer     | Email notifications         |
| Multer         | File handling               |

## Database

| Technology    | Purpose                   |
| ------------- | ------------------------- |
| MongoDB       | Primary database          |
| MongoDB Atlas | Cloud database            |
| Mongoose      | ODM and schema management |

## Development & Testing

| Tool    | Purpose                   |
| ------- | ------------------------- |
| Git     | Version control           |
| GitHub  | Source-code collaboration |
| Postman | API testing               |
| VS Code | Development environment   |

---

# 🗄️ Database Structure

The database is designed around separate collections for different application modules.

### Main Collections

```text
Users
 ├── Authentication
 ├── Role
 └── Profile

AttendanceSessions
 ├── Faculty
 ├── Subject
 ├── Classroom
 ├── QR Token
 ├── Expiry
 └── Session Status

AttendanceRecords
 ├── Student
 ├── Session
 ├── Timestamp
 ├── GPS Verification
 └── Attendance Status

Courses
 ├── Subject
 ├── Faculty
 └── Students

Assignments
 ├── Course
 ├── Faculty
 ├── Deadline
 └── Submissions

Notices
 ├── Course
 ├── Faculty
 └── Content

Resources
 ├── Resource Information
 ├── Quantity
 └── Availability

Events
 ├── Title
 ├── Date
 └── Location

QuestionBanks
 ├── Course
 ├── Questions
 └── Answers

Notifications
 ├── User
 ├── Type
 └── Status
```

Indexes can be added to frequently queried fields to improve performance.

---

# 🔒 Security

Security is an important part of the system.

### Authentication

* Passwords are hashed using `bcryptjs`
* JWT is used for authentication
* Authentication tokens are stored using secure HTTP-only cookies
* Protected backend routes require authentication

### Authorization

Role-based middleware verifies whether the authenticated user has permission to access a particular endpoint.

```text
Request
   ↓
JWT Verification
   ↓
Authenticated User
   ↓
Role Check
   ↓
Permission Granted?
   ↓
Controller
```

### Attendance Security

The attendance system adds multiple validation layers:

```text
Authenticated Student
        +
Valid QR Token
        +
QR Not Expired
        +
Active Attendance Session
        +
GPS Location Verification
        +
Duplicate Attendance Check
        ↓
    Attendance
     Accepted
```

This multi-step approach is designed to reduce unauthorized and proxy attendance.

---

# 📁 Suggested Project Structure

```text
CLASS-IFY/
│
├── client/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── layouts/
│   │   ├── context/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── utils/
│   │   └── App.jsx
│   │
│   └── package.json
│
├── server/
│   ├── controllers/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   ├── services/
│   ├── utils/
│   ├── config/
│   ├── jobs/
│   └── server.js
│
├── README.md
├── .gitignore
└── package.json
```

---

# 🔄 Attendance Implementation Details

The attendance system is one of the most important technical components of CLASS-IFY.

### Faculty Side

```text
Faculty Login
     ↓
Select Subject
     ↓
Start Attendance Session
     ↓
Backend Creates Session
     ↓
Temporary QR Token Generated
     ↓
QR Displayed
     ↓
Token Expires After Defined Time
```

### Student Side

```text
Student Login
     ↓
Open Attendance
     ↓
Scan QR
     ↓
QR Token Sent to Backend
     ↓
Token + Expiry Validation
     ↓
Request Browser Location
     ↓
Get GPS Coordinates
     ↓
Calculate Distance
     ↓
Check Classroom Radius
     ↓
Create Attendance Record
```

### Important Backend Checks

The backend should never trust only the frontend.

The server should validate:

1. Student authentication
2. JWT validity
3. QR token validity
4. QR expiry
5. Attendance session status
6. Student eligibility for the subject
7. Duplicate attendance
8. GPS coordinates
9. Allowed classroom radius
10. Attendance timestamp

---

# 🧪 Testing Strategy

The project will be tested at multiple levels.

### Frontend Testing

* UI component testing
* Form validation
* Responsive design testing
* QR scanner testing
* GPS permission handling

### Backend Testing

* Authentication APIs
* JWT validation
* RBAC authorization
* QR generation and validation
* QR expiry
* Attendance APIs
* GPS distance validation
* Duplicate attendance prevention

### API Testing

Postman can be used to test:

```text
POST   /api/auth/register
POST   /api/auth/login
POST   /api/auth/logout

POST   /api/attendance/session
GET    /api/attendance/session/:id
POST   /api/attendance/mark
GET    /api/attendance/student/:id

POST   /api/notices
GET    /api/notices

POST   /api/assignments
GET    /api/assignments

GET    /api/events
POST   /api/events
```

---

# 🌐 Deployment

The application can be deployed using:

### Frontend

**Vercel**

### Backend

**Render / Railway**

### Database

**MongoDB Atlas**

### Deployment Architecture

```text
                  Internet
                     │
          ┌──────────┴──────────┐
          ↓                     ↓
       Vercel                 Render
      Frontend                Backend
          │                     │
          └──────────┬──────────┘
                     ↓
                MongoDB Atlas
```

Environment variables should be used for sensitive configuration.

Example:

```env
MONGO_URI=
JWT_SECRET=
CLIENT_URL=
COOKIE_SECRET=
EMAIL_USER=
EMAIL_PASSWORD=
```

> `.env` files must never be committed to GitHub.

---

# 👥 Team & Responsibilities

| Team Member            | Role               | Responsibility              |
| ---------------------- | ------------------ | --------------------------- |
| **Daksh Kumar Saxena** | Frontend Developer | React, UI Integration       |
| **Nitesh Singh Negi**  | Backend Developer  | Node.js, Express, APIs      |
| **Sumit Sonkar**       | Database Manager   | MongoDB, Mongoose           |
| **Vansh Singh**        | UI/UX Designer     | Interface & User Experience |

---

# 🌿 GitHub Collaboration Workflow

The project is developed collaboratively using Git and GitHub.

### Recommended Workflow

```text
main
 │
 ├── frontend
 │
 ├── backend
 │
 ├── database
 │
 └── ui-design
```

Each team member should work on their own feature branch.

### Example

```bash
git clone <repository-url>

git checkout -b feature/attendance

git add .

git commit -m "Add QR attendance session"

git push origin feature/attendance
```

Then create a Pull Request into `main`.

### Rules

* Do not directly push unfinished work to `main`
* Pull the latest changes before starting work
* Use meaningful commit messages
* Create separate branches for features
* Review Pull Requests before merging
* Never commit `.env` or credentials
* Keep frontend and backend changes organized

---

# 🗺️ Development Roadmap

## Phase 1 — Foundation

* [x] Project planning
* [x] Architecture design
* [x] UI/UX planning
* [ ] Repository setup
* [ ] Frontend/backend initialization

## Phase 2 — Authentication

* [ ] User registration
* [ ] Login
* [ ] JWT authentication
* [ ] HTTP-only authentication cookies
* [ ] Role-based authorization
* [ ] Protected routes

## Phase 3 — Attendance

* [ ] Faculty attendance session
* [ ] Expiring QR generation
* [ ] QR scanner
* [ ] QR token validation
* [ ] Browser GPS verification
* [ ] Haversine distance calculation
* [ ] Duplicate attendance prevention
* [ ] Attendance history
* [ ] Attendance percentage

## Phase 4 — Academic Management

* [ ] Notices
* [ ] Assignments
* [ ] Resources/library
* [ ] Events
* [ ] Student dashboard
* [ ] Faculty dashboard

## Phase 5 — Analytics & Learning

* [ ] Performance analytics
* [ ] Attendance analytics
* [ ] Automated reminders
* [ ] Quiz module

## Phase 6 — Testing & Deployment

* [ ] API testing
* [ ] Integration testing
* [ ] Security testing
* [ ] Responsive testing
* [ ] Production deployment
* [ ] Final documentation

---

# 📌 Project Scope

The primary scope of CLASS-IFY is to provide a centralized classroom-management platform with practical, implementable features.

### Core Implementation

* JWT authentication
* Student and Faculty role management
* QR-based attendance
* Expiring/time-bound QR codes
* GPS-based attendance verification
* Attendance history and percentage
* Notices
* Assignments
* Resource/library management
* Events
* Performance analytics
* Automated notifications
* Quiz functionality

### Deliberately Not Claimed as Current Implementation

The following advanced concepts are **not treated as completed features** in this README:

* Facial recognition
* Fingerprint/biometric attendance
* AI chatbot
* Multiplayer learning games
* XP/streak systems
* Real-time peer messaging
* Emergency hardware integration
* Smart-board integration

These can be considered future enhancements only if the team decides to implement them.

---

# 🔮 Future Enhancements

After completing the core system, the architecture can be extended with:

* Administrator dashboard
* AI-powered learning assistant
* Advanced predictive analytics
* Mobile application
* More advanced anti-proxy verification
* Real-time collaborative learning
* Advanced gamification
* Additional institutional integrations

These are **future possibilities and are not part of the current core implementation**.

---

# 📊 Expected Outcomes

CLASS-IFY aims to:

* Reduce manual classroom-management work
* Make attendance faster and more structured
* Reduce proxy attendance through expiring QR + GPS verification
* Centralize academic information
* Improve assignment and deadline visibility
* Provide better attendance and performance tracking
* Improve communication between students and faculty
* Provide a scalable foundation for future classroom-management features

---

# 🎓 Academic Information

**Project:** CLASS-IFY — Smart Classroom Management System
**Problem Statement:** SIH1625
**Course:** Bachelor of Computer Applications (BCA)
**College:** Bareilly College, Bareilly
**University:** Mahatma Jyotiba Phule Rohilkhand University
**Session:** 2026–2027
**Project Guide:** Roma Mam

---

# 📚 References & Documentation

The project uses official documentation for its major technologies and libraries.

* React.js
* Node.js
* Express.js
* MongoDB
* Mongoose
* Tailwind CSS
* html5-qrcode
* Recharts / Chart.js
* Node-Cron
* Nodemailer

The uploaded architecture specification identifies the main implementation libraries and their respective purposes, including React, Socket.io, MongoDB/Mongoose, Tailwind CSS, html5-qrcode, Recharts, node-cron, and Nodemailer.

---

# 🚀 Project Vision

> **CLASS-IFY aims to transform traditional classroom management into a centralized, secure, and student-friendly digital experience.**

The project focuses on combining essential classroom operations into one platform while keeping the architecture modular enough to support future improvements.

### CLASS-IFY

**Intellect | Functionality | Youth**

---
