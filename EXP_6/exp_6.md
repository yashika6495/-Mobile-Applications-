# Experiment 5 — Develop an Application Using Basic Android Views

## Student Information

| Field      | Details               |
| ---------- | --------------------- |
| Name       | **Yashika Chaudhary** |
| USN        | **25MCAR0139**        |
| Experiment | 5                     |
| Technology | Android Development   |
| Language   | Kotlin                |
| UI         | XML                   |

---

# 1. Aim

To develop an Android application using basic Android UI Views such as **TextView, EditText, Button, ImageButton, CheckBox, ToggleButton, RadioButton, and RadioGroup**, and demonstrate how these components are used to accept and process user input.

---

# 2. Experiment Description

This experiment demonstrates the use of fundamental Android Views to create an interactive **Student Registration Application**.

The application contains a registration form where the user can enter personal information, select their gender, choose multiple interests, enable or disable notifications, submit the form, and clear the entered information.

The application uses the following Android Views:

* `TextView`
* `EditText`
* `Button`
* `ImageButton`
* `CheckBox`
* `ToggleButton`
* `RadioButton`
* `RadioGroup`

A `ScrollView` and `LinearLayout` are also used to organize the user interface.

---

# 3. Scenario Used

A simple student-registration scenario is used to demonstrate the functionality of basic Android Views.

The user enters:

```text
Name: Yashika Chaudhary
Email: yashika@gmail.com
Phone: 9876543210
```

The user can then select their gender and interests.

For example:

```text
Student Registration

Full Name
[ Yashika Chaudhary ]

Email Address
[ yashika@gmail.com ]

Phone Number
[ 9876543210 ]

Gender
○ Male
● Female
○ Other

Interests
☑ Android Development
☑ Web Development
☐ Artificial Intelligence / ML

Notifications
[ ON ]

[ CREATE PROFILE ]

       [ X ]
```

When **CREATE PROFILE** is clicked, the application reads the entered information and displays it using a Toast message.

---

# 4. Concepts / Technology

## TextView

`TextView` is used to display text to the user.

Examples in this application include:

```text
Student Registration
Personal Information
Gender
Interests
Notifications
```

Example:

```xml
<TextView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Full Name" />
```

---

## EditText

`EditText` allows the user to enter information.

The application uses three EditTexts for:

* Full Name
* Email Address
* Phone Number

Example:

```xml
<EditText
    android:id="@+id/nameEditText"
    android:layout_width="match_parent"
    android:layout_height="52dp"
    android:hint="Enter your full name" />
```

The entered value is retrieved in Kotlin using:

```kotlin
val name = nameEditText.text.toString()
```

---

## Button

A `Button` performs an action when clicked.

The application uses a button named:

```text
CREATE PROFILE
```

Example:

```xml
<Button
    android:id="@+id/submitButton"
    android:text="CREATE PROFILE" />
```

The click event is handled using:

```kotlin
submitButton.setOnClickListener {
    // Perform action
}
```

---

## ImageButton

An `ImageButton` is a button that displays an image or icon.

In this application, it is used to clear the registration form.

```xml
<ImageButton
    android:id="@+id/clearImageButton"
    android:contentDescription="Clear form" />
```

When clicked, all entered information is reset.

---

## CheckBox

A `CheckBox` allows the user to select multiple options.

The application provides:

```text
☐ Android Development
☐ Web Development
☐ Artificial Intelligence / ML
```

Multiple options can be selected at the same time.

The state of a CheckBox can be checked using:

```kotlin
if (androidCheckBox.isChecked) {
    // Android selected
}
```

---

## ToggleButton

A `ToggleButton` provides an ON/OFF state.

The application uses it for notifications:

```text
Notifications

[ ON ]
```

The state can be retrieved using:

```kotlin
val notificationsEnabled =
    notificationToggleButton.isChecked
```

---

## RadioButton

A `RadioButton` allows the user to select one option from a group.

The application provides:

```text
○ Male
○ Female
○ Other
```

---

## RadioGroup

`RadioGroup` is used to group multiple RadioButtons.

```xml
<RadioGroup
    android:id="@+id/genderRadioGroup">

    <RadioButton
        android:id="@+id/maleRadioButton"
        android:text="Male" />

    <RadioButton
        android:id="@+id/femaleRadioButton"
        android:text="Female" />

    <RadioButton
        android:id="@+id/otherRadioButton"
        android:text="Other" />

</RadioGroup>
```

Only one RadioButton inside the group can be selected at a time.

