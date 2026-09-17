# CLASS-IFY — Smart Classroom Management System

### *Intellect | Functionality | Youth*

A modern full-stack **Smart Classroom Management System (SCMS)** designed to centralize and simplify essential classroom and academic activities through a single web-based platform.

Developed as a final-year BCA project based on **SIH1625 — Smart Classroom Management Software for Enhanced Learning Environments**.

---

## 📌 Overview

Traditional classroom management often relies on manual attendance registers, scattered announcements, spreadsheets, and separate platforms for academic activities.

**CLASS-IFY** brings these activities together into one centralized system for students and faculty.

The system focuses on:

* Secure authentication and role-based access
* QR-based attendance with expiry
* GPS-based attendance verification
* Attendance tracking and analytics
* Notices and announcements
* Assignment management
* Resource and library management
* Events and scheduling
* Performance analytics
* Automated academic alerts
* Online quizzes

---

## 🎯 Problem Statement

Educational institutions can face several challenges with traditional classroom management:

* Time-consuming manual attendance
* Risk of proxy attendance
* Scattered academic notices and resources
* Difficulty tracking assignments and deadlines
* Limited visibility of attendance and performance
* Lack of centralized classroom information
* Delayed academic reminders

CLASS-IFY addresses these challenges through a centralized digital classroom-management platform.

---

## 💡 Objectives

The main objectives of CLASS-IFY are to:

* Provide secure authentication with role-based access.
* Automate classroom attendance using expiring QR codes.
* Add GPS verification to reduce unauthorized attendance.
* Centralize notices, assignments, and academic resources.
* Manage library and classroom resources.
* Provide event and schedule information.
* Track attendance and academic performance.
* Provide automated reminders for important academic activities.
* Provide quizzes for student learning and assessment.

---

# ⭐ Core Features

## 🔐 1. JWT Authentication & Role-Based Access

CLASS-IFY uses **JSON Web Tokens (JWT)** for authentication and role-based authorization.

### Authentication

* User registration and login
* Password hashing using `bcryptjs`
* JWT-based authentication
* HTTP-only cookies
* Protected routes
* Role-based authorization middleware

### User Roles

**Student**

* Access student dashboard
* View attendance
* Mark attendance
* Access academic information
* View assignments and events
* Participate in quizzes

**Faculty**

* Access faculty dashboard
* Create attendance sessions
* Generate attendance QR codes
* Manage attendance
* Post notices
* Manage assignments and resources
* Manage events
* View analytics
* Manage quizzes

---

# 📱 2. QR + GPS Attendance

Attendance is implemented using **two verification layers**:

> **Expiring QR Code + GPS Location Verification**

### Attendance Flow

```text
Faculty
   ↓
Start Attendance Session
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
Student Authentication
   ↓
Browser GPS Verification
   ↓
Haversine Distance Calculation
   ↓
Location Within Allowed Radius?
   ↓
Attendance Marked
```

### QR Verification

The QR code is associated with an active attendance session and has a limited validity period.

The backend checks:

* Token validity
* Token expiry
* Active session
* Student authentication
* Duplicate attendance

This prevents an expired or reused QR code from being accepted.

### GPS Verification

After scanning the QR code, the student's browser requests location access through the **Geolocation API**.

The system compares:

* Student's GPS coordinates
* Classroom's configured coordinates

The distance is calculated using the **Haversine formula**.

Attendance is accepted only when the student is within the configured classroom radius.

> GPS accuracy may vary depending on the device, browser, network, and indoor environment. A faculty/manual attendance option can therefore be used as a fallback when location verification is unavailable.

---

# 📊 3. Attendance Management

Students can view their attendance information, including:

* Subject-wise attendance
* Attendance history
* Present/absent records
* Attendance percentage
* Attendance trends

Faculty can:

* Start attendance sessions
* Generate temporary QR codes
* Monitor attendance
* View attendance records
* Handle attendance manually when required

---

# 📢 4. Notices & Academic Feed

A centralized academic feed provides students with important information without depending on multiple communication platforms.

Faculty can publish:

* Notices
* Announcements
* Lecture resources
* Academic updates

Students can view relevant information from their dashboard.

---

# 📝 5. Assignment Management

Faculty can create and manage assignments containing:

* Assignment title
* Description
* Subject
* Instructions
* Deadline
* Supporting resources

Students can view assignments and track upcoming deadlines.

---

# 📚 6. Resource & Library Management

CLASS-IFY provides centralized management of academic and library resources.

The system can maintain:

* Resource information
* Total quantity
* Available quantity
* Issue/request status
* Due dates

This helps organize resource availability and usage.

---

# 📅 7. Events & Scheduling

The event module provides a centralized place for academic and institutional activities.

Events can contain:

* Title
* Description
* Date
* Start time
* End time
* Location

Students can view upcoming events from the application.

---

# 📈 8. Performance Analytics

The analytics dashboard provides visual information about academic performance.

It can include:

* Attendance percentage
* Attendance trends
* Assignment records
* Quiz performance
* Academic progress

Charts and visualizations can be implemented using **Recharts / Chart.js**.

---

# 🔔 9. Automated Alerts

The system can provide automated reminders for important academic activities.

Examples:

* Low attendance alerts
* Assignment deadline reminders
* Important academic notifications

Scheduled background tasks can be handled using **Node-Cron**, with email notifications supported through **Nodemailer**.

---

# 🧠 10. Quiz Zone

The Quiz Zone provides basic online assessments for students.

Faculty can create subject-based questions, while students can:

* Attempt quizzes
* Answer MCQs
* Submit responses
* View scores
* Track quiz performance

Quiz questions and results are stored through the application's database.

---

# 🏗️ System Architecture

CLASS-IFY follows a three-layer architecture:

