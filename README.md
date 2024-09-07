# Querying-with-Transact-SQL-

Challenge 1: Retrieve customer data
Adventure Works Cycles sells directly to retailers, who then sell products to consumers. Each retailer that is an Adventure Works customer has provided a named contact for all communication from Adventure Works. The sales manager at Adventure Works has asked you to generate some reports containing details of the company’s customers to support a direct sales campaign.

a) Retrieve customer details
Familiarize yourself with the SalesLT.Customer table by writing a Transact-SQL query that retrieves all columns for all customers.

SELECT * FROM SalesLT.Customer;

b) Retrieve customer name data
Create a list of all customer contact names that includes the title, first name, middle name (if any), last name, and suffix (if any) of all customers.

SELECT ISNULL(Title,'') + FirstName + ' ' +    ISNULL(MiddleName, '') + LastName  AS CustumerName 
FROM SalesLT.Customer;

c) Retrieve customer names and phone numbers
Each customer has an assigned salesperson. You must write a query to create a call sheet that lists:
   The salesperson, a column named CustomerName that displays how the customer contact should be     
   SELECT *greeted (for example, Mr Smith)
   The customer’s phone number.

SELECT SalesPerson, ISNULL(Title,'') + ' ' + LastName as CustomerName, PhoneFROM SalesLT.Customer;
_______________________________________________________________________________________

Challenge 2: Retrieve customer order data
As you continue to work with the Adventure Works customer data, you must create queries for reports that have been requested by the sales team.

a) Retrieve a list of customer companies
    You have been asked to provide a list of all customer companies in the format     
    Customer ID : Company Name - for example, 78: Preferred Bikes.

SELECT CAST(CustomerID AS varchar(5)) + ': ' + CompanyName AS CustomerCompany
FROM SalesLT.Customer;

b) Retrieve a list of sales order revisions
  The SalesLT.SalesOrderHeader table contains records of sales orders. You have been     asked to retrieve data for a report that shows: The sales order number and revision number in the format () –        for example SO71774 (2), the order date converted to ANSI standard 102 format (yyyy.mm.dd – for example 2015.01.31).

SELECT SalesOrderNumber + ' (' + CAST(RevisionNumber AS varchar(5)) + ')' AS SalesOrder,CONVERT(nvarchar(30), OrderDate, 102) AS OrderDateFROM SalesLT.SalesOrderHeader;

SELECT SalesOrderNumber + ' (' + STR(RevisionNumber, 1) + ')' AS OrderRevision,   CONVERT(nvarchar(30), OrderDate, 102) AS OrderDateFROM SalesLT.SalesOrderHeader;

    
Challenge 3: Retrieve customer contact details
Some records in the database include missing or unknown values that are returned as NULL. You must create some queries that handle these NULL values appropriately.

Retrieve customer contact names with middle names if known

You have been asked to write a query that returns a list of customer names. The list must consist of a single column in the format first last (for example Keith Harris) if the middle name is unknown, or first middle last (for example Jane M. Gates) if a middle name is known.
Retrieve primary contact details

Customers may provide Adventure Works with an email address, a phone number, or both. If an email address is available, then it should be used as the primary contact method; if not, then the phone number should be used. You must write a query that returns a list of customer IDs in one column, and a second column named PrimaryContact that contains the email address if known, and otherwise the phone number.

IMPORTANT: In the sample data provided, there are no customer records without an email address. Therefore, to verify that your query works as expected, run the following UPDATE statement to remove some existing email addresses before creating your query:

sql
UPDATE SalesLT.Customer
SET EmailAddress = NULL
WHERE CustomerID % 7 = 1;
Retrieve shipping status

You have been asked to create a query that returns a list of sales order IDs and order dates with a column named ShippingStatus that contains the text Shipped for orders with a known ship date, and Awaiting Shipment for orders with no ship date.

IMPORTANT: In the sample data provided, there are no sales order header records without a ship date. Therefore, to verify that your query works as expected, run the following UPDATE statement to remove some existing ship dates before creating your query.

sql
UPDATE SalesLT.SalesOrderHeader
SET ShipDate = NULL
WHERE SalesOrderID > 71899;





