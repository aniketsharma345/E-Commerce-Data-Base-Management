## Introduction
The advanced SQL project for an e-commerce database involves creating, managing, and analyzing a comprehensive set of data tables to facilitate in-depth data analysis, customer insights, product performance evaluation, and anomaly detection. The project includes several key tables, such as Products, Categories, Customers, Orders, OrderDetails, Payments, Returns, Reviews, and ProductPreferences. This database schema allows for robust data operations, supporting the needs of an e-commerce business in tracking inventory, order status, customer preferences, and more.


## Detailed Information About All Tables
## 1. Categories
   This table stores information about the different categories of products available in the e-commerce platform.

   1. CategoryID (INT): Primary key, auto-incremented.
   2. CategoryName (VARCHAR(255)): Name of the category.
   3. Description (TEXT): Description of the category.

 ##  2. Products
    
  This table contains details about each product available for sale.
  1. ProductID (INT): Primary key, auto-incremented.
  2. ProductName (VARCHAR(255)): Name of the product.
  3. CategoryID (INT): Foreign key referencing Categories table.
  4. Price (DECIMAL(10, 2)): Price of the product.
  5. StockQuantity (INT): Quantity of the product in stock.
  6. Description (TEXT): Description of the product.

##  3. Customers

 This table stores information about the customers who make purchases.CustomerID (INT): 
 1. CustimweID(INT): Primary key, auto-incremented.
 2. FirstName (VARCHAR(255)): First name of the customer.
 3. LastName (VARCHAR(255)): Last name of the customer.
 4. Email (VARCHAR(255)): Email address of the customer, unique.
 5. Password (VARCHAR(255)): Password for the customer's account.
 6. Address (VARCHAR(255)): Address of the customer.
 7. City (VARCHAR(255)): City where the customer resides.
 8. State (VARCHAR(255)): State where the customer resides.
 9. ZipCode (VARCHAR(10)): ZIP code of the customer’s address.
 10. Country (VARCHAR(255)): Country of the customer.

## 4. Orders

  This table tracks orders placed by customers.

  1. OrderID (INT): Primary key, auto-incremented.
  2. CustomerID (INT): Foreign key referencing Customers table.
  3. OrderDate (DATETIME): Date and time when the order was placed.
  4. TotalAmount (DECIMAL(10, 2)): Total amount of the order.
  5. OrderStatus (VARCHAR(50)): Status of the order (e.g., Pending, Shipped, Delivered).

## 5. OrderDetails

 This table stores details about each product included in an order.
 
 1. OrderDetailID (INT): Primary key, auto-incremented.
 2. OrderID (INT): Foreign key referencing Orders table.
 3. ProductID (INT): Foreign key referencing Products table.
 4. Quantity (INT): Quantity of the product ordered.
 5. UnitPrice (DECIMAL(10, 2)): Price of a single unit of the product.

##  6. Payments

This table tracks payments made for orders.

1. PaymentID (INT): Primary key, auto-incremented.
2. OrderID (INT): Foreign key referencing Orders table.
3. PaymentDate (DATETIME): Date and time when the payment was made.
4. Amount (DECIMAL(10, 2)): Amount paid.
5. PaymentMethod (VARCHAR(50)): Method of payment (e.g., Credit Card, PayPal, UPI).

## 7. Returns

This table tracks product returns.

1. ReturnID (INT): Primary key, auto-incremented.
2. OrderID (INT): Foreign key referencing Orders table.
3. ProductID (INT): Foreign key referencing Products table.
4. ReturnDate (DATETIME): Date and time when the return was made.
5. Quantity (INT): Quantity of the product returned.
6. Reason (TEXT): Reason for the return.

## 8. Reviews

This table stores customer reviews for products.

1. ReviewID (INT): Primary key, auto-incremented.
2. CustomerID (INT): Foreign key referencing Customers table.
3. ProductID (INT): Foreign key referencing Products table.
4. ReviewDate (DATETIME): Date and time when the review was made.
5. Rating (INT): Rating given to the product (e.g., 1-5 stars).
6. Comment (TEXT): Textual comment for the review.

## 9. ProductPreferences

This table tracks customer preferences for products based on their order history.

1. PreferenceID (INT): Primary key, auto-incremented.
2. CustomerID (INT): Foreign key referencing Customers table.
3. ProductID (INT): Foreign key referencing Products table.
4. PreferenceScore (INT): Score indicating the customer's preference for the product (e.g., based on order frequency).


Certainly! Here are the relationship statuses for the e-commerce project tables:

### Relationships in the E-commerce Database

1. **Categories and Products**
    - **Relationship:** "has"
    - **Type of Relation:** 1 to many
    - **Explanation:** A category can have many products. One product belongs to one category.

2. **Customers and Orders**
    - **Relationship:** "places"
    - **Type of Relation:** 1 to many
    - **Explanation:** A customer can place many orders. One order is placed by one customer.

3. **Orders and OrderDetails**
    - **Relationship:** "contains"
    - **Type of Relation:** 1 to many
    - **Explanation:** An order can contain many order details (products). One order detail belongs to one order.

4. **Products and OrderDetails**
    - **Relationship:** "is part of"
    - **Type of Relation:** 1 to many
    - **Explanation:** A product can be part of many order details. One order detail is for one product.

