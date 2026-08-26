
# Experiment 4 — Develop an Application to Link Activities Using Intents

## Student Information

| Field      | Details                 |
| ---------- | ----------------------- |
| Name       | **Yashika Chaudhary** |
| USN        | **25MCAR0139**            |
| Experiment | 4                       |
| Technology | Android Development     |
| Language   | Kotlin                  |
| UI         | XML                     |


---

# 1. Aim

To develop an Android application that demonstrates how to link multiple Activities using **Explicit Intents** and transfer data between Activities.

---

# 2. Experiment Description

This experiment demonstrates the use of Android **Intents** for communication between Activities.

The application contains two Activities:

### MainActivity

The first screen accepts:

* User's Name
* User's USN

After entering the details, the user clicks the **Open Second Activity** button.

### SecondActivity

The second screen receives the Name and USN from the Intent and displays them.

The user can then click **Go Back** to return to the MainActivity.

---

# 3. Scenario Used

A simple student-information scenario is used to demonstrate Activity linking.

The user enters their:

```text
Yashika Chaudhary
25MCAR0139
```

The application transfers this information from `MainActivity` to `SecondActivity` using an Explicit Intent.

For example:

```text
MainActivity

Name: Yashika Chaudhary
USN: 25MCAR0139

        ↓
      Intent
        ↓

SecondActivity

Welcome!

Name: Yashika Chaudhary
USN: 25MCAR0139
```

---

# 4. Concept / Technology

## Android Activity

An Activity represents a single screen of an Android application.

This project contains:

```text
MainActivity
SecondActivity
```

---

## Intent

An Intent is a messaging object used to communicate between Android components.

In this experiment, an Explicit Intent is used to open a specific Activity.

```kotlin
val intent = Intent(
    this,
    SecondActivity::class.java
)
```

---

## Explicit Intent

An Explicit Intent specifies exactly which Activity should be opened.

```kotlin
Intent(this, SecondActivity::class.java)
```

This is different from an Implicit Intent, where Android determines which application/component can handle an action.

---

## Intent Extras

Intent Extras are used to send data from one Activity to another.

The application sends the student's name and USN:

```kotlin
intent.putExtra("USER_NAME", name)
intent.putExtra("USER_USN", usn)
```

The receiving Activity retrieves the data using:

```kotlin
val name = intent.getStringExtra("USER_NAME")
val usn = intent.getStringExtra("USER_USN")
```

---

# 5. Application Flow

```text
┌─────────────────────────┐
│      MainActivity       │
│                         │
│  Enter Name             │
│  Enter USN              │
│                         │
│  [Open Second Activity] │
└────────────┬────────────┘
             │
             │ Explicit Intent
             │
             │ USER_NAME
             │ USER_USN
             ↓
┌─────────────────────────┐
│     SecondActivity      │
│                         │
│       Welcome!          │
│                         │
│  Name: Student Name     │
│  USN: Student USN       │
│                         │
│       [Go Back]         │
└─────────────────────────┘
```

---

# 6. Technologies Used

* Android Studio
* Kotlin
* XML
* Android SDK
* Gradle
* Android Emulator

---

# 7. Project Configuration

| Configuration         | Value                    |
| --------------------- | ------------------------ |
| Application Name      | IntentDemo               |
| Package Name          | `com.example.intentdemo` |
| Language              | Kotlin                   |
| UI                    | XML                      |
| Minimum SDK           | 24                       |
| Compile SDK           | 36                       |
| Target SDK            | 36                       |
| Android Gradle Plugin | 8.11.2                   |

---

# 8. Folder and File Structure

```text
Android-Experiment-4-Intents/
│
├── app/
│   │
│   ├── build.gradle.kts
│   │
│   └── src/
│       │
│       └── main/
│           │
│           ├── AndroidManifest.xml
│           │
│           ├── java/
│           │   └── com/
│           │       └── example/
│           │           └── intentdemo/
│           │               ├── MainActivity.kt
│           │               └── SecondActivity.kt
│           │
│           └── res/
│               │
│               └── layout/
│                   ├── activity_main.xml
│                   └── activity_second.xml
│
├── gradle/
│
├── screenshots/
│   ├── output/
│   │   └── main-output.png
│   │
│   └── test-cases/
│       ├── test-case-1.png
│       ├── test-case-2.png
│       └── test-case-3.png
│
├── build.gradle.kts
├── settings.gradle.kts
├── gradlew
├── gradlew.bat
└── README.md
```

---

# 9. Important Files

