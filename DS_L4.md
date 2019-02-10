# Database Systems
### Letcure 4 - Advanced SQL & Analytics
---

### Inner Join

**INNER JOIN** matches tuples using FK and PK.

For example:

    SELECT Fname, Lname, Address
    FROM (Employee JOIN Department ON Dno=Dnumber)
    WHERE Dname="Research"
    
### Inner and Outer joins

INNER JOIN (vs OUTER JOIN):
- A tuple is retrieved if and only if there exists a matching tuple (FK is not null)

LEFT OUTER JOIN 
- Every tuple in the left relation **must** appear in the result
- If no matching tuple exists, just add NULL values for the attributes of right relation RR

Query: Show the last name of an employee and the last name of their supervisor *if there exists*.

    SELECT E.Lname, S.Lname
    FROM (EMPLOYEE AS E LEFT OUTER JOIN EMPLOYEE AS S ON E.Super_SSN = S.SSN)
    
    RESULTS:
    E.Lname:     S.Lname:
    Smith       Wong
    Borg        NULL
    Franklin    Jennifer

RIGHT OUTER JOIN
- Every tuple in the right relation must appear in the result
- If not mathcing tuple exists, just add NULL values for the attributes of left relation

---

### Aggregate Function

An **aggregate function** summarizes statistical information from a group of tuples into a single value.

There are built in aggregate functions for SQL:
- COUNT(*): How many employees working in Dept 5?
- SUM (X): Sum up all salaries of employees in Dept 5.
- MAX(X)/MIN(X): Who is the youngest employee in Dept 5?
- AVG(X): Average salary of employees in Dept 5.
- CORR(X,Y): Correlation between Age and Salary of employees in Dept 5.

NOTE: Null values are *discarded* apart from when using COUNT(*) and we can also make our own aggregate functions.

Query:  Show the summation of the salary, the maximum, the minimum and the average salary of those employees who work in Dept. 5

    SELECT  SUM(Salary) AS Total_Sal,
            MAX(Salary) AS Highest_Sal,
            MIN(Salary) AS Lowest_Sal,
            AVG(Salary) AS Average_Sal
    FROM    EMPLOYEE
    WHERE   DNO=5;

---
### Analytics: Grouping

We can partition a relation into groups based on a grouping attribute, tuples will be clustered depending on that attribute. 

    GROUP BY {grouping attribute}
    
Query: Show the number of employees per department & average salary per department. 

    SELECT      DNO, COUNT(*), AVG(Salary)
    FROM        EMPLOYEE
    GROUP BY    DNO
    
This partitions EMPLOYEE into separate groups by department. Then for each group, calculate its cardinality and average salary

### GROUP BY & HAVING

**HAVING** is a condition that select/rejects an entire group after grouping.

Query: Show the number of employees per project only from those project with more than 2 employees. Include the project name at the results.

    SELECT      P.Pname, Count(*)
    FROM        PROJECT AS P, WORKS_ON AS W
    WHERE       P.Pnumber = W.PNO
    HAVING      COUNT(*) > 2

---
READ LECTURE NOTES FOR:

- INSERT
- UPDATE
- DELETE
- ALTER
- DROP