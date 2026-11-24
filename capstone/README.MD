# Sport Scout – A Rural Sports Talent Identification Platform with Mobile Video Performance Analysis

> **College Capstone Project / Sports Technology Startup Platform**
> *"Discover Hidden Talent. Build Future Champions."*

**Sport Scout** is an enterprise-grade sports technology platform engineered to identify, assess, and nurture athletic talent from rural communities. Using mobile computer vision and explainable AI biomechanics, the platform enables rural athletes to record or upload sports performances (running, long jump, cricket bowling, football, basketball) and receive automated joint kinematic tracking, posture analysis, consistency scoring, training plans, and scouting trials matching without expensive laboratory equipment.

---

## Phased Implementation Roadmap

- [x] **PHASE 1: Project Structure, Backend, Database & Authentication** (COMPLETED)
- [ ] **PHASE 2: Premium Flutter Mobile UI & Navigation**
- [ ] **PHASE 3: React.js Web Application & Dashboards**
- [ ] **PHASE 4: Athlete Profile & Video Upload/Recording**
- [ ] **PHASE 5: OpenCV & MediaPipe AI Video Analysis Engine**
- [ ] **PHASE 6: Performance Reports & Analytics**
- [ ] **PHASE 7: Scout Dashboard, Talent Discovery Heatmap & Comparison**
- [ ] **PHASE 8: AI Sports Coach, Talent Matching & Training Plans**
- [ ] **PHASE 9: Gamification, Badges, Leaderboards & Trial Opportunities**
- [ ] **PHASE 10: Admin Dashboard, Notifications, Multilingual & Offline Mode**
- [ ] **PHASE 11: Full Integration, End-to-End Testing & Demonstration Preparation**

---

## Phase 1 Deliverables Summary (Completed)

1. **Enterprise Database Architecture (`models.py`)**:
   - 17 Relational Tables: `Users`, `Sports`, `Athletes`, `Scouts`, `Videos`, `VideoAnalysis`, `PerformanceReports`, `TrainingPlans`, `TrainingSessions`, `Challenges`, `Achievements`, `AthleteAchievements`, `Leaderboards`, `Shortlists`, `TrialOpportunities`, `TrialApplications`, `Notifications`.
   - SQLite development database with clean PostgreSQL migration readiness.
   - Unique Sport Scout ID generation scheme: `SS-IND-2026-XXX`.

2. **JWT Authentication & RBAC Security (`auth.py`)**:
   - Signed JSON Web Tokens (`HS256`) with expiration claims.
   - Salted `bcrypt` password hashing.
   - Role-Based Access Control (`athlete`, `scout`, `admin`) dependencies enforcing authorization.

3. **REST API Endpoints**:
   - `/api/auth/register`, `/api/auth/login`, `/api/auth/me`, `/api/auth/forgot-password`
   - `/api/athletes` (CRUD, demographic search by village/district, sport filter)
   - `/api/scouts` (profile, shortlists, scout stats)
   - `/api/trials` (browse opportunities, publish trials, athlete applications)
   - `/api/gamification` (challenges, achievement badges catalog, leaderboard)
   - `/api/admin` (governance, user status toggle, scout verification, platform stats)
   - `/api/reports/detail/{id}/pdf` (Official PDF report generation via ReportLab)

4. **Automated Verification Test Suite**:
   - `test_phase1.py`: 100% test pass rate across schema, JWT, RBAC, and PDF generation.

---

## 1. System Architecture

```
                                  +---------------------------------------+
                                  |         Sport Scout Mobile App        |
                                  |    (Flutter / Dart / Material 3)      |
                                  +-------------------+-------------------+
                                                      |
                                                      | REST APIs / JSON / Multipart
                                                      v
                                  +---------------------------------------+
                                  |          FastAPI REST Backend         |
                                  |   (Python 3.12 / Pydantic / Auth)     |
                                  +---------+-------------------+---------+
                                            |                   |
                        +-------------------+                   +-------------------+
                        v                                                           v
+---------------------------------------+                   +---------------------------------------+
|            SQLite Database            |                   |       AI Video Analysis Engine        |
| (Users, Athletes, Videos, Reports)    |                   |   - OpenCV (Frame extraction & HUD)   |
|            SQLAlchemy ORM             |                   |   - MediaPipe Pose Landmarker         |
+---------------------------------------+                   |   - NumPy (2D Kinematics & Scoring)   |
                                                            +---------------------------------------+
```

---

## 2. Technology Stack

