## I. Stored Procedure

> A set of SQL statements assigned a name, stored in a relational db management system as a group for reusing and sharing by multiple  programs.
* SP can access and modify data in database, but *not be tied to a specific db or object*.

### 1. Benefits:
1. Provides a **security layer** between user interface and db.
2. Preserves **data integrity**
3. Improves **productivity**, avoids repeating statements
4. Offers advantages over **embedding queries** in GUI.
5. Is easier to **troubleshoot problems**
6. Eliminates the need to modify the GUI source code
7. **Reduces network traffic** between clients and servers, since the commands are executed as a single batch of code.
8. In SQL Server, SP can accept input parameters and return multiple values of output parameters

**STORED PROCEDURE** vs **FUNCTION**
* ***Functions*** are designed to send their output to a query or T-SQL statement.

* ***Stored procedures*** are designed to return outputs to the application

* ***User-defined function*** returns table variables and cannot change the server environment or operating system environment

### 2. Types of SP
* ***System SP***:
  * provided by SQL Server
  * named with prefix "sp_"
  * used to manage SQL Server, display db and user-infor
* ***SP extensions***
  > Dynamic link libraries (DLLs), written in languages C, C++ ... that SQL Server can load and execute.
  * ***External SP***: name starts with "xp_"
  * ***User-defined SP***

### Syntax

```sql
-- Transact-SQL Syntax for Stored Procedures in SQL Server 
-- and Azure SQL Database

CREATE [ OR ALTER ] { PROC | PROCEDURE }
    [schema_name.] procedure_name [ ; number ]
    [ { @parameter_name [ type_schema_name. ] data_type }
        [ VARYING ] [ = default ] [ OUT | OUTPUT | [READONLY]
    ] [ ,...n ]
[ WITH <procedure_option> [ ,...n ] ]
[ FOR REPLICATION ]
AS { [ BEGIN ] sql_statement [;] [ ...n ] [ END ] }
[;]

<procedure_option> ::=
    [ ENCRYPTION ]
    [ RECOMPILE ]
    [ EXECUTE AS Clause ]
```

