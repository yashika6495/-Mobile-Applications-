# Course Explorer

**Name:** Yashika
**USN:** 25MCAR0139

## 1. Project Overview

**Course Explorer** is an Android application developed using Kotlin and Android Studio. The application displays a list of courses and allows users to select a course to view its details through an Android Fragment.

This project demonstrates:

* Android project structure
* XML-based user interface design
* Kotlin data classes
* Custom ListView adapters
* Fragment implementation
* Passing data using Bundles
* Debugging with normal and conditional breakpoints
* Functional testing using test cases

## 2. Objective

The objective of this project is to create a simple course-exploration application that displays available courses and shows detailed information about a selected course using a Fragment.

## 3. Technologies Used

* **IDE:** Android Studio
* **Programming Language:** Kotlin
* **UI Design:** XML
* **Platform:** Android
* **Architecture Components:** Activities and Fragments
* **UI Components:** ConstraintLayout, ListView, TextView, ImageView
* **Debugging Tool:** Android Studio Debugger

## 4. Application Features

1. Displays a list of courses.
2. Shows a course image, name, and description.
3. Allows the user to select a course.
4. Displays the selected course details in `DetailFragment`.
5. Transfers course information using a `Bundle`.
6. Supports debugging using breakpoints.
7. Uses a conditional breakpoint that triggers when **Android Development** is selected.

## 5. Project Structure

```text
CourseExplorer/
│
├── app/
│   └── src/
│       └── main/
│           ├── java/com/example/courseexplorer/
│           │   ├── MainActivity.kt
│           │   ├── Course.kt
│           │   ├── CourseAdapter.kt
│           │   └── DetailFragment.kt
│           │
│           └── res/
│               ├── layout/
│               │   ├── activity_main.xml
│               │   ├── item_course.xml
│               │   └── fragment_detail.xml
│               │
│               └── values/
│                   └── strings.xml
│
└── README.md
```

## 6. Important Files

### `MainActivity.kt`

* Loads the main activity layout.
* Creates the course list.
* Connects the `CourseAdapter` to the `ListView`.
* Detects when a course is selected.
* Opens `DetailFragment` with the selected course information.

### `Course.kt`

Contains the data class used to represent a course.

```kotlin
data class Course(
    val name: String,
    val description: String,
    val imageResId: Int
)
```

### `CourseAdapter.kt`

Connects course data to the custom course item layout. It displays the course image, name, and description in each ListView row.

### `DetailFragment.kt`

Displays the selected course's name and description. The information is received through Fragment arguments using a `Bundle`.

### `activity_main.xml`

Contains the application title, course ListView, and Fragment container.

### `item_course.xml`

Defines the appearance of an individual course item.

### `fragment_detail.xml`

Defines the layout used to display course details.

## 10. Output Screenshots

<img width="479" height="771" alt="Screenshot 2026-09-17 at 10 46 00 AM" src="https://github.com/user-attachments/assets/42f5b7a1-d41d-45d6-97cc-34a8523d923d" />

<img width="469" height="782" alt="Screenshot 2026-09-17 at 10 47 11 AM" src="https://github.com/user-attachments/assets/25406acf-d6e7-4ddd-b132-4d7661d361d7" />

<img width="889" height="456" alt="Screenshot 2026-09-17 at 10 46 52 AM" src="https://github.com/user-attachments/assets/d297692f-7617-4d9e-942f-b35479a26d52" />

## 11. Learning Outcomes

After completing this project, the following concepts were practiced:

* Understanding Android Studio project structure
* Creating Android layouts using XML
* Using Kotlin data classes
* Displaying data using a custom adapter
* Implementing and managing Fragments
* Passing data between an Activity and Fragment
* Using Android Studio Debug Mode
* Creating normal and conditional breakpoints
* Preparing functional test cases and documenting results

## 12. Conclusion

The Course Explorer application successfully demonstrates how an Android application can display a list of courses and show the details of a selected course using a Fragment. The project also demonstrates debugging techniques and functional testing in Android Studio.

The application can be extended in the future by adding:

* A back button
* Course search functionality
* Multiple Fragment layouts for tablets
* Course images from external resources
* A database for storing courses
* Navigation using the Navigation Component
