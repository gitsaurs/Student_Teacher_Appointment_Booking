# 🎓 EduBook — Student-Teacher Booking Appointment System

A web-based appointment booking system built with **HTML, CSS, Vanilla JS + Firebase** for the Unified Mentor internship project.

---

## 🚀 Live Usage

Just open `index.html` in any modern browser — no build step required.

---

## 👥 Roles & Features

### ⚙️ Admin
| Feature | Description |
|---|---|
| Add Teacher | Create teacher account with name, dept, subject, cabin, availability |
| Edit Teacher | Update teacher details |
| Delete Teacher | Remove teacher from system |
| Approve Students | Approve pending student registrations |
| Delete Students | Remove student accounts |
| View All Appointments | See every appointment across the system with status |
| Messages | View all system messages |

### 📚 Teacher
| Feature | Description |
|---|---|
| Login | Secure email/password login |
| Dashboard | See pending requests, upcoming sessions, stats |
| View Appointments | See all appointment requests from students |
| Approve Appointment | Accept student appointment request |
| Cancel Appointment | Decline or cancel an appointment |
| View Messages | Read messages from students, reply back |

### 🎓 Student
| Feature | Description |
|---|---|
| Register | Self-register (requires admin approval before login) |
| Login | Email/password login after approval |
| Search Teacher | Browse teachers by name, subject, department |
| Book Appointment | Select teacher, pick date/time, state purpose |
| Send Message | Direct message to a teacher |
| View Appointments | Track status of all bookings |
| Cancel Appointment | Cancel pending appointments |

---

## 🏗 System Architecture

```
Browser (Single HTML file)
        │
Firebase Auth ─── Email/Password for all roles
        │
Firebase Firestore
    ├── users          (uid, email, name, role, status, department, subject, ...)
    ├── appointments   (studentId, teacherId, date, time, purpose, message, status)
    └── messages       (fromId, toId, fromName, toName, body, read, createdAt)
```

---

## 🔄 Workflow

```
Admin creates account → sets up Teachers
          ↓
Student registers → Admin approves → Student logs in
          ↓
Student searches for teacher → Books appointment with message
          ↓
Teacher receives request → Approves or cancels
          ↓
Student sees status update → Can message teacher for follow-up
```

---

## 📁 Files

```
student-teacher-booking/
└── index.html    ← Complete app (HTML + CSS + JS in one file)
```

---

## ▶ Running Locally

1. Clone/download the repo
2. Open `index.html` in Chrome/Firefox/Edge
3. Create an admin account (use any email, role: Admin tab)
4. Add teachers via Admin panel
5. Students register and await approval

> No server needed. Firebase SDK loads via CDN.

---

## 🧪 Test Cases

| Test | Expected |
|---|---|
| Student registers | Status = pending, cannot login until approved |
| Admin approves student | Student can now login |
| Student books appointment | Status = pending, teacher notified |
| Teacher approves appointment | Status = approved, visible in student dashboard |
| Teacher cancels appointment | Status = cancelled |
| Student sends message | Message appears in teacher's inbox |
| Admin adds teacher | Teacher can login, visible to students |
| Search teacher | Filters by name/subject/dept in real time |

---

## 📊 Logging

All actions logged to console and sessionStorage with timestamps:
```
[2025-02-18T10:00:00Z] [INFO] Login: student@edu.com
[2025-02-18T10:05:00Z] [INFO] Appointment booked: uid123 → Dr. Smith
[2025-02-18T10:10:00Z] [INFO] Message sent to Dr. Smith
```

---

## ⚙ Firebase Firestore Rules (Recommended)

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

---

## 👤 Author
Built for Unified Mentor Internship — Student-Teacher Booking Appointment project.
