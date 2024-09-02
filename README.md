# Querying-with-Transact-SQL-

5- Handle NULLs

4- Work with data types

3- Use the SELECT statement to query tables in a database

2- Identify SQL statement types
  In SQL, statements are categorized into several types:
  
  - Data Manipulation Language (DML): Focuses on querying and modifying data, including SELECT, INSERT, UPDATE, and DELETE statements.
  
  - Data Definition Language (DDL): Manages the definition and life cycle of database objects like tables and views, using statements such as CREATE, ALTER, and DROP.
  
  - Data Control Language (DCL): Manages security permissions for users and objects, including GRANT, REVOKE, and DENY statements.

1- Identify database objects in schemas
  - In SQL Server database systems, tables are organized within schemas, which act as logical namespaces. For instance, a Customer table might be in the Sales schema, while a Product table is in the 
  Production schema. This allows the same table names to exist in different schemas, such as having an Order table in both the Sales and Production schemas for different purposes. 
  - SQL Server uses a hierarchical naming system where the full name of an object includes the database server instance, database name, schema name, and table name (e.g., Server1.StoreDB.Sales.Order). Within a single database, it's common to refer to tables by including the schema name, like Sales.Order.
