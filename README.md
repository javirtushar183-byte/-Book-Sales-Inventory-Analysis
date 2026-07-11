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

---

### 🔹 Q15. Top 5 Most Ordered Books

**Business Request:**  
Find best-selling books.

```sql
SELECT b.book_id, b.title, COUNT(o.order_id) AS order_count  
FROM orders o  
JOIN book b ON o.book_id = b.book_id  
GROUP BY b.book_id, b.title  
ORDER BY order_count DESC  
LIMIT 5;
```

**Output:** 
<img width="562" height="145" alt="image" src="https://github.com/user-attachments/assets/50dcc38b-b4c3-40af-8251-683ec3cefab1" />


---

### 🔹 Q16. Top 10 Expensive Fantasy Books

**Business Request:**  
Analyze premium Fantasy books.

```sql
SELECT * FROM book  
WHERE genre = 'Fantasy'  
ORDER BY price DESC  
LIMIT 10;
```

**Output:** 
<img width="561" height="265" alt="image" src="https://github.com/user-attachments/assets/453399fc-88dc-4066-a32e-9dd5d476d2d5" />

---

### 🔹 Q17. Sales by Author

**Business Request:**  
Evaluate author performance.

```sql
SELECT b.author, SUM(o.quantity) AS total_quantity  
FROM orders o  
JOIN book b ON o.book_id = b.book_id  
GROUP BY b.author  
ORDER BY total_quantity DESC;
```

**Output:**
<img width="250" height="289" alt="image" src="https://github.com/user-attachments/assets/638b4365-3352-4ac0-81bb-0806ce3768ab" />


---

### 🔹 Q18. High Spending Cities

**Business Request:**  
Identify cities with total spending above 300.

```sql
SELECT c.city, SUM(o.total_amount) AS total_spend
FROM customers c  
JOIN orders o ON c.customer_id = o.customer_id  
GROUP BY c.city  
HAVING SUM(o.total_amount) > 300;
```

**Output:** 
<img width="246" height="265" alt="image" src="https://github.com/user-attachments/assets/08f984ff-09d9-430f-be50-6cf5ae0da65c" />


---

### 🔹 Q19. Top Spending Customers

**Business Request:**  
Identify highest spending customers.

```sql
SELECT c.name, o.customer_id, SUM(o.total_amount) AS total_spend  
FROM orders o  
JOIN customers c ON o.customer_id = c.customer_id  
GROUP BY o.customer_id, c.name  
ORDER BY total_spend DESC  
LIMIT 10;
```

**Output:** 
<img width="330" height="265" alt="image" src="https://github.com/user-attachments/assets/1ad9d253-a4ad-4845-b39a-cc8f5129170e" />


---

### 🔹 Q20. Remaining Stock

**Business Request:**  
Calculate remaining inventory after sales.

```sql
SELECT b.book_id, b.title,  
COALESCE(SUM(o.quantity),0) AS order_quantity,  
b.stock - COALESCE(SUM(o.quantity),0) AS remaining_stock  
FROM book b  
LEFT JOIN orders o ON b.book_id = o.book_id  
GROUP BY b.book_id, b.title, b.stock;
```

**Output:**
<img width="774" height="289" alt="image" src="https://github.com/user-attachments/assets/749566ce-20d2-4fa2-b85e-d318c4b5f47d" />


---
## 📊 Book Sales & Inventory Analysis

![Book Performance Dashboard](https://github.com/user-attachments/assets/9546f703-e487-497d-8c11-8755067f8efe)

---