### Mobile Frontend
- **Framework**: Flutter 3.44+
- **Language**: Dart 3.12+
- **Design System**: Material Design 3
- **Color Palette**:
  - Dark Navy Blue (`#0A1128`, `#141E38`, `#1C274C`)
  - Crisp White (`#F8FAFC`, `#FFFFFF`)
  - High-Visibility Green Accents (`#00E676`)
  - Energy Orange Highlights (`#FF9100`)
- **Key Packages**:
  - `http`: REST API communication
  - `image_picker`: Camera video capture & gallery picking
  - `fl_chart`: Athletic progression & improvement curves
  - `intl`: Formatted dates and numbers

### Backend & Database
- **Framework**: FastAPI (High-performance async Python REST framework)
- **ASGI Server**: Uvicorn
- **Database**: SQLite with SQLAlchemy 2.0 ORM
- **Authentication**: Salted SHA-256 with Bearer Session Tokens
- **Static File Serving**: FastAPI StaticFiles for annotated skeleton videos

### AI & Computer Vision
- **MediaPipe Pose Landmarker**: 33 full-body 3D anatomical landmarks tracked with LiteRT on CPU.
- **OpenCV (`cv2`)**: Frame-by-frame video extraction, kinematic HUD overlay rendering, skeleton connection drawing, and MP4 generation.
- **NumPy**: Planar vector joint angle calculation, stride cadence zero-crossing detection, torso inclination, and symmetry deviations.

---

## 3. Implemented Mobile Screens

| Screen | Title | Key Features |
|---|---|---|
| **Screen 1** | Splash Screen | Animated radar scouting motif, Sport Scout logo, tagline *"Discover Rural Talent, Build Future Champions."*, auto-session check. |
| **Screen 2** | Login & Registration | Role selector (Athlete vs. Scout), quick demo credentials toggle, server IP configuration dialog. |
| **Screen 3** | Athlete Registration | Captures rural demographics: full name, age, gender, village, district, state, height, weight, selected sport. |
| **Screen 4** | Athlete Dashboard | Welcome greeting, athlete physical stats, sport badge, composite performance gauge, quick camera record and gallery upload buttons, recent reports list. |
| **Screen 5** | Video Upload & Recording | Live camera recording with timer, gallery file selector, video preview card, sport selector, rural video recording guide. |
| **Screen 6** | AI Video Analysis | Multi-stage CV progress HUD (OpenCV frame extraction -> MediaPipe 33-point tracking -> Kinematics -> Rule-based scoring) with radar scanner animation. |
| **Screen 7** | Performance Report | Overall score (/100), sub-scores (Posture, Consistency, Balance), joint angle telemetry, posture analysis, movement analysis, strengths, improvement areas, actionable training drills, rule-based disclaimer. |
| **Screen 8** | Scout Dashboard | Search by athlete, village, district; filter by sport; overview statistics; side-by-side **Athlete Comparison Tool**; talent identification. |
| **Screen 9** | Athlete History | Chronological training session timeline, previous performance scores, interactive multi-session score progression chart powered by `fl_chart`. |

---

## 4. Biomechanical Analysis Methodology

### Transparent Rule-Based Scoring Formula
$$ \text{Composite Score} = (0.40 \times \text{Posture Score}) + (0.35 \times \text{Consistency Score}) + (0.25 \times \text{Balance Score}) $$

1. **Running (Sprint Mechanics)**:
   - **Step Frequency (Cadence)**: Computed via zero-crossing frequency of hip and ankle vertical oscillation cycles.
   - **Torso Lean**: Measured as angular deviation of shoulder-to-hip vector from true vertical ($8^\circ - 12^\circ$ ideal).
   - **Consistency & Stability**: Standard deviation of trunk sway across 150+ frames.
2. **Long Jump**:
   - **Take-off Posture**: Evaluates peak hip extension angle ($> 155^\circ$ for strong propulsion).
   - **Flight Launch Angle**: Torso alignment at take-off transition.
   - **Landing Cushion**: Knee flexion angle ($< 110^\circ$ safe impact buffer).
3. **Cricket Bowling**:
   - **Arm Extension**: Tracks elbow angle through the delivery arc (ICC educational rule check: $< 15^\circ$ flex change).
   - **Shoulder Tilt**: Lateral trunk sway during delivery crease impact.
   - **Front Knee Bracing**: Front leg brace stability rating.

> **Ethical AI Disclaimer**: All metrics represent uncalibrated 2D video estimates. The system provides objective biomechanical feedback and transparent rule-based coaching indicators; it does not claim to predict professional championships without certified biometric validation.

---

## 5. Execution Instructions (Windows)

### Step 1: Start the FastAPI Backend

Open PowerShell and run:

