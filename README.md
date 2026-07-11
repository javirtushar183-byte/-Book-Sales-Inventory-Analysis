# 📚 Book Sales & Inventory Analysis | SQL + Power BI + Excel

## 🗄️ Database Setup

```sql
CREATE DATABASE BookDB;
USE BookDB;

SELECT * FROM book;
SELECT * FROM customers;
SELECT * FROM orders;
```

---

## 📊 SQL Analysis & Business Requests

### 🔹 Q1. Retrieve All Fiction Books

```sql
SELECT * FROM book 
WHERE genre = 'Fiction';
```

**Output:**  
<img width="755" height="190" alt="1" src="https://github.com/user-attachments/assets/f0abe7b0-3f39-44ec-8bba-37876694e951" />


---

### 🔹 Q2. Books Published After 1950

```sql
SELECT * FROM book 
WHERE published_year > 1950 
ORDER BY published_year;
```

**Output:**  
<img width="477" height="267" alt="2" src="https://github.com/user-attachments/assets/41a149b4-1479-4b35-bb0b-bf1e6b1ce36c" />

---

### 🔹 Q3. Customers from Canada

```sql
SELECT * FROM customers 
WHERE country = 'Canada';
```

**Output:**  
<img width="669" height="97" alt="image" src="https://github.com/user-attachments/assets/18b17871-f682-4d7d-b1fa-228f01d1f480" />

---

### 🔹 Q4. Orders in November 2023

```sql
SELECT * FROM orders 
WHERE order_date BETWEEN '2023-11-01' AND '2023-11-30';
```

**Output:**  
<img width="520" height="240" alt="4" src="https://github.com/user-attachments/assets/c254f76c-9c3c-4aa5-a998-57d444e585be" />

---

### 🔹 Q5. Total Book Stock

```sql
SELECT SUM(stock) AS total_stock FROM book;
```

**Output:**  
total_stock
  25056


---

### 🔹 Q6. Most Expensive Book

```sql
SELECT * FROM book 
ORDER BY price DESC 
LIMIT 1;
```

**Output:**  
<img width="761" height="49" alt="image" src="https://github.com/user-attachments/assets/4c91c888-92b7-49a1-98ff-a0903b8b2162" />

---

### 🔹 Q7. Orders with Quantity > 1

```sql
SELECT * FROM orders 
WHERE quantity > 1;
```

**Output:**  
<img width="524" height="265" alt="image" src="https://github.com/user-attachments/assets/d4bb4281-7329-4a87-ba64-40696f3f69cd" />

---

### 🔹 Q8. Orders with Amount > 200

```sql
SELECT order_date, quantity, total_amount 
FROM orders 
WHERE total_amount > 200;
```

**Output:**  
<img width="273" height="265" alt="image" src="https://github.com/user-attachments/assets/3dd31ebe-8816-44a1-aef7-95b868cb5122" />


---

### 🔹 Q9. Unique Genres

```sql
SELECT DISTINCT genre FROM book;
```

**Output:**  
<img width="119" height="193" alt="image" src="https://github.com/user-attachments/assets/e62afa19-ba50-45ae-b810-2b798220a795" />
---

### 🔹 Q10. Book with Lowest Stock

```sql
SELECT book_id, title, stock 
FROM book 
ORDER BY stock ASC 
LIMIT 1;
```

**Output:**  
<img width="444" height="49" alt="image" src="https://github.com/user-attachments/assets/48eb88e2-a552-4f61-8cd1-bf4ec4a9c7f7" />

---

### 🔹 Q11. Total Revenue

```sql
SELECT SUM(total_amount) AS revenue FROM orders;
```

**Output:**  
revenue
75628.66

---

### 🔹 Q12. Books Sold per Genre

```sql
SELECT b.genre, SUM(o.quantity) AS books_sold  
FROM orders o  
JOIN book b ON b.book_id = o.book_id  
GROUP BY b.genre;
```

**Output:**  
<img width="211" height="193" alt="image" src="https://github.com/user-attachments/assets/02606a1e-aa35-489e-a8d7-8648c7d04612" />

---

### 🔹 Q13. Average Price of Fantasy Books
```sql
SELECT AVG(price) 
FROM book 
WHERE genre = 'Fantasy';
```
**Output:** 
 avg_price
 
25.98169014

---

### 🔹 Q14. Customers with Multiple Orders
```sql
SELECT customer_id,quantity
FROM orders  
GROUP BY customer_id  
HAVING COUNT(order_id) >= 2;
```
**Output:** 
<img width="161" height="265" alt="image" src="https://github.com/user-attachments/assets/ac2b154d-9374-44b2-ad59-4d8e5280739d" />

---

### 🔹 Q15. Top 5 Best-Selling Books
```sql
SELECT b.title, SUM(o.quantity) AS total_sold  
FROM orders o  
JOIN book b ON b.book_id = o.book_id  
GROUP BY b.title  
ORDER BY total_sold DESC  
LIMIT 5;
```
**Output:** 

<img width="474" height="145" alt="image" src="https://github.com/user-attachments/assets/d3ffdbef-b1e1-4dc4-9ba6-2e8a37b88711" />


---

### 🔹 Q16. Total Orders per Customer
```sql
SELECT customer_id, COUNT(order_id) AS total_orders  
FROM orders  
GROUP BY customer_id;
```
**Output:** 
<img width="181" height="265" alt="image" src="https://github.com/user-attachments/assets/c42ae423-c28f-41c3-9c89-114e087956d4" />


---

### 🔹 Q17. Revenue by Genre
```sql
SELECT b.genre, SUM(o.total_amount) AS revenue  
FROM orders o  
JOIN book b ON b.book_id = o.book_id  
GROUP BY b.genre;
```
**Output:** 
<img width="161" height="193" alt="image" src="https://github.com/user-attachments/assets/2c944553-7570-4c3c-b08f-58fcb7b37080" />

---


### 🔹 Q18. Most Popular Author
```sql
SELECT b.author, SUM(o.quantity) AS books_sold  
FROM orders o  
JOIN book b ON b.book_id = o.book_id  
GROUP BY b.author  
ORDER BY books_sold DESC  
LIMIT 1;
```
**Output:** 
<img width="229" height="49" alt="image" src="https://github.com/user-attachments/assets/e66a553c-f871-4c3f-8251-c8e7f7577a59" />


---

### 🔹 Q19. Monthly Sales Analysis
```sql
SELECT MONTH(order_date) AS month, SUM(total_amount) AS revenue  
FROM orders  
GROUP BY month  
ORDER BY month;
```
**Output:**
<img width="161" height="313" alt="image" src="https://github.com/user-attachments/assets/653d8b68-7889-4958-bc14-8c20be483988" />


---

### 🔹 Q20. Customers Who Spent the Most
```sql
SELECT c.name, SUM(o.total_amount) AS total_spent  
FROM orders o  
JOIN customers c ON c.customer_id = o.customer_id  
GROUP BY c.name  
ORDER BY total_spent DESC  
LIMIT 5;
```
**Output:** 
<img width="247" height="145" alt="image" src="https://github.com/user-attachments/assets/1db5794f-aceb-4e61-8e10-96a5b60dc0ed" />



---


