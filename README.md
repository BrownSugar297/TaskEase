# 📋 TaskEase — Web-Based Task Management System


> A modular, role-based task management application built with **PHP** and **MySQL**, designed to streamline task assignment, progress tracking, and leave management in organizational environments.

![PHP](https://img.shields.io/badge/PHP-8.1-777BB4?style=flat&logo=php&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-MariaDB_10.4-4479A1?style=flat&logo=mysql&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap-5-7952B3?style=flat&logo=bootstrap&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=flat)


---

## 📑 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [File Structure](#-file-structure)
- [Database Schema](#-database-schema)
- [Installation](#-installation)
- [Usage](#-usage)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🚀 Overview

**TaskEase** is a clean and intuitive web-based Task Management System designed for teams and organizations. It provides a two-role structure — **Administrators** and **Regular Users** — each with a dedicated dashboard and a tailored set of capabilities.

Admins can assign tasks, manage users, and handle leave requests. Users can track their assigned tasks, update progress, and submit leave applications — all through a simple, responsive interface.

---

## ✨ Features

### 👤 User Roles
- Separate **Admin** and **User** portals with independent login flows
- Role-based access control to protect admin-only functionality

### 📌 Task Management
- Admins can **create and assign tasks** to specific users
- Tasks include description, start date, end date, and current status
- Users can **update task progress** in real time

### 🗓️ Leave Management
- Users can **submit leave requests** with a subject and message
- Admins can **approve or reject** leave applications from the dashboard
- Users can track the **status of submitted leaves**

### 🎨 User Interface
- Responsive, clean design using **Bootstrap 5** and custom CSS
- Dynamic sidebar loading with **jQuery AJAX** (no full-page reloads)
- Session-based authentication with secure redirects

---

## 🛠️ Tech Stack

| Layer       | Technology                        |
|-------------|-----------------------------------|
| Backend     | PHP 8.1                           |
| Database    | MySQL / MariaDB 10.4 (via phpMyAdmin) |
| Frontend    | HTML5, CSS3, JavaScript, Bootstrap 5 |
| JS Library  | jQuery (latest)                   |
| Server      | Apache (XAMPP / WAMP recommended) |

---

## 📁 File Structure

```
TaskEase-main/
├── index.php               # Landing page — role selection (User / Admin)
├── register.php            # New user registration
├── user_login.php          # User login page
├── user_dashboard.php      # User dashboard with sidebar navigation
├── task.php                # Displays tasks assigned to the logged-in user
├── update_status.php       # Allows users to update task status
├── leaveForm.php           # Leave application form
├── leave_status.php        # Displays status of submitted leave requests
├── logout.php              # Session destruction and redirect
├── tms_db.sql              # Full database schema with sample data
├── admin/
│   ├── admin_login.php     # Admin login page
│   ├── admin_dashboard.php # Admin dashboard
│   ├── assign_task.php     # Task creation and assignment
│   └── manage_leaves.php   # Leave approval/rejection panel
├── includes/
│   ├── connection.php      # MySQL database connection
│   └── jquery_latest.js    # jQuery library
├── bootstrap/
│   ├── css/bootstrap.min.css
│   └── js/bootstrap.min.js
├── css/
│   └── styles.css          # Custom application styles
└── assets/
    └── logo.png            # Application logo
```

---

## 🗄️ Database Schema

The database is named **`tms_db`** and contains the following tables:

### `users`
| Column     | Type          | Description              |
|------------|---------------|--------------------------|
| `uid`      | INT (PK, AI)  | Unique user ID           |
| `name`     | VARCHAR(100)  | Full name                |
| `email`    | VARCHAR(100)  | Email address            |
| `password` | VARCHAR(100)  | Login password           |
| `mobile`   | BIGINT        | Mobile number            |

### `admins`
| Column     | Type          | Description              |
|------------|---------------|--------------------------|
| `id`       | INT (PK, AI)  | Unique admin ID          |
| `name`     | VARCHAR(100)  | Full name                |
| `email`    | VARCHAR(100)  | Email address            |
| `password` | VARCHAR(100)  | Login password           |
| `mobile`   | BIGINT        | Mobile number            |

### `tasks`
| Column        | Type          | Description                    |
|---------------|---------------|--------------------------------|
| `tid`         | INT (PK, AI)  | Unique task ID                 |
| `uid`         | INT (FK)      | Assigned user (ref: users.uid) |
| `description` | VARCHAR(250)  | Task description               |
| `start_date`  | DATE          | Task start date                |
| `end_date`    | DATE          | Task deadline                  |
| `status`      | VARCHAR(100)  | Current progress status        |

### `leaves`
| Column    | Type          | Description                        |
|-----------|---------------|------------------------------------|
| `lid`     | INT (PK, AI)  | Unique leave request ID            |
| `uid`     | INT (FK)      | Requesting user (ref: users.uid)   |
| `subject` | VARCHAR(100)  | Leave subject                      |
| `message` | VARCHAR(250)  | Leave justification message        |
| `status`  | VARCHAR(100)  | `Approved` / `Rejected` / `No Action` |

> 📦 The complete schema with sample data is available in [`tms_db.sql`](tms_db.sql). Import it directly to get started.

---

## ⚙️ Installation

### Prerequisites
- [XAMPP](https://www.apachefriends.org/) or [WAMP](https://www.wampserver.com/) (Apache + MySQL + PHP)
- PHP 8.0+
- A modern web browser

### Step 1 — Clone the Repository
```bash
git clone https://github.com/your-username/TaskEase.git
```
Place the project folder inside your server's root directory:
- XAMPP: `C:/xampp/htdocs/TaskEase`
- WAMP: `C:/wamp64/www/TaskEase`

### Step 2 — Set Up the Database
1. Start **Apache** and **MySQL** from your control panel
2. Open **phpMyAdmin** at `http://localhost/phpmyadmin`
3. Create a new database named `tms_db`
4. Click **Import** and select the [`tms_db.sql`](tms_db.sql) file
5. Click **Go** — all tables and sample data will be created automatically

### Step 3 — Configure Database Connection
Open `includes/connection.php` and update the credentials if needed:
```php
$connection = mysqli_connect("localhost", "root", "", "tms_db");
```

### Step 4 — Run the Application
Navigate to:
```
http://localhost/TaskEase/index.php
```

---

## 🧭 Usage

### Landing Page
The homepage presents three options:
- **User Login** — for registered employees
- **User Registration** — to create a new account
- **Admin Login** — for administrators

### As an Admin
1. Log in at the **Admin Login** page
2. From the admin dashboard you can:
   - **Assign tasks** to users with description and date range
   - **View all submitted leave requests** and approve/reject them
   - **Monitor task statuses** across all users

### As a User
1. Register or log in at the **User Login** page
2. From the user dashboard you can:
   - **View assigned tasks** — see description, dates, and current status
   - **Update task progress** — click _Update_ next to any task
   - **Apply for leave** — submit a subject and message to the admin
   - **Check leave status** — track whether your request was approved or rejected

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

1. Fork the repository
2. Create your feature branch
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. Commit your changes
   ```bash
   git commit -m "Add: your feature description"
   ```
4. Push to the branch
   ```bash
   git push origin feature/your-feature-name
   ```
5. Open a **Pull Request**

### Development Guidelines
- Follow consistent PHP and HTML formatting
- Keep database queries parameterized to prevent SQL injection
- Test all role-based flows (admin and user) before submitting a PR
- Update this README if new pages or features are added

---

## 🔮 Future Roadmap

- [ ] Password hashing (bcrypt) for secure authentication
- [ ] Email notifications on task assignment and leave updates
- [ ] Task priority levels (Low / Medium / High / Critical)
- [ ] Admin analytics dashboard with charts
- [ ] REST API layer for mobile app integration
- [ ] Prepared statements / PDO to prevent SQL injection

---

## 📄 License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- [Bootstrap](https://getbootstrap.com/) — for the responsive UI framework
- [jQuery](https://jquery.com/) — for dynamic content loading
- [phpMyAdmin](https://www.phpmyadmin.org/) — for database management
- [XAMPP](https://www.apachefriends.org/) — for the local development environment

---

<p align="center">Built with ❤️ for productive teams and seamless task management</p>