The selected option is retrieved using:

```kotlin
val selectedGenderId =
    genderRadioGroup.checkedRadioButtonId
```

---

# 5. Application Flow

```text
┌───────────────────────────────┐
│       Student Registration    │
│                               │
│  Enter Name                   │
│  Enter Email                  │
│  Enter Phone                  │
│                               │
│  Select Gender                │
│                               │
│  Select Interests             │
│                               │
│  Enable/Disable Notifications │
│                               │
│       [ CREATE PROFILE ]      │
│                               │
│            [ X ]              │
└───────────────┬───────────────┘
                │
                │
        ┌───────┴────────┐
        │                │
        ▼                ▼
     Submit            Clear
        │                │
        ▼                ▼
   Read Input       Reset Form
        │
        ▼
   Validate Name
        │
        ▼
   Display Result
        │
        ▼
      Toast
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

| Configuration         | Value                       |
| --------------------- | --------------------------- |
| Application Name      | BasicViewsApp               |
| Package Name          | `com.example.basicviewsapp` |
| Language              | Kotlin                      |
| UI                    | XML                         |
| Minimum SDK           | 23                          |
| Compile SDK           | 36                          |
| Target SDK            | 36                          |
| Android Gradle Plugin | 8.11.2                      |
| Kotlin                | 2.0.21                      |

---

# 8. Folder and File Structure

```text
Android-Basic-Views/
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
│           │           └── basicviewsapp/
│           │               └── MainActivity.kt
│           │
│           └── res/
│               │
│               └── layout/
│                   └── activity_main.xml
│
├── gradle/
│   │
│   └── libs.versions.toml
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

* Reading user input
* Connecting XML Views with Kotlin
* Handling the Submit button
* Reading CheckBox states
* Reading RadioButton selection
* Reading ToggleButton state
* Clearing the form
* Displaying Toast messages

### `activity_main.xml`

Defines the complete user interface.

It contains:

* TextViews
* EditTexts
* Button
* ImageButton
* CheckBoxes
* ToggleButton
* RadioButtons
* RadioGroup
* ScrollView
* LinearLayouts

### `AndroidManifest.xml`

Contains the application configuration and declares the application's Activity.

### `libs.versions.toml`

Contains the versions of Android Gradle Plugin, Kotlin, AndroidX libraries, Material libraries, and other dependencies.

---

# 10. Implementation

## Connecting XML Views with Kotlin

Each important View is assigned an ID in XML.

For example:

```xml
<EditText
    android:id="@+id/nameEditText"
    ... />
```

The View is accessed in Kotlin using:

```kotlin
val nameEditText =
    findViewById<EditText>(R.id.nameEditText)
```

This establishes the connection between the XML UI and Kotlin logic.

---

## Reading EditText Data

The user's name is retrieved using:

```kotlin
val name = nameEditText.text.toString()
```

Similarly:

```kotlin
val email = emailEditText.text.toString()
val phone = phoneEditText.text.toString()
```

---

## Reading RadioButton Data

First, the selected RadioButton ID is obtained:

```kotlin
val selectedGenderId =
    genderRadioGroup.checkedRadioButtonId
```

The selected RadioButton is then found:

```kotlin
val selectedRadioButton =
    findViewById<RadioButton>(selectedGenderId)
```

Its text can then be retrieved:

```kotlin
val gender =
    selectedRadioButton.text.toString()
```

---

## Reading CheckBox Data

The application checks each CheckBox:

```kotlin
if (androidCheckBox.isChecked) {
    interests.add("Android Development")
}

if (webCheckBox.isChecked) {
    interests.add("Web Development")
}

if (aiCheckBox.isChecked) {
    interests.add("AI / ML")
}
```

This allows the user to select multiple interests.

---

## Reading ToggleButton Data

The notification status is obtained using:

```kotlin
val notificationsEnabled =
    notificationToggleButton.isChecked
```

If the value is `true`, notifications are enabled.

If the value is `false`, notifications are disabled.

---

# 11. Submit Button

The Submit button uses an `OnClickListener`:

```kotlin
submitButton.setOnClickListener {

    val name = nameEditText.text.toString()
    val email = emailEditText.text.toString()
    val phone = phoneEditText.text.toString()

    // Process information
}
```

When the user clicks:

```text
[ CREATE PROFILE ]
```

the application collects all the information entered or selected by the user.

---

# 12. Input Validation

The application checks whether the Name field is empty.

