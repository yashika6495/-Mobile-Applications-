# Experiment 8 — Implement Menus and WebView in an Android Application

## Student Details

| Field | Details |
|---|---|
| **Name** | Yashika Chaudhary |
| **USN** | 25MCAR0139 |
| **Experiment** | Experiment 8 |
| **Topic** | Menus and WebView in Android |
| **Technology** | Kotlin + XML |
| **IDE** | Android Studio |

---

## 1. Aim

To implement **Menus and WebView** in an Android application using Kotlin and XML. The application demonstrates an options/kebab menu, context menu, sharing functionality, a GridView image gallery, and a WebView for displaying web content.

---

## 2. Concept / Technology Behind the Experiment

### Options Menu / Kebab Menu

An Android **Options Menu** provides actions that are not directly visible on the main screen. In this experiment, the options menu is displayed through the three-dot/kebab menu and provides:

- Select All
- Share
- Open Web Page

The menu is created using an XML menu resource and inflated in `MainActivity.kt`.

### Context Menu

A **Context Menu** provides actions related to a particular UI element. In this experiment, long-pressing an image displays:

- Edit
- Delete
- Share

### WebView

`WebView` is an Android UI component that displays web content inside an application instead of opening a separate browser.

The application configures the WebView using:

```kotlin
webView.settings.javaScriptEnabled = true
webView.settings.domStorageEnabled = true
webView.webViewClient = WebViewClient()
```

The application initially attempts to load:

```text
https://www.google.com
```

The **Open Web Page** menu option loads:

```text
https://www.android.com
```

### Intent / Sharing

The Share option uses Android's `ACTION_SEND` intent to open the system share chooser.

---

## 3. Scenario Used

The experiment is demonstrated using a simple **Image Gallery application**.

The scenario is:

1. The user opens the application.
2. A WebView is displayed at the top of the screen.
3. An Image Gallery is displayed below the WebView.
4. The user can open the three-dot menu.
5. The user can select all images, share content, or open a web page.
6. The user can long-press an image to open a context menu.
7. The user can select Edit, Delete, or Share from the context menu.

This scenario demonstrates how menus and embedded web content can be combined in a practical Android application.

---

## 4. Features

- WebView for displaying web pages
- Options/kebab menu
- Select All action
- Share action
- Open Web Page action
- Context menu
- Edit/Delete/Share context actions
- GridView image gallery
- Android Intent-based sharing
- Internet permission
- Student name and USN identification

---

## 5. Project Structure

```text
Experiment8/
│
├── app/
│   └── src/
│       └── main/
│           │
│           ├── java/
│           │   └── com/example/experiment8/
│           │       ├── MainActivity.kt
│           │       └── ImageAdapter.kt
│           │
│           ├── res/
│           │   │
│           │   ├── drawable/
│           │   │   ├── image1.jpg
│           │   │   ├── image2.jpg
│           │   │   └── image3.jpg
│           │   │
│           │   ├── layout/
│           │   │   ├── activity_main.xml
│           │   │   └── grid_item.xml
│           │   │
│           │   ├── menu/
│           │   │   └── main_menu.xml
│           │   │
│           │   └── values/
│           │       ├── strings.xml
│           │       ├── colors.xml
│           │       └── themes.xml
│           │
│           └── AndroidManifest.xml
│
├── screenshots/
│   ├── output.png
│   ├── test-case-1-usn-name.png
│   ├── test-case-2-menu.png
│   └── test-case-3-context-menu.png
│
└── README.md
```

---

## 6. Important Files

### `MainActivity.kt`

Responsible for:

- Initializing the WebView
- Initializing the GridView
- Loading web content
- Creating the options menu
- Handling menu actions
- Creating the context menu
- Handling context-menu actions
- Handling image selection

### `ImageAdapter.kt`

Responsible for displaying the images and their names inside the GridView.

### `activity_main.xml`

Contains:

- WebView
- Student details
- Image Gallery title
- GridView

### `grid_item.xml`

Defines the appearance of each image item.

### `main_menu.xml`

Defines the options/kebab menu items.

### `AndroidManifest.xml`

Contains the Internet permission required for WebView:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

---

## 7. Application UI / Wireframe

```text
┌─────────────────────────────────────┐
│ Name: Yashika Chaudhary             │
│ USN: 25MCAR0139                     │
├─────────────────────────────────────┤
│           WebView                   │
│       Web Page Content              │
├─────────────────────────────────────┤
│ Image Gallery                    ⋮  │
├─────────────┬─────────────┬─────────┤
│   Image 1   │   Image 2   │ Image 3 │
│             │             │         │
└─────────────┴─────────────┴─────────┘
```

---

## 8. Implementation

### Internet Permission

Add the following to `AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

### WebView

```kotlin
webView = findViewById(R.id.webView)

webView.settings.javaScriptEnabled = true
webView.settings.domStorageEnabled = true
webView.webViewClient = WebViewClient()

