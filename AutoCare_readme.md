AutoCare – Vehicle Service Manager
Overview

AutoCare is an Android application developed in Kotlin and XML to manage vehicle servicing appointments.

The application allows users to:

Enter vehicle registration details.
Enter the vehicle model.
Select the fuel type.
Select the required service type.
Specify whether vehicle pickup is required.
Select additional service options through a Fragment.
View a complete service summary.
Receive a notification confirming that the service appointment has been created.
Demonstrate Android Activity lifecycle events through Logcat.
Student Information
Field	Details
Application Name	AutoCare
Application Type	Vehicle Service Manager
Platform	Android
Language	Kotlin
UI	XML
IDE	Android Studio
Architecture	Activity + Fragment + Intent
Minimum SDK	API 24+
Features
1. Vehicle Information

The VehicleActivity provides fields for entering:

Vehicle Registration Number
Vehicle Model

Both fields use EditText.

2. Fuel Type Selection

The user can select one fuel type using a RadioGroup.

Available options:

Petrol
Diesel
Electric

Only one fuel type can be selected at a time.

3. Service Type Selection

The application provides another RadioGroup for selecting the required service.

Available options:

General Service
Oil Change
Full Service
4. Pickup Requirement

A ToggleButton is provided for specifying whether vehicle pickup is required.

The button displays:

Pickup Required: YES

or:

Pickup Required: NO
Application Flow

The complete application follows this flow:

                    AutoCare
                       |
                       ▼
              VehicleActivity
                       |
        ┌──────────────┼──────────────┐
        │              │              │
 Vehicle Number    Fuel Type     Service Type
 Vehicle Model                    Pickup Status
        │
        ▼
   Book Service
        |
        ▼
ServiceOptionsFragment
        |
        ├── Car Wash
        ├── Interior Cleaning
        ├── AC Check
        └── Additional Notes
        |
        ▼
 Continue to Summary
        |
        ▼
ServiceSummaryActivity
        |
        ├── Vehicle Number
        ├── Vehicle Model
        ├── Fuel Type
        ├── Service Type
        ├── Pickup Status
        ├── Additional Services
        └── Additional Notes
        |
        ▼
   Notification
Project Structure
AutoCare/
│
├── app/
│   │
│   └── src/
│       │
│       └── main/
│           │
│           ├── java/
│           │   └── com/
│           │       └── example/
│           │           └── autocare/
│           │               │
│           │               ├── VehicleActivity.kt
│           │               ├── ServiceOptionsFragment.kt
│           │               └── ServiceSummaryActivity.kt
│           │
│           ├── res/
│           │   │
│           │   ├── layout/
│           │   │   ├── activity_vehicle.xml
│           │   │   ├── fragment_service_options.xml
│           │   │   └── activity_service_summary.xml
│           │   │
│           │   ├── drawable/
│           │   │
│           │   └── values/
│           │
│           └── AndroidManifest.xml
│
└── README.md
Activities and Fragment
VehicleActivity

VehicleActivity is the main screen of the application.

It is responsible for collecting:

Vehicle Registration Number
Vehicle Model
Fuel Type
Service Type
Pickup Requirement

The Activity validates the required fields and then opens the ServiceOptionsFragment.

Main components
EditText
RadioGroup
RadioButton
ToggleButton
Button
FrameLayout
ServiceOptionsFragment

ServiceOptionsFragment displays additional service information after the user clicks Book Service.

The Fragment provides:

Car Wash
Interior Cleaning
AC Check
Additional Notes

The Fragment receives the vehicle information from VehicleActivity using a Bundle.

ServiceSummaryActivity

ServiceSummaryActivity displays the information collected throughout the application.

The summary includes:

Vehicle Number
Vehicle Model
Fuel Type
Service Type
Pickup Status
Additional Services
Additional Notes

The Activity receives the information using an Intent.

Data Passing

Data is passed from VehicleActivity to ServiceOptionsFragment.

Example:

val fragment = ServiceOptionsFragment.newInstance(
    vehicleNumber,
    vehicleModel,
    fuelType,
    serviceType,
    pickupRequired
)

The Fragment then passes the collected information to ServiceSummaryActivity using an Intent.

Example:

intent.putExtra(
    "vehicleNumber",
    vehicleNumber
)

intent.putExtra(
    "vehicleModel",
    vehicleModel
)

intent.putExtra(
    "fuelType",
    fuelType
)

intent.putExtra(
    "serviceType",
    serviceType
)

intent.putExtra(
    "pickupRequired",
    pickupRequired
)

The Summary Activity retrieves the values using:

intent.getStringExtra("vehicleNumber")

and:

intent.getBooleanExtra(
    "pickupRequired",
    false
)
Fragment Navigation

When the user clicks Book Service, the application creates the Fragment:

val fragment = ServiceOptionsFragment.newInstance(
    vehicleNumber,
    vehicleModel,
    fuelType,
    serviceType,
    pickupRequired
)

The Fragment is displayed using:

supportFragmentManager.beginTransaction()
    .replace(
        R.id.fragmentContainer,
        fragment
    )
    .addToBackStack(null)
    .commit()

This demonstrates the use of Fragment Transactions in Android.

Intent Navigation

After selecting additional service information, the user clicks:

Continue to Summary

An explicit Intent is created:

val intent = Intent(
    requireContext(),
    ServiceSummaryActivity::class.java
)

The required data is attached using putExtra() and the Summary Activity is launched using:

startActivity(intent)
Notification

After the Summary Activity is opened, AutoCare generates a notification confirming that the appointment has been created.

