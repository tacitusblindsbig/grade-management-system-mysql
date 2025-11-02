# 🚀 ULTRA-QUICK FIX (Just Copy/Paste)

## For Saqib (Windows) - 5 Minutes Total

### Commands to Run (in order):

#### 1. Pull Latest Code
```cmd
cd C:\Users\saqib\OneDrive\Desktop\DBMS Mini Project\Nishad\grade-management-system-mysql
git pull origin main
```

#### 2. Reset Database
```cmd
mysql -u root -p
```

Paste this in MySQL:
```sql
DROP DATABASE IF EXISTS grade_management_db;
CREATE DATABASE grade_management_db;
EXIT;
```

#### 3. Load Fresh Data
```cmd
cd backend
mysql -u grade_user -p grade_management_db < database_setup.sql
```
Password when asked: `password123`

#### 4. Verify Fix
```cmd
venv\Scripts\activate
python test_migration.py
```

**Expected**: All tests PASS ✓

#### 5. Start Server
```cmd
python server.py
```

**Expected**: Server runs on port 8000, no errors

---

## Done! 🎉

Login credentials:
- Email: `rajesh@university.edu`
- Password: `password123`

---

**What was fixed**: Old plain text passwords → Fresh bcrypt hashed passwords
