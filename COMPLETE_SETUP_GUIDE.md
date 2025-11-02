# 🚀 COMPLETE SETUP GUIDE - Grade Management System

## ⚠️ CRITICAL: Your Current Status

**What's Fixed:**
- ✅ All code is updated (MongoDB → MySQL migration complete)
- ✅ Dependencies are installed in venv
- ✅ No more Pydantic or FastAPI deprecation warnings

**What's Missing:**
- ❌ MySQL is NOT installed on your Mac
- ❌ Database setup not completed yet

---

## 📋 STEP-BY-STEP SETUP FOR YOUR MAC

### Step 1: Install MySQL (Using Homebrew - Recommended)

#### Install Homebrew (if not installed):
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

#### Install MySQL:
```bash
brew install mysql
```

#### Start MySQL Service:
```bash
brew services start mysql
```

#### Secure MySQL Installation:
```bash
mysql_secure_installation
```
- Press Enter for "No password"  
- Set root password: **password123** (or any strong password)
- Answer 'Y' to all questions

---

### Step 2: Create Database and User

#### Login to MySQL:
```bash
mysql -u root -p
# Enter the password you just set
```

#### Run these SQL commands:
```sql
-- Create database
CREATE DATABASE grade_management_db;

-- Create user
CREATE USER 'grade_user'@'localhost' IDENTIFIED BY 'password123';

-- Grant privileges
GRANT ALL PRIVILEGES ON grade_management_db.* TO 'grade_user'@'localhost';
FLUSH PRIVILEGES;

-- Exit
EXIT;
```

---

### Step 3: Load Database Schema

```bash
cd /Users/tacitus/Developer/VibeCodCursor/grade-management-system/backend

mysql -u grade_user -p grade_management_db < database_setup.sql
# Password: password123
```

---

### Step 4: Start Backend Server

```bash
cd /Users/tacitus/Developer/VibeCodCursor/grade-management-system/backend
source venv/bin/activate
python3 server.py
```

**Expected Output:**
```
Application started. Ensure database_setup.sql has been executed.
INFO:     Started server process [xxxxx]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
```

---

### Step 5: Test Backend

Open new terminal and run:
```bash
curl http://localhost:8000/api/health
```

**Expected:** `{"status":"healthy"}`

---

### Step 6: Start Frontend

```bash
cd /Users/tacitus/Developer/VibeCodCursor/grade-management-system/frontend
npm install
npm start
```

Browser opens at `http://localhost:3000`

---

### Step 7: Test Login

**Default Credentials:**
- Email: `rajesh@university.edu`
- Password: `password123`

---

## 🪟 FOR YOUR TEAMMATES ON WINDOWS

### Prerequisites:
1. Download and install MySQL Community Server from: https://dev.mysql.com/downloads/mysql/
2. During installation:
   - Choose "Developer Default"
   - Set root password: **password123**
   - Keep default settings

### Installation Steps:

#### 1. Clone Repository:
```cmd
git pull origin main
cd grade-management-system\backend
```

#### 2. Create Virtual Environment:
```cmd
python -m venv venv
venv\Scripts\activate
```

#### 3. Install Dependencies:
```cmd
pip install -r requirements.txt
```

#### 4. Setup Database:
```cmd
mysql -u root -p
```

Run these SQL commands:
```sql
CREATE DATABASE grade_management_db;
CREATE USER 'grade_user'@'localhost' IDENTIFIED BY 'password123';
GRANT ALL PRIVILEGES ON grade_management_db.* TO 'grade_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

Then load schema:
```cmd
mysql -u grade_user -p grade_management_db < database_setup.sql
```

#### 5. Start Backend:
```cmd
venv\Scripts\activate
python server.py
```

#### 6. Start Frontend (New CMD window):
```cmd
cd grade-management-system\frontend
npm install
npm start
```

---

## 🔧 TROUBLESHOOTING

### Error: "Access denied for user 'grade_user'"
```bash
# Mac:
mysql -u root -p
# Windows:
mysql -u root -p

# Then run:
DROP USER IF EXISTS 'grade_user'@'localhost';
CREATE USER 'grade_user'@'localhost' IDENTIFIED BY 'password123';
GRANT ALL PRIVILEGES ON grade_management_db.* TO 'grade_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

### Error: "Can't connect to MySQL server"
```bash
# Mac:
brew services restart mysql

# Windows:
# Open Services → MySQL80 → Restart
```

### Error: "ModuleNotFoundError"
```bash
# Ensure you're in venv and reinstall:
pip install -r requirements.txt
```

---

## ✅ FINAL VERIFICATION CHECKLIST

- [ ] MySQL installed and running
- [ ] Database `grade_management_db` created
- [ ] User `grade_user` created with proper privileges
- [ ] Schema loaded from `database_setup.sql`
- [ ] Backend running on port 8000
- [ ] Health check returns `{"status":"healthy"}`
- [ ] Frontend running on port 3000
- [ ] Can login with default credentials

---

## 🎯 NEXT STEPS AFTER SETUP

1. **Push to GitHub:**
```bash
cd /Users/tacitus/Developer/VibeCodCursor/grade-management-system
git add .
git commit -m "Fix: MySQL migration complete with updated dependencies"
git push origin main
```

2. **Share with team:**
   - Send them the GitHub repository link
   - Share this COMPLETE_SETUP_GUIDE.md file
   - Ensure they follow the Windows-specific steps

3. **Test all features:**
   - Login as faculty
   - View students
   - Assign marks
   - Verify marks calculation

---

**Need Help?** Contact: [Your Contact Info]
