# Mobile Applications Lab

# Experiment 3

## Objective

Develop an Android application using **Fragments** to create a flexible user interface. The application contains a **List Fragment** that displays a list of courses and a **Detail Fragment** that displays the selected course. Android Studio debugging tools were used to demonstrate normal and conditional breakpoints.

---

## Technologies Used

- Android Studio
- Kotlin
- XML
- Fragments
- ListView
- TextView

---

## Application Output

The application consists of two fragments:

- **List Fragment** displays a list of courses.
- **Detail Fragment** displays the selected course.
- Selecting a course updates the Detail Fragment.
- A **normal breakpoint** is placed in `DetailFragment` to inspect the Fragment lifecycle and variables.
- A **conditional breakpoint** is placed in the item selection event and pauses execution only when **"Android"** is selected.

---

## Test Cases

### Test Case 1

**Input:** Launch the application.

**Expected Result:** The List Fragment displays the list of courses and the Detail Fragment is visible.

**Actual Result:** Passed.

![Test Case 1](two%20fragments.jpeg)

---

### Test Case 2

**Input:** Select a course from the list.

**Expected Result:** The Detail Fragment displays the selected course.

**Actual Result:** Passed.

![Test Case 2](two%20fragments.jpeg)

---

### Test Case 3

**Input:** Select the **Android** course while running the application in Debug Mode.

**Expected Result:** The conditional breakpoint pauses program execution only when **Android** is selected.

**Actual Result:** Passed.

![Test Case 3](conditional%20breakpoint.png)

---

## Conclusion

This experiment demonstrates the use of **Fragments** to build a flexible Android user interface. It also illustrates the use of **Android Studio's debugging tools**, including normal and conditional breakpoints, to inspect application execution, variable values, and program flow.