# 🕐 EZTIME-TMP – Time & Attendance Payroll Management System

A modern, fast, and user-friendly time tracking and payroll calculation system with a beautiful web interface and comprehensive REST API.

---

## 📑 Table of Contents

1. [✨ Key Features](#key-features)
2. [🚀 Quick Start](#quick-start)
3. [📂 Project Structure](#project-structure)
4. [⚙️ Installation Guide](#installation-guide)
5. [🌐 Using the System](#using-the-system)
6. [📡 API Endpoints](#api-endpoints)
7. [🔐 Security & Authentication](#security--authentication)
8. [💼 Business Rules](#business-rules)
9. [🧪 Testing & Quality](#testing--quality)
10. [📝 Postman Examples](#postman-examples)
11. [🐛 Troubleshooting](#troubleshooting)

---
<a name="key-features"></a>
## ✨ Key Features

### 🎯 Leading System Features

#### 1. 📱 Smart User Interface
- ✅ Autocomplete employee selection
- ✅ Responsive design for mobile/tablet
- ✅ Real-time visual feedback (success/error messages)
- ✅ Modern, clean design (Material Design principles)

#### 2. 💰 Automatic Payroll Calculation
- ✅ Instant salary calculation based on shifts
- ✅ Support for overtime with multiplier rates (100%, 125%, 150%)
- ✅ Automatic night shift detection (22:00-06:00)
- ✅ Daily deficit calculation

#### 3. 🌙 Advanced Business Rules
- ✅ Max Rate Rule - uses highest rate for entire day
- ✅ Midnight Crossing - correctly handles shifts past midnight
- ✅ Accurate night hours calculation
- ✅ Support for multiple shifts per day

#### 4. 📊 Deep Data Analytics
- ✅ Hours breakdown by subsidiary
- ✅ Hours breakdown by role
- ✅ Detailed daily shift report
- ✅ Shift deletion with automatic recalculation

#### 5. 🔌 Professional REST API
- ✅ Bearer Token authentication
- ✅ Multiple data retrieval endpoints
- ✅ Optional parameters support
- ✅ Standard HTTP status codes

#### 6. 🗄️ Database Management
- ✅ Automatic database creation on first run
- ✅ Automatic Excel data import
- ✅ Real-time data updates
- ✅ Support for UTF-8 and special characters

#### 7. 🔒 Security & Compliance
- ✅ Bearer Token authentication
- ✅ CORS support for external services
- ✅ Input validation on all endpoints
- ✅ Precise timezone (Asia/Jerusalem)

---

<a name="quick-start"></a>
## 🚀 Quick Start

### Get Running in 60 Seconds

```bash
# 1. Create Virtual Environment
python -m venv venv
source venv/bin/activate  # macOS/Linux
# or
venv\Scripts\activate  # Windows

# 2. Install Dependencies
pip install -r requirements.txt

# 3. Start Server
uvicorn main:app --reload --host 0.0.0.0 --port 8000

# 4. Open Browser
http://localhost:8000
```

**System is now running!** ✅

---

<a name="project-structure"></a>
## 📂 Project Structure

```
EZTIME-ANOG/
│
├── 📄 main.py                      ← FastAPI Server + Business Logic
├── 📄 requirements.txt             ← Python Dependencies
├── 📊 EZTIME_DATA.xlsx            ← Your Data File (required)
├── 🗄️ eztime.db                   ← SQLite Database (auto-created)
├── 🧪 test_payroll.py             ← Unit Tests
├── 📄 README.md                   ← This Documentation
│
└── 📁 templates/
    └── 🌐 index.html              ← Web User Interface
```

### Important Files Explanation

| File | Description |
|------|-------------|
| `main.py` | All business logic, API routes, database operations |
| `requirements.txt` | List of all required Python libraries |
| `EZTIME_DATA.xlsx` | Your data file (employees, rates, shifts) |
| `eztime.db` | Database file (created automatically on first run) |
| `templates/index.html` | Web user interface |

---

<a name="installation-guide"></a>
## ⚙️ Installation Guide

### Prerequisites

- ✅ **Python 3.9+** - Check: `python --version`
- ✅ **pip** - Package manager (usually comes with Python)
- ✅ **Excel File** - `EZTIME_DATA.xlsx` with your data
- ✅ **Git** (optional) - For cloning the repository

### Step 1️⃣ - Clone Repository

```bash
git clone https://github.com/anogshtorper-dev/EZTIME-ANOG.git
cd EZTIME-ANOG
```

### Step 2️⃣ - Create Virtual Environment

**macOS/Linux:**
```bash
python -m venv venv
source venv/bin/activate
```

**Windows (Command Prompt):**
```bash
python -m venv venv
venv\Scripts\activate
```

**Windows (PowerShell):**
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

**Success indicator:**
```
(venv) user@computer:~/EZTIME-ANOG$
```

### Step 3️⃣ - Install Dependencies

```bash
pip install -r requirements.txt
```

**Installation time:** ~30-60 seconds

**Libraries installed:**
- 📦 fastapi==0.111.0
- 📦 uvicorn[standard]==0.29.0
- 📦 jinja2==3.1.4
- 📦 pandas==2.2.2
- 📦 openpyxl==3.1.2
- 📦 pydantic==2.7.1
- 📦 python-multipart==0.0.9
- 📦 tzdata==2024.1

### Step 4️⃣ - Prepare Data File

```bash
# Copy EZTIME_DATA.xlsx to project root if it's not there yet
cp /path/to/EZTIME_DATA.xlsx ./EZTIME_DATA.xlsx
```

**Excel file must contain three sheets:**

#### Sheet 1 - Employees
```
employee_id  | name        | daily_standard
E1022        | John Doe    | 8.0
E1023        | Jane Smith  | 8.5
```

#### Sheet 2 - Rates & Roles
```
employee_id | role              | subsidiary    | hourly_rate
E1022       | Warehouse Manager | Subsidiary A  | 62.0
E1022       | Picker            | Subsidiary B  | 50.0
E1023       | Manager           | Subsidiary A  | 75.0
```

#### Sheet 3 - Shifts
```
employee_id | date       | start_time | end_time | subsidiary   | role
E1022       | 2026-01-19 | 07:45      | 16:30    | Subsidiary A | Warehouse Manager
E1023       | 2026-01-19 | 08:00      | 17:00    | Subsidiary A | Manager
```

### Step 5️⃣ - Start Server

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

**Expected output:**
```
INFO:     Uvicorn running on http://0.0.0.0:8000
INFO:     Application startup complete
[SEED] Sheet names: ['Employees', 'Rates', 'Shifts']
[SEED] DB already seeded – skipping.
[AUTH] Token: 'demo-token' (default)
```

### Step 6️⃣ - Open in Browser

```
http://localhost:8000
```

**Congratulations!** System is ready to use! ✅

---

<a name="using-the-system"></a>
## 🌐 Using the System

### Complete User Guide

#### 1. Select Employee
```
1. Type employee name in the "Employee" field
2. Select from the displayed list
3. Or use "📱 Scan QR" to scan QR code
```

#### 2. Pick Date
```
1. Click on "Date" field
2. Select date from calendar widget
3. Or type manually in format: YYYY-MM-DD
```

#### 3. Choose Subsidiary & Role
```
1. Select Subsidiary from dropdown (auto-filtered by employee)
2. Select Role from dropdown (auto-filtered by subsidiary)
3. Fields update automatically
```

#### 4. Add Work Hours
```
1. Enter Start Time in HH:MM format (e.g., 07:45)
2. Enter End Time in HH:MM format (e.g., 16:30)
3. Click "+ Add Shift"
```

#### 5. Calculate Payroll
```
1. Click "⟳ Calculate"
2. System automatically calculates all data
3. View detailed report in "Daily Payroll Result" panel
```

#### 6. Edit & Delete
```
1. See shift in table? Click ✕ to delete
2. System automatically recalculates
```

### Payroll Results Report

When clicking "Calculate", you get a detailed report including:

```
📊 Daily Payroll Result

👤 Employee: John Doe | 2026-01-19

💰 Salary Simulation: ₪554.13
   (Calculated salary based on rate and work type)

📋 Statistics:
   • Total Hours: 8.75 hours
   • Hours @100%: 8.0 hours (regular salary)
   • Hours @125%: 0.75 hours (overtime 1st tier)
   • Hours @150%: 0.0 hours (overtime 2nd tier)

🌙 Night Rule Active: NO
   • Night Hours in Window: 0.0 hours

⚠️ Daily Deficit: 0.25 hours
   (Missing 0.25 hours from daily standard of 9.0)

🔧 Overtime Threshold: 8 hours
💵 Max Rate: ₪62.0 per hour

📦 Hours by Subsidiary:
   • Subsidiary A: 8.75 hours

👔 Hours by Role:
   • Warehouse Manager: 8.75 hours

📋 Shifts Table:
   [1] Warehouse Manager @ Subsidiary A
       07:45 → 16:30 (8.75h) | ₪62.0/h
```

---

<a name="api-endpoints"></a>
## 📡 API Endpoints

### 🌍 UI Endpoints (No Authentication)

#### 1. List All Employees
```http
GET /employees
```

**Response:**
```json
[
  {"id": "E1022", "name": "John Doe", "daily_standard": 8.0},
  {"id": "E1023", "name": "Jane Smith", "daily_standard": 8.5}
]
```

#### 2. Get Available Roles for Employee
```http
GET /allowed/{employee_id}
```

**Example:**
```http
GET /allowed/E1022
```

**Response:**
```json
[
  {"role": "Warehouse Manager", "subsidiary": "Subsidiary A", "hourly_rate": 62.0},
  {"role": "Picker", "subsidiary": "Subsidiary B", "hourly_rate": 50.0}
]
```

#### 3. Add Shift
```http
POST /shifts

Content-Type: application/json

{
  "employee_id": "E1022",
  "date": "2026-01-19",
  "subsidiary": "Subsidiary A",
  "role": "Warehouse Manager",
  "start_time": "07:45",
  "end_time": "16:30"
}
```

**Response:**
```json
{"status": "ok", "message": "Shift added."}
```

#### 4. Calculate Daily Payroll
```http
GET /daily/{employee_id}/{date}
```

**Example:**
```http
GET /daily/E1022/2026-01-19
```

**Response:**
```json
{
  "employee_id": "E1022",
  "employee_name": "John Doe",
  "date": "2026-01-19",
  "total_hours": 8.75,
  "hours_100": 8.0,
  "hours_125": 0.75,
  "hours_150": 0.0,
  "salary_simulation": 554.13,
  "max_rate": 62.0,
  "overtime_threshold": 8,
  "night_hours_in_window": 0.0,
  "daily_deficit": 0.25
}
```

#### 5. List Shifts for Date
```http
GET /shifts_list/{employee_id}/{date}
```

**Example:**
```http
GET /shifts_list/E1022/2026-01-19
```

#### 6. Delete Shift
```http
DELETE /shifts/{shift_id}
```

**Example:**
```http
DELETE /shifts/1
```

### 🔒 v1 API (Requires Bearer Token)

#### Calculate Payroll via API
```http
GET /v1/payroll/daily?employee_id=E1022&date=2026-01-19
Authorization: Bearer demo-token
```

**Query Parameters:**

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| employee_id | string | ✅ | — | Employee ID |
| date | string | ✅ | — | Date (YYYY-MM-DD) |
| include_shifts | boolean | ❌ | true | Include shift details |
| include_breakdown | boolean | ❌ | true | Include hours breakdown |

---

<a name="security--authentication"></a>
## 🔐 Security & Authentication

### Default Token

```
demo-token
```

### Change API Token

**Using Environment Variable:**

```bash
export EZTIME_API_TOKEN=my-secret-token
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

**Windows (PowerShell):**
```powershell
$env:EZTIME_API_TOKEN="my-secret-token"
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

### Token Security

| ⚠️ Warning | Action |
|-----------|--------|
| **Don't use default in production** | Change to strong, random token |
| **Don't put token in code** | Use environment variables only |
| **Don't share token in files** | Keep it secret and secure |

### API Request with Token

```bash
curl -H "Authorization: Bearer your-secret-token" \
  "http://localhost:8000/v1/payroll/daily?employee_id=E1022&date=2026-01-19"
```

---

<a name="business-rules"></a>
## 💼 Business Rules

### Payroll Calculation - Detailed Explanation

#### 1. Threshold Determination

```
IF night_hours_in_window >= 2.0
  THEN threshold = 7 hours
ELSE
  threshold = 8 hours
```

**Example:**
- Employee worked 2.5 night hours → threshold = 7 hours
- Employee worked 1 night hour → threshold = 8 hours

#### 2. Hours Distribution

```
hours_100% = MIN(total_hours, threshold)
hours_125% = MAX(0, MIN(total_hours - threshold, 2.0))
hours_150% = MAX(0, total_hours - threshold - 2.0)
```

**Example with 10 total hours:**
```
threshold = 8
hours_100% = MIN(10, 8) = 8 hours
hours_125% = MIN(10-8, 2) = 2 hours
hours_150% = 10-8-2 = 0 hours
```

#### 3. Salary Calculation

```
salary = (hours_100 × rate) + (hours_125 × rate × 1.25) + (hours_150 × rate × 1.5)
```

**Example with ₪50/hour:**
```
salary = (8 × 50) + (2 × 50 × 1.25) + (0 × 50 × 1.5)
salary = 400 + 125 + 0
salary = ₪525
```

#### 4. Daily Deficit

```
deficit = MAX(0, daily_standard - total_hours)
```

**Example:**
- daily_standard = 9 hours
- total_hours = 8.75 hours
- deficit = MAX(0, 9 - 8.75) = 0.25 hours

### Night Work (Night Window)

**Night Window:** 22:00 → 06:00

**Night Hours Calculation:**
- Each hour within this window counts as "night hour"
- If ≥2 night hours → threshold becomes 7 hours

**Examples:**
```
Shift 20:00-23:00
├─ Night hours: 1 hour (23:00-24:00)
└─ Threshold: 8 hours

Shift 22:00-06:00
├─ Night hours: 8 hours (entire shift)
└─ Threshold: 7 hours

Shift 04:00-08:00
├─ Night hours: 2 hours (04:00-06:00)
└─ Threshold: 7 hours
```

### Max Rate Rule

**Rule:** If employee worked with different rates on same day - use highest rate

**Example:**
```
Shift 1: 8 hours @ Subsidiary A @ ₪50/hour
Shift 2: 2 hours @ Subsidiary B @ ₪75/hour

Max Rate = ₪75 (highest)
Salary = (8+2) × ₪75 × [rates] = ...
```

---

<a name="testing--quality"></a>
## 🧪 Testing & Quality

### Run Unit Tests

```bash
# Basic test
python test_payroll.py

# Verbose test with pytest
python -m pytest test_payroll.py -v

# With coverage report
python -m pytest test_payroll.py --cov=main
```

### What's Tested

- ✅ Overtime bucket calculations (3 scenarios)
- ✅ Night window detection
- ✅ Early morning shifts (04:00-08:00)
- ✅ Midnight crossing logic (23:00-03:00)
- ✅ Bearer token validation
- ✅ Timezone handling (Asia/Jerusalem)
- ✅ Missing parameter validation

### Example Test

```python
import unittest
from main import compute_daily

class TestPayroll(unittest.TestCase):
    def test_simple_shift(self):
        result = compute_daily("E1022", "2026-01-19")
        self.assertEqual(result["total_hours"], 8.75)
        self.assertEqual(result["hours_100"], 8.0)
        
if __name__ == '__main__':
    unittest.main()
```

---

<a name="postman-examples"></a>
## 📝 Postman Examples

### ✅ Example 1 - Successful Request (200 OK)

**Setup:**
```
Method:  GET
URL:     http://localhost:8000/v1/payroll/daily
         ?employee_id=E1022&date=2026-01-19
Headers: Authorization: Bearer demo-token
```

**Steps in Postman:**
1. Open Postman
2. Click "New Request"
3. Select "GET"
4. Paste the URL
5. Go to "Headers" tab
6. Add: `Authorization: Bearer demo-token`
7. Click "Send"

**Response:**
```json
{
  "employee_id": "E1022",
  "employee_name": "John Doe",
  "date": "2026-01-19",
  "total_hours": 8.75,
  "hours_100": 8.0,
  "hours_125": 0.75,
  "hours_150": 0.0,
  "salary_simulation": 554.13,
  "max_rate": 62.0,
  "overtime_threshold": 8,
  "night_hours_in_window": 0.0,
  "night_rule_active": false,
  "daily_standard": 9.0,
  "daily_deficit": 0.25,
  "calculated_at": "2026-01-19T10:00:00+02:00"
}
```

### ❌ Example 2 - Invalid Token (401)

```
Headers: Authorization: Bearer wrong-token
```

**Response:**
```json
{
  "error": {
    "code": "UNAUTHORIZED",
    "message": "Invalid or missing API token"
  }
}
```

### ❌ Example 3 - Employee Not Found (404)

```
URL: /v1/payroll/daily?employee_id=NOTEXIST&date=2026-01-19
```

**Response:**
```json
{
  "error": {
    "code": "EMPLOYEE_NOT_FOUND",
    "message": "Employee not found"
  }
}
```

### ❌ Example 4 - Missing Parameter (400)

```
URL: /v1/payroll/daily?employee_id=E1022
```

**Response:**
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Missing required parameter: date"
  }
}
```

---


<a name="troubleshooting"></a>
## 🐛 Troubleshooting

### Common Issues & Solutions

#### 🔴 Port 8000 Already in Use

```bash
# Check what's using port 8000
lsof -i :8000  # macOS/Linux

# Or
netstat -ano | findstr :8000  # Windows

# Solution: use different port
uvicorn main:app --port 8001
```

#### 🔴 `requirements.txt` Not Found

```bash
# Create the file
cat > requirements.txt << 'EOF'
fastapi==0.111.0
uvicorn[standard]==0.29.0
jinja2==3.1.4
pandas==2.2.2
openpyxl==3.1.2
pydantic==2.7.1
python-multipart==0.0.9
tzdata==2024.1
EOF
```

#### 🔴 Excel File Not Found

```bash
# Verify file exists
ls -la EZTIME_DATA.xlsx  # macOS/Linux

# Or
dir EZTIME_DATA.xlsx  # Windows

# If missing, copy it
cp /path/to/EZTIME_DATA.xlsx ./
```

#### 🔴 Database Already Seeded

```bash
# Delete the database
rm eztime.db  # macOS/Linux
del eztime.db  # Windows

# Restart server - it will recreate automatically
uvicorn main:app --reload
```

#### 🔴 No Employees Showing

**Check:**
1. Excel file has Employees sheet?
2. Correct columns? (employee_id, name, daily_standard)
3. Data format accepted?

**Fix:**
```bash
# Check database
sqlite3 eztime.db
sqlite> SELECT COUNT(*) FROM Employees;
```

#### 🔴 Token Not Working

```bash
# Test your token
curl -H "Authorization: Bearer demo-token" \
  http://localhost:8000/v1/payroll/daily?employee_id=E1022&date=2026-01-19

# Or change token
export EZTIME_API_TOKEN=my-new-token
uvicorn main:app --reload
```

#### 🔴 Timezone Not Correct

```bash
# Check timezone
python -c "from datetime import datetime; from zoneinfo import ZoneInfo; print(datetime.now(ZoneInfo('Asia/Jerusalem')))"

# If not working, install tzdata
pip install tzdata
```

### Debug Mode

```bash
# Run with debug logging
LOGLEVEL=debug uvicorn main:app --reload

# Or in code
import logging
logging.basicConfig(level=logging.DEBUG)
logger = logging.getLogger(__name__)
logger.debug("Debug message")
logger.info("Info message")
logger.error("Error message")
```


## 📞 Getting Help

### Resources

1. **Documentation:** This README file

### Report an Issue

When there's a problem:
1. Email: anogshtorper@gmail.com

---

## 📄 License & Credits

**Project:** EZTIME-ANOG  
**Version:** 1.0  
**Last Updated:** 01-03-2026  
**Repository:** https://github.com/anogshtorper-dev/EZTIME-ANOG 
**Author:** anogshtorper-dev  

---

**Tip:** Bookmark this README for quick reference!

**Happy time tracking! ⏰✨**