```powershell
# Navigate to backend directory
cd "c:\Users\MANASA PURIPARTHI\OneDrive\Documents\mobile computing cap\sport_scout\backend"

# (Optional) Verify dependencies
python -m pip install -r requirements.txt

# Start the FastAPI server
python -m uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

The server will automatically:
- Initialize the SQLite database `sport_scout.db`.
- Seed realistic rural talent profiles across Telangana, Haryana, Punjab, and Rajasthan.
- Provide Swagger API documentation at: `http://localhost:8000/docs`.

### Step 2: Verify API Endpoints

In a new PowerShell window:

```powershell
cd "c:\Users\MANASA PURIPARTHI\OneDrive\Documents\mobile computing cap\sport_scout\backend"
python verify_api.py
```

### Step 3: Run the Flutter Mobile Application

In another PowerShell window:

```powershell
# Navigate to mobile directory
cd "c:\Users\MANASA PURIPARTHI\OneDrive\Documents\mobile computing cap\sport_scout\mobile"

# Get packages (if not already fetched)
flutter pub get

# Run on connected Android device or emulator:
flutter run

# To run in Chrome / Web mode:
flutter run -d chrome

# To build release APK for Android phone:
flutter build apk --release
```

The APK file will be generated at:
`sport_scout\mobile\build\app\outputs\flutter-apk\app-release.apk`

---

## 6. Pre-Configured Demo Credentials

For testing and demonstration, use the following pre-seeded accounts:

| Role | Email | Password | Details |
|---|---|---|---|
| **Athlete (Running)** | `ramesh@athlete.org` | `athlete123` | Ramesh Kumar (Rampur, Nizamabad, TS) |
| **Athlete (Long Jump)** | `priya@athlete.org` | `athlete123` | Priya Devi (Kishangarh, Ajmer, RJ) |
| **Scout / Coach** | `scout@sportscout.org` | `scout123` | Coach Rajesh Verma (Regional Talent Scout) |

---

## 7. Project Directory Structure

```
sport_scout/
|-- backend/
|   |-- app/
|   |   |-- assets/
|   |   |   `-- pose_landmarker_lite.task   # MediaPipe model asset
|   |   |-- routes/
|   |   |   |-- athletes.py                # Athlete listing, search, filtering
|   |   |   |-- reports.py                 # Reports & scout intelligence
|   |   |   |-- users.py                   # Register, login, me
|   |   |   `-- videos.py                  # Video upload & AI trigger
|   |   |-- auth.py                        # Passwords & token management
|   |   |-- database.py                    # SQLite engine & sessions
|   |   |-- main.py                        # FastAPI app & static file mounts
|   |   |-- models.py                      # SQLAlchemy models
|   |   |-- sample_data.py                 # Seeded rural athlete datasets
|   |   |-- schemas.py                     # Pydantic schemas
|   |   `-- video_analyzer.py              # OpenCV + MediaPipe CV engine
|   |-- uploads/                           # Uploaded & processed video files
|   |-- requirements.txt
|   |-- sport_scout.db                     # SQLite database file
|   |-- test_backend.py                    # End-to-end CV engine test
|   `-- verify_api.py                      # Full REST endpoint test suite
|
|-- mobile/
|   |-- android/                           # Native Android configuration
|   |   `-- app/src/main/AndroidManifest.xml
|   |-- lib/
|   |   |-- models/
|   |   |   |-- athlete_model.dart
|   |   |   |-- report_model.dart
|   |   |   `-- user_model.dart
|   |   |-- screens/
|   |   |   |-- ai_analysis_screen.dart       # Screen 6: AI CV Analysis HUD
|   |   |   |-- athlete_dashboard_screen.dart # Screen 4: Athlete Dashboard
|   |   |   |-- athlete_history_screen.dart   # Screen 9: Athlete History
|   |   |   |-- athlete_reg_screen.dart       # Screen 3: Athlete Registration
|   |   |   |-- auth_screen.dart              # Screen 2: Login & Role Selection
|   |   |   |-- report_screen.dart            # Screen 7: Performance Report
|   |   |   |-- scout_dashboard_screen.dart   # Screen 8: Scout Portal & Comparison
|   |   |   |-- splash_screen.dart            # Screen 1: Splash Screen
|   |   |   `-- video_upload_screen.dart      # Screen 5: Camera Record & Upload
|   |   |-- services/
|   |   |   `-- api_service.dart              # REST HTTP API Client
|   |   |-- theme/
|   |   |   `-- app_theme.dart                # Material 3 Sports Theme
|   |   |-- widgets/
|   |   |   |-- athlete_card.dart             # Athlete summary list card
|   |   |   `-- score_gauge.dart              # Circular performance score gauge
|   |   `-- main.dart                         # Flutter entry point
|   `-- pubspec.yaml
|
`-- README.md
```

