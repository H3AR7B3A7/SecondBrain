# Relational Databases  
  
### Unstructured Data:  
- More than 80% of all data  
  
### Structured Data:  
- SQL data  
  
Advantages:  
- Data consistency  
- More information from the same data  
- Improved data integrity  
- Improved security  
- Improved maintenance  
  
  
## Elements of a Database  
  
- Schema’s  
- Catalogues & extensions  
- Relation / Table  
  - Attributes / Columns (# = Degree) – Domain (For example €: 0 -> ∞)  
 - Tuples / Rows (# = Cardinality)  
- Primary / Foreign Keys  
  
  
## Fields  
- Exact numeric  
  - Bit: 0 - 1 (1/8 Byte)  
 - Tinyint: 0 - 255 (1 Byte)  
 - Smallint: -32,768 - 32,767 (2 Bytes)  
 - Int: -2,147,483,648 - 2,147,483,647 (4 Bytes)  
 - Bigint: -9,223,372,036,854,775,808 - 9,223,372,036,854,775,807 (8 Bytes)  
 - Decimal(p,s): p = precision, s = scale (5-17 Bytes)  
 - Smallmoney: -214,748.3648 - 214,748.3647 (4 Bytes)  
 - Money: -922,337,203,685,477.5808 - 922,337,203,685,477.5807 (8 Bytes)  
- Approximate numeric  
  - Float([n]): n=1-24: 7 digits precision (4 Bytes)  
 - Float([n]): n=25-53: 15 digits precision (8 Bytes)  
 - Real: [=float(24)] (4 Bytes)  
- Date & time  
  - Date: Year 1 - 9999 (3 Bytes)  
 - Datetime: 0.003s, Year 1753 - 9999 (8 Bytes)  
 - Datetime2(n): 0.000,000,1s, Year 1 - 9999 (6-8 Bytes)  
 - Datetimeoffset(n): 0.000,000,1s with offset between -12:59 to +14:00, Year 1 - 9999 (8-10 Bytes)  
 - Smalldatetime: Nearest minute, Year 1900 – 2079 (4 Bytes)  
 - Time(n): 0.000,000,1s (3-5 Bytes)  
- Character strings  
  - Char(n): UTF-8; 1-8000 characters (n Bytes)  
 - Varchar(n): UTF-8; 1-8000 characters (Char + 2 Bytes)  
 - Text: UTF-8; 1-2,147,483,647 characters (variable) Deprecated  
  - Varchar(max): UTF-8; 1-2,147,483,647 characters (variable)  
- Unicode character strings  
  - Nchar(n): Unicode; 1-4000 characters (2n Bytes)  
 - Nvarchar(n) : Unicode; 1-4000 characters (2Char + 2 Bytes)  
 - Ntext: Unicode; 1-1,073,741,823 characters (2Char Bytes) Deprecated  
  - Nvarchar(max) : Unicode; 1-1,073,741,823 characters (2Char Bytes)  
- Binary strings  
  - Binary: For consistent sizes  
  - Varbinary: For varying sizes  
  - Varbinary(max): For more than 8000 bytes  
- Other data types  
  - Cursor  
  - Geography  
  - Geometry  
  - Hierarchyid  
  - Rowversion  
  - Sql_variant  
  - Table  
  - Uniqueidentifier: Unique value using NEWID or NEWSEQUENTIALID  
  - Xml: XML data  
    
  
## Relational Keys  
  
- **Superkey**: any combination of columns that uniquely identify a row in a table  
- **Candidate key**: A superkey such that no proper subset is a superkey, with the following two properties:  
  - Uniqueness  
  - Irreducibility  
- **Primary key**: The candidate key that is selected to identify tuples uniquely within the relation  
- **Foreign key**: An attribute, or set of attributes, within one relation that matches the candidate key of some other relation  
  
  
## Relations  
  
- One-to-One  
- One-to-Many  
- Many-to-many  
  
  
## Relational Database  
  
A set of tables that satisfy following data integrity:  
- **Entity Integrity**: No duplicate rows  
- **Domain Integrity**: Enforcing valid entries for a given column  
- **Referential Integrity**: Rows can not be deleted when referenced by other records  
- **User-Defined Integrity**: Enforces some specific business rules  
  
  
## Functional Dependency  
  
Dependency occurs when an attribute or set of attributes identifies a particular value of another attribute.  
When designing an efficient database that avoids redundancy, identifying dependencies help us to:  
- Ensure every column in a table is dependent on the primary key  
- Have the primary key as simple as possible  
  
  
## Types of Joins  
  
- **Inner Join**: Only rows with a match in both tables  
- **Outer Join**  
 - **Left Join**: All rows from the left table, even if there are no matches in the right  
      - Where: A-Key = B-Key  
      - Where: B-Key = NULL  
    - **Right Join**: All rows from the right table, even if there are no matches in the left  
      - Where: A-Key = B-Key  
      - Where: A-Key = NULL  
    - **Full Join**: Combines the results of both left and right outer joins  
      - Where: A-Key = B-Key  
      - Where: A-Key = NULL OR B-Key = NULL  
  
![[SQL-Joins.png]]
  
- **Self Join**: Used to join a table to itself as if it were two tables, temporarily renaming at least one table in the SQL statement  
- **Cartesian Join (Cross Join)**: Cartesian product of the sets of records from the two or more joined tables  
  
  
## Database Design  
  
Importance of knowing about good design:  
- Understand why a database you are working with was designed a certain way  
- Learn quicker how to navigate your way around  
- See the potential vulnerabilities and flaws  
- Communicate effectively  
  
**Prime Attributes** are attributes that belong to at least 1 candidate key.  
**Non-Prime Attributes** do not belong to any candidate key.  
  
**Normalization** is the process of organizing the columns and tables of a relational database to reduce data redundancy and improve data integrity.  
  
- **First normal form (1NF)**:  
  - Does not contain duplicate rows  
  - Every cell contains only one value  
  - Every value is atomic (indivisible)  
- **Second normal form (2NF)**:  
  - 1NF  
  - Every non-prime attribute of the table is dependent on the whole of every candidate key  
- **Third normal form (3NF)**:  
  - 2NF  
  - Every non-prime attribute is non-transitively dependent on every candidate key  
- **Fourth normal form (4NF)**:  
  - 3NF  
  - There should be no multi-valued dependency  
- **Fifth normal form (5NF)**:  
  - 4NF  
  - There should be no join dependency  
  
In general the higher the normal form the better:  
- Less prone to errors  
- Faster adding of records in database  
  
We can improve normalization by splitting the table in multiple tables.  
  
*In practice, everything above the 3d normal form often just makes things more complex rather than less. For this reason we usually want to normalize our tables to the 3d normal form. Except for with data warehouses that are mostly read-only. For data-warehouses the 1st normal form is faster to query.*  
  
  
## DML  
*Data Manipulation Language*  
- SELECT  
- INSERT  
- UPDATE  
- DELETE  
- MERGE  
- ...  
  
  
## DDL  
*Data Definition Language*  
- CREATE  
- ALTER  
- DROP  
- ...  
  
Objects:  
- TABLE  
- COLUMN  
- VIEW  
- PROC (Stored procedure)  
- FUNCTION  
- TRIGGER  
- ...  
  
  
## ACID  
- Atomic: Transactions are units  
- Consistency: Transactions are reliable  
- Isolation: Transactions are independent  
- Durability: Once saved, transactions are persistent  
  
All transactions are implicitly placed between TRAN statements:  
```  
BEGIN TRAN  
...  
COMMIT TRAN  
```  
When we are updating data we might want to place our statement between:  
```  
BEGIN TRAN  
...  
ROLLBACK TRAN  
```  
We can change ‘rollback’ to a commit when we know the right number of rows are affected.  
  
  
## Indexes  
  
*Indexes allow your database to seek for values instead of scanning for them, which can drastically speed up statements using the WHERE clause.  
The drawback is that updating indexes can slow down the entirety of the database. Indexes can increase the overall performance of our database, when used correctly.*  
- Unique clustered index  
- Clustered index  
- Non – clustered index  
  
There can only be one clustered index, but many non-clustered indexes.