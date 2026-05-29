**Might Xyrel A. Malinay**
**BSIT 2-2**

# Student Record Management System

A desktop CRUD application built with JavaFX, JDBC, and PostgreSQL.  
Manage student records — add, update, delete, and view in a live table.

---

## Project Structure

```
StudentManagement/
├── src/                  # Java source files
│   ├── MainApp.java
│   ├── Controller.java
│   ├── Student.java
│   ├── DBConnection.java
│   └── YearLevel.java
├── resources/
│   └── main.fxml         # GUI layout
├── lib/
│   └── postgresql-42.x.x.jar
├── javafx-sdk/           # JavaFX SDK (bundled)
│   └── lib/
└── README.md
```

---
## Note for Reviewers
The `.vscode/` folder is included in this repository — it contains VS Code-specific
run configuration and can be ignored if using IntelliJ IDEA.

---

## Requirements

- JDK 17 or higher
- PostgreSQL installed and running
- JavaFX SDK 17+ (already bundled in `javafx-sdk/` folder)
- PostgreSQL JDBC driver (already in `lib/` folder)

---

## Database Setup

Open pgAdmin or any PostgreSQL client and run:

```sql
CREATE DATABASE studentdb;

\c studentdb

CREATE TABLE students (
    id         SERIAL PRIMARY KEY,
    name       VARCHAR(100),
    course     VARCHAR(50),
    year_level VARCHAR(20)
);
```

Then open `src/DBConnection.java` and update the password to match yours:

```java
return DriverManager.getConnection(
    "jdbc:postgresql://localhost:5432/studentdb",
    "postgres",
    "your_password"   // <-- change this
);
```

---

## Running in IntelliJ IDEA

1. Open IntelliJ → **File → Open** → select the `StudentManagement` folder
2. Go to **File → Project Structure** (`Ctrl + Alt + Shift + S`)
3. Under **Project**, set SDK to JDK 17+
4. Under **Modules → Dependencies**, click **+** → **JARs or directories**
   - Add all `.jar` files inside `javafx-sdk/lib/`
   - Add `lib/postgresql-42.x.x.jar`
   - Click **Apply → OK**
5. Go to **Run → Edit Configurations** → click **+** → **Application**
   - Main class: `MainApp`
   - Under **VM options**, paste:
     ```
     --module-path javafx-sdk/lib --add-modules javafx.controls,javafx.fxml
     ```
   - Click **Apply → OK**
6. Click the green **Run** button or press `Shift + F10`

---

## Running in VS Code

Open the terminal (`Ctrl + `` `) from the project root and run in order:

**1. Create bin folder (first time only)**
```bash
mkdir bin
```

**2. Compile**
```bash
javac --module-path javafx-sdk/lib --add-modules javafx.controls,javafx.fxml -cp "lib/*" -d bin src/*.java
```

**3. Run**
```bash
java --module-path javafx-sdk/lib --add-modules javafx.controls,javafx.fxml -cp "bin;lib/*;resources" MainApp
```

> On Mac/Linux replace semicolons `;` with colons `:` in the `-cp` argument.

---

## Features

- Add new student records
- View all records in a live TableView
- Click any row to load it into the form
- Update selected student record
- Delete selected student record
- Input validation on all fields
