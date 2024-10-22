# SQL Basics

## 1. `SELECT ... FROM`
- **Explanation:** This is used to retrieve data from a table.
- **Example:**
    ```sql
    SELECT naam AS cursus, uren, credits * 28 AS ECTS_uren
    FROM Cursus;
    ```
---

## 2. `DISTINCT`
- **Explanation:** `DISTINCT` removes duplicate values from the result.
- **Example:**
    ```sql
    SELECT DISTINCT uren, credits
    FROM Cursus;
    ```
---

## 3. `CAST()`
- **Explanation:** Converts data from one type to another.
- **Example:**
    ```sql
    SELECT naam || ' heeft een studieduur van ' || 
    CAST(uren AS varchar(3)) || ' uren' AS studieduur
    FROM Cursus;
    ```
---

## 4. `CASE`
- **Explanation:** Used for conditional logic, similar to `IF` in other languages.
- **Example:**
    ```sql
    SELECT student, cursus,
           CASE
               WHEN cijfer >= 6 THEN 'voldoende'
               WHEN cijfer < 6 THEN 'onvoldoende'
               ELSE 'ingeschreven'
           END AS resultaat
    FROM Tentamen;
    ```
---

## 5. `IIF()`
- **Explanation:** A simplified `IF` function for conditional logic.
- **Example:**
    ```sql
    SELECT nr, naam,
           IIF(mentor IS NULL, 'heeft geen mentor', 'heeft mentor') AS mentor_status
    FROM Student;
    ```
---

## 6. `COALESCE()`
- **Explanation:** Returns the first non-null value from a list.
- **Example:**
    ```sql
    SELECT nr, naam, COALESCE(mentor, 'geen mentor') AS mentor
    FROM Student;
    ```
---

## 7. `WHERE`
- **Explanation:** Filters data based on conditions.
- **Example:**
    ```sql
    SELECT code, naam, credits  
    FROM Cursus                      
    WHERE examinator = 'DAT';  
    ```
---

## 8. `ORDER BY`
- **Explanation:** Sorts the result set in ascending or descending order.
- **Example:**
    ```sql
    SELECT * 
    FROM Inschrijving
    ORDER BY cijfer ASC;
    ```
---

## 9. `JOIN`
- **Explanation:** Combines rows from two or more tables based on a related column between them.
- **Example:**
    ```sql
    SELECT Student.naam, Cursus.naam AS cursus_naam 
    FROM Student 
    JOIN Inschrijving ON Student.nr = Inschrijving.student_nr
    JOIN Cursus ON Inschrijving.cursus_code = Cursus.code;
    ```
---

## 10. `COUNT`
- **Explanation:** Counts the number of rows or non-null values in a column.
- **Example:**
    ```sql
    SELECT COUNT(*) AS aantal_studenten
    FROM Student;
    ```
---

## 11. `SUM` / `AVG`
- **Explanation:** 
  - `SUM` adds up values in a column.
  - `AVG` calculates the average value in a column.
  
- **Example (SUM):**
    ```sql
    SELECT SUM(credits) AS totaal_credits
    FROM Cursus;
    ```
- **Example (AVG):**
    ```sql
    SELECT AVG(cijfer) AS gemiddelde_cijfer
    FROM Tentamen;
    ```
---

## 12. `MAX` / `MIN`
- **Explanation:**
  - `MAX` finds the largest value in a column.
  - `MIN` finds the smallest value in a column.
  
- **Example (MAX):**
    ```sql
    SELECT MAX(credits) AS hoogste_credits
    FROM Cursus;
    ```

- **Example (MIN):**
    ```sql
    SELECT MIN(cijfer) AS laagste_cijfer
    FROM Tentamen;
    ```
---

## 13. `GROUP BY`
- **Explanation:** Groups rows sharing a value in one or more columns.
- **Example:**
    ```sql
    SELECT student, cursus, COUNT(*)
    FROM Tentamen
    GROUP BY student, cursus;
    ```
---

## 14. `HAVING`
- **Explanation:** Filters groups based on a condition.
- **Example:**
    ```sql
    SELECT cursus, COUNT(*) AS aantal
    FROM Inschrijving                     
    WHERE vrijstelling = 'N'               
    GROUP BY cursus                              
    HAVING COUNT(*) >= 2;
    ```
---

