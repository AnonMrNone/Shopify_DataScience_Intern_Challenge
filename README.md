# Shopify_DataScience_Intern_Challenge

## Question 1: Given some sample data, write a program to answer the following: [click here to access the required data set](https://docs.google.com/spreadsheets/d/16i38oonuX1y1g7C_UAmiK9GkY7cS-64DfiDMNiR41LM/edit#gid=0)

On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 

### a. Think about what could be going wrong with our calculation. Think about a better way to evaluate this data.

Answer a. The incorrect AOV of $3145.13 was misscalculated by missunderstanding count() function with sum(), instead of using the sum() function on total number of items count() was used. The proof of which is shown in the 6 & 7 cell of the [notebook](https://github.com/AnonMrNone/Shopify_DataScience_Intern_Challenge/blob/main/DataScience_Intern_Challenge_Question1.ipynb)

```python
#actual Average Order Value (AOV)
order_amount_sum = data['order_amount'].sum()
total_items_sum = data['total_items'].sum()
AOV = order_amount_sum / total_items_sum
print(round(AOV,2))

357.92
```

```python
#incorrect AOV calculation
order_amount_sum_incorrect = data['order_amount'].sum()
total_items_sum_incorrect = data['total_items'].count() #count was the mistake
AOV = order_amount_sum_incorrect / total_items_sum_incorrect
print(round(AOV,2))

3145.13
```

### b. What metric would you report for this dataset?

Answer b. We have to calculate using the following code snippet:
```python
order_amount_sum = data['order_amount'].sum()
total_items_sum = data['total_items'].sum()
AOV = order_amount_sum / total_items_sum
print(round(AOV,2))

357.92
```

### c. What is its value?

Answer c. The actual AOV is $357.92

## NOTE: RFM Analysis of this data using K-means clustering and finding insights on the data [code](https://github.com/AnonMrNone/Shopify_DataScience_Intern_Challenge/blob/main/DataScience_Intern_Challenge_Question1.ipynb)
## Question 2: For this question you’ll need to use SQL. [Follow this link](https://www.w3schools.com/SQL/TRYSQL.ASP?FILENAME=TRYSQL_SELECT_ALL) to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

### a. How many orders were shipped by Speedy Express in total?

Answer a. 
```sql
create view orders_by_shipper as
select Orders.OrderID, Orders.ShipperID, Shippers.ShipperName
from Orders join Shippers on Shippers.ShipperID=Orders.ShipperID;

SELECT count(*) FROM [orders_by_shipper] where ShipperName = "Speedy Express”;

Answer: 54
```

### b. What is the last name of the employee with the most orders?

Answer b.
```sql
create view employee_orders as
select Orders.EmployeeID, Employees.LastName
from Orders join Employees on Employees.EmployeeID=Orders.EmployeeID;

SELECT LastName, count(*) FROM [employee_orders] group by LastName order by count(*) desc;

Answer: Peacock 40
```

### c. What product was ordered the most by customers in Germany?
```sql
CREATE VIEW Products_Ordered AS SELECT Orders.OrderID, Customers.Country, OrderDetails.Quantity, Products.ProductName FROM Orders, OrderDetails JOIN Customers ON Orders.CustomerID=Customers.CustomerID JOIN Products ON OrderDetails.ProductID=Products.ProductID WHERE Country='Germany';

SELECT ProductName, (count(*) * Quantity) FROM [products_ordered_germany] group by ProductName order by (count(*) * Quantity)  desc;

Answer: Nord-Ost Matjeshering 12000
        Camembert Pierrot 12000
```
OR
```sql
CREATE VIEW Products_Ordered AS SELECT Orders.OrderID, Customers.Country, OrderDetails.Quantity, Products.ProductName FROM Orders, OrderDetails JOIN Customers ON Orders.CustomerID=Customers.CustomerID JOIN Products ON OrderDetails.ProductID=Products.ProductID WHERE Country='Germany';

SELECT ProductName, (count(*) * Quantity) FROM [products_ordered_germany] group by ProductName order by (count(*) * Quantity)  desc limit 1;

Answer: Nord-Ost Matjeshering 12000
```

### Que1: [code_file](https://github.com/AnonMrNone/Shopify_DataScience_Intern_Challenge/blob/main/DataScience_Intern_Challenge_Question1.ipynb)

### Que2: [code_file](https://github.com/AnonMrNone/Shopify_DataScience_Intern_Challenge/blob/main/DataScience_Intern_Challenge_Question2)