5. **Orders and Payments**
    - **Relationship:** "is paid by"
    - **Type of Relation:** 1 to many
    - **Explanation:** An order can have many payments (e.g., partial payments). One payment is for one order.

6. **Orders and Returns**
    - **Relationship:** "can be returned by"
    - **Type of Relation:** 1 to many
    - **Explanation:** An order can have many returns. One return is associated with one order.

7. **Products and Returns**
    - **Relationship:** "is returned"
    - **Type of Relation:** 1 to many
    - **Explanation:** A product can be part of many returns. One return is for one product.

8. **Customers and Reviews**
    - **Relationship:** "writes"
    - **Type of Relation:** 1 to many
    - **Explanation:** A customer can write many reviews. One review is written by one customer.

9. **Products and Reviews**
    - **Relationship:** "receives"
    - **Type of Relation:** 1 to many
    - **Explanation:** A product can receive many reviews. One review is for one product.

10. **Customers and ProductPreferences**
    - **Relationship:** "has"
    - **Type of Relation:** 1 to many
    - **Explanation:** A customer can have many product preferences. One product preference belongs to one customer.

11. **Products and ProductPreferences**
    - **Relationship:** "is preferred by"
    - **Type of Relation:** 1 to many
    - **Explanation:** A product can be preferred by many customers. One product preference is for one product.
   
### SQL QUERIES
    

## 1. Retrieve the total number of orders for each customer
``` SQL
  SELECT CustomerID, COUNT(OrderID) AS TotalOrders
  FROM Orders
  GROUP BY CustomerID;

``` 

## 2. Find the top 5 products with the highest sales.
``` SQL
SELECT p.ProductID, p.ProductName, SUM(od.Quantity) AS TotalQuantitySold
FROM Products p
JOIN OrderDetails od ON p.ProductID = od.ProductID
GROUP BY p.ProductID, p.ProductName
ORDER BY TotalQuantitySold DESC
LIMIT 5;
```

## 3. Calculate the total revenue generated by each product.
``` SQL
SELECT p.ProductID, p.ProductName, SUM(od.Quantity * od.UnitPrice) AS TotalRevenue
FROM Products p
JOIN OrderDetails od ON p.ProductID = od.ProductID
GROUP BY p.ProductID, p.ProductName
ORDER BY TotalRevenue DESC;

```

## 4. Identify customers who have spent more than $500 in total.

``` SQL
SELECT c.CustomerID, c.FirstName, c.LastName, SUM(o.TotalAmount) AS TotalSpent
FROM Customers c
JOIN Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID, c.FirstName, c.LastName
HAVING TotalSpent > 500;

```

## 5. Retrieve the average rating for each product

``` SQL
SELECT p.ProductID, p.ProductName, AVG(r.Rating) AS AverageRating
FROM Products p
JOIN Reviews r ON p.ProductID = r.ProductID
GROUP BY p.ProductID, p.ProductName;

```

## 6. Find the most recent order for each customer

``` SQL
SELECT o.CustomerID, o.OrderID, o.OrderDate
FROM Orders o
INNER JOIN (
    SELECT CustomerID, MAX(OrderDate) AS LatestOrderDate
    FROM Orders
    GROUP BY CustomerID
) AS RecentOrders
ON o.CustomerID = RecentOrders.CustomerID AND o.OrderDate = RecentOrders.LatestOrderDate;

```
By Using CTE
``` SQL
with cte as (
select customerid,max(orderdate) as recent_date  from orders
group by customerid)
select o.customerID,o.orderid,o.orderdate
from orders o
join cte on o.customerid = cte.customerid
where o.orderdate = cte.recent_date;
```

## 7. Identify products that have never been sold.
``` SQL
SELECT p.ProductID, p.ProductName
FROM Products p
LEFT JOIN OrderDetails od ON p.ProductID = od.ProductID
WHERE od.ProductID IS NULL;
```
## 
8. Calculate the return rate for each product
``` SQL
with cte as (
SELECT o.productid,count(o.orderid),count(r.returnid),
count(r.returnid)/count(o.orderid) *100 as return_rate
FROM orderdetails o
left JOIN RETURNS R
ON o.orderid = r.returnid
group by o.productid)
select cte.productid,p.productname,cte.return_rate
from cte 
join products p
on p.productid = cte.productid;
```

## 9.Get the list of customers along with their most preferred product.

``` SQL
with cte as (
select pp.customerid,p.productname from productpreferences pp
join products p
on p.productid = pp.productid
where PreferenceScore = 1)
select cte.customerid,concat(c.firstname,' ',c.lastname) as name,cte.productname
from cte 
join customers c
on c.customerid = cte.customerid;
```

## 10. List all orders along with the payment status
``` SQL
select *,case when paymentid is not null then "paid" else "pending" end as payment_status
from (
select o.OrderID,o.customerid,o.orderstatus,p.paymentid from orders o
left join payments p
on p.orderid = o.orderid) a 
;
``` 


## For Detailed Sql Query Click [HERE](https://github.com/aniketsharma345/E-Commerce-Data-Base-Managment/blob/main/E_commerce.sql)

## Conclusion

This advanced SQL project for an e-commerce database involves creating a comprehensive schema that includes tables for products, categories, customers, orders, order details, payments, returns, reviews, and product preferences. These tables allow for detailed data analysis, enabling the business to understand customer behavior, product performance, and sales trends, as well as manage inventory and detect anomalies effectively.


