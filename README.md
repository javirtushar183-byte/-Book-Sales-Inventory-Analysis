# 📚 Book Sales & Inventory Analysis | SQL + Power BI + Excel  

## 📌 Project Overview  
This project analyzes book sales and inventory data to identify pricing trends, stock distribution, genre popularity, and customer behavior.  
SQL is used for data analysis, Excel is used to store query outputs, and Power BI is used to build an interactive dashboard for insights.  

---

## 🛠 Tools & Technologies Used  
• SQL  
• Excel  
• Power BI  
• Data Modeling  
• DAX  
• Data Visualization  

---

## 🗄 Database Setup  
```sql
CREATE DATABASE BookDB;
USE BookDB;

SELECT * FROM book;
SELECT * FROM customers;
SELECT * FROM orders;
📊 SQL Analysis & Business Requests
1️⃣ Retrieve All Fiction Books

Business Request:
Identify all books that belong to the Fiction genre.

SQL Query:

SELECT * FROM book WHERE genre = 'Fiction';

Output:
<img width="755" height="190" alt="1" src="https://github.com/user-attachments/assets/f0abe7b0-3f39-44ec-8bba-37876694e951" />


2️⃣ Books Published After 1950

Business Request:
Retrieve books published after 1950 to analyze modern literature trends.

SQL Query:

SELECT * FROM book WHERE published_year > 1950 ORDER BY published_year;

Output:
<img width="477" height="267" alt="2" src="https://github.com/user-attachments/assets/41a149b4-1479-4b35-bb0b-bf1e6b1ce36c" />


3️⃣ Customers from Canada

Business Request:
Identify customers located in Canada.

SQL Query:

SELECT * FROM customers WHERE country = 'Canada';

Output:
<img width="669" height="97" alt="image" src="https://github.com/user-attachments/assets/18b17871-f682-4d7d-b1fa-228f01d1f480" />


4️⃣ Orders in November 2023

Business Request:
Analyze orders placed within November 2023.

SQL Query:

SELECT * FROM orders 
WHERE order_date BETWEEN '2023-11-01' AND '2023-11-30';

Output:
<img width="520" height="240" alt="4" src="https://github.com/user-attachments/assets/c254f76c-9c3c-4aa5-a998-57d444e585be" />


5️⃣ Total Book Stock

Business Request:
Calculate total inventory across all books.

SQL Query:

SELECT SUM(stock) AS total_stock FROM book;

Output:
total_stock
  25056


6️⃣ Most Expensive Book

Business Request:
Identify the highest priced book.

SQL Query:

SELECT * FROM book ORDER BY price DESC LIMIT 1;

Output:
<img width="761" height="49" alt="image" src="https://github.com/user-attachments/assets/4c91c888-92b7-49a1-98ff-a0903b8b2162" />



7️⃣ Orders with Quantity > 1

Business Request:
Find bulk purchase orders.

SQL Query:

SELECT * FROM orders WHERE quantity > 1;

Output:
<img width="524" height="265" alt="image" src="https://github.com/user-attachments/assets/d4bb4281-7329-4a87-ba64-40696f3f69cd" />


8️⃣ Orders with Amount > 200

Business Request:
Identify high-value transactions.

SQL Query:

SELECT order_date, quantity, total_amount 
FROM orders 
WHERE total_amount > 200;

Output:
<img width="273" height="265" alt="image" src="https://github.com/user-attachments/assets/3dd31ebe-8816-44a1-aef7-95b868cb5122" />



9️⃣ Unique Genres

Business Request:
List all available book genres.

SQL Query:

SELECT DISTINCT genre FROM book;

Output:
<img width="119" height="193" alt="image" src="https://github.com/user-attachments/assets/e62afa19-ba50-45ae-b810-2b798220a795" />



🔟 Book with Lowest Stock

Business Request:
Identify books with lowest inventory.

SQL Query:

SELECT book_id, title, stock 
FROM book 
ORDER BY stock ASC 
LIMIT 1;

Output:
<img width="444" height="49" alt="image" src="https://github.com/user-attachments/assets/48eb88e2-a552-4f61-8cd1-bf4ec4a9c7f7" />



Insight:
This book is out of stock and requires immediate restocking.

1️⃣1️⃣ Total Revenue

Business Request:
Calculate total revenue generated from all orders.

SQL Query:

SELECT SUM(total_amount) AS revenue FROM orders;

Output:
revenue
75628.66



1️⃣2️⃣ Books Sold per Genre

Business Request:
Analyze sales distribution by genre.

SQL Query:

SELECT b.genre, SUM(o.quantity) AS books_sold  
FROM orders o  
JOIN book b ON b.book_id = o.book_id  
GROUP BY b.genre;

Output:
<img width="211" height="193" alt="image" src="https://github.com/user-attachments/assets/02606a1e-aa35-489e-a8d7-8648c7d04612" />



1️⃣3️⃣ Average Fantasy Price

Business Request:
Find average price of Fantasy books.

SQL Query:

SELECT AVG(price) FROM book WHERE genre = 'Fantasy';

Output:
avg_price
  25.98

1️⃣4️⃣ Repeat Customers

Business Request:
Identify customers with multiple orders.

SQL Query:

SELECT customer_id  
FROM orders  
GROUP BY customer_id  
HAVING COUNT(order_id) >= 2;

Output:
<img width="161" height="265" alt="image" src="https://github.com/user-attachments/assets/ac2b154d-9374-44b2-ad59-4d8e5280739d" />



1️⃣5️⃣ Top 5 Most Ordered Books

Business Request:
Find best-selling books.

SQL Query:

SELECT b.book_id, b.title, COUNT(o.order_id) AS order_count  
FROM orders o  
JOIN book b ON o.book_id = b.book_id  
GROUP BY b.book_id, b.title  
ORDER BY order_count DESC  
LIMIT 5;

Output:
<img width="562" height="145" alt="image" src="https://github.com/user-attachments/assets/9a656984-d4f3-46af-85ac-4e682161db56" />



1️⃣6️⃣ Top 10 Expensive Fantasy Books

Business Request:
Analyze premium Fantasy books.

SQL Query:

SELECT * FROM book  
WHERE genre = 'Fantasy'  
ORDER BY price DESC  
LIMIT 10;

Output:
<img width="831" height="265" alt="image" src="https://github.com/user-attachments/assets/f81fbdbf-c006-41b5-b276-ca710461e106" />



1️⃣7️⃣ Sales by Author

Business Request:
Evaluate author performance.

SQL Query:

SELECT b.author, SUM(o.quantity) AS total_quantity  
FROM orders o  
JOIN book b ON o.book_id = b.book_id  
GROUP BY b.author  
ORDER BY total_quantity DESC;

Output:
<img width="250" height="265" alt="image" src="https://github.com/user-attachments/assets/5a6ca1dd-36c1-4eb6-b14b-9a53932bf870" />



1️⃣8️⃣ High Spending Cities

Business Request:
Identify cities with total spending above 300.

SQL Query:

SELECT c.city, SUM(o.total_amount) AS total_spend  
FROM customers c  
JOIN orders o ON c.customer_id = o.customer_id  
GROUP BY c.city  
HAVING SUM(o.total_amount) > 300;

Output:
<img width="376" height="265" alt="image" src="https://github.com/user-attachments/assets/24a950d6-280d-43d9-83a1-8f6cbb29c5b7" />



1️⃣9️⃣ Top Spending Customers

Business Request:
Identify highest spending customers.

SQL Query:

SELECT c.name, o.customer_id, SUM(o.total_amount) AS total_spend  
FROM orders o  
JOIN customers c ON o.customer_id = c.customer_id  
GROUP BY o.customer_id, c.name  
ORDER BY total_spend DESC  
LIMIT 10;

Output:
<img width="330" height="265" alt="image" src="https://github.com/user-attachments/assets/2aa0a919-a2b7-4acb-b219-f11f01229786" />



2️⃣0️⃣ Remaining Stock

Business Request:
Calculate remaining inventory after sales.

SQL Query:

SELECT b.book_id, b.title,  
COALESCE(SUM(o.quantity),0) AS order_quantity,  
b.stock - COALESCE(SUM(o.quantity),0) AS remaining_stock  
FROM book b  
LEFT JOIN orders o ON b.book_id = o.book_id  
GROUP BY b.book_id, b.title, b.stock;

Output:
<img width="445" height="265" alt="image" src="https://github.com/user-attachments/assets/4006f3c1-518a-4ac8-843e-e07bc238ae86" />

