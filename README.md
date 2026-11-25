# Hackathon
Hackathon by 3am engineers


Topic: Student Attendance Analyzer.

Members:-

1.) Prakritik Sarmah (590032813)

2.) Sarthak (590033651)

3.) Arya (590042061)

# Student Attendance Management System in C

A console-based Student Attendance Management System written in C that calculates student attendance percentages, flags attendance shortages (`Eligible` vs. `Short`), validates user inputs, and persists records in a formatted plain-text file (`attendance.txt`).

---

## 1. Objectives and Features

### Objectives
* Automate attendance percentage calculations and eligibility tracking based on the 75% attendance threshold.
* Maintain persistent, human-readable student records across multiple program runs without requiring an external database.
* Prevent runtime crashes and input-buffer errors through strict input validation.

### Key Features
* **Single-Prompt Total Classes Setup:** Prompts for `Total Classes Held` once during initial setup and automatically loads it from `attendance.txt` on subsequent runs.
* **Automatic Percentage & Status Calculation:** Computes exact attendance percentage (`(Attended / Total) * 100`) and classifies students as `Eligible` ($\ge 75\%$) or `Short` ($< 75\%$).
* **Multi-Word Name Support:** Accepts full names containing spaces (e.g., `Aarav Sharma`).
* **Strict Input Validation:**
  * Rejects numbers or special symbols in student names.
  * Rejects alphabets, negative signs, or symbols in numeric fields (`Roll Number`, `Total Classes`, `Classes Attended`, and `Menu Choice`).
  * Prevents `Classes Attended` from exceeding `Total Classes Held`.
* **Record Editing:** Search any student by Roll Number to update their name, attended classes, or both, immediately recalculating status and updating `attendance.txt`.
* **Formatted Plain-Text Storage:** Saves records in an aligned, tab-separated table inside `attendance.txt` readable in any text editor.

---

## 2. Algorithm:

### Algorithm
1. **Start** the program.
2. **Load Existing Data:** Attempt to open `attendance.txt` in read (`"r"`) mode.
   * If the file exists, skip the 2 header lines, parse existing records into the `students` structure array, increment `count`, and set `initial_total_classes` from the loaded data.
   * If the file does not exist (or is empty), prompt the user to enter a valid positive integer for `initial_total_classes`.
3. **Display Menu Loop:** Prompt the user to select an option:
   * **Option 1 (Add Student):**
     1. Validate `Roll Number` (digits only) and `Full Name` (alphabets and spaces only).
     2. Validate `Classes Attended` (digits only and  `initial_total_classes`).
     3. Calculate `percentage = ((float)attended / total) * 100.0`.
     4. Assign `status = "Eligible"` if `percentage >= 75.0`, else `"Short"`.
     5. Increment `count` and rewrite all records to `attendance.txt`.
   * **Option 2 (View All Records):**
     1. If `count == 0`, display `"No records found."`
     2. Otherwise, print all stored records in a formatted console table.
   * **Option 3 (Edit Student Details):**
     1. Prompt for target `Roll Number` and search the `students` array.
     2. If found, allow editing `Name`, `Classes Attended`, or `Both` with validation.
     3. Recalculate `percentage` and `status`, then overwrite `attendance.txt` with updated records.
   * **Option 4 (Exit):** Terminate the loop and exit the program.

## 3. C Programming Concepts Used

* **Structures (`struct Student`):** Groups heterogeneous data types (`int`, `char[]`, `float`) representing a single student entity into a cohesive record.
* **Arrays of Structures (`struct Student students[100]`):** Stores and manages up to 100 student records in memory.
* **File Handling (`FILE *`, `fopen`, `fgets`, `fprintf`, `fclose`):** Reads existing data on startup and writes formatted tabular output to `attendance.txt`.
* **Character Classification & Conversion (`<ctype.h>`, `<stdlib.h>`,):** Validates raw string inputs character-by-character before converting numeric strings to integers.
* **Functions & Modular Design:** Separates validation (`isValidNumber`, `isValidName`) and persistence (`saveToFile`) into reusable functions.
* **Type Casting & Formatted I/O:** Uses explicit `(float)` casting to prevent integer division truncation and width specifiers (`%-10d`, `%-24s`, `%-11.2f%%`) for column alignment.

---

## 4. Instructions to Compile and Execute

### Prerequisites
* A C compiler such as **GCC** (MinGW on Windows, GCC on Linux, or Clang on macOS).

### Using Terminal / Command Prompt
1. Clone the repository and navigate into the project directory:
   ```bash
   git clone <your-repository-url>
   cd <repository-folder-name>
