# Old Age Home Management System

## Project Overview
This Old Age Home Management System is built using Oracle 10g as a database management tool. The project is designed to handle the operations of an old age home, including managing information about caretakers, elderly residents, visitors, and medical personnel. The project focuses on normalizing the database structure, implementing efficient queries, and ensuring the system is optimized for day-to-day operations.

### Key Features:
- Management of caretakers, elderly residents, and visitors.
- Tracking of recreational activities for the elderly.
- Medical records managed by doctors and nurses.
- Comprehensive query operations including joins (EQUI-JOINS, OUTER-JOINS, SELF-JOINS).
- Subqueries and views for easy data extraction.

---

## Project Structure:

### Database Tables:
The project uses multiple tables to store different sets of data. Below is a summary of the major tables and their columns:

1. **Manager Table**  
   Attributes:  
   - `M_Id`: Manager ID (Primary Key)  
   - `M_name`: Manager's Name  
   - `Section`: Manager’s Assigned Section  

2. **Caretaker Table**  
   Attributes:  
   - `C_Id`: Caretaker ID (Primary Key)  
   - `C_Name`: Caretaker's Name  
   - `C_PhoneNumber`: Caretaker's Phone Number  
   - `C_Area`: Caretaker's Area  
   - `C_District`: Caretaker's District  
   - `Section`: Section assigned to the caretaker (Foreign Key from Manager Table)

3. **Elderly Table**  
   Attributes:  
   - `E_Id`: Elderly ID (Primary Key)  
   - `E_name`: Elderly's Name  
   - `E_PhoneNumber`: Elderly's Phone Number  
   - `E_Area`: Elderly's Area  
   - `E_District`: Elderly's District  

4. **Medical Table**  
   Attributes:  
   - `Doctors`: Doctor's Name  
   - `Medicine_name`: Name of the Medicine  
   - `Medicine_type`: Type of the Medicine  

5. **Gate Pass Table**  
   Attributes:  
   - `Pass_Id`: Gate Pass ID (Primary Key)  
   - `P_Name`: Person's Name  

6. **Visitor Table**  
   Attributes:  
   - `V_Id`: Visitor ID (Primary Key)  
   - `V_Name`: Visitor's Name  
   - `VPhone_Number`: Visitor's Phone Number  
   - `V_email`: Visitor's Email  

7. **Recreation Table**  
   Attributes:  
   - `Game_Zone`: Recreational Game Zone  
   - `Social_act`: Social Activities for elderly residents  

### Queries Implemented:

#### Joins:
1. **EQUI-JOINS**:  
   - Query: Retrieve all caretakers who work in section A4 along with their respective managers.  
   ```sql
   SELECT * 
   FROM caretaker c, manager m 
   WHERE c.section = m.section;
   ```

2. **OUTER-JOINS**:  
   - Query: Get all matching and non-matching records from both `caretaker` and `manager` tables.  
   ```sql
   SELECT * 
   FROM caretaker c, manager m 
   WHERE c.section(+) = m.section;
   ```

3. **SELF-JOINS**:  
   - Query: Display all managers who work in the same sections as A1.  
   ```sql
   SELECT * 
   FROM manager m, manager n 
   WHERE m.section = n.section AND m.section = 'A1';
   ```

#### Views:
- **Create a View**: A view to retrieve caretakers who work in Section A1.  
   ```sql
   CREATE VIEW carevu12 
   AS SELECT C_Id, C_Name 
   FROM caretaker 
   WHERE Section = 'A1';
   ```

#### Subqueries:
- **Subquery**: Retrieve the name and ID of the elderly who live in Nikunja-2.  
   ```sql
   SELECT E_name, E_Id, E_Area 
   FROM elderly 
   WHERE E_Area = (SELECT E_Area FROM elderly WHERE E_Id = 2);
   ```

### Data Normalization:

The project has been normalized to **Third Normal Form (3NF)** to avoid redundancy and ensure data integrity.

#### Example of Normalization:
- **UNF to 1NF**: Breaking down the attributes to atomic values.
- **1NF to 2NF**: Ensuring partial dependency removal by separating composite keys.
- **2NF to 3NF**: Removing transitive dependencies for data consistency.

---

## Database Queries:

### Manager Table Creation:
```sql
CREATE TABLE manager (
    M_name VARCHAR2(30),
    M_Id NUMBER(10) PRIMARY KEY NOT NULL,
    Section VARCHAR2(30)
);
```

### Caretaker Table Creation:
```sql
CREATE TABLE caretaker (
    C_Name VARCHAR2(30),
    C_Id NUMBER(10) PRIMARY KEY NOT NULL,
    C_PhoneNumber NUMBER(30),
    C_Area VARCHAR2(200),
    C_District VARCHAR2(20),
    Section VARCHAR2(30)
);
```

### Elderly Table Creation:
```sql
CREATE TABLE elderly (
    E_name VARCHAR2(30),
    E_Id NUMBER(10) PRIMARY KEY NOT NULL,
    E_PhoneNumber NUMBER(30),
    E_Area VARCHAR2(30),
    E_District VARCHAR2(30)
);
```

### Other Table Creations:
Similar queries exist for `medical`, `gate_pass`, `visitor`, and `recreation`.

---

## Sample Data:

### Manager Data:
```sql
INSERT INTO manager VALUES ('TALHA', 101, 'A1');
INSERT INTO manager VALUES ('HASIB', 102, 'A2');
```

### Caretaker Data:
```sql
INSERT INTO caretaker VALUES ('Md Islam', 1111, 01791, 'Mirpur', 'Dhaka', 'A1');
INSERT INTO caretaker VALUES ('Tania Akter', 1112, 01792, 'Mirpur1', 'Dhaka', 'A4');
```

### Elderly Data:
```sql
INSERT INTO elderly VALUES ('Md Ali', 0001, 0175588, 'NIKUNJA 1', 'DHAKA');
```

---

## Conclusion:
This project demonstrates the efficient management of an old age home through database normalization, complex queries, and data structuring. The system covers various aspects including manager oversight, caretaking, recreational activities, medical needs, and visitor management.