```kotlin
if (name.isEmpty()) {

    nameEditText.error =
        "Please enter your name"

    return@setOnClickListener
}
```

If the user doesn't enter a name, the application displays an error and stops the submission process.

---

# 13. Displaying the Result

After collecting the information, a message is created:

```kotlin
val message = """
    Name: $name
    Email: $email
    Phone: $phone
    Gender: $gender
    Interests: ${interests.joinToString(", ")}
    Notifications: ${
        if (notificationsEnabled) "ON" else "OFF"
    }
""".trimIndent()
```

The result is displayed using a Toast:

```kotlin
Toast.makeText(
    this,
    message,
    Toast.LENGTH_LONG
).show()
```

---

# 14. Clear Button

The ImageButton is used to reset the form.

When clicked:

```kotlin
clearImageButton.setOnClickListener {

    nameEditText.text.clear()
    emailEditText.text.clear()
    phoneEditText.text.clear()

    genderRadioGroup.clearCheck()

    androidCheckBox.isChecked = false
    webCheckBox.isChecked = false
    aiCheckBox.isChecked = false

    notificationToggleButton.isChecked = true
}
```

The form returns to its initial state.

---

# 15. UI Design

The application uses a dark-themed interface.

```text
Background       → #000000
Cards            → #171717
Input Fields     → #242424
Primary Text     → #FFFFFF
Secondary Text   → #A0A0A0
Accent           → #7C4DFF
```

The dark theme provides a modern and visually pleasing appearance while maintaining good contrast between the different sections.

---

# 16. Output

The final application successfully demonstrates the use of basic Android Views.

### Main Screen

The application displays a dark-themed Student Registration form containing:

* Student Registration heading
* Personal Information section
* Full Name EditText
* Email EditText
* Phone EditText
* Gender RadioGroup
* Interest CheckBoxes
* Notification ToggleButton
* Create Profile Button
* Clear ImageButton

### Expected Flow

```text
┌───────────────────────────────┐
│     Student Registration      │
│                               │
│  Personal Information        │
│  ┌─────────────────────────┐ │
│  │ Enter your full name    │ │
│  └─────────────────────────┘ │
│                               │
│  ┌─────────────────────────┐ │
│  │ Enter your email        │ │
│  └─────────────────────────┘ │
│                               │
│  ┌─────────────────────────┐ │
│  │ Enter phone number      │ │
│  └─────────────────────────┘ │
│                               │
│  Gender                       │
│  ○ Male                       │
│  ○ Female                     │
│  ○ Other                      │
│                               │
│  Interests                    │
│  ☐ Android Development        │
│  ☐ Web Development            │
│  ☐ Artificial Intelligence    │
│                               │
│  Notifications        [ ON ]  │
│                               │
│  ┌─────────────────────────┐ │
│  │    CREATE PROFILE      │ │
│  └─────────────────────────┘ │
│                               │
│             [ X ]             │
└───────────────────────────────┘
```

---

# 17. How to Run

## Using Android Studio

1. Open the project in Android Studio.
2. Allow Gradle synchronization to complete.
3. Start an Android Emulator or connect a physical Android device.
4. Select the device.
5. Click **Run**.
6. The Student Registration screen will appear.
7. Enter the required information.
8. Select gender.
9. Select one or more interests.
10. Turn notifications ON or OFF.
11. Click **CREATE PROFILE**.
12. Verify the Toast message.
13. Click the clear button to reset the form.

---

## Using Terminal

Check connected devices:

```bash
~/Library/Android/sdk/platform-tools/adb devices
```

Build and install the application:

```bash
./gradlew installDebug
```

Launch the application:

```bash
~/Library/Android/sdk/platform-tools/adb shell monkey -p com.example.basicviewsapp 1
```

---

# 18. Result

The Android application was successfully developed using basic Android Views.

The application successfully demonstrates:

* `TextView` for displaying text.
* `EditText` for accepting user input.
* `Button` for submitting the form.
* `ImageButton` for clearing the form.
* `CheckBox` for selecting multiple interests.
* `ToggleButton` for enabling/disabling notifications.
* `RadioButton` for selecting gender.
* `RadioGroup` for grouping gender options.
* `ScrollView` for handling content that exceeds the screen size.
* Kotlin event handling using `setOnClickListener`.
* Reading and processing user input.
* Basic form validation.
* Displaying results using Toast messages.

Thus, the experiment successfully demonstrates the implementation and interaction of fundamental Android UI Views using **Kotlin and XML**.