*Further syntax explaination: [**MS Docs**](https://docs.microsoft.com/en-us/sql/t-sql/statements/create-procedure-transact-sql?view=sql-server-ver16)*

* Simple example:
```sql
USE CompanySupplyProduct
GO
IF EXISTS(SELECT name FROM sysobjects
WHERE name='pCompany' AND type='P')
DROP PROCEDURE pCompany
GO
CREATE PROCEDURE pCompany
AS SELECT Name, NumberofEmployee
FROM Company
ORDER BY Name DESC
GO
```

* To run procedure
  ```sql
  EXEC proc_name
  ```

* To see the content of a SP
  ```sql
  EXEC sp_helptext proc_name
  ```

* To drop a SP
  ```sql
  DROP PROCEDURE proc_name
  ```

### 3. Create a group of SP
We can group procedures of the same name so that they can be dropped together with a single drop procedure statement.

```sql
CREATE PROC group_sp;1
AS SELECT * FROM Company
GO
CREATE PROC group_sp;2
AS SELECT Name FROM Company
GO
CREATE PROC group_sp;2
AS SELECT Name, Address FROM Company
GO
```

* To drop all the procedure in the group
  ```sql
  drop procedure group_sp
  -- it is impossible to drop seperate proc
  ```
* To execute a procedure in the group
  ```sql
  exec group_sp;3
  ```

<mark>*Procedures used in the same application are often grouped this way.*</mark>

### 4. Parameters

**Syntax**
```sql
@parameter data_type [=default | NULL]
[VARYING] [OUTPUT]
```
* `@parameter` - name of parameter, can declare up to 1024 pars inside a SP
* `data_type` - system data type or user-defined (except the image type)
* `default` - the default value of the parameter
* `VARYING` - applies to the returned recordset
* `OUTPUT` - return parameter

Example:

```sql
-- proc that have 5 parameters input and 1 output
CREATE PROCEDURE scores
@score1 smallint,
@score2 smallint,
@score3 smallint,
@score4 smallint,
@score5 smallint,
@myAvg smallint OUTPUT
AS SELECT @myAvg = (@score1 + @score2 +
@score3 + @score4 + @score5) / 5
```

* Transmitting parameters
  * In the order:
    ```sql
    DECLARE @AvgScore smallint
    EXEC scores 11, 12, 34, 45, 56, @AvgScore OUTPUT
    SELECT 'The result is: ', @AvgScore
    GO
    ```

  * In any order:
    ```sql
    DECLARE @AvgScore smallint
    EXEC scores
    @score1=10, @score3=9, @score2=8, @score4=8,
    @score5=10, @myAvg = @AvgScore OUTPUT
    SELECT 'The Average Score is: ',@AvgScore
    Go
    ```

* Return value
  ```sql
  CREATE PROCEDURE ReturnFunc
  @p1 smallint, @p2 smallint, @p3 smallint, @return_val smallint
  AS SELECT @return_val = ((@p1 + @p2) * @p3)/3
  RETURN @return_val

  DECLARE @myVal smallint
  EXEC @myVal = ReturnFunc 10, 11, 2, 3
  SELECT 'The return value is: ', @myVal
  ```

**`RECOMPILE` option**

```sql
CREATE PROCEDURE proc_name RECOMPILE
```
* The whole procedure recompile every time it runs
-> The procedure can be optimized for new parameters.

```sql
EXEC proc_name RECOMPILE
```
* Compile the SP for that execution and store the new plan in the procedure buffer for later execution

**`ENCRYPTION` option**
```sql
CREATE PROCEDURE proc_name ENCRYPTION
```
* Contents of the procedure can't be view.

---

## II. Trigger
> A special SP executed automatically when there are data-changing events (UPDATE, INSERT or DELETE) - ***procedural data integrity***

* Triggers are used when other data integrity (toàn vẹn) measures, such as ***Constraint***, cann't satisfy the application's requirements.
  * Constraint is a declared integrity type: check the data before allowing it enter into the table

* Triggers cannot be created on temp or system tables

* It can't be manually run. (Only *automatically*)

* Triggers can be applied to a ***view***

### Process when trigger is activated

* The newly inserted data will be contained in the **inserted table**

* The newly deleted data will be stored in the **deleted table**

* ***Temporary tables***: **inserted table** and **deleted table**:
  * Referred to as the real table but stored in *internal memory* (RAM), not on disk
  * Values in these table are *only accessible in triggers*. Once it completed, data on these tables are no longer accessible.

### Syntax

```sql
-- SQL Server Syntax  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  
  
CREATE [ OR ALTER ] TRIGGER [ schema_name . ]trigger_name   
ON { table | view }   
[ WITH <dml_trigger_option> [ ,...n ] ]  
{ FOR | AFTER | INSTEAD OF }   
{ [ INSERT ] [ , ] [ UPDATE ] [ , ] [ DELETE ] }   
[ WITH APPEND ]  
[ NOT FOR REPLICATION ]   
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME <method specifier [ ; ] > }  
  
<dml_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name

```

*Further syntax explaination: [**MS Docs**](https://docs.microsoft.com/en-us/sql/t-sql/statements/create-trigger-transact-sql?view=sql-server-ver16)*

Example:
* Create the AddCompany trigger on the Company table: print a message whenever data is added to the table
  ```sql
  USE CompanySupplyProduct
  GO
  IF EXISTS(SELECT name FROM sysobjects
  WHERE name='AddCompany' AND Type='TR')
  DROP TRIGGER AddCompany
  GO
  CREATE TRIGGER AddCompany
  ON Company
  FOR INSERT
  AS
  PRINT 'The Company table has just been inserted data'
  GO
  ```

* Create the table DeletedCompany to store the deleted item from the Company table (it should have the same configuration as Company table)
```sql
CREATE TABLE [DeletedCompany] (
[CompanyID] int,
[Name] varchar(40),
[NumberofEmployee] int,
[Address] varchar(50),
[Telephone] char(15),
[EstablishmentDay] date,
PRIMARY KEY ([CompanyID])
);
GO

CREATE TRIGGER tg_DeleteCompany
ON Company
FOR DELETE
AS
INSERT INTO DeletedCompany SELECT * FROM deleted
GO
```

* Create update trigger when new price is inserted
```sql
CREATE TRIGGER tg_CheckPrice
ON Product
FOR UPDATE
AS
DECLARE @oldprice decimal(10,2), @newprice decimal(10,2)
SELECT @oldprice = Price FROM deleted
PRINT 'Old price ='
PRINT CONVERT(varchar(6), @oldprice)
SELECT @newprice = Price FROM inserted
PRINT 'New price ='
PRINT CONVERT(varchar(6), @newprice)
IF(@newprice > (@oldprice*1.10))
BEGIN
PRINT 'New price increased over 10%, not update'
ROLLBACK
END
ELSE
PRINT 'New price is accepted'
```

