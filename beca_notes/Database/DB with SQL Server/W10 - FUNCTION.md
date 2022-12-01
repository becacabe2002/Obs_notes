## Syntax

### Create a function

```sql
CREATE FUNCTION [schema_name].function_name
([@parameter [AS] [type_schema_name.]datatype]
[=default] [READONLY])
RETURNS return_datatype
[WITH {ENCRYPTION
|SCHEMABINDING
| RETURNS NULL ON NULL INPUT
| CALLED ON NULL INPUT
| EXECUTE AS Clause]
AS
BEGIN
[declaration_section]
executable_section
RETURN return_value
END;
```
* `schema_name` - name of the schema that owns the function
* `function_name` - name assigned to the function
* `@parameter` - parameters passed to the function
* `type_schema_name` - the datatype of the schema
* `default` - default value assigned to @parameter
* `READONLY` - @parameters cannot be overridden by functions
* `return_datatype` - the data type of the return value
* `ENCRYPTION` - function's source code will not be stored as text in the system.
---
* `SCHEMABINDING` - Ensures objects are not modified to affect the function
* `RETURNS NULL ON NULL INPUT` - The function will return NULL if any parameter is NULL
* `CALL ON NULL INPUT` - The function will execute even if the parameter is NULL
* `EXECUTE AS Clause` - Defines the security context to execute the function
---
* `return_value` - The value to be returned

Example:
```sql
CREATE FUNCTION fStaff
(@staff_id INT)
RETURNS VARCHAR(50)
AS
BEGIN
  DECLARE @staff_name VARCHAR(50);
  IF @staff_id < 10
  SET @staff_name = 'Smith';
  ELSE
  SET @staff_name = 'Lawrence';
  RETURN @staff_name;
END;

SELECT dbo.fStaff(8);
```

### Modifying a scalar function

```sql
ALTER FUNCTION [schema_name.]function_name
(
  parameter_list
)
RETURN data_type AS
BEGIN
  statements
  RETURN value
END
```

### Drop a scalar function
```sql
DROP FUNCTION [IF EXISTS] [schema_name.]function_name;
```
### Remove multiple funcs

```sql
DROP FUNCTION [IF EXISTS]
  schema_name.function_name1,
  schema_name.function_name2,
  ...;
```
**Delete will fail if:**
* If the function is referenced in a view or another function is created with the `WITH SCHEMABINDING` option 
-> Alter func without `WITH SCHEMABINDING` or `DROP VIEW view_name`
* If there are constraints CHECK, DEFAULT and computed columns related to function

## Some key points about scalar function

* Can be used almost anywhere in T-SQL statements

* Accepts one or more parameters but only return a **single value** (one `RETURN` statement is required)

* Can use logic like `IF` block or `WHILE` loop

* Unable to `UPDATE` data. **Data should not be accessed**.

* Can call another function

## Table Variables in SQL Server
> Allow data records to be stored, similar to the temporary tables

* [**Scope**]:
  * No longer exists after the end of the command block
  * If a table var is defined in an SP or Function, it won't exist after the SP or Func ends.

### Syntax

* Declaration
  ```sql
  DECLARE @table_variable_name TABLE
  (
    column_list
  );
  ```

Example:
```sql
DECLARE @product_table TABLE
(
  product_name VARCHAR(MAX) NOT NULL,
  brand_id INT NOT NULL,
  list_price DEC(11,2) NOT NULL
);
```

* Insert data into a table variable
  ```sql
  INSERT INTO @table_var_name
  SELECT column_list
  FROM table_name
  WHERE conditions
  ```

* View data inside table variable
  ```sql
  SELECT column_list
  FROM @tb_var_name
  ```
### Limitations
* The structure of tb var must be defined, and **can't be changed**.

* Since tb vars don't contain statistics, it doesn't help optimizer query execution
  -> **Should only be used to store few records.**

* Shouldn't be used as input/output parameters. But it is possible to **return a tb var from function**.

* It is impossible to **add a non-clustered index to a tb var** (*but not with clustered index*)

* When using tb var with `JOIN`, it has to be set with an alias
```sql
SELECT brand_name, product_name, list_price
FROM production.brands b
INNER JOIN @product_table pt
ON b.brand_id = pt.brand_id;
```

### Performance
* **Reduce time needed for recompiling**, compare to using *temporary table*

* Use **less resources** than a temp tb (less locking and logging overhead)

* Table variables execute in the **tempdb database**, not in memory (similar to the temp tb)

## Table function in SQL Server
> A user-defined function that returns a table data type. And it can also be used as the table.

### Syntax

* Create tb func

* Execute tb func

* Modifying the table functions

### Multi-statement tb func

### When to use tb func


