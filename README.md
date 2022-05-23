# SQLLitestudio1.7
#In this SQL, I'm querying a database with multiple tables in it to quantify statistics about customer and order data. 

#1. How many orders were placed in January? 
SELECT COUNT(orderid)
FROM BIT_DB.JanSales

#2. How many of those orders were for an iPhone? 
SELECT COUNT(orderid)
FROM BIT_DB.JanSales
WHERE Product='iPhone'

#3. Select the customer account numbers for all the orders that were placed in February. 
SELECT acctnum
FROM BIT_DB.customers cust

INNER JOIN BIT_DB.FebSales Feb
ON cust.order_id=FEB.orderid

#4. Which product was the cheapest one sold in January, and what was the price? 
SELECT distinct Product, price
FROM BIT_DB.JanSales
WHERE  price in (SELECT min(price) FROM BIT_DB.JanSales)
#OR 
SELECT distinct product, price FROM BIT_DB.JanSales 
ORDER BY price ASC LIMIT 1

#5. What is the total revenue for each product sold in January?
SELECT sum(quantity)*price as revenue
,product
FROM BIT_DB.JanSales
GROUP BY product

#6. Which products were sold in February at 548 Lincoln St, Seattle, WA 98101, how many of each were sold, and what was the total revenue?
select 
sum(Quantity), 
product, 
sum(quantity)*price as revenue
FROM BIT_DB.FebSales 
WHERE location = '548 Lincoln St, Seattle, WA 98101'
GROUP BY product

#7. How many customers ordered more than 2 products at a time, and what was the average amount spent for those customers? 
select 
count(cust.acctnum), 
avg(quantity)*price
FROM BIT_DB.FebSales Feb
LEFT JOIN BIT_DB.customers cust
ON FEB.orderid=cust.order_id
WHERE Feb.Quantity>2

#8. List all the products sold in Los Angeles in February, and include how many of each were sold.
SELECT PRODUCT,SUM(QUANTITY)
FROM BIT_DB.FEBSALES
WHERE LOCATION LIKE '%LOS ANGELES%'
GROUP BY PRODUCT

#9 Which locations in New York received at least 3 orders in January, and how many orders did they each receive?
SELECT DISTINCT LOCATION, COUNT(ORDERID)
FROM BIT_DB.JanSales
WHERE LOCATION LIKE'%NEW YORK%'
GROUP BY LOCATION 
HAVING COUNT(ORDERID)>2

#10 How many of each type of headphone were sold in February?
SELECT SUM(QUANTITY) AS QUANTITY, PRODUCT
FROM BIT_DB.FEBSALES
WHERE PRODUCT LIKE'%HEADPHONES%'
GROUP BY PRODUCT

#11 What was the average amount spent per account in February? 



#12 What was the average quantity of products purchased per account in February?




#13 Which product brought in the most revenue in January and how much revenue did it bring in total?