```text
┌───────────────────────────────┐
│           FRONTEND            │
│                               │
│ React + Vite                  │
│ Tailwind CSS                  │
│ React Router                  │
│ QR Scanner                    │
│ Geolocation API               │
│ Analytics                     │
└───────────────┬───────────────┘
                │
                │ REST API
                ↓
┌───────────────────────────────┐
│            BACKEND            │
│                               │
│ Node.js + Express.js          │
│ JWT Authentication            │
│ RBAC Middleware               │
│ QR Validation                 │
│ GPS Verification              │
│ Business Logic                │
└───────────────┬───────────────┘
                │
                │ Mongoose
                ↓
┌───────────────────────────────┐
│           DATABASE            │
│                               │
│ MongoDB / MongoDB Atlas       │
│                               │
│ Users                         │
│ Attendance                    │
│ Assignments                   │
│ Notices                       │
│ Resources                     │
│ Events                        │
│ Quizzes                       │
│ Notifications                 │
└───────────────────────────────┘
```

---

# 🛠️ Technology Stack

### Frontend

| Technology                  | Purpose                    |
| --------------------------- | -------------------------- |
| React.js                    | User interface             |
| Vite                        | Frontend development/build |
| React Router DOM            | Application routing        |
| Tailwind CSS                | Styling                    |
| Context API / Redux Toolkit | State management           |
| Framer Motion               | UI animations              |
| html5-qrcode                | QR scanning                |
| Geolocation API             | Location verification      |
| Recharts / Chart.js         | Analytics                  |
| Lucide React                | Icons                      |

### Backend

| Technology    | Purpose                     |
| ------------- | --------------------------- |
| Node.js       | Server runtime              |
| Express.js    | Backend framework           |
| REST API      | Client-server communication |
| JWT           | Authentication              |
| bcryptjs      | Password hashing            |
| cookie-parser | Cookie handling             |
| Node-Cron     | Scheduled tasks             |
| Nodemailer    | Email notifications         |
| Multer        | File handling               |

### Database & Services

| Technology          | Purpose                |
| ------------------- | ---------------------- |
| MongoDB             | Primary database       |
| MongoDB Atlas       | Cloud database         |
| Mongoose            | Database modeling      |
| Cloudinary / AWS S3 | File and media storage |
| Postman             | API testing            |
| Git & GitHub        | Version control        |

---

# 🗄️ Database

The system uses MongoDB with separate collections for different modules.

### Main Collections

```text
Users
AttendanceSessions
AttendanceRecords
Courses
Assignments
Notices
Resources
Events
QuestionBanks
Notifications
```

Relationships between collections are managed using MongoDB references and Mongoose schemas.

Indexes can be used for frequently queried fields such as student attendance and resource availability.

---

# 🔒 Security

Security is incorporated at both the authentication and application levels.

### Authentication Security

* Password hashing with `bcryptjs`
* JWT authentication
* HTTP-only cookies
* Protected API routes
* Role-based authorization

### Attendance Security

Attendance requires multiple checks:

```text
Valid User
    +
Valid JWT
    +
Valid QR
    +
QR Not Expired
    +
Active Session
    +
GPS Verification
    +
Duplicate Check
    ↓
Attendance Accepted
```

The backend performs the important validation rather than relying solely on frontend checks.

---

# 📁 Project Structure

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
│   │   └── utils/
│   └── package.json
│
├── server/
│   ├── controllers/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   ├── services/
│   ├── config/
│   ├── jobs/
│   └── server.js
│
├── README.md
└── .gitignore
```

---

# 🧪 Testing

The application will be tested through:

### Frontend

* UI testing
* Form validation
* Responsive design testing
* QR scanner testing
* GPS permission handling

### Backend

* Authentication testing
* JWT validation
* Role authorization
* QR validation
* QR expiry
* GPS distance validation
* Attendance validation
* Duplicate attendance prevention
* API testing using Postman

---

# 🌐 Deployment

The planned deployment architecture is:

```text
          Users
            │
            ↓
     ┌──────────────┐
     │    Vercel    │
     │   Frontend   │
     └──────┬───────┘
            │
            ↓
     ┌──────────────┐
     │ Render /     │
     │ Railway      │
     │   Backend    │
     └──────┬───────┘
            │
            ↓
     ┌──────────────┐
     │   MongoDB    │
     │     Atlas    │
     └──────────────┘
```

Sensitive configuration should be stored using environment variables and should not be committed to the repository.

---

# 📌 Project Scope

The current project focuses on the following core functionality:

* JWT authentication
* Student and Faculty roles
* Expiring QR attendance
* GPS-based attendance verification
* Haversine distance checking
* Attendance tracking
* Notices
* Assignments
* Resource/library management
* Events
* Performance analytics
* Automated alerts
* Quiz functionality

Features outside this scope should not be considered part of the current implementation unless they are subsequently developed and integrated.

---

# 🔮 Future Enhancements

Potential future improvements include:

* Administrator role
* AI-based learning assistant
* Advanced analytics
* Mobile application
* Advanced learning and gamification features
* Additional institutional integrations

---

# 👥 Team

| Member                 | Role                                         |
| ---------------------- | -------------------------------------------- |
| **Daksh Kumar Saxena** | Frontend Developer • React / UI Integration  |
| **Nitesh Singh Negi**  | Backend Developer • Node.js / Express / APIs |
| **Sumit Sonkar**       | Database Manager • MongoDB / Mongoose        |
| **Vansh Singh**        | UI/UX Designer • Interface & User Experience |

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

# 🚀 Vision

**CLASS-IFY** aims to make classroom management more organized, secure, and accessible by bringing essential academic operations into one centralized digital platform.

### *Intellect | Functionality | Youth*
