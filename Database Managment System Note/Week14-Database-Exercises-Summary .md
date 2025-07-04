# Week14-Database-Exercises-Summary

# Week14-Database-Exercises-Summary

# 📘 Summary: Week 14 - Database Exercises-EN

This document contains SQL exercises designed to reinforce database concepts before the final exam. The main topics are:

- SELECT, INSERT, DELETE, UPDATE queries
- Creating and modifying tables
- VIEW, Stored Procedure, Trigger, User-Defined Function definitions
- Normalization (Normal Form transformations)

Each section includes practical questions, SQL command writing, and statements aimed at reinforcing theoretical knowledge.

## 📄 Detailed Content

### 🟦 Select Queries

- Write a query that lists restaurant names, product names, and prices.
- ( Restoran isimlerini, ürün isimlerini ve fiyatlarını listeleyen bir sorgu yazınız.)

```sql
SELECT r.name, p.name ,  pr.price
FROM Restaurants r , Product p , Product_Restaurant pr
WHERE p.productID = pr.productID 
	AND  r.restID = pr.restID

```

- Write a query that lists the number of products for each restaurant.
- ( Her restoran için ürün sayısını listeleyen bir sorgu yazınız.)

```sql
SELECT r.name, COUNT(*) AS pC
FROM Restaurants r ,Product_Restaurant pr
WHERE r.restID = pr.restID 
GROUP BY r.name
ORDER BY pC DESC

```

- Write a query that lists the names of restaurants that offer “adana” cuisine.
- (“Adana” mutfağı sunan restoranların isimlerini listeleyen bir sorgu yazınız.)

```sql
SELECT R.name, P.cuisine ,P.name
FROM Restaurants R, Product P, Product_Restaurant PR
WHERE P.productID = Pr.productID 
  AND PR.restID = R.restID 
  AND P.cuisine = 'adana';

```

### 🟩 Insert Queries

Add a new product:
- productID = 20
- name = hamburger
- cuisine = american

```sql
INSERT INTO Product (productID, name, cuisine)
VALUES (20, 'hamburger', 'american');
```

### 🟥 Delete Queries

Delete the product with productID = 20: 

```sql
-- First delete from Product_Restaurant (child table)
DELETE FROM Product_Restaurant
WHERE productID = 20;
-- Then delete from Product (parent table)
DELETE FROM Product
WHERE productID = 20;
```

### 🟨 Update Queries

Update the name of the product with productID = 6 to “Chicken Fajita”:

 (productID = 6 olan ürünün adını “Chicken Fajita” olarak güncelleyiniz:)

```sql
UPDATE Product
SET name = 'Chicken Fajita'
WHERE productID = 6;
```

Increase the price of all products in the restaurant named “kebapçı Ali” by 20%: 

(“Kebapçı Ali” adlı restorandaki tüm ürünlerin fiyatını %20 artırınız:)

```sql

UPDATE Product_Restaurant
SET price = price*1.20
from Restaurants
where Restaurants.name =  'kebabçı Ali'
```

### 📑 Table Queries

Create a Customer table:

```sql
CREATE TABLE Customers (
  custID int NULL,
  name nvarchar(50) NULL,
  phone nchar(15) NULL,
  email nvarchar(50) NULL,
  username nchar(10) NULL);
```

Add and remove columns:

```sql
ALTER TABLE Customers ADD department int;
ALTER TABLE Customers DROP COLUMN department;
```

### 🔍 Views

Which of the following statements will create a view named v_EmployeeNames? 

(Aşağıdaki ifadelerden hangisi v_EmployeeNames adında bir görünüm (view) oluşturacaktır?)

✅ A) CREATE VIEW v_EmployeeNames AS SELECT * FROM Employee WHERE Age > 30;
❌B) CREATE TABLE v_EmployeeNames AS SELECT Name FROM
Employee;
❌C) SELECT INTO v_EmployeeNames FROM Employee;
❌D) ALTER VIEW v_EmployeeNames SELECT Name FROM
Employee;

Which of the following best describes a view in SQL Server? 

(SQL Server’da bir görünüm (view) en iyi aşağıdakilerden hangisiyle tanımlanır?)

❌A) A temporary table that stores data permanently
❌B) A stored procedure that modifies data
✅C) A virtual table based on a SELECT query
❌D) A physical copy of another table

If this is the creation script of COURSEDETAIL_V view. Write Sql script that list the Courses if the number of students are greater than or equal to 15. 

( Bu COURSEDETAIL_V görünümünün oluşturma betiğiyse, öğrenci sayısı 15 veya daha fazla olan dersleri listeleyen SQL sorgusunu yazınız.)

—> Write a query to list courses with a student count ≥ 15:

```sql
CREATE VIEW COURSEDETAIL_V AS
SELECT    
		t.cCode AS 'Course Code',
    c.cName AS 'Course Name',
    COUNT(*) AS 'Enrollment Count',
    AVG(t.grade4) AS 'Average Grade'FROM
    dbo.TRANSCRIPT t
        dbo.COURSE c
WHERE    t.cCode = c.cCode
GROUP BY
    t.cCode,
    c.cName
GO
```

```sql
CREATE VIEW COURSEDETAIL_V AS
SELECT    
		dbo.TRANSCRIPT.cCode,
    dbo.COURSE.cName,
    COUNT(*) AS CNT,
    AVG(dbo.TRANSCRIPT.grade4) AS AVERAGE
FROM
    dbo.TRANSCRIPT
INNER JOIN    dbo.COURSE
    ON dbo.TRANSCRIPT.cCode = dbo.COURSE.cCode
GROUP BY
    dbo.TRANSCRIPT.cCode,
    dbo.COURSE.cName
GO
```

### ⚙️ Stored Procedures

What is a stored procedure in SQL?
❌A) A table storing previously run queries
✅B) A compiled program that resides in the server and performs specific tasks
❌C) A view that updates data automatically
❌D) A trigger activated by a query

Write the code to execute the following stored procedure from the .sql query window (TÜRKÇESİ: .sql sorgu penceresinden aşağıdaki saklı yordamı çalıştırmak için kodu yazınız.)

```sql
CREATE PROCEDURE GetAllCustomers
ASBEGINSELECT * FROM Customers;
END;
```

To execute the **GetAllCustomers** stored procedure in SQL Server, run the following command: (TÜRKÇESİ: SQL Server’da **GetAllCustomers** saklı yordamını çalıştırmak için aşağıdaki komutu çalıştırın:)

```sql
EXEC GetAllCustomers;
```

True/False:
- ❌ Procedures never return values. (False - they can return values using OUTPUT parameters)
- ✅ They can have input parameters. (True)
- ✅ CRUD operations can be performed. (True)
- ❌ Loops cannot be written. (False - loops can be written in stored procedures)

### 🔄 Triggers

What is the purpose of a trigger in SQL Server? (TÜRKÇESİ: SQL Server’da bir trigger (tetikleyici) amacı nedir?)
❌A) To prevent stored procedures from executing
✅B) To automatically execute code in response to an event such as INSERT, UPDATE, or DELETE
❌C) To display error messages only
❌D) To create backup copies of tables

How do you execute the following trigger: (TÜRKÇESİ: Aşağıdaki trigger’ı nasıl çalıştırırsınız:)

```sql
CREATE TRIGGER trg_AfterInsert
ON Orders
AFTER INSERTASBEGIN
PRINT 'New order added';
END;
```

To execute this trigger, simply insert a new record into the Orders table. For example: (TÜRKÇESİ: Bu trigger’ı çalıştırmak için, Orders tablosuna yeni bir kayıt ekleyin. Örneğin:)

```sql
INSERT INTO Orders (orderID, custID, restID, deliveryTime, paymentTotal, paymentMethod, time)
VALUES (1001, 501, 201, '30 minutes', 75, 'Credit Card', GETDATE());
```

True/False:
- ❌ Triggers return output. (False - triggers don’t return values directly)
- ❌ They are called with SELECT. (False - triggers are activated by database events)
- ✅ They can contain CRUD operations. (True)

If we try to remove the department with deptCode “xx”, what will be the content of deleted tuple when the department_Delete trigger runs?

 (TÜRKÇESİ: deptCode “xx” olan departmanı silmeye çalışırsak, department_Delete trigger’ı çalıştığında silinen tuple’ın içeriği ne olacaktır?)

```sql
CREATE TRIGGER [dbo].[Department_Delete] ON [dbo].[DEPARTMENT]
INSTEAD OF DELETE
AS
BEGIN
    UPDATE dep
    SET dep.statusOfDept = 0
    FROM DEPARTMENT dep, deleted d
    WHERE dep.deptCode = d.deptCode ;
END
```

ANSWER:
The `deleted` table holds the complete row data of the record that was targeted for deletion. Since this is an `INSTEAD OF DELETE` trigger, the actual deletion doesn’t occur - instead, the department’s `statusOfDept` is set to 0, performing a soft delete while preserving the original data.
(TÜRKÇESİ: `deleted` tablosu, silme işlemi hedeflenen kaydın tüm satır verilerini içerir. Bu bir `INSTEAD OF DELETE` trigger olduğundan, gerçek silme işlemi gerçekleşmez - bunun yerine, departmanın `statusOfDept` değeri 0 olarak ayarlanır, böylece orijinal veri korunurken bir yumuşak silme işlemi gerçekleştirilir.)

### 🧮 User Defined Functions

