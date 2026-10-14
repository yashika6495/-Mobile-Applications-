# Experiment 9 — Data Persistence using SharedPreferences and SQLite

## 1. AIM

To demonstrate data persistence in an Android application using **SharedPreferences** and **SQLite Database**.

---

## 2. Concept / Technology

### SharedPreferences

SharedPreferences is used to store small amounts of persistent key-value data.

In this experiment, it is used to store:

- Student Name
- Student USN
- Remember Me preference

### SQLite

SQLite is a lightweight relational database provided by Android.

It is used to store student records containing:

- ID
- Name
- USN
- Course

---

## 3. Scenario

A **Student Data Persistence Application** is developed.

The application allows a student to:

1. Save their Name and USN using SharedPreferences.
2. Store student records using SQLite.
3. Retrieve saved data after closing and reopening the application.

**Student Name:** Yashika Chaudhary  
**USN:** 25MCAR0139

---

## 4. Technologies Used

- Android Studio
- Kotlin
- XML
- Android SDK
- SharedPreferences
- SQLite
- SQLiteOpenHelper

---

## 5. Features

- Save student Name and USN using SharedPreferences.
- Retrieve saved preferences after restarting the application.
- Add student records to SQLite.
- View stored student records.
- Verify data persistence.

---

## 6. Project Structure

```text
Experiment9/
├── app/
│   └── src/
│       └── main/
│           ├── java/com/example/experiment9/
│           │   ├── MainActivity.kt
│           │   └── DatabaseHelper.kt
│           │
│           ├── res/
│           │   ├── layout/
│           │   │   └── activity_main.xml
│           │   └── values/
│           │
│           └── AndroidManifest.xml
│
├── screenshots/
│   ├── output.png
│   ├── test-case-1-usn-name.png
│   ├── test-case-2-sqlite.png
│   └── test-case-3-persistence.png
│
└── README.md
```

---

## 7. Application Output

The application provides a user interface for saving student information using SharedPreferences and storing student records using SQLite.

![Application Output](screenshots/output.png)

---

## 8. Test Cases

### Test Case 1 — SharedPreferences

**Input:**

- Student Name: Yashika Chaudhary
- Student USN: 25MCAR0139
- Remember Me: Checked

**Expected Result:**

The Name and USN should be saved and automatically retrieved after reopening the application.

![Test Case 1](screenshots/test-case-1-usn-name.png)

---

### Test Case 2 — SQLite

**Input:**

- Student Name: Yashika Chaudhary
- USN: 25MCAR0139
- Course: MCA

**Expected Result:**

The student record should be successfully inserted into SQLite and displayed.

![Test Case 2](screenshots/test-case-2-sqlite.png)

---

### Test Case 3 — Data Persistence

**Action:**

1. Add the student record.
2. Close the application.
3. Reopen the application.
4. View the student records.

**Expected Result:**

The previously stored SQLite record should still be available.

![Test Case 3](screenshots/test-case-3-persistence.png)

---

## 9. Screenshot Checklist

Before submitting to GitHub, make sure the repository contains:

```text
screenshots/
│
├── output.png
├── test-case-1-usn-name.png
├── test-case-2-sqlite.png
└── test-case-3-persistence.png
```

| Screenshot | Requirement |
|---|---|
| `output.png` | Overall application output |
| `test-case-1-usn-name.png` | Must show Yashika Chaudhary + 25MCAR0139 |
| `test-case-2-sqlite.png` | Must show SQLite record |
| `test-case-3-persistence.png` | Must show data after reopening |

---

## 10. GitHub Submission

Initialize Git:

```bash
git init
```

Add project files:

```bash
git add .
```

Commit:

```bash
git commit -m "Experiment 9 - SharedPreferences and SQLite"
```

Create a GitHub repository:

```text
Experiment-9-SharedPreferences-SQLite
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

## 11. GitHub Submission Link

```text
YOUR_GITHUB_REPOSITORY_URL
```

---

## 12. Final GitHub Repository Checklist

Before submitting, verify that the repository contains:

- [ ] Complete Android Studio project
- [ ] Comprehensive README
- [ ] Explanation of SharedPreferences and SQLite
- [ ] Scenario used for demonstration
- [ ] Project folder and file structure
- [ ] Main output screenshot
- [ ] Three test cases
- [ ] Screenshot for each test case
- [ ] At least one screenshot showing Name and USN

---

## 13. Result

**Successfully implemented and tested an Android application demonstrating data persistence using SharedPreferences and SQLite for Yashika Chaudhary (USN: 25MCAR0139).**
