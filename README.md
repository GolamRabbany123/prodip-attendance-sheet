# PRODIP Volunteer Attendance & Milestone Tracking Portal

An end-to-end, full-stack web application developed for **PRODIP** to manage volunteer presence, time tracking, class milestone progress towards official certification (36 classes), consecutive attendance streaks with substitute/replacement protection, multi-activity volunteering, role-based access control, and a dual-tier coordinator-to-admin approval workflow.

---

## 🌟 Key Features

1. **5 Role-Based System (Customizable & Manageable):**
   - **Mentor / Instructor:** Personal dashboard showing live streak, completed classes (out of 36), days left, certificate progress bar, and verified in/out class logs.
   - **Coordinator:** Interactive attendance sheet on designated days (Sunday, Tuesday, Friday) with live **"Now"** check-in timer, **"Check Out"** button, replacement logging, and 1-click submission to Admin.
   - **Senior Coordinator:** Review submissions forwarded by coordinators, audit hours and substitute notes, approve or return records.
   - **Executive Member:** High-level dashboard monitoring all 3 volunteer activities, student engagement, and certificate readiness.
   - **Central Admin:** Full system control, role assignments/promotions, designated schedule adjustments, private WhatsApp directory management, and certificate data export.

2. **Streak Engine with Replacement Protection:**
   - Default designated class days: **Sunday, Tuesday, Friday** (customizable per volunteer).
   - If a mentor cannot attend but arranges a **replacement volunteer**, the session is logged with the substitute and credited to the original mentor upon approval so their **consecutive streak continues uninterrupted**.

3. **36-Class Milestone & Certificate Readiness:**
   - Real-time progress bar towards 36 approved classes.
   - Days remaining countdown.
   - When 36 classes are completed:
     - Unlocks the **Certified Mentor** milestone badge.
     - Automatically generates a pre-filled congratulatory email notification with 1-click `mailto:` dispatch.
     - Adds volunteer to the Admin Certificate Audit export table (CSV / Print).
     - Organization performs certificate printing manually using the verified data.

4. **3 Distinct Volunteer Activities:**
   - **Activity 1:** Mentorship / Taking Classes (Core 36-class certificate program).
   - **Activity 2:** Medical Camp Volunteer (Health clinics, triage, community screenings).
   - **Activity 3:** Donation Volunteer (Charity drives, relief collections, sorting).

5. **Volunteer Directory & Privacy:**
   - Centralized table with Student ID, Name, Email, Role, and Designated Schedule.
   - **Private WhatsApp Protection:** Masked by default (`+88017*****78`) with a secure toggle to reveal/copy and a direct WhatsApp Web chat shortcut.

---

## 🚀 How to Run Locally

### Prerequisites:
- Python 3.10+ (Your system has Python 3.14 with `uv`)

### Quick Start (1 Command):
Inside the project folder:
```powershell
# 1. Activate the environment
.venv\Scripts\activate

# 2. Run the server (auto-reloads on edits)
uvicorn app.main:app --reload --port 8000
```
Then open your browser at:
👉 **`http://127.0.0.1:8000`**

### Running Automated Tests:
```powershell
$env:PYTHONPATH="."
.venv\Scripts\pytest tests
```

---

## 🌐 How to Host Online for FREE (Step-by-Step)

You can host this web application 100% free on **Render.com** (with free SSL/HTTPS and zero maintenance):

### Option 1: Deploy on Render (Recommended)
1. **Push your code to GitHub:**
   - Create a free GitHub repository (e.g. `prodip-volunteer-tracker`).
   - Push this project folder to your GitHub repo.
2. **Deploy on Render:**
   - Go to [render.com](https://render.com) and sign in with GitHub.
   - Click **New +** -> **Web Service**.
   - Select your `prodip-volunteer-tracker` repository.
   - Configure the settings:
     - **Runtime:** `Python 3`
     - **Build Command:** `pip install -r requirements.txt && python -m app.seed_data`
     - **Start Command:** `uvicorn app.main:app --host 0.0.0.0 --port $PORT`
     - **Plan:** Free
   - Click **Create Web Service**.
3. Render will automatically build, seed the database, and provide you with a live URL like:
   `https://prodip-volunteer-tracker.onrender.com`

---

## 📁 Project Architecture

```
prodip-volunteer-tracker/
│
├── app/
│   ├── __init__.py
│   ├── database.py              # SQLite / PostgreSQL engine & session
│   ├── models.py                # User, AttendanceRecord, Activity models
│   ├── schemas.py               # Pydantic schemas for data validation
│   ├── main.py                  # FastAPI routes, handlers, and endpoints
│   ├── seed_data.py             # Initial users, roles, and sample history
│   └── services/
│       ├── __init__.py
│       ├── streak_service.py    # Streak calculation & replacement credit
│       └── email_service.py     # 36-class completion notifications & mailto
│
├── templates/
│   ├── base.html                # Global layout, navbar, role switcher
│   ├── index.html               # Home landing & module navigation
│   ├── mentor_dashboard.html    # Streak flame, 36-class progress, history
│   ├── coordinator_attendance.html # Live "Now" check-in/out, replacements
│   ├── approvals.html           # Senior Coordinator & Admin approval queue
│   ├── volunteers.html          # 5 Roles & WhatsApp privacy directory
│   ├── activities.html          # Mentorship, Medical Camp & Donation logs
│   └── reports.html             # Certificate audit & CSV export
│
├── tests/
│   ├── test_streak_and_replacement.py # Unit tests for streak logic
│   └── test_attendance_flow.py        # Integration test for full flow
│
├── Dockerfile                   # Container configuration
├── render.yaml                  # 1-click cloud deployment config
├── requirements.txt             # Python dependencies
└── README.md                    # Documentation
```

---

## 🔒 Security & Data Integrity
- Passwords & private data: WhatsApp numbers are masked in UI views.
- Status integrity: Direct transitions enforce that hours only credit to mentors upon official approval by Senior Coordinator or Admin.