What is a scalar-valued function in SQL Server? (TÜRKÇESİ: SQL Server’da skaler değerli fonksiyon nedir?)
❌A) A function that returns a table
❌B) A function that modifies data in a table
✅C) A function that returns a single value
❌D) A function that deletes records

What is the duty of this function? (TÜRKÇESİ: Bu fonksiyonun görevi nedir?)

```sql
CREATE FUNCTION Square(@x INT)
RETURNS INTASBEGIN  RETURN @x * @x;
END;
```

ANSWER:

The duty of this function is to **calculate and return the square of an integer number**.
(TÜRKÇESİ: Bu fonksiyonun görevi, bir tamsayının karesini hesaplamak ve döndürmektir.)

The function:

- Takes one input parameter `@x` of type INT
- Multiplies the input value by itself (`@x * @x`)
- Returns the result as an INT

For example: If you call `Square(5)`, it will return `25`.

Create a scalar-valued function dbo.GetFullName that takes FirstName and LastName as inputs and returns the full name in the format “LastName, FirstName” (TÜRKÇESİ: FirstName ve LastName girdilerini alan ve tam adı “LastName, FirstName” formatında döndüren bir dbo.GetFullName skaler değerli fonksiyonu oluşturunuz.)

ANSWER:

GetFullName function:

```sql
CREATE FUNCTION dbo.GetFullName(@FirstName NVARCHAR(50), @LastName NVARCHAR(50))
RETURNS NVARCHAR(100)
AS BEGIN  RETURN @LastName + ', ' + @FirstName;
END;
```

Create a function dbo.CalculateDiscount that
accepts a customer’s total purchase amount and
returns the applicable discount percentage:
If total ≥ 1000 → 10%
If total ≥ 500 → 5%
Otherwise → 0%
(TÜRKÇESİ: Müşterinin toplam satın alma tutarını kabul eden ve uygulanabilir indirim yüzdesini döndüren bir dbo.CalculateDiscount fonksiyonu oluşturun:
Toplam ≥ 1000 → %10
Toplam ≥ 500 → %5
Aksi takdirde → %0)

ANSWER:
CalculateDiscount function:

```sql
CREATE FUNCTION dbo.CalculateDiscount(@TotalAmount FLOAT)
RETURNS FLOATASBEGIN  IF @TotalAmount >= 1000 RETURN 10;
  ELSE IF @TotalAmount >= 500 RETURN 5;
  ELSE RETURN 0;
END;
```

### 🧩 Normalization

Given functional dependencies:
- employeeId → employeeName, managerId
- managerId → managerName, managerAddress
- departmentid → departmentName

Tasks: (TÜRKÇESİ: Görevler:)
- This relationship is not in 1NF because it may contain multiple values. 

(TÜRKÇESİ: Bu ilişki, birden fazla değer içerebileceği için 1NF’de değildir.)
- It needs to be transformed into second and third normal form. 

(TÜRKÇESİ: İkinci ve üçüncü normal forma dönüştürülmesi gerekiyor.)

### 1NF Solution

First, ensure all values are atomic (no multi-valued attributes): (TÜRKÇESİ: Öncelikle, tüm değerlerin atomik olduğundan emin olun (çok değerli öznitelikler olmamalı):)

**Employee Table (1NF)**

| employeeId | employeeName | managerId | departmentId | managerName | managerAddress | departmentName |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | John Smith | 101 | 201 | Mary Jones | 123 Main St | HR |
| 2 | Jane Doe | 102 | 202 | Bob Brown | 456 Oak Rd | IT |

### 2NF Solution

Remove partial dependencies (non-key attributes depending on part of the key): (TÜRKÇESİ: Kısmi bağımlılıkları kaldırın (anahtar olmayan özniteliklerin anahtarın bir kısmına bağlı olması):)

**Employee Table (2NF)**

| employeeId | employeeName | managerId | departmentId |
| --- | --- | --- | --- |
| 1 | John Smith | 101 | 201 |
| 2 | Jane Doe | 102 | 202 |

**Manager Table (2NF)**

| managerId | managerName | managerAddress |
| --- | --- | --- |
| 101 | Mary Jones | 123 Main St |
| 102 | Bob Brown | 456 Oak Rd |

**Department Table (2NF)**

| departmentId | departmentName |
| --- | --- |
| 201 | HR |
| 202 | IT |

### 3NF Solution

Remove transitive dependencies (non-key attributes depending on other non-key attributes): (TÜRKÇESİ: Geçişli bağımlılıkları kaldırın (anahtar olmayan özniteliklerin diğer anahtar olmayan özniteliklere bağlı olması):)

The tables are already in 3NF since there are no transitive dependencies after the 2NF transformation.

 (TÜRKÇESİ: Tablolar zaten 2NF dönüşümünden sonra geçişli bağımlılıklar olmadığı için 3NF’dedir.)