webView.loadUrl("https://www.google.com")
```

### Options Menu

```kotlin
override fun onCreateOptionsMenu(menu: Menu): Boolean {
    menuInflater.inflate(R.menu.main_menu, menu)
    return true
}
```

### Context Menu

```kotlin
registerForContextMenu(gridView)
```

The context menu provides:

```text
Edit
Delete
Share
```

### Share Intent

```kotlin
val shareIntent = Intent(Intent.ACTION_SEND)

shareIntent.type = "text/plain"

shareIntent.putExtra(
    Intent.EXTRA_TEXT,
    "Check out this Android application!"
)

startActivity(
    Intent.createChooser(
        shareIntent,
        "Share using"
    )
)
```

---

# 9. Test Cases

Three test cases are required for the submission. Each test case must have its own screenshot.

---

## Test Case 1 — Student Identification

### Objective

Verify that the application clearly displays the student's **USN and name**.

### Test Data

```text
Name: Yashika Chaudhary
USN: 25MCAR0139
```

### Steps

1. Launch the application.
2. Display the student identification section.
3. Verify that the name and USN are visible.

### Expected Result

The application should clearly display:

```text
Name: Yashika Chaudhary
USN: 25MCAR0139
```

### Screenshot

Save the screenshot as:

```text
screenshots/test-case-1-usn-name.png
```

> The screenshot must visibly contain both the student's name and USN.

---

## Test Case 2 — Options / Kebab Menu

### Objective

Verify that the options menu works correctly.

### Steps

1. Launch the application.
2. Click the three-dot/kebab menu.
3. Verify that the following options are displayed:
   - Select All
   - Share
   - Open Web Page
4. Click **Share** and verify that the Android share chooser appears.

### Expected Result

The kebab menu should display:

```text
Select All
Share
Open Web Page
```

The Share option should open the Android sharing interface.

### Screenshot

Save the screenshot as:

```text
screenshots/test-case-2-menu.png
```

The screenshot should clearly show the open menu.

---

## Test Case 3 — Context Menu / WebView

### Objective

Verify that the context menu and WebView functionality work correctly.

### Steps

1. Launch the application.
2. Verify that the WebView is visible at the top.
3. Long-press an image.
4. Verify that the context menu appears.
5. Check that the following options are displayed:
   - Edit
   - Delete
   - Share

### Expected Result

The WebView should display web content when network access is available, and long-pressing an image should display the context menu.

### Screenshot

Save the screenshot as:

```text
screenshots/test-case-3-context-menu.png
```

The screenshot should show the context menu over the image gallery.

---

# 10. Output Screenshot

Add the main application screenshot to:

```text
screenshots/output.png
```

The output screenshot should show:

- Student name and USN
- WebView
- Image Gallery
- At least three images
- Overall application UI

---

# 11. Screenshot Checklist

Before submitting to GitHub, make sure the repository contains:

```text
screenshots/
│
├── output.png
├── test-case-1-usn-name.png
├── test-case-2-menu.png
└── test-case-3-context-menu.png
```

| Screenshot | Requirement |
|---|---|
| `output.png` | Overall application output |
| `test-case-1-usn-name.png` | Must show **Yashika Chaudhary + 25MCAR0139** |
| `test-case-2-menu.png` | Must show the options/kebab menu |
| `test-case-3-context-menu.png` | Must show the context menu |

---

# 12. Emulator Setup

List available Android Virtual Devices:

```bash
emulator -list-avds
```

Start the emulator:

```bash
emulator -avd Pixel_8a
```

Check connected devices:

```bash
adb devices
```

Expected:

```text
List of devices attached
emulator-5554    device
```

---

# 13. WebView DNS Troubleshooting

If WebView displays:

```text
Webpage not available

net::ERR_NAME_NOT_RESOLVED
```

the emulator may not have working DNS resolution.

Stop the emulator:

```bash
adb emu kill
```

Start it with explicit DNS servers:

```bash
emulator -avd Pixel_8a -dns-server 8.8.8.8,1.1.1.1
```

Test DNS:

```bash
adb shell ping -c 3 google.com
```

If the domain resolves successfully, restart the application.

---

# 14. GitHub Submission

Initialize Git:

```bash
git init
```

Add all project files:

```bash
git add .
```

Commit:

```bash
git commit -m "Experiment 8 - Menus and WebView"
```

Create a GitHub repository, for example:

```text
Experiment-8-Menus-WebView-Yashika
```

Add the remote repository:

```bash
git branch -M main
git remote add origin YOUR_GITHUB_REPOSITORY_URL
```

Push the project:

```bash
git push -u origin main
```

---

# 15. Final GitHub Repository Checklist

Before submitting, verify that the repository contains:

- [x] Complete Android Studio project
- [x] Comprehensive README
- [x] Explanation of concepts and technologies
- [x] Scenario used for demonstration
- [x] Folder and file structure
- [x] Main output screenshot
- [x] Three test cases
- [x] Screenshot for each test case
- [x] At least one screenshot showing USN and name
- [x] Kotlin source code
- [x] XML layouts
- [x] Menu resource
- [x] AndroidManifest.xml

---

# 16. Result

**Successfully implemented and tested an Android application demonstrating Options/Kebab Menus, Context Menus, WebView, GridView, and Android sharing functionality using Kotlin and XML.**
