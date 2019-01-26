# Database Systems
### Lecture 3 - SQL
---
### Database Schema

        CREATE SCHEMA Company;

### Create Table 

A new relation:
- Specifiy the *name* of the relation
- Specify the *attributes*, their *types* and *constraints*

        CREATE SCHEMA Company
        CREATE TABLE Employee
        

### Value Constraints

Default value of an attribute:
- DEFAULT {value}
- NULL is not permitted for a attribute (NOT NULL)

CHECK clause:
- Dnumber INT NIT NULL CHECK (Dnumber > 0 AND Dnumber <21)

### Key Constraints

**Key constraint**: a **primary key value** is unique.

**Entity Integrity constraint**: a primary key cannot be NULL.

Primary Key Clause:
- Dnumber INT NOT NULL, PRIMARY KEY (Dnumber);

UNIQUE clause, specifies *candidate* keys
- Dname VARCHAR(15) NOT NULL, UNIQUE (Dname);

### Referential Constraints

**Foreign Key Clause**:
- FOREIGN KEY (Super_ssn) REFERENCES Employee(Ssn)

**Triggered Actions**:
- ON DELETE SET NULL/DEFAULT/CASCADE
- ON UPDATE SET NULL/DEFAULT/CASCADE

The CASCADE options *propagates* DELETE/UPDATE to **all** referential tuples. 

---

### SELECT-FROM-WHERE

1. Declare **what** to retrieve (attributes of interest)
2. Declare **from** where to retrieve (table/relation)
3. Declare with what **condition** to retrieve (conditions)

        SELECT <attribute list>
        FROM <table list>
        WHERE <condition>;

### Query Examples:

Retrieve the names and address of all employees who work for the 'Research' department:

        SELECT Fname, Lname, Address
        FROM EMPLOYEE, DEPARTMENT
        WHERE Dname='Research' AND Dnumber=Dno;

For every project located in 'Stafford', list the project number, the controlling department number, and the department manager's last name, address, adn birth date:

        SELECT Pnumber, Dnum, Lname, Address, Bdate
        FROM PROJECT, DEPARTMENT, EMPLOYEE
        WHERE Dnum=Dnumber AND Mgr_ssn=Ssn AND Plocation="Stafford";

For each employee, retrieve the employee's first and last name and the first and last name of his or her immediate supervisor:

        SELECT E.Fname, E.Lname, S.Fname, S.Lname
        FROM EMPLOYEE AS E, EMPLOYEE AS S
        WHERE E.Super_ssn = S.Ssn;
        
For each employee, if their supervisor is a manager of a department, show the department name and number:

        SELECT D.Dname, D.Dnumber
        FROM EMPLOYEE AS E, EMPLOYEE AS S, DEPARTMENT AS D
        WHERE E.Super_ssn=S.Ssn AND S.Ssn = D.Mgr_Ssn
        
### Tables as Multi-Sets

**Sets** only have unique(distinct) elements
**Multiset** hight have duplicates

Operators: UNION, EXCEPT, INTERSECT

        SELECT DISTINCT salary
        FROM EMPLOYEE;
        (Sets the collumn 'salary')
---

### Three-Valued Logic

SQL is a three-valued logic: TRUE (1), FALSE (0) and UNKNOWN (0.5)

Remember: Each NULL value is *different* from **any other** NULL value!

*Any* value compared with NULL evaluates to UNKNOWN. 

---

### Comparison involving NULL
Retrieve the first and last names of *all* employees who do not have supervisors:

        DELECT Fname, Lname
        FROM EMPLOYEE
        WHERE Super_ssn IS NULL;
        
---

### Nested (Inner) Query

Nexted query is a query within another (outer) query:
- SELECT-FROM-WHERE block within another WHERE clause

**Nested Uncorrelated Query**: *first* execute the nested query, and *then* execute the outer query using inner's output.

**Correlated Query**: for *each* tuple of the outer query, we execute the nested query. 


### Nested Uncorrelated Query

The operator **IN**. It checks whether a value belongs to the inner's output set (or multiset).

Show the SSN of those employees who work in the projects with number: either 1, or 2 or 3

        SELECT Essn
        FROM WORKS_ON
        WHERE PNO IN (1, 2, 3);
        
Show the names of those employees who work in the department research

        SELECT Fname, Lname
        FROM EMPLOYEE
        WHERE Dno IN (SELECT Dnumber
                        FROM DEPARTMENT
                        WHERE Dname = 'Research')
                        () = 5
        SELECT Fname
        FROM Employee
        WHERE Dno IN (5);

The Operator **ALL**: Compares a value with *all* the values from the inner's output *set*. 


Show the last and first names of those eomployees whose salary is *greater* than the salaries of *all* employees in Department 5:

        SELECT Lname, Fname
        FROM EMPLOYEE
        WHERE Salary > ALL (
                            SELECT Salary
                            FROM EMPLOYEE
                            WHERE Dno = 5);
    First finds all salaries from department no 5, then finds all employees who have a higher salary than the max value from Dno = 5
    
### Nested Correlated Query

For **each** tuple of the *outer* query, we execute the *inner* query!

Retrieve the name of *each* employee who has a dependant with the same first name and same gender as that employee. 

        SELECT E.Fname, E.Lname
        FROM EMPLOYEE AS E
        WHERE E.Ssn IN (
                        SELECT Essn
                        FROM DEPENDANT AS D
                        WHERE E.Fname = D.Dependant_name AND E.Sex = D.Sex);
    For each outer employee E, retrieve the dependants D and check.
    
Correlated queries using **IN** can be collapsed into one *single* block. 

Retrieve the name of *each* employee who has a dependant with the same first name and is the same gender as that employee.

        SELECT E.Fname, E.Lname
        FROM EMPLOYEE AS E, DEPENDANT AS D
        WHERE E.Ssn = D.Essn
            AND E.Sex = D.Sex
            AND E.Fname = D.Dependant_name;
            
            
**EXISTS** operator: checks whether the inner's output is *empty set* or *not*, and returns FALSE or TRUE, respectively (opposite: NOT EXISTS).

        SELECT E.Fname, E.Lname
        FROM EMPLOYEE AS E
        WHERE EXISTS (
                        SELECT * 
                        FROM DEPARTMENT AS D
                        WHERE E.Dno = D.Dnumber)

Checks if a *given* employee is working at *some* department.

