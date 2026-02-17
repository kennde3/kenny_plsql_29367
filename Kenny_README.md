# oracle_pdb_ass_II_29367_Kenny

## Introduction
This repository holds my completed work for **Individual Assignment II** in **INSY 8311 — Database Development with PL/SQL**. The assignment focused on practical Oracle database administration, specifically around creating and managing Pluggable Databases (PDBs).

---

## Student Profile
| | |
|---|---|
| **Name** | NIYONSHUTI Kenny |
| **Student ID** | 29367 |
| **Group** | C — Monday |
| **Instructor** | Eric Maniraguha |
| **Course** | INSY 8311 — Database Development with PL/SQL |
| **Submission Date** | February 16, 2026 |

---

## Technical Setup
- **Oracle Version:** Oracle Database 21c
- **Operating System:** Windows 10
- **IDE:** Oracle SQL Developer
- **CDB Name:** ORCL

---

## Tasks Completed

---

### 1. Personal Pluggable Database Setup

For this task I created my own PDB that will serve as my personal workspace for all upcoming PL/SQL labs and exercises throughout the semester.

**PDB Name:** `ke_pdb_29367`
**Username:** `kenny_plsqlauca_29367`

The process involved creating the PDB from Oracle's seed template, opening it, and setting up a dedicated user account with the appropriate privileges.

**PDB successfully created:**

![PDB Creation](https://github.com/kennde3/kenny_plsql_29367/blob/main/Screenshots/task1_pdb_creation.png)

**PDB opened and running:**

![PDB Open](https://github.com/kennde3/kenny_plsql_29367/blob/main/Screenshots/task1_pdb_open.png)

**User created inside the PDB:**

![User Created](https://github.com/kennde3/kenny_plsql_29367/blob/main/Screenshots/task1_user_created.png)

**User confirmed with query:**

![User Verified](screenshots/task1_user_verified.png)

---

### 2. Temporary PDB — Full Lifecycle

This task required me to demonstrate full control over a PDB from creation to deletion.

**Temporary PDB Name:** `ke_to_delete_pdb_29367`

I created the PDB, verified it appeared in the database list, closed it, dropped it completely with all its data files, and then confirmed it no longer existed.

**Temporary PDB created:**

![Temp PDB Created](screenshots/task2_temp_created.png)

**Verified it exists:**

![Temp PDB Verified](screenshots/task2_temp_verified.png)

**Dropped completely:**

![Temp PDB Dropped](screenshots/task2_temp_dropped.png)

**Confirmed no longer exists:**

![Temp PDB Gone](screenshots/task2_temp_confirmed.png)

---

### 3. Oracle Enterprise Manager Dashboard

I configured and accessed Oracle Enterprise Manager (OEM) through the browser. The dashboard displays my full Oracle 21c environment including the PDBs created in the previous tasks.

**OEM Dashboard:**

![OEM Dashboard](screenshots/task3_oem_dashboard.png)

---

## SQL Commands Used

```sql
-- Enable Oracle Managed Files
ALTER SYSTEM SET db_create_file_dest = 'C:\ORACLE21C\ORADATA\ORCL' SCOPE=BOTH;

-- Create main PDB
CREATE PLUGGABLE DATABASE ke_pdb_29367
ADMIN USER ke_admin IDENTIFIED BY kenny123;

-- Open the PDB
ALTER PLUGGABLE DATABASE ke_pdb_29367 OPEN;

-- Save open state
ALTER PLUGGABLE DATABASE ke_pdb_29367 SAVE STATE;

-- Switch into PDB
ALTER SESSION SET CONTAINER = ke_pdb_29367;

-- Create personal user
CREATE USER kenny_plsqlauca_29367 IDENTIFIED BY kenny123;

-- Grant privileges
GRANT CONNECT, RESOURCE, UNLIMITED TABLESPACE TO kenny_plsqlauca_29367;

-- Go back to root
ALTER SESSION SET CONTAINER = CDB$ROOT;

-- Create temporary PDB
CREATE PLUGGABLE DATABASE ke_to_delete_pdb_29367
ADMIN USER temp_admin IDENTIFIED BY kenny123;

-- Verify PDBs
SELECT name, open_mode FROM v$pdbs;

-- Close temporary PDB
ALTER PLUGGABLE DATABASE ke_to_delete_pdb_29367 CLOSE IMMEDIATE;

-- Drop temporary PDB
DROP PLUGGABLE DATABASE ke_to_delete_pdb_29367 INCLUDING DATAFILES;

-- Confirm deletion
SELECT name, open_mode FROM v$pdbs;
```

---

## Challenges and Solutions

**Challenge 1 — Folder Deletion Permission Error**
When setting up the environment, Windows blocked the deletion of certain Oracle folders even with administrator rights. I resolved this by stopping all Oracle-related Windows services through `services.msc` before attempting deletion again through Command Prompt running as Administrator.

**Challenge 2 — File Path Issues**
The documentation I referenced used Linux-style paths which are not valid on Windows. I ran the query below to identify the correct Windows paths on my machine and used those instead:

```sql
SELECT NAME FROM v$datafile;
```

This returned the correct path `C:\ORACLE21C\ORADATA\ORCL\` which I then used for all file-related configurations.

---

## Academic Integrity

I, **NIYONSHUTI Kenny**, declare that everything in this repository represents my own individual work. All tasks were performed personally on my own machine. No work was shared with or copied from any other student.

**NIYONSHUTI Kenny | 29367 | INSY 8311 Group C | February 2026**
