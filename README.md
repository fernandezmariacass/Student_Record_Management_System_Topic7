# Student Record Management System

Name: Fernandez, Maria Cassandra M.
Section: BSIT 2-2

A JavaFX desktop application for managing student records, connected to a PostgreSQL database via pgAdmin.

---

## Requirements

- Java 21 (Liberica Full JDK recommended)
- IntelliJ IDEA
- pgAdmin / PostgreSQL installed locally
- PostgreSQL JDBC Driver (`.jar` file)

---

## 1. Set Up the Database in pgAdmin

1. Open **pgAdmin** and connect to your local PostgreSQL server.
2. Right-click **Databases** → click **Create** → **Database**.
3. Name it `studentdb` and click **Save**.
4. Open the **Query Tool** for `studentdb` and run:

```sql
CREATE TABLE students (
    id         SERIAL PRIMARY KEY,
    name       VARCHAR(100),
    course     VARCHAR(50),
    year_level VARCHAR(20)
);
```

5. Click the ▶ **Execute** button. The `students` table should appear under **Tables**.

---

## 2. Configure the Database Connection

Open `src/DBConnection.java` and update the credentials to match your local PostgreSQL setup:

```java
return DriverManager.getConnection(
    "jdbc:postgresql://localhost:5432/studentdb",
    "postgres",
    "your_password"
);
```

Replace `your_password` with the password you set for the `postgres` user when you installed PostgreSQL.

> **Recommended:** Store your credentials in a `.env` file instead of hardcoding them directly in `DBConnection.java`. This keeps your password out of your source code, especially if you plan to share or upload your project.
>
> Create a `.env` file in your project root:
> ```
> DB_URL=jdbc:postgresql://localhost:5432/studentdb
> DB_USER=postgres
> DB_PASSWORD=your_password
> ```
> Then use a library like [dotenv-java](https://github.com/cdimascio/dotenv-java) to load the values, and reference them in `DBConnection.java` instead of plain text.

---

## 3. Add the PostgreSQL JDBC Driver

1. Download the driver from https://jdbc.postgresql.org/download/ (e.g. `postgresql-42.x.x.jar`).
2. In IntelliJ, go to **File → Project Structure → Libraries**.
3. Click **+** → **Java** → select the downloaded `.jar` file.
4. Click **Apply** then **OK**.

---

## 4. Open the Project in IntelliJ

1. Extract the zip file if you haven't already.
2. Open **IntelliJ IDEA**.
3. Click **Open** and select the `StudentManagementSystem` folder.
4. Wait for IntelliJ to finish indexing the project.

---

## 5. Set Up the Run/Debug Configuration

1. Go to **Run** in the top menu → click **Edit Configurations**.
2. Click **+** and select **Application**.
3. Fill in the fields:

```
Name:       StudentApp
Module:     StudentManagementSystem
Main class: MainApp
```

4. Click **Apply** then **OK**.

To **run**: click the green ▶ Run button or press `Shift + F10`.  
To **debug**: click the 🐛 Debug button or press `Shift + F9`.

---

## 6. Using the Application

| Action | How |
|--------|-----|
| **Add** a student | Fill in Name, Course, and Year Level → click **Add** |
| **Update** a student | Click a row to select → edit the fields → click **Update** |
| **Delete** a student | Click a row to select → click **Delete** |
| **Clear** the form | Click **Clear** to reset all fields |

> All records are displayed automatically in the table when the app loads.

---

## Troubleshooting

**"No suitable driver found" error**  
Make sure the PostgreSQL JDBC `.jar` is added under File → Project Structure → Libraries.

**Table shows no data / connection fails**  
Check that PostgreSQL is running locally and that the password in `DBConnection.java` matches your `postgres` user password in pgAdmin.

**"MainApp class not found" error**  
In Edit Configurations, confirm the **Module** and **Main class** fields are set correctly.

**Changes not reflecting after editing**  
Go to **Build → Rebuild Project**, then run again.