### `MainActivity.kt`

Handles:

* User input
* Input validation
* Creation of Explicit Intent
* Passing Name and USN
* Starting `SecondActivity`

### `SecondActivity.kt`

Handles:

* Receiving Intent data
* Displaying Name and USN
* Returning to MainActivity

### `activity_main.xml`

Defines the UI of the first Activity.

### `activity_second.xml`

Defines the UI of the second Activity.

### `AndroidManifest.xml`

Declares the Activities belonging to the application.

---

# 10. Implementation

## Sending Data

The application creates an Explicit Intent:

```kotlin
val intent = Intent(
    this,
    SecondActivity::class.java
)
```

The student's details are attached:

```kotlin
intent.putExtra("USER_NAME", name)
intent.putExtra("USER_USN", usn)
```

The second Activity is launched:

```kotlin
startActivity(intent)
```

---

## Receiving Data

The second Activity retrieves the data:

```kotlin
val name = intent.getStringExtra("USER_NAME")
val usn = intent.getStringExtra("USER_USN")
```

The values are then displayed:

```kotlin
detailsText.text = """
    Name: $name
    
    USN: $usn
""".trimIndent()
```

---

# 11. Input Validation

The application checks whether both fields contain data:

```kotlin
if (name.isEmpty() || usn.isEmpty()) {
    Toast.makeText(
        this,
        "Please enter both Name and USN",
        Toast.LENGTH_SHORT
    ).show()
}
```

If either field is empty, the second Activity is not opened.

---

# 12. Test Cases

## Test Case 1 — Valid Student Details

### Input

```text
Name: Yashika Chaudhary
USN: 25MCAR0139
```

### Action

Click **Open Second Activity**.

### Expected Result

The second Activity opens and displays the Name and USN.

### Screenshot

![Test Case 1](screenshots/test-cases/test-case-1.png)

---

## Test Case 2 — Empty Input

### Input

```text
Name: Empty
USN: Empty
```

### Action

Click **Open Second Activity**.

### Expected Result

A Toast message is displayed:

```text
Please enter both Name and USN
```

The second Activity should not open.

### Screenshot

![Test Case 2](screenshots/test-cases/test-case-2.png)

---

## Test Case 3 — Student Identity Verification

### Input

```text
Name: Yashika Chaudhary
USN: 25MCAR0139
```

### Action

Click **Open Second Activity**.

### Expected Result

The second Activity displays the student's Name and USN.

### Screenshot

![Test Case 3 — Name and USN](screenshots/test-cases/test-case-3.png)

> This test case specifically demonstrates the student's Name and USN as required for the experiment submission.

---

# 13. Output

The final application successfully links the two Activities.

### Main Output

<img width="1470" height="879" alt="Screenshot 2026-08-20 at 10 47 34 AM" src="https://github.com/user-attachments/assets/65ba7603-2083-4a0b-bfd2-b3e06b782ad7" /><img width="1470" height="879" alt="Screenshot 2026-08-20 at 10 47 43 AM" src="https://github.com/user-attachments/assets/3bff3b7b-3f91-4757-9a9f-5b7e19406d34" />
<img width="1470" height="879" alt="Screenshot 2026-08-20 at 10 47 40 AM" src="https://github.com/user-attachments/assets/031d3256-02a3-47ec-a963-702c6a8038cd" />
<img width="1470" height="879" alt="Screenshot 2026-08-20 at 10 47 37 AM" src="https://github.com/user-attachments/assets/411ec11d-aadc-45e3-8850-612852fb4edf" />


---

# 14. How to Run

## Using Android Studio

1. Open the project in Android Studio.
2. Allow Gradle synchronization to complete.
3. Start an Android Emulator or connect an Android device.
4. Select the device.
5. Click **Run**.
6. Enter the student's Name and USN.
7. Click **Open Second Activity**.
8. Verify that the details are displayed.

---

## Using Terminal

Check connected devices:

```bash
~/Library/Android/sdk/platform-tools/adb devices
```

Build and install:

```bash
./gradlew installDebug
```

Launch:

```bash
~/Library/Android/sdk/platform-tools/adb shell monkey -p com.example.intentdemo 1
```


# 15. Result

The Android application was successfully developed to demonstrate Activity linking using Explicit Intents.

The application successfully:

* Opens a second Activity.
* Transfers the student's Name.
* Transfers the student's USN.
* Retrieves Intent Extras.
* Displays the received data.
* Handles empty input.
* Navigates back to the first Activity.

