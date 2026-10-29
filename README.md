# 🌿 Eco-Track AI

> **An intelligent, full-stack carbon footprint tracking platform** that helps individuals measure, analyse, and reduce their environmental impact using AI-powered insights, real-time analytics, and community leaderboards.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Architecture](#architecture)
- [Database Schema](#database-schema)
- [API Reference](#api-reference)
- [Carbon Calculation Engine](#carbon-calculation-engine)
- [AI Engine](#ai-engine)
- [Frontend Pages](#frontend-pages)
- [Getting Started](#getting-started)
- [Environment Setup](#environment-setup)
- [Running the Project](#running-the-project)
- [Build for Production](#build-for-production)
- [Screenshots](#screenshots)

---

## 🌍 Overview

Eco-Track AI is a **SaaS-grade sustainability platform** built for the modern climate-conscious individual. It enables users to log their daily activities across four emission categories — **Transport**, **Energy**, **Diet**, and **Waste** — and translates them into precise CO₂ equivalent figures using India-calibrated emission factors.

The platform features:
- A scientifically modelled **Carbon Calculation Engine** with 500+ lines of emission factor logic
- A **Machine Learning AI Engine** (Linear Regression via scikit-learn) that predicts future emissions
- A real-time **Analytics Dashboard** with charts, trend lines, and category breakdowns
- A **Global Leaderboard** (Hall of Fame) ranking users by sustainability score
- **CSV and PDF export** for personal reporting
- A polished, animated **React + Tailwind UI** with full dark/light mode support

---

## ✨ Features

### 🔐 Authentication
- Register with **email or phone number**
- JWT-based authentication (1-day token expiry)
- Persistent login via `localStorage`
- Profile picture upload (stored in `/uploads`)
- Password change with validation

### 📊 Dashboard
- Live sustainability **score ring** (0–100) coloured by risk level
- **4 metric cards**: Latest Footprint, All-Time Total, Sustainability Score, Carbon Streak
- **Emission Trend** — area chart of historical CO₂ over time
- **Source Breakdown** — donut pie chart by category (Transport / Energy / Diet / Waste)
- **AI Insight Banner** with rule-based eco suggestions
- **Quick Actions** panel linking to all key pages
- CSV export of all data
- Refresh button with live re-fetch

### ➕ Add Emission Entry
Two input modes:

**Quick Mode** — Dropdown-based sliders for fast daily logging (transport usage level, home size, diet type, waste level)

**Detailed Mode** — Full form across 4 tabbed categories:
| Tab | Fields |
|-----|--------|
| 🚗 Transport | Vehicle type, brand, model, year, fuel type, km travelled, driving condition, actual mileage |
| ⚡ Energy | kWh consumed, AC hours, house size, geyser, refrigerator |
| 🍽️ Diet | Diet type (Vegan → Non-Veg), meal frequency, dairy level, family size |
| 🗑️ Waste | Waste kg, waste type, recycling habit, composting |

### 🔬 Calculation Process
After submission, a dedicated animated page shows:
- Per-category CO₂ breakdown with live progress bars
- Sustainability score with classification badge (Excellent → Critical)
- Trees-to-offset counter
- Risk indicators
- AI-generated recommendations
- Option to view full analytics or log another entry

### 📈 Reports
- **Emission Trajectory** area chart (full history)
- **Category Impact** donut pie chart with legend
- **Weekly vs Monthly Comparison** toggle bar chart
- **KPI Insight Cards**: Total footprint, average daily, sustainability score, carbon streak, prediction, highest impact category
- PDF + CSV download buttons

### 🕰️ Data History
- Full table of all emission records with date, total CO₂, and per-category details
- **Edit** and **Delete** individual records inline
- Empty state with call-to-action
- Loading skeleton animation

### 🏆 Hall of Fame (Leaderboard)
- **Top 3 Podium** with animated gold/silver/bronze cards, rank badges, and rotating badge icons
- **Full ranked table** with columns: Rank, Environmentalist, Eco Score, Badge
- Badge tiers: 🏆 Eco Legend (90+) → 🏅 Green Guardian (70+) → 🌿 Eco Warrior (50+) → ⭐ Earth Citizen (0+)
- Highlights current user's row in green
- **Community stats panel**: Total Users, Average Score, Best Streak

### 💡 Eco Tips
- **AI Dynamic Recommendations** fetched from your latest data
- **Offset Strategy** — Trees-needed calculator
- **6 Static Sustainability Cards** covering transport, energy, diet, waste habits
- CTA to join the community leaderboard

### 👤 Profile
- Edit name, username, phone, email
- Upload profile picture
- Change password (current → new → confirm)
- **Sustainability Badges** gallery (earned by eco journey milestones)

### ⚙️ Settings
- Toggle daily reminder, weekly summary, goal reminder
- Set reminder frequency (daily / weekly / monthly)
- Toggle UI animations

### 🌐 Landing Page
- Animated hero section with live CO₂ demo chart
- Feature cards with hover animations
- "Ready to Synchronize?" full-width CTA section
- Responsive navigation with login/register links

---

## 🛠️ Tech Stack

### Frontend
| Technology | Version | Purpose |
|------------|---------|---------|
| **React** | 18.2 | UI framework |
| **React Router DOM** | 6.18 | SPA routing |
| **Tailwind CSS** | 3.3.5 | Utility-first styling |
| **Framer Motion** | 12.x | Animations & transitions |
| **Recharts** | 2.9 | Data visualisation (Area, Bar, Pie, Line charts) |
| **Lucide React** | 0.290 | Icon library |
| **Axios** | 1.6 | HTTP client |
| **Vite** | 5.0 | Build tool & dev server |
| **jsPDF + jspdf-autotable** | 4.x / 5.x | PDF report export |

### Backend
| Technology | Version | Purpose |
|------------|---------|---------|
| **Flask** | — | Web framework |
| **Flask-JWT-Extended** | — | JWT authentication |
| **Flask-SQLAlchemy** | — | ORM |
| **Flask-Migrate** | — | Database migrations |
| **Flask-Bcrypt** | — | Password hashing |
| **Flask-CORS** | — | Cross-origin requests |
| **SQLite** | — | Database (`instance/ecotrack.db`) |
| **pandas** | — | Data processing for ML |
| **scikit-learn** | — | Linear Regression prediction |
| **NumPy** | — | Numerical operations |

---

## 📁 Project Structure

```
Eco-TrackAI/
├── backend/                        # Flask REST API
│   ├── app.py                      # App factory, blueprint registration
│   ├── models.py                   # SQLAlchemy ORM models
│   ├── calculator.py               # Carbon calculation engine (506 lines)
│   ├── ai_engine.py                # ML prediction + rule-based suggestions
│   ├── extensions.py               # db, bcrypt, jwt, cors, migrate
│   ├── routes/
│   │   ├── auth.py                 # Register, login, profile, image upload
│   │   ├── emissions.py            # Add, get, update, delete emission records
│   │   ├── analytics.py            # Dashboard aggregates, leaderboard, insights
│   │   └── settings.py             # User notification & UI settings
│   ├── instance/
│   │   └── ecotrack.db             # SQLite database
│   └── uploads/                    # Profile image storage
│
└── frontend/                       # React + Vite SPA
    ├── src/
    │   ├── App.jsx                 # Router, layouts (Auth / App), route definitions
    │   ├── index.css               # CSS variables (light/dark), custom components
    │   ├── context/
    │   │   ├── AuthContext.jsx     # JWT auth state, login/logout/refreshProfile
    │   │   └── ThemeContext.jsx    # Dark/light mode toggle
    │   ├── components/
    │   │   ├── Sidebar.jsx         # Navigation sidebar with route links
    │   │   ├── Topbar.jsx          # Header: search, notifications, profile dropdown, theme toggle
    │   │   └── Navbar.jsx          # Landing page navbar
    │   ├── pages/
    │   │   ├── LandingPage.jsx     # Public marketing page
    │   │   ├── Login.jsx           # Login form
    │   │   ├── Register.jsx        # Registration form
    │   │   ├── Dashboard.jsx       # Main analytics dashboard
    │   │   ├── AddEmissionPage.jsx # Tabbed data entry (Quick + Detailed)
    │   │   ├── CalculationProcess.jsx # Post-submission breakdown page
    │   │   ├── QuickCheck.jsx      # Fast footprint estimator
    │   │   ├── DataHistory.jsx     # Record table with edit/delete
    │   │   ├── Reports.jsx         # Charts + KPIs + export
    │   │   ├── EcoTips.jsx         # AI tips + static sustainability cards
    │   │   ├── HallOfFame.jsx      # Global leaderboard
    │   │   ├── Profile.jsx         # User profile editor
    │   │   └── Settings.jsx        # Notification & UI settings
    │   └── utils/
    │       └── exportUtils.js      # CSV + PDF export helpers
    ├── tailwind.config.js          # Custom colours, fonts, animations
    ├── vite.config.js
    └── package.json
```

---

## 🏗️ Architecture

```
┌────────────────────────────────────────────────────────────────┐
│                        Browser (React SPA)                     │
│  Vite Dev Server :3000  /  Production Build (dist/)            │
│                                                                │
│  AuthContext (JWT + localStorage)  ←→  ThemeContext (dark/light)│
│  React Router DOM (SPA navigation)                             │
│  Recharts (data viz)  +  Framer Motion (animations)            │
└────────────────────┬───────────────────────────────────────────┘
                     │  HTTP / Axios  (localhost:5000)
                     ▼
┌────────────────────────────────────────────────────────────────┐
│                     Flask REST API (:5000)                      │
│                                                                │
│  /api/auth/       → auth.py     (register, login, profile)     │
│  /api/emissions/  → emissions.py (CRUD + stats)                │
│  /api/analytics/  → analytics.py (leaderboard, insights)       │
│  /api/settings/   → settings.py  (preferences)                 │
│  /uploads/<file>  → static file serving                        │
└────────────────────┬───────────────────────────────────────────┘
                     │  SQLAlchemy ORM
                     ▼
┌────────────────────────────────────────────────────────────────┐
│                  SQLite  (instance/ecotrack.db)                 │
│                                                                │
│  User  ·  EmissionRecord  ·  UserSettings                      │
│  Goal  ·  Leaderboard     ·  OTPRecord                         │
└────────────────────────────────────────────────────────────────┘
```

---

## 🗃️ Database Schema

### `User`
| Column | Type | Description |
|--------|------|-------------|
| id | Integer PK | Auto-increment |
| name | String(100) | Full name |
| username | String(80) | Display name (leaderboard) |
| email | String(120) unique | Login identifier |
| phone | String(20) unique | Alternative login |
| profile_image | String(255) | Path to uploaded image |
| password_hash | String(128) | Bcrypt hash |
| verified | Boolean | Account verified flag |
| created_at | DateTime | Registration timestamp |

### `EmissionRecord`
| Category | Key Fields |
|----------|-----------|
| Transport | `transport_km`, `transport_type`, `vehicle_brand`, `vehicle_model`, `vehicle_year`, `fuel_detail`, `vehicle_age_years`, `age_multiplier`, `base_factor`, `driving_condition`, `actual_mileage`, `ref_mileage` |
| Energy | `electricity_kwh`, `ac_hours`, `house_size`, `geyser_usage`, `has_refrigerator` |
| Gas | `gas_usage`, `cooking_fuel`, `cooking_frequency` |
| Waste | `waste_kg`, `waste_type`, `recycling_habit`, `composting` |
| Diet | `diet_type`, `meal_frequency`, `dairy_level` |
| Meta | `family_size`, `entry_mode`, `total_co2`, `created_at` |

### `UserSettings`
| Column | Type | Default |
|--------|------|---------|
| daily_reminder | Boolean | True |
| weekly_summary | Boolean | True |
| goal_reminder | Boolean | True |
| reminder_frequency | String | `"daily"` |
| animations_enabled | Boolean | True |

---

## 📡 API Reference

### Auth — `/api/auth/`

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| POST | `/register` | ❌ | Create account (email or phone) |
| POST | `/login` | ❌ | Get JWT token |
| GET | `/profile` | ✅ | Get current user profile |
| PUT | `/profile` | ✅ | Update name, username, email, phone, password |
| POST | `/upload-image` | ✅ | Upload profile picture |

### Emissions — `/api/emissions/`

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| POST | `/add` | ✅ | Log new emission record (returns CO₂, score, breakdown) |
| GET | `/dashboard` | ✅ | Full dashboard payload (stats, charts, suggestions) |
| GET | `/history` | ✅ | All records for user |
| PUT | `/<id>` | ✅ | Update a record (recalculates CO₂) |
| DELETE | `/<id>` | ✅ | Delete a record |
| GET | `/weekly-stats` | ✅ | This week vs last week comparison |
| GET | `/monthly-stats` | ✅ | This month vs last month comparison |

### Analytics — `/api/analytics/`

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| GET | `/` | ✅ | Category breakdown + historical trend |
| GET | `/leaderboard` | ✅ | Top-10 users ranked by sustainability score |
| GET | `/insights` | ✅ | Personalised analytics insights |

### Settings — `/api/settings/`

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| GET | `/` | ✅ | Get user settings |
| PUT | `/` | ✅ | Update settings |

---

## ⚙️ Carbon Calculation Engine

`backend/calculator.py` — **506 lines** of modelled emission logic.

### Emission Factors Used

#### Transport (kg CO₂ / km)
| Vehicle | Fuel | Factor |
|---------|------|--------|
| Bike | Petrol | 0.05 |
| Bike | Electric | 0.02 |
| Car | Petrol | 0.12 |
| Car | Diesel | 0.14 |
| Car | Electric | 0.03 |
| Car | CNG | 0.09 |
| Bus / Train | — | 0.04 |
| Walk / Cycle | — | 0.00 |

**Vehicle Age Multiplier:**
- < 2 years → ×1.00
- 2–5 years → ×1.10
- 5–10 years → ×1.25
- 10+ years → ×1.50

**Driving Condition Factor:**
- City → ×1.20 | Mixed → ×1.00 | Highway → ×0.85

#### Energy
- **Electricity**: `0.82 kg CO₂/kWh` (India average grid intensity)
- **LPG**: `1.5 kg CO₂/day` | **PNG**: `1.2 kg CO₂/day`

#### Diet (kg CO₂ / day base)
| Diet | Base |
|------|------|
| Vegan | 1.5 |
| Vegetarian | 2.5 |
| Eggetarian | 3.0 |
| Non-Vegetarian | 5.0 |

Plus dairy addon: Low `+0.0` | Medium `+0.3` | High `+0.6`

#### Waste
- Base: `0.5 kg CO₂ / kg waste`
- Recycling reduction: Always `−30%` | Sometimes `−15%`
- Composting reduction: `−20%`

### Sustainability Score Formula
```
score = max(0, round(100 − (avg_co2 × 2)))
```
Capped at 100, floored at 0.

### Carbon Classification
| Score | Class | Label |
|-------|-------|-------|
| ≥ 80 | 🟢 | Excellent |
| ≥ 60 | 🔵 | Good |
| ≥ 40 | 🟡 | Moderate |
| ≥ 20 | 🟠 | High |
| < 20 | 🔴 | Critical |

---

## 🤖 AI Engine

`backend/ai_engine.py` — Two functions:

### 1. `get_eco_suggestions(data)` — Rule-Based
Generates personalised recommendations based on latest record:
- Transport > 20 km → suggest public transport / carpooling
- Non-veg diet → suggest Meatless Monday
- Electricity > 10 kWh → suggest LED + appliance management
- Waste > 2 kg → suggest composting

### 2. `predict_future_emissions(records)` — ML (Linear Regression)
Uses **scikit-learn LinearRegression** on historical `(date_ordinal, total_co2)` pairs to predict next 30-day footprint. Requires minimum **5 records** to activate.

```python
model = LinearRegression()
model.fit(X_dates, y_co2)
prediction = model.predict([[future_date_ordinal]])
```

---

## 🖥️ Frontend Pages

| Route | Page | Auth Required |
|-------|------|:---:|
| `/` | Landing Page | ❌ |
| `/login` | Login | ❌ |
| `/register` | Register | ❌ |
| `/dashboard` | Dashboard | ✅ |
| `/add-data` | Add Emission | ✅ |
| `/calculation-process` | Result Breakdown | ✅ |
| `/quick-check` | Quick Estimator | ✅ |
| `/history` | Data History | ✅ |
| `/reports` | Reports & Analytics | ✅ |
| `/tips` | Eco Tips | ✅ |
| `/leaderboard` | Hall of Fame | ✅ |
| `/profile` | User Profile | ✅ |
| `/settings` | Settings | ✅ |

---

## 🚀 Getting Started

### Prerequisites

- **Node.js** ≥ 18.x
- **Python** ≥ 3.10
- **pip**
- Git

---

## 🔧 Environment Setup

### Backend

```bash
cd Eco-TrackAI/backend

# Create and activate virtual environment
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # macOS/Linux

# Install dependencies
pip install flask flask-jwt-extended flask-sqlalchemy flask-migrate \
            flask-bcrypt flask-cors pandas scikit-learn numpy werkzeug
```

### Frontend

```bash
cd Eco-TrackAI/frontend

npm install
```

---

## ▶️ Running the Project

### 1. Start the Backend

```bash
cd backend
venv\Scripts\activate
python app.py
```

Flask will start at **`http://localhost:5000`**

> On first run, the SQLite database `instance/ecotrack.db` is created automatically via `db.create_all()`.

### 2. Start the Frontend Dev Server

```bash
cd frontend
npm run dev
# or
npm start   # starts on :3000
```

The React app will be available at **`http://localhost:3000`**

---

## 📦 Build for Production

```bash
cd frontend
npm run build
```

The production-optimised build is output to `frontend/dist/`. Serve it with any static file server or integrate with the Flask backend.

---

## 🎨 Design System

### Colour Palette

| Token | Light | Dark | Usage |
|-------|-------|------|-------|
| `--eco-primary` | `#16A34A` | `#22C55E` | Brand green, buttons, accents |
| `--eco-secondary` | `#22C55E` | `#4ADE80` | Hover states |
| `--analytics-blue` | `#2563EB` | `#3B82F6` | Charts, secondary actions |
| `--bg-base` | `#F8FAFC` | `#0F172A` | Page background |
| `--bg-card` | `#FFFFFF` | `#1E293B` | Card surfaces |
| `--text` | `#1E293B` | `#F1F5F9` | Primary text |
| `--text-muted` | `#64748B` | `#94A3B8` | Secondary text |

### Custom CSS Classes
- `.neo-card` — Glassmorphism card with blur, border, shadow, and hover lift
- `.btn-neo` — Primary action button (eco-green)
- `.btn-neo-outline` — Outlined secondary button
- `.neo-table` — Styled data table with zebra striping
- `.nav-link` — Sidebar navigation link with active state

### Fonts
- **Inter** — Body text, UI elements
- **Orbitron** — Monospace display font
- **Rajdhani** — Condensed headings

---

## 📊 Key Metrics Tracked

- **CO₂ Emissions** (kg) per entry and aggregated
- **Sustainability Score** (0–100 index)
- **Carbon Streak** (consecutive days of tracking)
- **Trees to Offset** (based on mature tree absorption rate)
- **Weekly & Monthly Comparisons** (% change)
- **Category Breakdown** (Transport / Energy / Diet / Waste)
- **Predicted Next Month** (ML forecast)
- **Global Leaderboard Rank** (community percentile)

---

## 🔒 Security

- Passwords hashed with **Bcrypt**
- All protected routes use **JWT Bearer tokens** validated on every request
- CORS restricted to `/api/*` endpoints
- File uploads validated by extension whitelist (`png`, `jpg`, `jpeg`, `gif`)
- User data scoped by `user_id` on every database query

---

## 📄 License

This project is for educational and personal use. All emission factors are approximations based on publicly available India-region environmental data.

---

<div align="center">

**Built with 💚 for a sustainable future**

*"The transition to a sustainable future is not an option, it is a technical necessity."*

</div>

