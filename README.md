# Querying-with-Transact-SQL-

5- Handle NULLs

4- Work with data types

3- Use the SELECT statement to query tables in a database

  - Server actually evaluates them: The FROM clause is evaluated first, to provide the source rows for the rest of the statement. A virtual table is created and passed to the next step.
  The WHERE clause is next to be evaluated, filtering those rows from the source table that match a predicate. The filtered virtual table is passed to the next step.
  GROUP BY is next, organizing the rows in the virtual table according to unique values found in the GROUP BY list. A new virtual table is created, containing the list of groups, and is passed to the next   step. From this point in the flow of operations, only columns in the GROUP BY list or aggregate functions may be referenced by other elements.
  The HAVING clause is evaluated next, filtering out entire groups based on its predicate. The virtual table created in step 3 is filtered and passed to the next step.
  The SELECT clause finally executes, determining which columns will appear in the query results. Because the SELECT clause is evaluated after the other steps, any column aliases (in our example, Orders)    created there cannot be used in the GROUP BY or HAVING clause.
  The ORDER BY clause is the last to execute, sorting the rows as determined by its column list

2- Identify SQL statement types
  In SQL, statements are categorized into several types:
  
  - Data Manipulation Language (DML): Focuses on querying and modifying data, including SELECT, INSERT, UPDATE, and DELETE statements.
  
  - Data Definition Language (DDL): Manages the definition and life cycle of database objects like tables and views, using statements such as CREATE, ALTER, and DROP.
  
  - Data Control Language (DCL): Manages security permissions for users and objects, including GRANT, REVOKE, and DENY statements.

1- Identify database objects in schemas
  - In SQL Server database systems, tables are organized within schemas, which act as logical namespaces. For instance, a Customer table might be in the Sales schema, while a Product table is in the 
  Production schema. This allows the same table names to exist in different schemas, such as having an Order table in both the Sales and Production schemas for different purposes. 
  - SQL Server uses a hierarchical naming system where the full name of an object includes the database server instance, database name, schema name, and table name (e.g., Server1.StoreDB.Sales.Order). Within a single database, it's common to refer to tables by including the schema name, like Sales.Order.