5- Handle NULLs
  A NULL value means no value or unknown. It does not mean zero or blank, or even an empty string. 
  a) ISNULL: The ISNULL function takes two arguments. The first is an expression we are testing. If the value of that first argument is NULL, the function returns the second argument. If the first       
  expression is not null, it is returned unchanged.
  SELECT FirstName, ISNULL(MiddleName, 'None') AS MiddleIfAny, LastName FROM Sales.Customer;
  
  b) COALESCE: The COALESCE function is ANSI standard it can take a variable number of arguments, each of which is an expression. It will return the first expression in the list that is not NULL.
   there are only two arguments, COALESCE behaves like ISNULL. However, with more than two arguments, COALESCE can be used as an alternative to a multipart CASE expression using ISNULL.
   If all arguments are NULL, COALESCE returns NULL. All the expressions must return the same or compatible data types.
   The syntax : SELECT COALESCE ( expression1, expression2, [ ,...n ] )

  c) NULLIF: The NULLIF function allows to return NULL under certain conditions. NULLIF takes two arguments and returns NULL if they're equivalent. If they aren't equal, NULLIF returns the first argument.
     SELECT SalesOrderID,  ProductID, UnitPrice, NULLIF(UnitPriceDiscount, 0) AS Discount FROM Sales.SalesOrderDetail;
4- Work with data types
  T-SQL include functions to help you explicitly convert between data types: 
  a) CAST and TRY_CAST: The CAST function converts a value to a specified data type if the value is compatible with the target data type. An error will be returned if incompatible.

  For example, the following query uses CAST to convert the integer values in the ProductID column to varchar values (with a maximum of 4 characters) in order to concatenate them with another 
  character-  based value: SELECT CAST(ProductID AS varchar(4)) + ': ' + Name AS ProductName FROM Production.Product;  This transformation laslts only for the life of the query
  
  b) CONVERT and TRY_CONVERT: Transact-SQL, we can also use the CONVERT function
  SELECT CONVERT(varchar(4), ProductID) + ': ' + Name AS ProductName FROM Production.Product;
  Like CAST, CONVERT has a TRY_CONVERT variant that returns NULL for incompatible values.

  Another benefit of using CONVERT over CAST is that CONVERT also includes a parameter that enables you specify a format style when converting numeric and date values to strings. For example, consider the   following query: SELECT SellStartDate,
         CONVERT(varchar(20), SellStartDate) AS StartDate,
         CONVERT(varchar(10), SellStartDate, 101) AS FormattedStartDate 
         FROM SalesLT.Product;

  c) PARSE and TRY_PARSE: The PARSE function is designed to convert formatted strings that represent numeric or date/time values
   SELECT PARSE('01/01/2021' AS date) AS DateValue, PARSE('$199.99' AS money) AS MoneyValue;
   
  d) STR: The STR function converts a numeric value to a varchar.
    SELECT ProductID,  '$' + STR(ListPrice) AS Price FROM Production.Product;

3- Use the SELECT statement to query tables in a database
  
  SELECT OrderDate
  FROM Sales.SalesOrder
  WHERE Status = 'Shipped'
  
The query consists of a SELECT statement, which is composed of multiple clauses, each of which defines a specific operation that must be applied to the data being retrieved.
The SELECT clause returns the OrderDate column, the FROM clause identifies which table is the source of the rows for the query,he WHERE clause filters rows out of the results, keeping only those rows that satisfy the specified condition; in this case, orders that have a status of "shipped":

Selecting all columns: SELECT * FROM Production.Product;
Selecting specific columns: SELECT ProductID, Name, ListPrice, StandardCost ‎FROM Production.Product;
Selecting expressions: SELECT ProductID, Name + '(' + ProductNumber + ')', ListPrice - StandardCost FROM Production.Product;
Specifying column aliases: SELECT ProductID AS ID, Name + '(' + ProductNumber + ')' AS ProductName, ListPrice - StandardCost AS Markup FROM Production.Product;

2- Identify SQL statement types
  In SQL, statements are categorized into several types:
  
  - Data Manipulation Language (DML): Focuses on querying and modifying data, including SELECT, INSERT, UPDATE, and DELETE statements.
  
  - Data Definition Language (DDL): Manages the definition and life cycle of database objects like tables and views, using statements such as CREATE, ALTER, and DROP.
  
  - Data Control Language (DCL): Manages security permissions for users and objects, including GRANT, REVOKE, and DENY statements.

1- Identify database objects in schemas
  - In SQL Server database systems, tables are organized within schemas, which act as logical namespaces. For instance, a Customer table might be in the Sales schema, while a Product table is in the 
  Production schema. This allows the same table names to exist in different schemas, such as having an Order table in both the Sales and Production schemas for different purposes. 
  - SQL Server uses a hierarchical naming system where the full name of an object includes the database server instance, database name, schema name, and table name (e.g., Server1.StoreDB.Sales.Order). Within a single database, it's common to refer to tables by including the schema name, like Sales.Order.
