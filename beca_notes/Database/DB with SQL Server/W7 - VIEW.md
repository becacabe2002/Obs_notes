## I. Definitions
> A virtual table based on the result-set of an SQL statement.
- It can consist of columns from more than one table.
- Can add func, `WHERE`, `JOIN` statements to a view
- Do not store data, *except indexed views*

## II. Types of Views
- Besides the standard role of basic user-defined views, SQL also provides 3 kinds of views:
### 1. Indexed Views
> A view that have been materialized (view definition has been computed and resulting data stored ***just like a table***)
* A view is indexed by creating a unique clustered index (chỉ số nhóm) on it.

* Indexed views can ***improve the performance*** of some types of queries a lot.
  * Work best for queries that consist of *many rows*.
  * Not suitable for underlying data sets that are *frequently updated*. (not stable)

### 2. Partitioned Views
* Join horizontally partitioned data from a set of member tables across *one or more servers*.

-> Make the data appear as if from one table.
* A view joining member tables on the same instance of SQL Server is a ***local partitioned view***.

### 3. System Views
> Expose catalog metadata.
* Can be used to return infor about the instance of SQL Server or the objects defined in the instance.

## III. Creating a view
🛑 **Limitations**:
* Can be created only in the current database
* Have the maximum of 1,024 columns

### Syntax

```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

## IV. Querying on a view
*Do it like with a normal table*

## V. Modifying a view
* Modifying a view doesn't affect any dependent objects, like ***stored procedures*** or ***triggers***. 

* Unless it changes the definition of the view in a way that the dependent object is *no longer valid*.

* We can modify indexed views, but it will *drop all indexes* on the view.
### Syntax
```sql
ALTER VIEW view_name AS
sql_statement
```

## VI. Deleting a view
### Syntax
```sql
DROP VIEW view_name;
```

## VII. Indexed view
* **Regular views** don't improve the underlying query performance, but **indexed views** do

### Steps to create an indexed view:
1. Create a view using `WITH SCHEMABINDING` (bind: ràng buộc, schema: lược đồ)
which binds the view to the schema of the underlying tables.

2. Create a unique clustered index on the view. (this help materialize the view)

⚠️ <mark style='background-color:#FFFFE0'> You have to *drop the indexed view* before changing the structure of the underlying tables. </mark>

### Example
* Create a view with schemabinding

```sql
create view product_master with schemabinding
as
select product_id, product_name, model_year, list_price,
branc_name, category_name
from production.products p inner join
production.brands b on b.brand_id = p.brand_id
inner join production.categories c 
on c.category_id = p.category_id
```

* Examine the I/O cost statistics

```sql
set statistics io on /*you can set it on/off*/
go
select * 
from production.product_master
order by product_name;
go
```

* Add a unique clustered index to the view
```sql
create unique clustered index ucidx_product_id
ON production.product_master(product_id);
```
or a non-clustered index
```sql
CREATE NONCLUSTERED INDEX ucidx_product_name
ON production.product_master(product_name);
```

Further details, visit [**this address**](https://www.sqlshack.com/using-sql-create-index-to-create-clustered-and-non-clustered-indexes/).

