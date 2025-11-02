# Quick Setup Guide for Grade Management System

## Prerequisites
- Python 3.11 installed
- MySQL 8.0+ installed and running
- Git installed

## Step-by-Step Setup

### 1. Clone Repository
```cmd
git clone <your-repo-url>
cd grade-management-system
```

### 2. Backend Setup

#### Create Virtual Environment
```cmd
cd backend
python -m venv venv
venv\Scripts\activate
```

#### Install Dependencies
```cmd
pip install -r requirements_mysql.txt
```

### 3. Database Setup

#### Start MySQL (if not running)
- Open MySQL Workbench or use Command Prompt:
```cmd
mysql -u root -p
```

#### Create Database and User
```sql
CREATE DATABASE IF NOT EXISTS grade_management_db;
CREATE USER IF NOT EXISTS 'grade_user'@'localhost' IDENTIFIED BY 'password123';
GRANT ALL PRIVILEGES ON grade_management_db.* TO 'grade_user'@'localhost';
FLUSH PRIVILEGES;
USE grade_management_db;
SOURCE C:/path/to/your/backend/database_setup.sql;
EXIT;
```

**Note:** Replace `C:/path/to/your/` with actual path

### 4. Start Backend Server
```cmd
cd backend
venv\Scripts\activate
python server.py
```

**Expected output:**
```
Application started. Ensure database_setup.sql has been executed.
INFO:     Uvicorn running on http://0.0.0.0:8000
```

### 5. Frontend Setup (New Terminal)
```cmd
cd frontend
npm install
npm start
```

Browser will open at `http://localhost:3000`

### 6. Test Login

#### Default Credentials:
- **Email:** `rajesh@university.edu`
- **Password:** `password123`

## Troubleshooting

### Error: "ModuleNotFoundError: No module named 'asyncmy'"
**Fix:** Make sure you installed from `requirements_mysql.txt`:
```cmd
pip install -r requirements_mysql.txt
```

### Error: "Access denied for user 'grade_user'"
**Fix:** Run the CREATE USER commands again in MySQL

### Error: "Can't connect to MySQL server"
**Fix:** Ensure MySQL service is running:
- Windows: Open Services, start MySQL80
- Or use MySQL Workbench

### Frontend won't connect to backend
**Fix:** 
1. Ensure backend is running on port 8000
2. Check CORS settings in backend/.env

## Verify Everything Works

1. **Health check:** http://localhost:8000/api/health
2. **Login:** http://localhost:3000
3. **View students:** Navigate to "View Students" after login

---

**Need Help?** Contact the team on Discord/Slack