## 15. Subqueries
- **Explanation:** A query inside another query.
- **Example:**
    ```sql
    SELECT code, naam
    FROM Cursus
    WHERE code IN
          (SELECT cursus
           FROM Inschrijving
           WHERE vrijstelling = 'J');
    ```
---

## 16. `INSERT`
- **Explanation:** Adds new data to a table.
- **Example:**
    ```sql
    INSERT INTO Student (nr, naam)
    VALUES (5, 'Stam');
    ```
---

## 17. `DELETE`
- **Explanation:** Removes data from a table.
- **Example:**
    ```sql
    DELETE FROM Cursus
    WHERE code = 'SW';
    ```
---

## 18. `UPDATE`
- **Explanation:** Modifies existing data in a table.
- **Example:**
    ```sql
    UPDATE Cursus                           
    SET uren = 140, credits = 5     
    WHERE code = 'DW';
    ```
---

## 19. `CREATE TABLE`
- **Explanation:** Used to create a new table in the database.
- **Example:**
    ```sql
    CREATE TABLE Student (
        nr INT PRIMARY KEY,
        naam VARCHAR(100),
        mentor VARCHAR(100)
    );
    ```
---

## 20. `ALTER TABLE`
- **Explanation:** Used to modify the structure of an existing table.
- **Example (Add Column):**
    ```sql
    ALTER TABLE Student
    ADD email VARCHAR(100);
    ```

- **Example (Modify Column):**
    ```sql
    ALTER TABLE Student
    MODIFY naam VARCHAR(150);
    ```
---

## 21. `DROP TABLE`
- **Explanation:** Removes a table from the database permanently.
- **Example:**
    ```sql
    DROP TABLE Student;
    ```
---

## 22. Adding/Removing Foreign Keys
- **Explanation:**
  - A **foreign key** is a field in one table that links to the primary key in another table.
  
- **Example (Add Foreign Key):**
    ```sql
    ALTER TABLE Inschrijving
    ADD CONSTRAINT fk_student
    FOREIGN KEY (student_nr) REFERENCES Student(nr);
    ```

- **Example (Remove Foreign Key):**
    ```sql
    ALTER TABLE Inschrijving
    DROP CONSTRAINT fk_student;
    ```
---

## 23. Adding Column Definitions
- **Explanation:** Adds a new column with its data type to an existing table.
- **Example:**
    ```sql
    ALTER TABLE Student
    ADD geboortedatum DATE;
    ```
---

## 24. `DEFAULT` Specifications
- **Explanation:** Specifies a default value for a column when no value is provided.
- **Example:**
    ```sql
    ALTER TABLE Student
    ADD land VARCHAR(50) DEFAULT 'Nederland';
    ```
---

## 25. `CREATE VIEW`
- **Explanation:** Creates a virtual table based on a query.
- **Example:**
    ```sql
    CREATE VIEW CursusView AS
    SELECT naam, credits 
    FROM Cursus
    WHERE credits > 5;
    ```
---

## 26. Using Views
- **Explanation:** You can use a view like a normal table in queries.
- **Example:**
    ```sql
    SELECT * FROM CursusView;
    ```
---

## 27. Dropping Views
- **Explanation:** Deletes a view from the database.
- **Example:**
    ```sql
    DROP VIEW CursusView;
    ```
---

## 28. Creating Users
- **Explanation:** Creates a new user in the database.
- **Example:**
    ```sql
    CREATE USER 'new_user' IDENTIFIED BY 'password';
    ```
---

## 29. Granting Privileges
- **Explanation:** Grants specific permissions to a user or role.
- **Example:**
    ```sql
    GRANT SELECT, INSERT ON Cursus TO 'new_user';
    ```
---

## 30. Revoking Privileges
- **Explanation:** Removes specific permissions from a user or role.
- **Example:**
    ```sql
    REVOKE INSERT ON Cursus FROM 'new_user';
    ```
---

## 31. LIKE
- **Explanation:** Used for pattern matching in text fields.
- **Example:**
    ```sql
    SELECT naam
    FROM Student
    WHERE naam LIKE 'A%';
    ```
---

## 32. IN
- **Explanation:** Filters the result set based on a list of specified values.
- **Example:**
    ```sql
    SELECT naam
    FROM Cursus
    WHERE code IN ('CS101', 'CS102', 'CS103');
    ```
---