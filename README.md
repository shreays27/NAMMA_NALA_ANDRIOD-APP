🌊 Namma-Nala — Canal Health Monitor
Android App (Kotlin + Room Database) — Project #69
📋 Project Overview
Namma-Nala empowers farmers to act as "Canal Guards." When a farmer spots a leak, blockage, or illegal water lifting, they report it via the app. It uses GPS and photos to pinpoint the exact location, allowing irrigation engineers to respond instantly.
🏗️ Architecture
MVVM Architecture
├── Models (Room Entities)
├── DAOs (Room Data Access Objects)
├── Database (NammaNalaDatabase)
├── Repository (NammaNalaRepository)
├── ViewModel (MainViewModel)
├── Fragments (UI)
└── Adapters (RecyclerView)
📦 Features Implemented

✅ 1. Breach Report
•Take photo of the leak → GPS auto-captures location → Submit
•Calculates distance to nearest milestone/village
•Report types: BREACH, BLOCKAGE, ILLEGAL_LIFTING, SILT
•Camera + Gallery photo support
•Works with simulated GPS for emulator testing

✅ 2. Water Status Feed (Crowdsourced)
•"Water reached [Village X] today" messages
•Shows water level percentage with progress bar
•Status: FLOWING / NORMAL / LOW / HIGH / BLOCKED
•Timestamp of last update shown on every entry ✓

✅ 3. Maintenance Tracker
•View upcoming cleaning/repair/inspection schedule
•Mark maintenance tasks as complete
•Shows assigned team and scheduled date
•Low-bandwidth optimized (no heavy images)

✅ 4. Silt Alert
•Log areas where heavy silt is reducing water flow
•Severity levels: LOW / MEDIUM / HIGH / CRITICAL
•Shows GPS coordinates + flow reduction percentage
•Mark alerts as resolved

✅ Success Criteria Met
•Distance from nearest Milestone/Village displayed on every report ✓
•Water Status feed shows timestamp of last update ✓
•UI optimized for low-bandwidth (no network calls, local Room DB) ✓

🛠️ Tech Stack
Component
Technology
Language
Kotlin
Database
Room (SQLite)
Architecture
MVVM + LiveData
Navigation
Jetpack Navigation Component
Location
FusedLocationProviderClient
UI
Material Design 3
Async
Kotlin Coroutines
Image
Glide

🚀 How to Open in Android Studio
Prerequisites
•Android Studio Hedgehog (2023.1.1) or newer
•JDK 17
•Android SDK 34
•Minimum API: 24 (Android 7.0)

Steps
1.Extract the ZIP file
2.Open Android Studio
3.Click File → Open
4.Navigate to the extracted NammaNala folder and click OK
5.Wait for Gradle sync to complete (downloads dependencies ~2-3 mins first time)
6.Connect a device or start an AVD Emulator (API 24+)
7.Click ▶️ Run

Optional: Google Maps API Key
To enable the map overlay feature:
1.Get a key from Google Cloud Console
2.Enable Maps SDK for Android
3.Open AndroidManifest.xml
4.Replace YOUR_GOOGLE_MAPS_API_KEY_HERE with your key

Note: The app works fully without a Maps key — GPS coordinates and milestone distances still work via FusedLocationProviderClient.
📱 App Screens
Screen
Description
Splash
Animated logo with app branding
Home
Dashboard with stats, latest water update, recent reports
Report Breach
GPS + photo + form submission
Water Status
Crowdsourced village water feed with timestamps
Maintenance
Canal cleaning/repair schedule tracker
Silt Alerts
Active silt blockage alerts with severity levels

🗄️ Database Schema
breach_reports
Column
Type
Description
id
INTEGER PK
Auto-generated
title
TEXT
Report title
reportType
TEXT
BREACH/BLOCKAGE/ILLEGAL_LIFTING/SILT
latitude
REAL
GPS latitude
longitude
REAL
GPS longitude
milestoneName
TEXT
Nearest milestone name
distanceToMilestone
REAL
Distance in km
photoPath
TEXT
Local photo file path
status
TEXT
PENDING/IN_PROGRESS/RESOLVED
timestamp
INTEGER
Unix timestamp
water_status
Column
Type
Description
villageName
TEXT
Village/town name
canalSection
TEXT
Canal section ID
waterLevel
REAL
0-100%
status
TEXT
FLOWING/BLOCKED/LOW/NORMAL/HIGH
timestamp
INTEGER
Last update time
maintenance_schedule
silt_alerts

📍 Simulated Canal Milestones (Kolar District, Karnataka)
KM-0   → Headworks        (13.0827°N, 78.0533°E)
KM-5   → Kolar Village    (13.1050°N, 78.0900°E)
KM-10  → Malur Nala       (13.1367°N, 78.1332°E)
KM-15  → Srinivaspur      (13.1650°N, 78.1700°E)
KM-20  → Bangarpet        (13.2180°N, 78.2147°E)
KM-25  → Mulbagal         (13.2650°N, 78.2580°E)
KM-30  → Tail-End         (13.3100°N, 78.3000°E)

🧪 Testing on Emulator
The app detects when GPS is unavailable and uses a simulated location in the Kolar region automatically — no additional setup needed for emulator testing.

📁 Project Structure
app/src/main/
├── java/com/nammanala/app/
│   ├── activities/
│   │   ├── SplashActivity.kt
│   │   ├── MainActivity.kt
│   │   └── ReportBreachActivity.kt
│   ├── fragments/
│   │   ├── HomeFragment.kt
│   │   ├── WaterStatusFragment.kt
│   │   ├── MaintenanceFragment.kt
│   │   └── SiltAlertFragment.kt
│   ├── adapters/
│   │   ├── RecentReportsAdapter.kt
│   │   ├── WaterStatusAdapter.kt
│   │   ├── MaintenanceAdapter.kt
│   │   └── SiltAlertAdapter.kt
│   ├── models/
│   │   ├── BreachReport.kt
│   │   ├── WaterStatus.kt
│   │   ├── MaintenanceSchedule.kt
│   │   └── SiltAlert.kt
│   ├── database/
│   │   ├── NammaNalaDatabase.kt
│   │   ├── BreachReportDao.kt
│   │   ├── WaterStatusDao.kt
│   │   ├── MaintenanceScheduleDao.kt
│   │   └── SiltAlertDao.kt
│   ├── repository/
│   │   └── NammaNalaRepository.kt
│   └── utils/
│       ├── MainViewModel.kt
│       ├── LocationHelper.kt
│       └── DateTimeUtils.kt
└── res/
    ├── layout/       (all XML layouts)
    ├── drawable/     (vector icons)
    ├── navigation/   (nav_graph.xml)
    ├── menu/         (bottom_nav_menu.xml)
    ├── anim/         (fade_in, slide_up)
    └── values/       (colors, strings, themes)
