# 🔧 WINDOWS FIX: Password Hash Error

## 🎯 Problem
You're getting this error:
```
passlib.exc.UnknownHashError: hash could not be identified
```

**Root Cause**: Your database has old data with plain text passwords instead of bcrypt hashed passwords.

---

## ✅ COMPLETE FIX (5 Minutes)

### Step 1: Drop and Recreate Database

Open **Command Prompt** or **PowerShell** and run:

```cmd
mysql -u root -p
```

Enter your MySQL root password, then run these commands:

```sql
-- Drop the old database (this removes ALL data)
DROP DATABASE IF EXISTS grade_management_db;

-- Recreate the database
CREATE DATABASE grade_management_db;

-- Verify user exists (should show grade_user)
SELECT User, Host FROM mysql.user WHERE User = 'grade_user';

-- If user doesn't exist, create it:
CREATE USER IF NOT EXISTS 'grade_user'@'localhost' IDENTIFIED BY 'password123';
GRANT ALL PRIVILEGES ON grade_management_db.* TO 'grade_user'@'localhost';
FLUSH PRIVILEGES;

-- Exit MySQL
EXIT;
```

---

### Step 2: Load Fresh Data with Hashed Passwords

**CRITICAL**: Navigate to your backend folder first!

```cmd
cd C:\Users\saqib\OneDrive\Desktop\DBMS Mini Project\Nishad\grade-management-system-mysql\backend
```

Now load the database schema:

```cmd
mysql -u grade_user -p grade_management_db < database_setup.sql
```

When prompted, enter password: `password123`

**Expected**: No output means success!

---

### Step 3: Verify Data Loaded Correctly

```cmd
mysql -u grade_user -p grade_management_db
```

In MySQL prompt, run:

```sql
-- Check faculty count
SELECT COUNT(*) FROM faculties;
-- Should show: 3

-- Check if passwords are hashed (should start with $2b$)
SELECT email, LEFT(password, 10) as password_prefix FROM faculties;
-- Should show: $2b$12$kge for all three

-- Check students
SELECT COUNT(*) FROM students;
-- Should show: 9

EXIT;
```

---

### Step 4: Run Tests Again

```cmd
cd C:\Users\saqib\OneDrive\Desktop\DBMS Mini Project\Nishad\grade-management-system-mysql\backend

# Activate virtual environment
venv\Scripts\activate

# Run tests
python test_migration.py
```

**Expected Output**: All tests should PASS ✓

---

### Step 5: Start Server and Test Login

#### Terminal 1 - Start Backend:
```cmd
cd C:\Users\saqib\OneDrive\Desktop\DBMS Mini Project\Nishad\grade-management-system-mysql\backend
venv\Scripts\activate
python server.py
```

**Expected**:
```
Application started. Ensure database_setup.sql has been executed.
INFO:     Uvicorn running on http://0.0.0.0:8000
```

#### Terminal 2 - Test Login:
```cmd
curl -X POST http://localhost:8000/api/auth/login -H "Content-Type: application/json" -d "{\"email\":\"rajesh@university.edu\",\"password\":\"password123\"}"
```

**Expected**: You should get a JWT token!

---

## 🎯 Quick Verification Checklist

- [ ] Dropped old database
- [ ] Created fresh database
- [ ] Loaded database_setup.sql
- [ ] Verified passwords are hashed ($2b$ prefix)
- [ ] test_migration.py shows all PASS ✓
- [ ] Server starts without errors
- [ ] Login returns JWT token
- [ ] Frontend can connect and login works

---

## 🆘 If Still Getting Errors

### Error: "Access denied for user 'grade_user'"

**Fix**:
```sql
-- In MySQL as root:
DROP USER IF EXISTS 'grade_user'@'localhost';
CREATE USER 'grade_user'@'localhost' IDENTIFIED BY 'password123';
GRANT ALL PRIVILEGES ON grade_management_db.* TO 'grade_user'@'localhost';
FLUSH PRIVILEGES;
```

### Error: "Can't connect to MySQL server"

**Fix**: Make sure MySQL service is running:
- Open **Services** (Press Win + R, type `services.msc`)
- Find **MySQL80** (or similar)
- Right-click → **Start**

### Error: "File not found: database_setup.sql"

**Fix**: Make sure you're in the backend folder:
```cmd
cd C:\Users\saqib\OneDrive\Desktop\DBMS Mini Project\Nishad\grade-management-system-mysql\backend
dir database_setup.sql
```

Should show the file. If not, pull latest from GitHub.

---

## 📧 After Fix is Working

Send message to Nishad:
```
✅ FIXED! Database reset with proper password hashing.
All tests passing now. Server running successfully.
Login working with JWT tokens.
```

---

## 🔐 Login Credentials (After Fix)

- **Email**: `rajesh@university.edu`
- **Password**: `password123`

**Note**: The password IS "password123" - it's just stored as a bcrypt hash in the database for security.

---

## 💡 What Was Wrong?

Your database had passwords stored as plain text `"password123"` from a previous setup.
The code expects bcrypt hashed passwords like `$2b$12$kgeKNV3Lpt...`

By dropping and recreating the database, you got fresh data with properly hashed passwords from `database_setup.sql`.

---

**Estimated Time**: 5 minutes
**Difficulty**: Easy - just copy/paste commands

You're doing great! This is the last bug. After this, everything will work perfectly! 🚀