Notification text:

AutoCare

Vehicle service appointment has been created.

For Android 13 and later, the application requests the notification permission:

<uses-permission
    android:name="android.permission.POST_NOTIFICATIONS" />

A notification channel is also created for Android 8.0 and later.

val channel = NotificationChannel(
    CHANNEL_ID,
    "AutoCare Service",
    NotificationManager.IMPORTANCE_DEFAULT
)
Activity Lifecycle

The application demonstrates Activity lifecycle callbacks using Logcat.

The following lifecycle methods are implemented:

onCreate()
onStart()
onResume()
onPause()
onStop()
onDestroy()

Example:

override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)

    setContentView(R.layout.activity_vehicle)

    Log.d(TAG, "onCreate called")
}

Other lifecycle events are similarly logged:

Log.d(TAG, "onStart called")
Log.d(TAG, "onResume called")
Log.d(TAG, "onPause called")
Log.d(TAG, "onStop called")
Log.d(TAG, "onDestroy called")
Logcat Demonstration

Open Android Studio:

View
 → Tool Windows
 → Logcat

Search for:

VehicleActivity

The application produces logs such as:

D/VehicleActivity: onCreate called
D/VehicleActivity: onStart called
D/VehicleActivity: onResume called

When the Activity loses focus or becomes invisible, corresponding lifecycle events can be observed.

For the Summary Activity, search for:

ServiceSummary
Android Manifest

The application declares notification permission and the required Activities.

<uses-permission
    android:name="android.permission.POST_NOTIFICATIONS" />

VehicleActivity acts as the launcher Activity:

<activity
    android:name=".VehicleActivity"
    android:exported="true">

    <intent-filter>

        <action
            android:name="android.intent.action.MAIN" />

        <category
            android:name="android.intent.category.LAUNCHER" />

    </intent-filter>

</activity>

ServiceSummaryActivity is launched through an explicit Intent.

UI Components Used
Component	Purpose
ScrollView	Makes the screen scrollable
LinearLayout	Organizes UI elements vertically
TextView	Displays labels and information
EditText	Accepts vehicle information
RadioGroup	Groups selectable options
RadioButton	Selects fuel/service type
ToggleButton	Specifies pickup requirement
Button	Performs actions
FrameLayout	Container for Fragment
CheckBox	Selects additional services
Validation

The application performs basic input validation before proceeding.

Vehicle Registration Number

The application checks that the registration number is not empty.

if (vehicleNumber.isEmpty()) {
    etVehicleNumber.error = "Enter vehicle number"
    return@setOnClickListener
}
Vehicle Model

The model is also checked:

if (vehicleModel.isEmpty()) {
    etVehicleModel.error = "Enter vehicle model"
    return@setOnClickListener
}
Fuel Type

The user must select one of:

Petrol
Diesel
Electric
Service Type

The user must select one of:

General Service
Oil Change
Full Service
Technologies Used
Kotlin – Application programming language
XML – User interface design
Android SDK – Android application development
Android Studio – Development environment
AppCompat – Activity support
Fragments – Additional service information
Explicit Intent – Activity navigation and data transfer
NotificationCompat – Notifications
Logcat – Lifecycle demonstration
How to Run
1. Open the Project

Open the AutoCare project in Android Studio.

2. Sync Gradle

Allow Android Studio to complete Gradle synchronization.

3. Start an Emulator

For example:

emulator -avd Pixel_8a

Verify the device:

adb devices

Expected:

List of devices attached
emulator-5554    device
4. Run the Application

Select the app run configuration and click:

Run ▶

The application launches with VehicleActivity.

Application Screens
Vehicle Activity
AutoCare
Vehicle Service Manager

Vehicle Registration Number
[ Enter registration number ]

Vehicle Model
[ Enter vehicle model ]

Fuel Type
○ Petrol
○ Diesel
○ Electric

Service Type
○ General Service
○ Oil Change
○ Full Service

[ Pickup Required: NO ]

[ Book Service ]
Service Options Fragment
Service Options

☐ Car Wash
☐ Interior Cleaning
☐ AC Check

[ Additional Notes ]

[ Continue to Summary ]
Service Summary Activity
Service Summary

Vehicle Number: KA01AB1234
Vehicle Model: Tata Nexon
Fuel Type: Electric
Service Type: Full Service
Pickup Status: Required
Additional Services: Car Wash, AC Check
Notes: Check brakes

[ Done ]
Notification
AutoCare

Output

<img width="460" height="778" alt="Screenshot 2026-09-18 at 3 46 36 PM" src="https://github.com/user-attachments/assets/120b7d6e-fde9-48db-a587-b29ddd774fe8" />
<img width="460" height="778" alt="Screenshot 2026-09-18 at 3 46 32 PM" src="https://github.com/user-attachments/assets/3b2dee04-2d6e-41ca-bded-e315addafd0e" />
<img width="460" height="778" alt="Screenshot 2026-09-18 at 3 46 25 PM" src="https://github.com/user-attachments/assets/f0096a46-f9cc-42ab-9a5a-371484cb8d9e" />
<img width="460" height="778" alt="Screenshot 2026-09-18 at 3 46 19 PM" src="https://github.com/user-attachments/assets/e9a345db-ada0-46aa-ad22-b95549d9968c" />
<img width="460" height="778" alt="Screenshot 2026-09-18 at 3 45 42 PM" src="https://github.com/user-attachments/assets/9b421f06-eb2a-44a6-9c6a-05f81923257b" />
