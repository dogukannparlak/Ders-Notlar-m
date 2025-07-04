# SQL-Detayli-Ders-Notu

# 📚 SQL Veritabanı Dersi - Kapsamlı Özet

Bu belge, SQL ve veritabanı konularını detaylı olarak ele alan, sınava hazırlık amaçlı bir kaynaktır. Teorik bilgiler, örnekler ve alıştırma soruları içermektedir.

## 📋 İçindekiler

1. [Temel SQL Sorguları](about:blank#temel-sql-sorgular%C4%B1)
    - [SELECT Sorguları](about:blank#select-sorgular%C4%B1)
    - [INSERT Sorguları](about:blank#insert-sorgular%C4%B1)
    - [DELETE Sorguları](about:blank#delete-sorgular%C4%B1)
    - [UPDATE Sorguları](about:blank#update-sorgular%C4%B1)
    - JOIN İşlemleri (INNER, LEFT, RIGHT, FULL JOIN)
    - GROUP BY
    - HAVING
    - ORDER BY
    - DISTINCT
    - LIMIT
    - TOP
2. [Tablo Oluşturma ve Değiştirme](about:blank#tablo-olu%C5%9Fturma-ve-de%C4%9Fi%C5%9Ftirme)
    - [CREATE TABLE](about:blank#create-table)
    - [ALTER TABLE](about:blank#alter-table)
    - [DROP TABLE](about:blank#drop-table)
    - [CONSTRAINTS](about:blank#constraints)
3. [VIEW, Stored Procedure, Trigger ve User-Defined Functions](about:blank#view-stored-procedure-trigger-ve-user-defined-functions)
    - [VIEW](about:blank#view)
    - [Stored Procedure](about:blank#stored-procedure)
    - [Trigger](about:blank#trigger)
    - [User-Defined Functions](about:blank#user-defined-functions)
4. [Normalizasyon](about:blank#normalizasyon)
    - [Birinci Normal Form (1NF)](about:blank#birinci-normal-form-1nf)
    - [İkinci Normal Form (2NF)](about:blank#ikinci-normal-form-2nf)
    - [Üçüncü Normal Form (3NF)](about:blank#%C3%BC%C3%A7%C3%BCnc%C3%BC-normal-form-3nf)
    - [Boyce-Codd Normal Form (BCNF)](about:blank#boyce-codd-normal-form-bcnf)

## Temel SQL Sorguları

### SELECT Sorguları

SELECT sorguları, veritabanından veri çekmek için kullanılır. Veritabanının “Read” (Okuma) işlemidir.

### Sözdizimi

```sql
SELECT sütun1, sütun2, ...
FROM tablo_adı
WHERE koşul
GROUP BY sütun
HAVING grup_koşulu
ORDER BY sütun ASC/DESCLIMIT sayı;
```

### Temel SELECT Örnekleri

```sql
-- Tüm sütunları seçme
SELECT * FROM Customers;
-- Belirli sütunları seçme
SELECT customerName, contactName, country FROM Customers;
-- WHERE ile filtreleme
SELECT * FROM Products WHERE price > 50;
-- Sıralama
SELECT * FROM Products ORDER BY price DESC;
-- DISTINCT ile tekrarsız değerler
SELECT DISTINCT country FROM Customers;
```

### İleri Düzey SELECT Örnekleri

```sql
-- Aggregate fonksiyonlarSELECT COUNT(*) FROM Orders;
SELECT AVG(price) FROM Products;
SELECT MAX(price) AS en_yüksek_fiyat FROM Products;
-- GROUP BY ile gruplamaSELECT country, COUNT(*) as müşteri_sayısı
FROM Customers
GROUP BY country
ORDER BY müşteri_sayısı DESC;
-- HAVING ile grup filtrelemeSELECT country, COUNT(*) as müşteri_sayısı
FROM Customers
GROUP BY country
HAVING COUNT(*) > 5ORDER BY müşteri_sayısı DESC;
-- JOIN işlemleriSELECT o.orderID, c.customerName, o.orderDate
FROM Orders o
INNER JOIN Customers c ON o.customerID = c.customerID;
-- Alt sorgularSELECT productName
FROM Products
WHERE categoryID IN (SELECT categoryID FROM Categories WHERE categoryName = 'Beverages');
```

### INSERT Sorguları

INSERT sorguları, veritabanına yeni kayıt eklemek için kullanılır. Veritabanının “Create” (Oluşturma) işlemidir.

### Sözdizimi

```sql
INSERT INTO tablo_adı (sütun1, sütun2, ...)
VALUES (değer1, değer2, ...);
```

### INSERT Örnekleri

```sql
-- Temel ekleme
INSERT INTO Customers (customerID, customerName, contactName, country)
VALUES (1, 'ABC Ltd.', 'John Doe', 'USA');
-- Birden fazla kayıt ekleme
INSERT INTO Products (productID, productName, price, categoryID)
VALUES
    (1, 'Chai', 18, 1),
    (2, 'Chang', 19, 1),
    (3, 'Aniseed Syrup', 10, 2);
-- SELECT sonucunu ekleme
INSERT INTO CustomerArchive (customerID, customerName, country)
SELECT customerID, customerName, country
FROM Customers
WHERE active = 0;
```

### DELETE Sorguları

### DELETE Örnekleri

DELETE sorguları, veritabanından kayıt silmek için kullanılır. Veritabanının “Delete” (Silme) işlemidir.

```sql
-- Tek bir kaydı silme
DELETE FROM Customers WHERE customerID = 1;
-- Birden fazla kaydı silme
DELETE FROM Products WHERE categoryID = 3;
-- Tüm tabloyu silme (DİKKAT!)
DELETE FROM OrderDetails;
-- Alt sorgu ile silme,
DELETE FROM Products
WHERE supplierID IN (SELECT supplierID FROM Suppliers WHERE country = 'Japan');
```

### Sözdizimi

```sql
DELETE FROM tablo_adı
WHERE koşul;
```

**Soft Delete (Yumuşak Silme) Nedir?**

Soft delete, bir kaydı veritabanından tamamen silmek yerine, genellikle bir "silindi" veya "aktif" gibi bir durum sütunu kullanarak kaydın silinmiş olarak işaretlenmesidir. Böylece veri kaybolmaz, sadece uygulama tarafından gizlenir veya kullanılmaz.

### **Soft Delete İçin Tipik Yaklaşım**

1. Tabloya bir durum sütunu eklenir (ör. `isDeleted`, `active`, `deleted_at`).
2. Silme işlemi, bu sütunun değerini güncelleyerek yapılır.
3. Gerçekten silmek için ise klasik `DELETE` sorgusu kullanılır.

**Soft Delete Örneği**

Tabloya sütun ekleme:

```sql
ALTER TABLE Customers ADD isDeleted BOOLEAN DEFAULT 0;

```

Soft delete işlemi:

```sql
-- Kaydı silmek yerine isDeleted alanını 1 yapıyoruz
UPDATE Customers SET isDeleted = 1 WHERE customerID = 1;

```

Silinmemiş kayıtları listeleme:

```sql
SELECT * FROM Customers WHERE isDeleted = 0;

```

### **Soft Delete Avantajları**

- Silinen veriler kurtarılabilir.
- Veri geçmişi ve loglama için uygundur.
- Yanlışlıkla silinen kayıtlar geri alınabilir.

### **Soft Delete ve Hard Delete Karşılaştırması**

| Özellik | Hard Delete (DELETE) | Soft Delete (UPDATE ile işaretleme) |
| --- | --- | --- |
| Veri kaybı | Kalıcı olarak silinir | Veri kaybolmaz, işaretlenir |
| Kurtarma | Geri alınamaz | Kolayca geri alınabilir |
| Performans | Daha hızlı | Biraz daha yavaş olabilir |
| Kullanım Alanı | Geçici/önemsiz veriler | Kritik/tarihi veriler |

### UPDATE Sorguları

UPDATE sorguları, veritabanındaki mevcut kayıtları güncellemek için kullanılır. Veritabanının “Update” (Güncelleme) işlemidir.

### Sözdizimi

```sql
UPDATE tablo_adı
SET sütun1 = değer1, sütun2 = değer2, ...
WHERE koşul;
```

### UPDATE Örnekleri

```sql
-- Tek bir kaydı güncelleme
UPDATE Customers
SET contactName = 'Alfred Schmidt', city = 'Frankfurt'WHERE customerID = 1;
-- Birden fazla kaydı güncelleme
UPDATE Products
SET price = price * 1.10WHERE categoryID = 1;
-- Alt sorgu ile güncelleme
UPDATE Products
SET stock = stock + 10WHERE productID IN 
(SELECT productID FROM OrderDetails WHERE quantity > 20);
```

## **JOIN İşlemleri**

JOIN işlemleri, birden fazla tablodan veri çekerek birleştirmek için kullanılır. İlişkisel veritabanlarının temel özelliklerinden biridir.

### **JOIN Türleri**

### **1. INNER JOIN**

İki tablodaki eşleşen kayıtları getirir. Sadece her iki tabloda da bulunan veriler gösterilir.

```sql
-- SözdizimiSELECT sütunlar
FROM tablo1
INNER JOIN tablo2 ON tablo1.anahtar = tablo2.anahtar;

-- Örnek: Müşteri siparişlerini getirme 
SELECT c.customerName, o.orderID, o.orderDate
FROM Customers c
INNER JOIN Orders o ON c.customerID = o.customerID;

```

### **2. LEFT JOIN (LEFT OUTER JOIN)**

Sol tablodaki tüm kayıtları ve sağ tablodaki eşleşen kayıtları getirir. Eşleşmeyen kayıtlar için NULL değer döner.

```sql
-- SözdizimiSELECT sütunlar
FROM tablo1
LEFT JOIN tablo2 ON tablo1.anahtar = tablo2.anahtar;

-- Örnek: Tüm müşterileri ve varsa siparişlerini getirme 
SELECT c.customerName, o.orderID, o.orderDate
FROM Customers c
LEFT JOIN Orders o ON c.customerID = o.customerID;

```

### **3. RIGHT JOIN (RIGHT OUTER JOIN)**

Sağ tablodaki tüm kayıtları ve sol tablodaki eşleşen kayıtları getirir.

```sql
-- SözdizimiSELECT sütunlar
FROM tablo1
RIGHT JOIN tablo2 ON tablo1.anahtar = tablo2.anahtar;

-- Örnek: Tüm siparişleri ve müşteri bilgilerini getirmeSELECT c.customerName, o.orderID, o.orderDate
FROM Customers c
RIGHT JOIN Orders o ON c.customerID = o.customerID;

```

### **4. FULL JOIN (FULL OUTER JOIN)**

Her iki tablodaki tüm kayıtları getirir. Eşleşmeyen kayıtlar için NULL değer döner.

```sql
-- SözdizimiSELECT sütunlar
FROM tablo1
FULL JOIN tablo2 ON tablo1.anahtar = tablo2.anahtar;

-- Örnek: Tüm müşteri ve sipariş verilerini getirme 
SELECT c.customerName, o.orderID, o.orderDate
FROM Customers c
FULL JOIN Orders o ON c.customerID = o.customerID;

```

### **Çoklu JOIN İşlemleri**

```sql
-- Üç tablo birleştirme 
SELECT c.customerName, o.orderID, p.productName, od.quantity
FROM Customers c
INNER JOIN Orders o ON c.customerID = o.customerID
INNER JOIN OrderDetails od ON o.orderID = od.orderID
INNER JOIN Products p ON od.productID = p.productID;

```

## **GROUP BY ve HAVING**

### **GROUP BY**

Verilen sütun(lar)a göre kayıtları gruplar ve toplama fonksiyonları (COUNT, SUM, AVG, MAX, MIN) ile birlikte kullanılır.

```sql
-- Sözdizimi 
SELECT sütun, TOPLAMA_FONKSIYONU(sütun)
FROM tablo
GROUP BY sütun;

-- Örnekler-- Ülkeye göre müşteri sayısı 
SELECT country, COUNT(*) as müşteri_sayısı
FROM Customers
GROUP BY country;

-- Kategoriye göre ürün sayısı ve ortalama fiyat 
SELECT categoryID, COUNT(*) as ürün_sayısı, AVG(price) as ortalama_fiyat
FROM Products
GROUP BY categoryID;

-- Çoklu gruplama 
SELECT country, city, COUNT(*) as müşteri_sayısı
FROM Customers
GROUP BY country, city
ORDER BY country, city;

```

### **HAVING**

GROUP BY ile oluşturulan gruplara koşul uygulamak için kullanılır. WHERE gruplanmadan önce, HAVING gruplandıktan sonra filtreleme yapar.

```sql
-- Sözdizimi
SELECT sütun, TOPLAMA_FONKSIYONU(sütun)
FROM tablo
GROUP BY sütun
HAVING koşul;

-- Örnekler-- 5'ten fazla müşterisi olan ülkeler
SELECT country, COUNT(*) as müşteri_sayısı
FROM Customers
GROUP BY country
HAVING COUNT(*) > 5;

-- Ortalama fiyatı 20'den yüksek olan kategoriler
SELECT categoryID, AVG(price) as ortalama_fiyat
FROM Products
GROUP BY categoryID
HAVING AVG(price) > 20;

-- WHERE ve HAVING birlikte kullanımı
SELECT country, COUNT(*) as aktif_müşteri_sayısı
FROM Customers
WHERE active = 1-- Gruplamadan önce filtreleme
GROUP BY country
HAVING COUNT(*) >= 3;-- Gruplamadan sonra filtreleme
```

## **ORDER BY**

Sonuçları belirli sütun(lar)a göre sıralar.

```sql
-- Sözdizimi
SELECT sütunlar
FROM tablo
ORDER BY sütun1 [ASC|DESC], sütun2 [ASC|DESC];

-- Örnekler-- Artan sıralama (varsayılan)
SELECT * FROM Products ORDER BY price;

-- Azalan sıralama
SELECT * FROM Products ORDER BY price DESC;

-- Çoklu sıralama
SELECT customerName, country, city
FROM Customers
ORDER BY country ASC, city ASC;

-- Sıra numarasına göre sıralama
SELECT customerName, country
FROM Customers
ORDER BY 2, 1; -- 2. sütun (country), sonra 1. sütun (customerName)
```

## **DISTINCT**

Tekrarlı kayıtları çıkararak benzersiz değerleri getirir.

```sql
-- Sözdizimi
SELECT DISTINCT sütun1, sütun2
FROM tablo;

-- Örnekler-- Benzersiz ülkeler
SELECT DISTINCT country FROM Customers;

-- Benzersiz ülke-şehir kombinasyonları
SELECT DISTINCT country, city FROM Customers;

-- DISTINCT ile COUNT
SELECT COUNT(DISTINCT country) as benzersiz_ülke_sayısı
FROM Customers;

```

## **LIMIT / TOP**

Sonuç kümesinin belirli sayıda kayıtla sınırlanması için kullanılır.

### **LIMIT (MySQL, PostgreSQL, SQLite)**

```sql
-- Sözdizimi
SELECT sütunlar
FROM tablo
LIMIT sayı;

-- Örnekler-- İlk 5 kaydı getir
SELECT * FROM Products LIMIT 5;

-- En pahalı 10 ürünü getir
SELECT * FROM Products
ORDER BY price DESC
LIMIT 10;

-- OFFSET ile atlama (sayfalama)
SELECT * FROM Products
ORDER BY productID
LIMIT 10 OFFSET 20;-- 21-30. kayıtları getir
```

### **TOP (SQL Server)**

```sql
-- Sözdizimi
SELECT TOP sayı sütunlar
FROM tablo;

-- Örnekler-- İlk 5 kaydı getir
SELECT TOP 5 * FROM Products;

-- En pahalı 10 ürünü getir
SELECT TOP 10 * FROM Products
ORDER BY price DESC;

-- Yüzde ile sınırlama
SELECT TOP 25 PERCENT * FROM Products;

```

## **Kombine Kullanım Örneği**

```sql
-- Kapsamlı örnek: Her ülkeden en az 2 müşterisi olan ülkelerin-- müşteri sayısını ve ortalama sipariş tutarını bulma
SELECT
    c.country,
    COUNT(DISTINCT c.customerID) as müşteri_sayısı,
    COUNT(o.orderID) as toplam_sipariş,
    AVG(od.quantity * p.price) as ortalama_sipariş_tutarı
FROM Customers c
LEFT JOIN Orders o ON c.customerID = o.customerID
LEFT JOIN OrderDetails od ON o.orderID = od.orderID
LEFT JOIN Products p ON od.productID = p.productID
GROUP BY c.country
HAVING COUNT(DISTINCT c.customerID) >= 2
ORDER BY ortalama_sipariş_tutarı DESC
LIMIT 10;
```

## Tablo Oluşturma ve Değiştirme

### CREATE TABLE

CREATE TABLE, veritabanında yeni bir tablo oluşturmak için kullanılır.

### Sözdizimi

```sql
CREATE TABLE tablo_adı (
    sütun1 veri_tipi [kısıtlama],
    sütun2 veri_tipi [kısıtlama],
    ...
    [tablo_kısıtlaması]
);
```

### CREATE TABLE Örnekleri

```sql
-- Basit tablo oluşturma 
CREATE TABLE Customers (
    customerID INT,
    customerName VARCHAR(100),
    contactName VARCHAR(100),
    country VARCHAR(50)
);
-- Kısıtlamalar ile tablo oluşturma 
CREATE TABLE Products (
    productID INT PRIMARY KEY,
    productName VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) DEFAULT 0,
    categoryID INT,
    FOREIGN KEY (categoryID) REFERENCES Categories(categoryID)
);
--AUTO_INCREMENT ile tablo oluşturma 
CREATE TABLE Orders (
    orderID INT AUTO_INCREMENT PRIMARY KEY,
    customerID INT NOT NULL,
    orderDate DATE NOT NULL,
    FOREIGN KEY (customerID) REFERENCES Customers(customerID)
);
```

### ALTER TABLE

ALTER TABLE, mevcut bir tablonun yapısını değiştirmek için kullanılır.

### Sözdizimi

```sql
ALTER TABLE tablo_adı
ADD/DROP/MODIFY/ALTER COLUMN sütun_adı veri_tipi [kısıtlama];
```

### ALTER TABLE Örnekleri

```sql
-- Sütun ekleme
ALTER TABLE Customers
ADD email VARCHAR(100);
-- Sütun silme
ALTER TABLE Customers
DROP COLUMN email;
-- Sütun değiştirme
ALTER TABLE Products
MODIFY COLUMN price DECIMAL(12,2);
-- Varsayılan değer ekleme
ALTER TABLE Orders
ALTER COLUMN orderDate SET DEFAULT CURRENT_DATE();
-- Kısıtlama ekleme
ALTER TABLE Products
ADD CONSTRAINT FK_Products_Categories
FOREIGN KEY (categoryID) REFERENCES Categories(categoryID);
```

### DROP TABLE

DROP TABLE, veritabanından bir tabloyu tamamen silmek için kullanılır.

### Sözdizimi

```sql
DROP TABLE [IF EXISTS] tablo_adı;
```

### DROP TABLE Örnekleri

```sql
-- Tabloyu silme
DROP TABLE TempProducts;
-- Varsa sil
DROP TABLE IF EXISTS OldCustomers;
```

### CONSTRAINTS

Kısıtlamalar (Constraints), tablolardaki veri bütünlüğünü sağlamak için kullanılan kurallardır.

### Temel Kısıtlamalar

- **PRIMARY KEY**: Tabloyu benzersiz şekilde tanımlayan değerler
- **FOREIGN KEY**: Diğer tabloyla ilişki kuran değerler
- **UNIQUE**: Benzersiz değerler
- **NOT NULL**: Null olamaz
- **CHECK**: Şartı karşılayan değerler
- **DEFAULT**: Değer belirtilmezse kullanılacak varsayılan değer

### Kısıtlama Örnekleri

```sql
-- PRIMARY KEY
CREATE TABLE Students (
    studentID INT PRIMARY KEY,
    name VARCHAR(100),
    age INT);
-- FOREIGN KEY
CREATE TABLE Enrollments (
    enrollmentID INT PRIMARY KEY,
    studentID INT,
    courseID INT,
    FOREIGN KEY (studentID) REFERENCES Students(studentID),
    FOREIGN KEY (courseID) REFERENCES Courses(courseID)
);
-- UNIQUE
CREATE TABLE Users (
    userID INT PRIMARY KEY,
    username VARCHAR(50) UNIQUE,
    email VARCHAR(100) UNIQUE);
-- CHECK
CREATE TABLE Products (
    productID INT PRIMARY KEY,
    productName VARCHAR(100),
    price DECIMAL(10,2) CHECK (price > 0)
);
-- DEFAULT
CREATE TABLE Orders (
    orderID INT PRIMARY KEY,
    customerID INT,
    orderDate DATE DEFAULT CURRENT_DATE()
);
```

# VIEW, Stored Procedure, Trigger ve User-Defined Functions

# **👁️ SQL VIEW Kavramı ve Örnekler - Detaylı Açıklama**

> 💡 VIEW Nedir?
> 
> 
> Bir veya daha fazla tablodan türetilmiş **sanal bir tablo**dur. Fiziksel olarak veri saklamaz, sadece bir sorgu tanımıdır.
> 

## **✨ VIEW'in Temel Özellikleri**

- 🌐 **Sanal Tablo**: Fiziksel veri saklamaz
- 🔄 **Dinamik**: Her sorgulandığında güncel veriyi getirir
- 🔒 **Güvenlik**: Hassas sütunları gizleyebilir
- 🎯 **Basitleştirme**: Karmaşık sorguları tek bir isimle kullanılabilir hale getirir

---

## **📝 VIEW Sözdizimi**

```sql
CREATE [OR REPLACE] VIEW görünüm_adı AS SELECT-sorgusu;

```

**🔧 Temel Yapı:**

- `CREATE VIEW` → Yeni görünüm oluştur
- `OR REPLACE` → Varsa güncelle (opsiyonel)
- `AS` → Sorgu tanımının başlangıcı

---

## **🚀 Pratik Örnekler**

### **1️⃣ Zor Dersleri Bulma Sorgusu - Adım Adım Analiz**

> 🎯 Amaç: "Zor ders" tanımını yapmak - Düşük not alan öğrencilerin çoğunlukta olduğu dersleri bulmak
> 

### **📊 Zor Ders Kriteri:**

- **3.0 ve üstü** not alan öğrenci sayısı **<** **2.9 ve altı** not alan öğrenci sayısı

### **🔍 Sorgu Yapısı:**

```sql
SELECT
    COURSE.cCode,-- Ders kodu
    COURSE.cName,-- Ders adı
    tableHigh.num AS yuksek_not,-- 3.0+ not alan öğrenci sayısı
    tableLow.num AS dusuk_not-- 2.9- not alan öğrenci sayısı
```

### **📈 Alt Sorgular:**

**🔺 tableHigh (Yüksek Notlar):**

```sql
(SELECT
     cCode,
     COUNT(*) AS num,-- 3.0+ not alan öğrenci sayısı
     AVG(grade4) AS average
 FROM
     TRANSCRIPT
 WHERE
     grade4 >= 3.0-- Sadece 3.0 ve üstü notlar
     GROUP BY
     cCode-- Her ders için ayrı hesaplama
) AS tableHigh

```

**🔻 tableLow (Düşük Notlar):**

```sql
(SELECT
     cCode,
     COUNT(*) AS num,-- 2.9- not alan öğrenci sayısı
     AVG(grade4) AS average
 FROM
     TRANSCRIPT
 WHERE
     grade4 <= 2.9-- Sadece 2.9 ve altı notlar
     GROUP BY
     cCode-- Her ders için ayrı hesaplama
) AS tableLow

```

### **🔗 JOIN Koşulları:**

```sql
WHERE
    tableHigh.cCode = COURSE.cCode-- Ders bilgilerini al
    AND tableLow.cCode = COURSE.cCode-- Her iki alt sorguyu birleştir
    AND tableHigh.num < tableLow.num-- ZOR DERS ŞARTI
```

**📋 Çalışma Mantığı:**

| Adım | İşlem | Açıklama |
| --- | --- | --- |
| 1 | **tableHigh** hesapla | Her ders için 3.0+ not alan öğrenci sayısı |
| 2 | **tableLow** hesapla | Her ders için 2.9- not alan öğrenci sayısı |
| 3 | **JOIN** yap | Ders bilgileri ile birleştir |
| 4 | **Filtrele** | Düşük not > Yüksek not olan dersleri al |

---

### **2️⃣ Zor Dersler Görünümü Oluşturma**

> 🎯 Amaç: Yukarıdaki karmaşık sorguyu bir VIEW olarak kaydetmek
> 

```sql
CREATE VIEW HARDCOURSES_V AS
SELECT
    COURSE.cCode,
    COURSE.cName,
    tableHigh.num1 AS yuksek_not,-- Sütun adı düzeltildi
    tableLow.num2 AS dusuk_not,-- Sütun adı düzeltildiFROM
    COURSE,
    
    (SELECT cCode, COUNT(*) AS num1, AVG(grade4) AS average1
     FROM TRANSCRIPT
     WHERE grade4 >= 3.0
     GROUP BY cCode) 
     AS tableHigh,
     
    (SELECT cCode, COUNT(*) AS num2, AVG(grade4) AS average2
     FROM TRANSCRIPT
     WHERE grade4 <= 2.9
     GROUP BY cCode)
     AS tableLow
WHERE
    tableHigh.cCode = COURSE.cCode
    AND tableLow.cCode = COURSE.cCode
    AND tableHigh.num1 < tableLow.num2;

```

**🔧 Önemli Değişiklik:**

- `num` → `num1` ve `num2` olarak düzeltildi (tutarlılık için)

**💡 Kullanım:**

```sql
SELECT * FROM HARDCOURSES_V;

```

> ✅ Avantaj: Artık karmaşık sorgu yerine tek satırla sonuç alabilirsiniz!
> 

---

### **3️⃣ Özel Danışmanlarla Öğrenci Sorgusu - Adım Adım**

> 🎯 Amaç: Belirli kriterleri karşılayan öğrencileri bulmak
> 

### **📋 Kriterler:**

1. **Ankara'da yaşayan** öğrenciler
2. **6'dan fazla öğrencisi olan danışmana** sahip öğrenciler

### **🔍 Ana Sorgu:**

```sql
SELECT
    city AS sehir,
    fName AS ad,
    lName AS soyad,
    advisorID AS danisman_id
FROM
    STUDENT
WHERE
    city = 'Ankara'-- KRİTER 1: Ankara'da yaşayanlar
```

### **🔗 Alt Sorgu (IN ile):**

```sql
AND advisorID IN (
-- 6'dan fazla öğrencisi olan danışmanları bul
SELECT
        st.staffID
    FROM
        STAFF st,
        STUDENT s
    WHERE
        st.staffID = s.advisorID-- Danışman-öğrenci eşleştirmesi
        GROUP BY
        st.fName, st.lName, st.staffID-- Her danışman için grupla
        HAVING
        COUNT(*) > 6-- 6'dan fazla öğrencisi olanlar
)

```

**⚙️ Çalışma Mantığı:**

| Sıra | İşlem | Açıklama |
| --- | --- | --- |
| 1 | **Alt sorgu** çalışır | 6+ öğrencisi olan danışman ID'leri bulunur |
| 2 | **Ana sorgu** çalışır | Ankara'daki ve bu danışmanlara sahip öğrenciler listelenir |

**🔍 Alt Sorgu Detayı:**

- `STAFF` ve `STUDENT` tabloları birleştirilir
- Her danışman için öğrenci sayısı hesaplanır
- `HAVING COUNT(*) > 6` ile filtreleme yapılır
- Sonuç olarak danışman ID'leri döndürülür

---

### **4️⃣ Öğrenci Detayları Görünümü**

> 🎯 Amaç: Yukarıdaki sorguyu VIEW olarak kaydetmek
> 

```sql
CREATE VIEW STUDENTDETAIL_V AS
SELECT
    city AS sehir,
    fName AS ad,
    lName AS soyad,
    advisorID AS danisman_id
FROM
    STUDENT
WHERE
    city = 'Ankara'
    AND advisorID IN (
        SELECT
            st.staffID
        FROM
            STAFF st,
            STUDENT s
        WHERE
            st.staffID = s.advisorID
        GROUP BY
            st.fName, st.lName, st.staffID
        HAVING
            COUNT(*) > 6
    );

```

**💡 Kullanım:**

```sql
SELECT * FROM STUDENTDETAIL_V;

```

---

## **🎯 VIEW'in Avantajları**

### **🎨 1. Basitleştirme**

- ✅ Karmaşık JOIN'li sorguları tek isimle kullanma
- ✅ Tekrar kullanılabilir sorgu şablonları
- ✅ Kod tekrarını önleme

### **🔒 2. Güvenlik**

- ✅ Hassas sütunları gizleme
- ✅ Belirli satırlara erişimi kısıtlama
- ✅ Kullanıcı bazlı veri filtreleme

### **📊 3. Tutarlılık**

- ✅ Aynı sorgu mantığının her yerde kullanılması
- ✅ Merkezi veri erişim kuralları
- ✅ Standart raporlama

### **⚡ 4. Performans**

- ✅ Sık kullanılan sorguların optimize edilmesi
- ✅ Karmaşık hesaplamaların önceden tanımlanması

---

## **💡 Pratik VIEW Örnekleri**

### **🎓 Basit VIEW:**

```sql
CREATE VIEW ACTIVE_STUDENTS AS
SELECT studentID, fName, lName, city
FROM STUDENT
WHERE status = 'Active';

```

### **🧮 Hesaplamalı VIEW:**

```sql
CREATE VIEW STUDENT_GPA AS
SELECT
    s.studentID,
    s.fName,
    s.lName,
    AVG(t.grade4) as gpa
FROM STUDENT s
JOIN TRANSCRIPT t ON s.studentID = t.studentID
GROUP BY s.studentID, s.fName, s.lName;

```

### **🔄 VIEW Güncelleme:**

```sql
CREATE OR REPLACE VIEW HARDCOURSES_V AS
-- Yeni sorgu tanımı
```

### **🗑️ VIEW Silme:**

```sql
DROP VIEW HARDCOURSES_V;

```

---

## **📋 VIEW Türleri**

### **🔍 1. Basit VIEW**

- Tek tablodan türetilir
- Basit filtreleme ve sütun seçimi

### **🔗 2. Karmaşık VIEW**

- Birden fazla tablodan türetilir
- JOIN, GROUP BY, HAVING kullanır

### **🧮 3. Hesaplamalı VIEW**

- Aggregate fonksiyonlar içerir
- SUM, AVG, COUNT gibi hesaplamalar

---

## **⚠️ Önemli Notlar**

> 🚀 Performans
> 
> - VIEW'ler her sorgulandığında yeniden hesaplanır
> - Karmaşık VIEW'ler yavaş olabilir

> 🔄 Güncelleme
> 
> - Basit VIEW'ler güncellenebilir
> - Karmaşık VIEW'ler (JOIN, GROUP BY) genelde read-only

> 🔒 Güvenlik
> 
> - VIEW'ler tablo izinlerini miras alır
> - Ek güvenlik katmanı sağlar

> 📊 Veri Tutarlılığı
> 
> - VIEW'ler her zaman güncel veriyi gösterir
> - Fiziksel veri saklamaz

---

## **💡 En İyi Uygulamalar**

> 🎯 Naming Convention
> 
> - VIEW adları açıklayıcı olmalı
> - Suffix olarak `_V` veya `_VIEW` kullanın

> 📊 Performans Optimizasyonu
> 
> - Gereksiz sütunları dahil etmeyin
> - WHERE koşullarını optimize edin

> 🛠️ Bakım
> 
> - VIEW'leri düzenli olarak gözden geçirin
> - Kullanılmayan VIEW'leri silin

> 📈 Dokümantasyon
> 
> - VIEW'lerin amacını belgelendirin
> - Bağımlılıkları takip edin

---

## **🎓 Özet**

VIEW'ler SQL'deki en güçlü araçlardan biridir. Özellikle:

**🔑 Ana Kullanım Alanları:**

- **Karmaşık raporlama** sorguları
- **Güvenlik gereksinimleri**
- **Veri soyutlama** ihtiyaçları
- **Kod standardizasyonu**

**✨ Temel Avantajlar:**

- Fiziksel tablo gibi kullanılır ama sanal olduğu için esnek ve dinamiktir
- Karmaşık sorguları basitleştirir
- Güvenlik katmanı sağlar
- Kod tekrarını önler

VIEW'ler, veritabanı tasarımında veri erişimini standartlaştırmak ve kullanıcı deneyimini iyileştirmek için vazgeçilmez araçlardır.

# **🗃️ SQL Server Stored Procedure (Saklı Yordam) Rehberi**

> 💡 Stored Procedure Nedir?
> 
> 
> Veritabanında önceden yazılmış ve derlenmiş SQL komutlarının bir araya getirildiği alt programlardır.
> 

### Sözdizimi

```sql
CREATE PROCEDURE prosedür_adı ([parametre_listesi])
BEGIN    -- SQL ifadeleri
END;
```

## **✨ Stored Procedure Avantajları**

- ⚡ **Performans avantajı** sağlar (önceden derlenmiş)
- 🔄 **Kod tekrarını** önler
- 🔒 **Güvenlik** sağlar (SQL injection saldırılarına karşı koruma)
- 🎯 **Merkezi yönetim** imkanı sunar
- 🧩 **Karmaşık işlemleri** basitleştirir

---

## **🚀 Pratik Örnekler**

### **1️⃣ Basit Stored Procedure Örneği**

> 📝 Amaç: Tüm öğrenci kayıtlarını getirmek
> 

```sql
CREATE PROCEDURE GetStudents AS
    SELECT * FROM STUDENT;
GO

-- Çalıştırma
EXEC GetStudents;

```

**🔧 Temel Yapı:**

- `CREATE PROCEDURE` → Yeni saklı yordam oluştur
- `GetStudents` → Prosedürün adı
- `AS` → SQL kodlarının başlangıcı
- `GO` → Batch ayırıcısı
- `EXEC` → Prosedürü çalıştır

**💡 Ne Yapar:**

- STUDENT tablosundaki tüm kayıtları getirir
- Parametre almaz, sadece veri döndürür

---

### **2️⃣ Parametreli Stored Procedure**

> 🎯 Amaç: Şehir ve cinsiyete göre öğrenci filtreleme
> 

```sql
CREATE PROCEDURE StudentsbyCityAndGender
    @City NVARCHAR(25),-- Şehir parametresi
    @Gender CHAR(1)-- Cinsiyet parametresi
    AS
    SELECT
        FNAME AS ad,
        LNAME AS soyad,
        city AS şehir,
        gender AS cinsiyet
    FROM STUDENT AS e
    WHERE e.city = @City
    AND e.GENDER = @Gender;
GO

```

**📋 Parametre Türleri:**

| Tür | Açıklama | Örnek |
| --- | --- | --- |
| `NVARCHAR(25)` | Unicode karakter dizisi (25 karakter) | Şehir adları |
| `CHAR(1)` | Sabit uzunlukta karakter (1 karakter) | Cinsiyet (M/F) |

**🔄 Çağırma Yöntemleri:**

```sql
-- 1. Pozisyonel (sırasıyla)
EXEC StudentsbyCityAndGender 'Ankara', 'F';

-- 2. İsimli (parametre adları ile)
EXEC StudentsbyCityAndGender @City = 'Ankara', @Gender = 'F';

```

---

### **3️⃣ OUTPUT Parametreli Stored Procedure**

> 📊 Amaç: Danışmanın öğrenci sayısını ve toplam zamanını hesaplamak
> 

```sql
CREATE PROC GetTotalTimeConsumption
    @staffid SMALLINT,-- Giriş parametresi
    @numberOfStudents INT OUTPUT,-- Çıkış parametresi
    @timeConsumed INT OUTPUT-- Çıkış parametresi
    AS
DECLARE
    @timeCons INT,-- Yerel değişken,
    @a INT;-- Kontrol değişkeni
    SELECT @numberOfStudents = COUNT(*) -- Öğrenci sayısını hesapla
FROM STAFF st
JOIN STUDENT s ON st.staffID = s.advisorID
WHERE st.staffID = @staffid;

-- Toplam zamanı hesapla (her öğrenci için 10 saat)
SET @timeCons = @numberOfStudents * 10;
SET @timeConsumed = @timeCons;

-- Koşullu kontrol
IF @numberOfStudents < 10 SET @a = 1;
IF @numberOfStudents > 10 SET @a = 0;
GO

```

**🔍 Yeni Kavramlar:**

> OUTPUT Parametreler
> 
> - Prosedürden değer döndürmek için kullanılır
> - `OUTPUT` anahtar kelimesi ile tanımlanır
> - Çağırırken de `OUTPUT` belirtilmeli

> DECLARE
> 
> - Yerel değişken tanımlamak için kullanılır
> - Sadece prosedür içinde geçerlidir

> JOIN İşlemi
> 
> - `STAFF` ve `STUDENT` tabloları arasında ilişki kurulur
> - Danışmanın öğrenci sayısını bulmak için kullanılır

**💡 Kullanım Örneği:**

```sql
DECLARE @studentCount INT, @totalTime INT;

EXEC GetTotalTimeConsumption 
    @staffid = 3,
    @numberOfStudents = @studentCount OUTPUT,
    @timeConsumed = @totalTime OUTPUT;

PRINT 'Öğrenci Sayısı: ' + CAST(@studentCount AS VARCHAR);
PRINT 'Toplam Zaman: ' + CAST(@totalTime AS VARCHAR) + ' saat';

```

---

### **4️⃣ Veri Değiştiren Stored Procedure**

> ⚙️ Amaç: Personelin yaşını değiştirmek
> 

```sql
CREATE PROCEDURE ChangeAge
    @fname NVARCHAR(25),-- Personel adı
    @lname NVARCHAR(25),-- Personel soyadı
    @arbiter INT,-- Değişim yönü (1: arttır, 0: azalt)
    @result INT OUTPUT-- Yeni yaş değeri
    AS
DECLARE
    @currentAge INT,-- Mevcut yaş
    @staffId INT;-- Personel ID
    SELECT
    @currentAge = age,-- Mevcut bilgileri al
    @staffId = staffID
FROM STAFF st
WHERE st.fName = @fname
AND st.lName = @lname;

-- Yaş değerini değiştir
IF @arbiter = 1 SET @currentAge = @currentAge + 5;
IF @arbiter = 0 SET @currentAge = @currentAge - 5;

SET @result = @currentAge;

-- Veritabanını güncelle
UPDATE STAFF
SET age = @currentAge
WHERE staffID = @staffId;
GO

```

**🔄 İşlem Akışı:**

1. **Veri Okuma** → `SELECT` ile mevcut veriyi al
2. **Hesaplama** → Yaşı arttır/azalt
3. **Veri Yazma** → `UPDATE` ile veriyi güncelle

**📊 Arbiter Değerleri:**

| Değer | İşlem | Sonuç |
| --- | --- | --- |
| `1` | Arttır | Yaş +5 |
| `0` | Azalt | Yaş -5 |

**💡 Kullanım Örneği:**

```sql
DECLARE @param1 INT;
EXEC ChangeAge 'Zuhal', 'Meral', 0, @param1 OUTPUT;
SELECT @param1 AS 'Yeni Yaş';

```

---

## **📊 Stored Procedure vs Function**

| Özellik | Stored Procedure | Function |
| --- | --- | --- |
| **Dönüş Değeri** | ✅ Opsiyonel | ✅ Mutlaka döndürür |
| **OUTPUT Parametre** | ✅ Kullanılabilir | ❌ Kullanılamaz |
| **Veri Değiştirme** | ✅ Yapabilir | ❌ Yapamaz |
| **SELECT'te Kullanım** | ❌ Kullanılamaz | ✅ Kullanılabilir |
| **Transaction Kontrolü** | ✅ Kontrol edebilir | ❌ Kontrolü yok |

---

## **🎯 Stored Procedure Avantajları**

### **🚀 1. Performans**

- ✅ Önceden derlenmiş kod
- ✅ Execution plan cache'lenir
- ✅ Ağ trafiği azalır

### **🔒 2. Güvenlik**

- ✅ SQL Injection saldırılarına karşı koruma
- ✅ Parametreli sorgular kullanır
- ✅ Kullanıcılar direkt tablo erişimi yapamaz

### **🔄 3. Kod Yeniden Kullanımı**

- ✅ Bir kez yazılır, birçok yerde kullanılır
- ✅ Merkezi güncelleme imkanı

### **📋 4. İş Kuralları**

- ✅ Karmaşık iş kuralları veritabanında saklanır
- ✅ Tutarlılık sağlanır

---

## **📝 Parametre Türleri Özeti**

| Tür | Açıklama | Tanımlama | Kullanım |
| --- | --- | --- | --- |
| **Giriş** | Prosedüre veri gönderir | `@City NVARCHAR(25)` | `EXEC Proc 'Ankara'` |
| **Çıkış (OUTPUT)** | Prosedürden veri alır | `@result INT OUTPUT` | `EXEC Proc @var OUTPUT` |
| **Yerel (DECLARE)** | Sadece prosedür içinde | `DECLARE @temp INT` | `SET @temp = 10` |

---

## **💡 En İyi Uygulamalar**

> 🎯 Naming Convention
> 
> - Prosedür adları açıklayıcı olmalı
> - Prefix kullanın (örn: `sp_`, `usp_`)

> 📊 Parametre Validasyonu
> 
> - Giriş parametrelerini kontrol edin
> - NULL değerler için varsayılan değerler belirleyin

> 🛠️ Hata Yönetimi
> 
> - `TRY...CATCH` blokları kullanın
> - Anlamlı hata mesajları döndürün

> 📈 Performans
> 
> - Gereksiz SELECT * kullanmayın
> - İndekslenmiş kolonları WHERE'de kullanın

---

## **🎓 Özet**

Bu örnekler, basit veri getirmekten karmaşık veri işleme operasyonlarına kadar Stored Procedure'ların farklı kullanım şekillerini göstermektedir.

**🔑 Anahtar Noktalar:**

- Stored Procedure'lar performans ve güvenlik sağlar
- Parametre kullanımı esneklik kazandırır
- OUTPUT parametreler ile veri döndürülebilir
- Karmaşık iş mantığı veritabanında saklanabilir

Stored Procedure (Saklı Prosedür), veritabanında saklanan ve tekrar tekrar çalıştırılabilen bir SQL kod bloğudur. Parametreler alabilir ve değerler döndürebilir.

### 

# **🔥 SQL Server Trigger (Tetikleyici) Kapsamlı Rehberi**

> 💡 Trigger Nedir?
> 
> 
> Veritabanında belirli olaylar gerçekleştiğinde otomatik olarak çalışan özel saklı yordam türleridir.
> 

### Sözdizimi

```sql
CREATE TRIGGER tetikleyici_adı
BEFORE/AFTER INSERT/UPDATE/DELETE ON tablo_adı
FOR EACH ROW BEGIN    -- SQL ifadeleri
END;
```

## **✨ Trigger Özellikleri**

- ⚡ **Otomatik çalışır** (manuel çağrılmaz)
- 👀 **Veri değişikliklerini izler** (INSERT, UPDATE, DELETE)
- 📋 **İş kurallarını uygular**
- 🔒 **Veri tutarlılığını sağlar**
- 📝 **Log/Audit işlemleri yapar**

---

## **📊 Trigger Türleri**

| Tür | Açıklama | Kullanım |
| --- | --- | --- |
| **AFTER** | İşlem tamamlandıktan sonra çalışır | En yaygın kullanılan |
| **INSTEAD OF** | İşlem yerine çalışır | Orijinal işlemi iptal eder |
| **BEFORE** | SQL Server'da bulunmaz | Oracle'da mevcut |

---

## **🗂️ Özel Tablolar**

> ⚠️ Önemli: Trigger içinde kullanılan özel sanal tablolar
> 

| Tablo | Açıklama | Kullanım Alanı |
| --- | --- | --- |
| **`inserted`** | Yeni eklenen/güncellenen kayıtlar | INSERT, UPDATE |
| **`deleted`** | Silinen/eski kayıtlar | DELETE, UPDATE |

---

## **🚀 Pratik Örnekler**

### **1️⃣ Basit Ekleme Tetikleyicisi**

> 📝 Amaç: COURSE tablosuna yeni ders eklendiğinde bunu kaydetmek
> 

```sql
CREATE TRIGGER insert_COURSELOG ON COURSE
AFTER INSERT AS
BEGIN
    INSERT INTO COURSELOG(cCode, ACTIONPERFORMED, ACTIONOCCURREDAT)
    SELECT i.cCode, 'I', GETDATE() FROM inserted i;
END;

```

**🔄 Nasıl Çalışır:**

1. **COURSE** tablosuna `INSERT` yapılır
2. Trigger otomatik devreye girer
3. **inserted** tablosundan yeni kaydın `cCode`'unu alır
4. **COURSELOG** tablosuna log kaydı ekler

**💡 Örnek Kullanım:**

```sql
INSERT INTO COURSE(cCode, cName, credits) VALUES('MATH201', 'Matematik II', 4);
-- ✅ COURSELOG'a otomatik kayıt: ('MATH201', 'I', '2024-01-15 14:30:25')
```

---

### **2️⃣ Gelişmiş Silme Tetikleyicisi**

> 🛡️ Amaç: Dersi silmeden önce güvenlik kontrolü yapmak
> 

```sql
CREATE TRIGGER delete_COURSELOG ON COURSE
AFTER DELETE AS
BEGIN
    DECLARE @hasRecords INT;

    SELECT @hasRecords = COUNT(*) FROM TRANSCRIPT
    WHERE TRANSCRIPT.cCode = (SELECT cCode FROM deleted);

    IF (@hasRecords) > 0
    BEGIN
        RAISERROR('Bu dersi silemezsiniz...', 16, 1);
        ROLLBACK TRANSACTION;
    END

    IF (@hasRecords) = 0
    BEGIN
        INSERT INTO COURSELOG(cCode, ACTIONPERFORMED, ACTIONOCCURREDAT)
        SELECT i.cCode, 'D', GETDATE() FROM deleted i;
    END
END;

```

**🔍 Çalışma Mantığı:**

> 1. Kontrol Aşaması
> 
> - Silinmek istenen dersin TRANSCRIPT tablosunda kaydı var mı kontrol et

> 2. Engelleme Aşaması
> 
> - İlişkili kayıt varsa: Hata mesajı + İşlemi geri al

> 3. Loglama Aşaması
> 
> - İlişkili kayıt yoksa: Silme işlemini logla

**📋 Senaryo Örnekleri:**

| Durum | Sonuç |
| --- | --- |
| TRANSCRIPT'te kayıt VAR | ❌ Hata mesajı, silme iptal |
| TRANSCRIPT'te kayıt YOK | ✅ Silme başarılı, log kaydı |
|  |  |

---

### **3️⃣ Güncelleme Tetikleyicisi**

```sql
CREATE TRIGGER update_COURSELOG ON COURSE
AFTER UPDATE AS
BEGIN
    INSERT INTO COURSELOG(cCode, ACTIONPERFORMED, ACTIONOCCURREDAT)
    SELECT i.cCode, 'U', GETDATE() FROM inserted i;
END;

```

> 💡 Not: UPDATE işleminde inserted tablosu güncellenen kayıtların yeni halini içerir
> 

---

### **4️⃣ İstatistik Güncelleme Tetikleyicisi**

> 📊 Amaç: Öğrenci notu eklendiğinde dersin istatistiklerini otomatik güncelle
> 

```sql
CREATE TRIGGER updateCourseAttributes ON TRANSCRIPT
AFTER INSERT, UPDATE AS
BEGIN
    DECLARE @newNumber AS INT;
    DECLARE @newAverage AS FLOAT;
    DECLARE @cCode AS VARCHAR(8);

    SELECT @cCode = cCode FROM inserted;

    SELECT
        @newNumber = COUNT(*),
        @newAverage = AVG(grade4)
    FROM TRANSCRIPT
    WHERE cCode = @cCode;

    UPDATE COURSE
    SET noOfAttendance = @newNumber, AverageGrades = @newAverage
    WHERE cCode = @cCode;
END;

```

**⚙️ İşlem Adımları:**

1. **Ders Kodunu Al** → `SELECT @cCode = cCode FROM inserted`
2. **İstatistikleri Hesapla** → Öğrenci sayısı + Ortalama not
3. **COURSE Tablosunu Güncelle** → Yeni değerlerle güncelle

---

### **5️⃣ Soft Delete Tetikleyicisi (INSTEAD OF)**

> 🗑️ Soft Delete: Veriyi gerçekten silmek yerine pasif olarak işaretleme
> 

```sql
CREATE TRIGGER Department_Delete
ON DEPARTMENT
INSTEAD OF DELETE AS
BEGIN
    DECLARE @DCODE VARCHAR(4);
    SELECT @DCODE = deptCode FROM deleted;

    UPDATE DEPARTMENT SET statusOfDept = 0
    WHERE deptCode = @DCODE;
END;

```

**🔄 Çalışma Prensibi:**

| Kullanıcı Yapar | Gerçekte Olan |
| --- | --- |
| `DELETE FROM DEPARTMENT WHERE deptCode='CSE'` | `UPDATE DEPARTMENT SET statusOfDept = 0 WHERE deptCode='CSE'` |

**📊 Statü Değerleri:**

- `statusOfDept = 1` → ✅ Aktif departman
- `statusOfDept = 0` → ❌ Silinmiş (pasif) departman

---

### **6️⃣ Karmaşık Log Tetikleyicisi**

> 🎯 Amaç: Tek trigger ile üç farklı işlemi (INSERT, UPDATE, DELETE) yakalamak
> 

```sql
CREATE TRIGGER Dep_Trigger ON DEPARTMENT
AFTER INSERT, UPDATE, DELETE AS
BEGIN
    IF @@ROWCOUNT = 0 RETURN;

    DECLARE @action CHAR(1);
    DECLARE @dCode VARCHAR(4);

    IF EXISTS(SELECT * FROM deleted)
    BEGIN
        IF EXISTS(SELECT * FROM inserted)
            SET @action = 'U';-- UPDATEELSE
            SET @action = 'D';-- DELETE

        SELECT @dCode = d.deptCode FROM deleted d;
    END
    ELSE
    BEGIN
        SET @action = 'I';-- INSERTSELECT 
		        @dCode = i.deptCode FROM inserted i;
    END

    INSERT INTO DEPLOG
        (deptCode, ActionPerformed, ActionOccurredAt)
    VALUES
        (@dCode, @action, SYSDATETIME());
END;

```

**🧠 İşlem Tespiti Mantığı:**

| Durum | inserted | deleted | Sonuç |
| --- | --- | --- | --- |
| INSERT | ✅ Var | ❌ Yok | 'I' |
| UPDATE | ✅ Var | ✅ Var | 'U' |
| DELETE | ❌ Yok | ✅ Var | 'D' |

---

### **7️⃣ Otomatik ID Atama Tetikleyicisi**

> 🔢 Amaç: Yeni ürün eklendiğinde otomatik ID atamak
> 

```sql
CREATE TRIGGER prodIdSet_T ON PRODUCT
AFTER INSERT AS
BEGIN
    DECLARE @PNAME VARCHAR(50);
    DECLARE @PID INT;

    SELECT @PNAME = productName FROM inserted;
    SELECT @PID = MAX(productId) FROM PRODUCT;
    SET @PID = @PID + 1;

    UPDATE PRODUCT SET productId = @PID WHERE productName = @PNAME;
END;

```

**⚙️ Çalışma Adımları:**

1. **Yeni Ürün Bilgisini Al** → `productName`
2. **En Büyük ID'yi Bul** → `MAX(productId)`
3. **Yeni ID Ata** → `@PID + 1`
4. **Güncelle** → Yeni ID'yi ata

---

## **🎯 Trigger Kullanım Senaryoları**

### **📋 1. Audit/Log İşlemleri**

- Veri değişikliklerini izleme
- Kim, ne zaman, ne yaptı kaydetme

### **🔒 2. İş Kuralları Uygulama**

- Silme engellemeleri
- Veri tutarlılık kontrolleri

### **🧮 3. Otomatik Hesaplamalar**

- İstatistik güncelleme
- Toplam hesaplama

### **🗑️ 4. Soft Delete**

- Veri silmek yerine pasif yapma
- Veri kurtarma imkanı

### **🔢 5. Otomatik Değer Atama**

- ID atama
- Varsayılan değer atama

---

## **⚠️ Önemli Noktalar**

> 🚀 Performans
> 
> - Trigger'lar her işlemde çalışır
> - Fazla karmaşık kod performansı düşürür

> 🛠️ Hata Yönetimi
> 
> - `RAISERROR` ile hata fırlatma
> - `ROLLBACK` ile işlem geri alma

> 📊 @@ROWCOUNT
> 
> - Etkilenen satır sayısını kontrol etme
> - Gereksiz işlemleri önleme

> ⏰ Tarih Fonksiyonları
> 
> - `SYSDATETIME()`: Daha hassas (microsaniye)
> - `GETDATE()`: Standart (millisaniye)

---

## **🎓 Özet**

Bu kapsamlı örnekler, trigger'ların farklı senaryolarda nasıl kullanılabileceğini göstermektedir. Her trigger farklı bir iş problemi çözmekte ve gerçek dünya uygulamalarında sıkça karşılaşılan durumları ele almaktadır.

**🔑 Anahtar Noktalar:**

- Trigger'lar otomatik çalışır
- Veri tutarlılığı sağlar
- Log ve audit işlemleri için idealdir
- Performans etkilerini göz önünde bulundur

### 📋 **Trigger Açıklamaları**

| 🏷️ Trigger Adı | ⚙️ Ne Yapar? | 🔍 Nasıl Çalışır? |
| --- | --- | --- |
| `insert_COURSELOG` | COURSE tablosuna yeni ders eklendiğinde COURSELOG'a 'I' logu atar. | `inserted` tablosundan alınan ders bilgisi `COURSELOG` tablosuna yazılır. |
| `delete_COURSELOG` | Silinecek ders TRANSCRIPT'te varsa silme engellenir, yoksa log atılır. | `deleted` verisi TRANSCRIPT ile kontrol edilir, varsa ROLLBACK yapılır. |
| `update_COURSELOG` | COURSE tablosundaki güncellemeler 'U' olarak COURSELOG'a loglanır. | Güncellenen `inserted` verileri log tablosuna yazılır. |
| `updateCourseAttributes` | TRANSCRIPT’e not eklendiğinde veya güncellendiğinde COURSE istatistikleri güncellenir. | COUNT ve AVG işlemleriyle yeni değerler hesaplanıp COURSE tablosuna yazılır. |
| `Department_Delete` | DEPARTMENT silme işlemi yerine statusOfDept = 0 yapar (soft delete). | `INSTEAD OF DELETE` ile fiziksel silme engellenir, sadece flag değeri değişir. |
| `Dep_Trigger` | DEPARTMENT tablosuna yapılan tüm işlemleri DEPLOG tablosuna loglar. | `inserted` ve `deleted` tablolarına göre işlem türü belirlenip log yazılır. |
| `prodIdSet_T` | PRODUCT tablosuna ürün eklenirken otomatik ID ataması yapar. | En büyük mevcut ID bulunur, 1 artırılarak yeni ürüne atanır. |

# **⚙️ SQL Server User-Defined Functions (Kullanıcı Tanımlı Fonksiyonlar) Rehberi**

> 💡 Fonksiyon Nedir?
> 
> 
> Kullanıcı tarafından oluşturulan ve belirli bir hesaplama yaparak sonuç döndüren veritabanı nesneleridir.
> 

### Sözdizimi

```sql
CREATE FUNCTION fonksiyon_adı([parametre_listesi])
RETURNS veri_tipi
BEGIN    -- SQL ifadeleri    
RETURN değer;
END;
```

## **✨ Fonksiyon Özellikleri**

- 🎯 **Tek bir değer döndürür** (Scalar Functions)
- 📥 **Parametre alabilir**
- 🔍 **SELECT sorgularında kullanılabilir**
- 🔄 **Tekrar kullanılabilir**
- 🧮 **Karmaşık hesaplamaları basitleştirir**

---

## **📊 Fonksiyon vs Stored Procedure**

| Özellik | Function | Stored Procedure |
| --- | --- | --- |
| **Dönüş Değeri** | ✅ Mutlaka döndürür | ⚠️ Opsiyonel |
| **SELECT'te Kullanım** | ✅ Kullanılabilir | ❌ Kullanılamaz |
| **Veri Değiştirme** | ❌ Yapamaz | ✅ Yapabilir |
| **OUTPUT Parametre** | ❌ Kullanılamaz | ✅ Kullanılabilir |
| **Transaction** | ❌ Kontrolü yok | ✅ Kontrol edebilir |

---

## **🚀 Pratik Örnekler**

### **1️⃣ Öğrenci Toplam Kredi Fonksiyonu**

> 🎯 Amaç: Bir öğrencinin aldığı tüm derslerin toplam kredisini hesaplamak
> 

```sql
CREATE FUNCTION get_student_total_credits(@student_id INT)
RETURNS INT
AS
BEGIN
    DECLARE @total_credits INT;

    SELECT @total_credits = SUM(c.credits)
    FROM TRANSCRIPT e
    JOIN COURSE c ON e.cCode = c.cCode
    WHERE e.studentID = @student_id;

    RETURN ISNULL(@total_credits, 0);
END;

```

**🔧 Fonksiyon Yapısı:**

> Fonksiyon İmzası
> 
> - `CREATE FUNCTION get_student_total_credits(@student_id INT)`
> - `RETURNS INT` → Tamsayı döndürür

> Fonksiyon Gövdesi
> 
> - `BEGIN...END` bloğu içinde kod
> - `DECLARE` ile yerel değişken
> - `RETURN` ile sonuç döndürme

**🔗 Tablo İlişkisi:**

- **TRANSCRIPT**: Öğrencilerin aldığı dersler
- **COURSE**: Ders bilgileri (kredi dahil)
- **JOIN**: İki tabloyu ders koduna göre birleştir

**🛡️ Null Kontrolü:**

```sql
RETURN ISNULL(@total_credits, 0);

```

- Öğrenci hiç ders almadıysa `SUM` NULL döner
- `ISNULL` ile NULL yerine 0 döndür

**💡 Kullanım Örneği:**

```sql
SELECT dbo.get_student_total_credits(12345) AS 'Toplam Kredi';
-- Sonuç: 45
```

---

### **2️⃣ Öğrenci Not Ortalaması (GPA) Fonksiyonu**

> 📊 Amaç: Öğrencinin ağırlıklı not ortalamasını hesaplamak
> 

```sql
CREATE FUNCTION get_student_gpa(@student_id INT)
RETURNS DECIMAL(4,2)
AS
BEGIN
    DECLARE @gpa DECIMAL(4,2);

    SELECT @gpa = (SUM(e.grade4 * c.credits) / SUM(c.credits))
    FROM TRANSCRIPT e
    JOIN COURSE c ON e.cCode = c.cCode
    WHERE e.studentID = @student_id;

    RETURN ISNULL(@gpa, 0.00);
END;

```

**🔢 Dönüş Tipi:**

```sql
RETURNS DECIMAL(4,2)

```

- `DECIMAL(4,2)`: 4 haneli, 2 ondalık basamaklı (örn: 12.34)
- GPA genelde 0.00-4.00 arası olduğu için uygun

**🧮 Ağırlıklı Ortalama Formülü:**

```
GPA = (Not1×Kredi1 + Not2×Kredi2 + ... + NotN×KrediN) / (Kredi1 + Kredi2 + ... + KrediN)

```

**📋 Örnek Hesaplama:**

| Ders | Kredi | Not | Ağırlıklı Not |
| --- | --- | --- | --- |
| Matematik | 3 | 3.5 | 3.5 × 3 = 10.5 |
| Fizik | 4 | 2.0 | 2.0 × 4 = 8.0 |
| Kimya | 2 | 4.0 | 4.0 × 2 = 8.0 |
| **Toplam** | **9** | - | **26.5** |

**GPA = 26.5 ÷ 9 = 2.94**

**💡 Kullanım Örneği:**

```sql
SELECT dbo.get_student_gpa(12345) AS 'Not Ortalaması';
-- Sonuç: 2.94
```

---

### **3️⃣ Öğrenci Ders Sayısı Fonksiyonu**

> 📚 Amaç: Öğrencinin aldığı toplam ders sayısını bulmak
> 

```sql
CREATE FUNCTION get_course_count(@stu_id INT)
RETURNS INT
BEGIN
    DECLARE @course_count INT;

    SELECT @course_count = COUNT(*)
    FROM TRANSCRIPT
    WHERE studentID = @stu_id;

    RETURN ISNULL(@course_count, 0);
END;

```

**🔍 Basit Sayma İşlemi:**

- **TRANSCRIPT** tablosunda öğrencinin kaç kayıtı var?
- Her kayıt = bir ders

**⚡ Alternatif Yazım:**

```sql
CREATE FUNCTION get_course_count(@stu_id INT)
RETURNS INT
AS
BEGIN
    RETURN (
        SELECT COUNT(*)
        FROM TRANSCRIPT
        WHERE studentID = @stu_id
    );
END;

```

---

### **4️⃣ Bölüm Öğrenci Sayısı Fonksiyonu**

> 🏫 Amaç: Belirli bir bölümdeki öğrenci sayısını bulmak
> 

```sql
CREATE FUNCTION get_department_student_count(@dcode VARCHAR(4))
RETURNS INT
BEGIN
    DECLARE @student_count INT;

    SELECT @student_count = COUNT(*)
    FROM STUDENT
    WHERE deptCode = @dcode;

    RETURN @student_count;
END;

```

**📝 Parametre Tipi:**

```sql
@dcode VARCHAR(4)

```

- Bölüm kodu genelde kısa olur (örn: "CSE", "MATH")
- `VARCHAR(4)` yeterli

**💡 Kullanım Örneği:**

```sql
SELECT dbo.get_department_student_count('CSE') AS 'Bilgisayar Mühendisliği Öğrenci Sayısı';
-- Sonuç: 150
```

---

### **5️⃣ Personel Yaş Hesaplama Fonksiyonu**

> 📅 Amaç: Personelin doğum tarihinden yaşını hesaplamak
> 

```sql
ALTER FUNCTION findAge(@id INT)
RETURNS INT
BEGIN
    DECLARE @age INT;

    SELECT @age = DATEDIFF(YEAR, birthDate, GETDATE())
    FROM STAFF
    WHERE staffID = @id;

    RETURN @age;
END;

```

**🔄 ALTER vs CREATE:**

```sql
ALTER FUNCTION findAge(@id INT)

```

- `ALTER`: Mevcut fonksiyonu değiştir
- `CREATE`: Yeni fonksiyon oluştur

**📅 Tarih Hesaplama:**

```sql
DATEDIFF(YEAR, birthDate, GETDATE())

```

- `DATEDIFF(YEAR, başlangıç, bitiş)`: Yıl farkını hesapla
- `birthDate`: Doğum tarihi
- `GETDATE()`: Bugünün tarihi

**📋 DATEDIFF Örneği:**

```sql
-- 1990-05-15 doğumlu biri için (2024-01-20'de)
DATEDIFF(YEAR, '1990-05-15', '2024-01-20')
-- Sonuç: 33 (yaş)
```

**💡 Kullanım Örneği:**

```sql
SELECT dbo.findAge(101) AS 'Personel Yaşı';
-- Sonuç: 45
```

---

## **📊 Kapsamlı Sorgu Örnekleri**

### **🎓 Örnek 1: Öğrenci Raporu**

```sql
SELECT
    studentID AS 'Öğrenci No',
    fName AS 'Adı',
    lName AS 'Soyadı',
    dbo.get_student_total_credits(studentID) AS 'Toplam Kredi',
    dbo.get_student_gpa(studentID) AS 'Not Ortalaması',
    dbo.get_course_count(studentID) AS 'Ders Sayısı'
FROM STUDENT;

```

**📋 Sonuç Tablosu:**

| Öğrenci No | Adı | Soyadı | Toplam Kredi | Not Ortalaması | Ders Sayısı |
| --- | --- | --- | --- | --- | --- |
| 12345 | Ahmet | Yılmaz | 45 | 3.25 | 8 |
| 12346 | Ayşe | Kaya | 38 | 2.85 | 7 |

### **🏫 Örnek 2: Bölüm Raporu**

```sql
SELECT
    dName AS 'Bölüm Adı',
    dbo.get_department_student_count(deptCode) AS 'Öğrenci Sayısı'
FROM DEPARTMENT;

```

**📋 Sonuç Tablosu:**

| Bölüm Adı | Öğrenci Sayısı |
| --- | --- |
| Bilgisayar Mühendisliği | 150 |
| Makine Mühendisliği | 120 |

### **👥 Örnek 3: Personel Yaş Raporu**

```sql
SELECT
    fName AS 'Adı',
    lName AS 'Soyadı',
    birthDate AS 'Doğum Tarihi',
    dbo.findAge(staffID) AS 'Yaş'
FROM STAFF;

```

### **📅 Örnek 4: Fonksiyonsuz Yaş Hesaplama**

```sql
SELECT
    fName AS 'Adı',
    lName AS 'Soyadı',
    birthDate AS 'Doğum Tarihi',
    DATEDIFF(YEAR, birthDate, GETDATE()) AS 'Yaş'
FROM STUDENT;

```

---

## **🎯 Fonksiyon Kullanımının Avantajları**

### **🔄 1. Kod Tekrarını Önleme**

**❌ Fonksiyonsuz (her seferinde yazmak gerekir):**

```sql
SELECT SUM(c.credits) FROM TRANSCRIPT e JOIN COURSE c ON e.cCode = c.cCode WHERE e.studentID = 123;
SELECT SUM(c.credits) FROM TRANSCRIPT e JOIN COURSE c ON e.cCode = c.cCode WHERE e.studentID = 456;

```

**✅ Fonksiyonlu (basit kullanım):**

```sql
SELECT dbo.get_student_total_credits(123);
SELECT dbo.get_student_total_credits(456);

```

### **🔧 2. Merkezi Güncelleme**

- Hesaplama mantığı değişirse sadece fonksiyon güncellenir
- Tüm kullanan yerler otomatik güncellenir

### **📖 3. Okunabilirlik**

**❌ Anlaşılması zor:**

```sql
SELECT (SUM(e.grade4 * c.credits) / SUM(c.credits)) FROM ...

```

**✅ Anlaşılması kolay:**

```sql
SELECT dbo.get_student_gpa(studentID) AS 'GPA'

```

---

## **📝 Fonksiyon Türleri**

### **🔢 1. Scalar Functions (Tekil Değer)**

- Tek bir değer döndürür
- Yukarıdaki tüm örnekler bu türden

### **📊 2. Table-Valued Functions (Tablo Değerli)**

- Tablo döndürür
- Daha karmaşık sorgularda kullanılır

---

## **⚠️ Önemli Notlar**

### **🚀 1. Performans**

> Dikkat: Fonksiyonlar her satır için çalışır Büyük veri setlerinde yavaş olabilir
> 

### **🔒 2. Schema Binding**

```sql
CREATE FUNCTION ... WITH SCHEMABINDING

```

- Fonksiyonun kullandığı tabloları "kilitler"
- Performans artışı sağlar

### **🎯 3. Deterministic vs Non-Deterministic**

| Tür | Açıklama | Örnek |
| --- | --- | --- |
| **Deterministic** | Aynı girdi, aynı çıktı | Matematiksel hesaplamalar |
| **Non-Deterministic** | Değişken çıktı | GETDATE() kullanan fonksiyonlar |

---

## **💡 En İyi Uygulamalar**

> 🎯 Naming Convention
> 
> - Fonksiyon adları açıklayıcı olmalı
> - Prefix kullanın (örn: `fn_`, `ufn_`)

> 📊 Parametre Validasyonu
> 
> - Giriş parametrelerini kontrol edin
> - NULL değerler için varsayılan değerler döndürün

> 🛠️ Hata Yönetimi
> 
> - ISNULL kullanarak NULL kontrolü yapın
> - Anlamlı varsayılan değerler döndürün

> 📈 Performans
> 
> - Karmaşık hesaplamaları minimize edin
> - Büyük veri setlerinde dikkatli kullanın

---

## **🎓 Özet**

Bu kapsamlı örnekler, SQL Server'da fonksiyonların nasıl oluşturulacağını ve kullanılacağını göstermektedir. Her fonksiyon farklı bir hesaplama türünü ele alarak, gerçek dünya uygulamalarında karşılaşabileceğiniz senaryoları kapsamaktadır.

**🔑 Anahtar Noktalar:**

- Fonksiyonlar SELECT sorgularında kullanılabilir
- Kod tekrarını önler ve okunabilirliği artırır
- Karmaşık hesaplamaları basitleştirir
- Performans etkilerini göz önünde bulundur

# **🗂️ Veritabanı Normalizasyonu (Database Normalization) Kapsamlı Rehberi**

> 💡 Normalizasyon Nedir?
> 
> 
> Veritabanı tablolarını **veri tekrarını minimize edecek** ve **veri tutarlılığını maksimize edecek** şekilde düzenleme sürecidir.
> 

## **✨ Normalizasyonun Amaçları**

- 🚫 **Veri Tekrarını Önleme** (Data Redundancy)
- 🔄 **Veri Tutarlılığını Sağlama** (Data Consistency)
- 💾 **Depolama Alanını Optimize Etme**
- 🛠️ **Güncelleme Anomalilerini Önleme**
- 🗑️ **Silme Anomalilerini Önleme**
- ➕ **Ekleme Anomalilerini Önleme**

---

## **🎯 Normalizasyon Türleri**

| Normal Form | Kısaltma | Ana Kural |
| --- | --- | --- |
| **First Normal Form** | **1NF** | Atomik değerler, tekrarlayan gruplar yok |
| **Second Normal Form** | **2NF** | 1NF + Kısmi bağımlılık yok |
| **Third Normal Form** | **3NF** | 2NF + Geçişli bağımlılık yok |
| **Boyce-Codd Normal Form** | **BCNF** | 3NF + Her determinant aday anahtar |
| **Fourth Normal Form** | **4NF** | BCNF + Çok değerli bağımlılık yok |
| **Fifth Normal Form** | **5NF** | 4NF + Birleştirme bağımlılığı yok |

---

## **🚀 Adım Adım Normalizasyon Süreci**

### **📊 Başlangıç Tablosu (Normalize Edilmemiş)**

> 🎯 Senaryo: Bir üniversitenin öğrenci, ders ve not bilgilerini tutan tablo
> 

```sql
STUDENT_COURSE_GRADE

```

| StudentID | StudentName | StudentCity | CourseID | CourseName | Credits | InstructorName | InstructorOffice | Grade |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1001 | Ahmet Yılmaz | Ankara | CS101 | Programming | 3 | Dr. Ali Veli | A101 | 85 |
| 1001 | Ahmet Yılmaz | Ankara | CS102 | Data Structures | 4 | Dr. Ayşe Kaya | B205 | 92 |
| 1002 | Fatma Demir | İstanbul | CS101 | Programming | 3 | Dr. Ali Veli | A101 | 78 |
| 1002 | Fatma Demir | İstanbul | CS103 | Algorithms | 3 | Dr. Mehmet Öz | C301 | 88 |
| 1003 | Can Özkan | İzmir | CS102 | Data Structures | 4 | Dr. Ayşe Kaya | B205 | 95 |

**❌ Bu tablodaki problemler:**

- Öğrenci bilgileri tekrar ediyor
- Ders bilgileri tekrar ediyor
- Öğretmen bilgileri tekrar ediyor
- Güncelleme, silme, ekleme anomalileri var

---

## **1️⃣ First Normal Form (1NF)**

> 🎯 Amaç: Her hücrede atomik (bölünemeyen) değerler olmalı, tekrarlayan gruplar olmamalı
> 

### **📋 1NF Kuralları:**

- ✅ Her sütun atomik değerler içermeli
- ✅ Aynı türde veri içeren sütunlar olmamalı
- ✅ Her satır benzersiz olmalı
- ✅ Sütun sırası önemli olmamalı

### **🔍 1NF Kontrolü:**

**✅ Mevcut tablomuz zaten 1NF'de:**

- Her hücre tek bir değer içeriyor
- Tekrarlayan grup yok
- Her satır benzersiz

> 💡 1NF İhlali Örneği:
> 
> 
> 
> | StudentID | Courses |
> | --- | --- |
> | 1001 | CS101, CS102, CS103 |
> 
> Bu durumda "Courses" sütunu atomik değil!
> 

---

## **2️⃣ Second Normal Form (2NF)**

> 🎯 Amaç: 1NF + Kısmi fonksiyonel bağımlılık olmamalı
> 

### **📋 2NF Kuralları:**

- ✅ Tablo 1NF'de olmalı
- ✅ Anahtar olmayan her sütun, birincil anahtarın tamamına bağımlı olmalı
- ✅ Kısmi bağımlılık olmamalı

### **🔍 Mevcut Tabloda Kısmi Bağımlılıklar:**

**🔑 Birincil Anahtar:** (StudentID, CourseID)

**❌ Kısmi Bağımlılıklar:**

- `StudentName` → `StudentID` (sadece StudentID'ye bağımlı)
- `StudentCity` → `StudentID` (sadece StudentID'ye bağımlı)
- `CourseName` → `CourseID` (sadece CourseID'ye bağımlı)
- `Credits` → `CourseID` (sadece CourseID'ye bağımlı)
- `InstructorName` → `CourseID` (sadece CourseID'ye bağımlı)
- `InstructorOffice` → `CourseID` (sadece CourseID'ye bağımlı)

### **🔧 2NF'ye Dönüştürme:**

### **📚 STUDENT Tablosu:**

| StudentID | StudentName | StudentCity |
| --- | --- | --- |
| 1001 | Ahmet Yılmaz | Ankara |
| 1002 | Fatma Demir | İstanbul |
| 1003 | Can Özkan | İzmir |

### **📖 COURSE Tablosu:**

| CourseID | CourseName | Credits | InstructorName | InstructorOffice |
| --- | --- | --- | --- | --- |
| CS101 | Programming | 3 | Dr. Ali Veli | A101 |
| CS102 | Data Structures | 4 | Dr. Ayşe Kaya | B205 |
| CS103 | Algorithms | 3 | Dr. Mehmet Öz | C301 |

### **📊 ENROLLMENT Tablosu:**

| StudentID | CourseID | Grade |
| --- | --- | --- |
| 1001 | CS101 | 85 |
| 1001 | CS102 | 92 |
| 1002 | CS101 | 78 |
| 1002 | CS103 | 88 |
| 1003 | CS102 | 95 |

> ✅ Artık 2NF'de: Her tablo kendi konusuna odaklanmış, kısmi bağımlılık yok
> 

---

## **3️⃣ Third Normal Form (3NF)**

> 🎯 Amaç: 2NF + Geçişli fonksiyonel bağımlılık olmamalı
> 

### **📋 3NF Kuralları:**

- ✅ Tablo 2NF'de olmalı
- ✅ Anahtar olmayan sütunlar arasında bağımlılık olmamalı
- ✅ Geçişli bağımlılık olmamalı

### **🔍 COURSE Tablosunda Geçişli Bağımlılık:**

**❌ Geçişli Bağımlılık:**

- `CourseID` → `InstructorName` → `InstructorOffice`
- Yani: Ders → Öğretmen → Ofis

Bu durumda `InstructorOffice`, `CourseID`'ye geçişli olarak bağımlı.

### **🔧 3NF'ye Dönüştürme:**

### **📖 COURSE Tablosu (Güncellenmiş):**

| CourseID | CourseName | Credits | InstructorID |
| --- | --- | --- | --- |
| CS101 | Programming | 3 | I001 |
| CS102 | Data Structures | 4 | I002 |
| CS103 | Algorithms | 3 | I003 |

### **👨‍🏫 INSTRUCTOR Tablosu (Yeni):**

| InstructorID | InstructorName | InstructorOffice |
| --- | --- | --- |
| I001 | Dr. Ali Veli | A101 |
| I002 | Dr. Ayşe Kaya | B205 |
| I003 | Dr. Mehmet Öz | C301 |

### **📚 STUDENT Tablosu (Değişmez):**

| StudentID | StudentName | StudentCity |
| --- | --- | --- |
| 1001 | Ahmet Yılmaz | Ankara |
| 1002 | Fatma Demir | İstanbul |
| 1003 | Can Özkan | İzmir |

### **📊 ENROLLMENT Tablosu (Değişmez):**

| StudentID | CourseID | Grade |
| --- | --- | --- |
| 1001 | CS101 | 85 |
| 1001 | CS102 | 92 |
| 1002 | CS101 | 78 |
| 1002 | CS103 | 88 |
| 1003 | CS102 | 95 |

> ✅ Artık 3NF'de: Geçişli bağımlılık yok, her tablo tek bir varlığa odaklanmış
> 

---

## **🔄 Boyce-Codd Normal Form (BCNF)**

> 🎯 Amaç: 3NF + Her determinant aday anahtar olmalı
> 

### **📋 BCNF Kuralları:**

- ✅ Tablo 3NF'de olmalı
- ✅ Her fonksiyonel bağımlılıkta sol taraf süper anahtar olmalı
- ✅ X → Y bağımlılığında X aday anahtar olmalı

### **🔍 BCNF Kontrolü:**

**Mevcut tablolarımızda BCNF ihlali var mı?**

### **📖 COURSE Tablosu Analizi:**

- `CourseID` → `CourseName, Credits, InstructorID` ✅
- `InstructorID` → `CourseID` (Eğer her öğretmen tek ders veriyorsa) ❌

> ⚠️ BCNF İhlali Senaryosu: Eğer bir öğretmen birden fazla ders verebiliyorsa, mevcut yapı BCNF'de kalır. Eğer her öğretmen sadece bir ders veriyorsa, BCNF ihlali vardır.
> 

### **🔧 BCNF'ye Dönüştürme (İhtiyaç Durumunda):**

### **👨‍🏫 INSTRUCTOR Tablosu:**

| InstructorID | InstructorName | InstructorOffice |
| --- | --- | --- |
| I001 | Dr. Ali Veli | A101 |
| I002 | Dr. Ayşe Kaya | B205 |
| I003 | Dr. Mehmet Öz | C301 |

### **📖 COURSE Tablosu:**

| CourseID | CourseName | Credits |
| --- | --- | --- |
| CS101 | Programming | 3 |
| CS102 | Data Structures | 4 |
| CS103 | Algorithms | 3 |

### **🔗 COURSE_INSTRUCTOR Tablosu:**

| CourseID | InstructorID |
| --- | --- |
| CS101 | I001 |
| CS102 | I002 |
| CS103 | I003 |

---

## **📊 Normalizasyon Öncesi vs Sonrası Karşılaştırma**

### **❌ Normalize Edilmemiş (Başlangıç):**

**Problemler:**

- 🔄 Veri tekrarı (Ahmet Yılmaz bilgisi 2 kez)
- 💾 Fazla depolama alanı kullanımı
- 🛠️ Güncelleme anomalisi (Öğrenci adı değişirse birden fazla yerde güncelleme)
- 🗑️ Silme anomalisi (Son dersi silinen öğrencinin bilgisi kaybolur)
- ➕ Ekleme anomalisi (Henüz ders almayan öğrenci eklenemez)

### **✅ 3NF'de Normalize Edilmiş:**

**Avantajlar:**

- 🚫 Veri tekrarı yok
- 💾 Optimal depolama kullanımı
- 🛠️ Güncelleme tek yerden yapılır
- 🗑️ Veri kaybı riski yok
- ➕ Bağımsız veri ekleme mümkün

---

## **🎯 Normalizasyon Seviyesi Seçimi**

### **📈 Normalizasyon Seviyeleri:**

| Seviye | Avantajlar | Dezavantajlar | Kullanım Alanı |
| --- | --- | --- | --- |
| **1NF** | Temel düzen | Çok fazla tekrar | Basit uygulamalar |
| **2NF** | Kısmi tekrar azalır | Hala bazı tekrarlar | Küçük sistemler |
| **3NF** | Minimal tekrar | Karmaşık sorgular | Çoğu uygulama |
| **BCNF** | Tam normalize | Çok fazla tablo | Kritik sistemler |
| **4NF/5NF** | Teorik mükemmellik | Aşırı karmaşıklık | Akademik çalışmalar |

### **💡 Pratik Öneriler:**

> 🎯 Çoğu Uygulama İçin 3NF Yeterlidir
> 
> - Veri tekrarını minimize eder
> - Performans dengesi sağlar
> - Anlaşılabilir yapı sunar

> ⚠️ Aşırı Normalizasyon Tehlikesi
> 
> - Çok fazla JOIN gerektirir
> - Sorgu performansını düşürür
> - Karmaşıklığı artırır

---

## **🔧 Denormalizasyon (Denormalization)**

> 💡 Denormalizasyon Nedir?
> 
> 
> Performans artışı için kasıtlı olarak normalizasyon kurallarını ihlal etme sürecidir.
> 

### **📊 Denormalizasyon Senaryoları:**

### **🚀 Performans Optimizasyonu:**

```sql
-- Normalize edilmiş (3NF) - Yavaş
SELECT s.StudentName, c.CourseName, e.Grade
FROM STUDENT s
JOIN ENROLLMENT e ON s.StudentID = e.StudentID
JOIN COURSE c ON e.CourseID = c.CourseID;

-- Denormalize edilmiş - Hızlı
SELECT StudentName, CourseName, Grade
FROM STUDENT_COURSE_SUMMARY;

```

### **📈 Raporlama Tabloları:**

```sql
-- Sık kullanılan rapor için denormalize tablo
CREATE TABLE MONTHLY_REPORT AS
SELECT
    s.StudentName,
    s.StudentCity,
    c.CourseName,
    i.InstructorName,
    e.Grade,
    MONTH(e.EnrollmentDate) as Month
FROM STUDENT s
JOIN ENROLLMENT e ON s.StudentID = e.StudentID
JOIN COURSE c ON e.CourseID = c.CourseID
JOIN INSTRUCTOR i ON c.InstructorID = i.InstructorID;

```

### **⚖️ Denormalizasyon Kararı:**

| Durum | Normalize Et | Denormalize Et |
| --- | --- | --- |
| **Sık güncellenen veriler** | ✅ | ❌ |
| **Sık okunan, az güncellenen** | ❌ | ✅ |
| **Karmaşık raporlar** | ❌ | ✅ |
| **Gerçek zamanlı analiz** | ❌ | ✅ |
| **OLTP sistemler** | ✅ | ❌ |
| **OLAP/DW sistemler** | ❌ | ✅ |

---

## **💡 Pratik Normalizasyon Adımları**

### **🔍 1. Veri Analizi:**

```sql
-- Tekrarlayan verileri tespit et
SELECT column_name, COUNT(*) as frequency
FROM table_name
GROUP BY column_name
HAVING COUNT(*) > 1;

```

### **📋 2. Fonksiyonel Bağımlılık Analizi:**

```
-- Bağımlılıkları listele
StudentID → StudentName, StudentCity
CourseID → CourseName, Credits
(StudentID, CourseID) → Grade

```

### **🔧 3. Tablo Ayrıştırma:**

```sql
-- Ana tabloyu parçala
CREATE TABLE STUDENT (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100),
    StudentCity VARCHAR(50)
);

CREATE TABLE COURSE (
    CourseID VARCHAR(10) PRIMARY KEY,
    CourseName VARCHAR(100),
    Credits INT
);

CREATE TABLE ENROLLMENT (
    StudentID INT,
    CourseID VARCHAR(10),
    Grade INT,
    PRIMARY KEY (StudentID, CourseID),
    FOREIGN KEY (StudentID) REFERENCES STUDENT(StudentID),
    FOREIGN KEY (CourseID) REFERENCES COURSE(CourseID)
);

```

### **✅ 4. Doğrulama:**

```sql
-- Veri bütünlüğünü kontrol et
SELECT COUNT(*) FROM original_table;
SELECT COUNT(*) FROM (
    SELECT s.*, c.*, e.*
    FROM STUDENT s
    JOIN ENROLLMENT e ON s.StudentID = e.StudentID
    JOIN COURSE c ON e.CourseID = c.CourseID
);

```

---

## **⚠️ Normalizasyon Tuzakları**

### **🚫 Yaygın Hatalar:**

> ❌ Aşırı Normalizasyon
> 
> - Her şeyi ayrı tabloya koymak
> - Gereksiz karmaşıklık yaratmak

> ❌ Eksik Normalizasyon
> 
> - Veri tekrarını görmezden gelmek
> - Güncelleme anomalilerini ihmal etmek

> ❌ Yanlış Anahtar Seçimi
> 
> - Birincil anahtarı yanlış belirlemek
> - Bileşik anahtarları gözden kaçırmak

### **💡 En İyi Uygulamalar:**

> 🎯 İş Kurallarını Anla
> 
> - Veri ilişkilerini doğru modellemek
> - Gerçek dünya kısıtlarını dikkate almak

> 📊 Performans Testleri Yap
> 
> - Sorgu performansını ölç
> - Gerekirse denormalize et

> 🔄 İteratif Yaklaşım
> 
> - Adım adım normalize et
> - Her adımda test et

---

## **🎓 Özet**

**🔑 Anahtar Noktalar:**

### **✨ Normalizasyonun Faydaları:**

- Veri tekrarını önler
- Veri tutarlılığını sağlar
- Depolama alanını optimize eder
- Güncelleme anomalilerini önler

### **📊 Normal Form Seviyeleri:**

- **1NF**: Atomik değerler
- **2NF**: Kısmi bağımlılık yok
- **3NF**: Geçişli bağımlılık yok
- **BCNF**: Her determinant aday anahtar

### **⚖️ Denge Kuralı:**

- Çoğu uygulama için 3NF yeterli
- Performans gereksinimlerine göre denormalize et
- İş kurallarını her zaman öncelikle

### **🎯 Pratik Yaklaşım:**

- Veriyi anla
- Adım adım normalize et
- Test et ve optimize et
- Gerektiğinde denormalize et

Normalizasyon, veritabanı tasarımının temel taşlarından biridir. Doğru uygulandığında güçlü, tutarlı ve sürdürülebilir veritabanları oluşturmanızı sağlar! 🚀

# 🧪 Uygulama Soruları - Bölüm 1

### SELECT Soruları

1. “Customers” tablosundan tüm müşterilerin adını ve ülkesini listeleyen bir SQL sorgusu yazınız.

```sql
SELECT customerName, country FROM Customers;
```

1. “Products” tablosundan fiyatı 50’den büyük olan ürünleri fiyata göre azalan sırada listeleyen bir SQL sorgusu yazınız.

```sql
SELECT * FROM Products WHERE price > 50 ORDER BY price DESC;
```

1. Her bir ülkedeki müşteri sayısını bulan ve sayıya göre azalan sırayla listeleyen bir SQL sorgusu yazınız.

```sql
SELECT country, COUNT(*) as customer_count
FROM Customers
GROUP BY country
ORDER BY customer_count DESC;
```

1. “Orders” ve “Customers” tablolarını birleştirerek, her müşterinin sipariş sayısını bulan bir SQL sorgusu yazınız.

```sql
SELECT c.customerName, COUNT(o.orderID) as order_count
FROM Customers c
LEFT JOIN Orders o ON c.customerID = o.customerID
GROUP BY c.customerID, c.customerName;
```

1. “USA” ülkesindeki müşterilerin yaptığı siparişleri listeleyen bir SQL sorgusu yazınız.

```sql
SELECT o.*FROM Orders o
INNER JOIN Customers c ON o.customerID = c.customerID
WHERE c.country = 'USA';
```

### INSERT, UPDATE, DELETE Soruları

1. “Products” tablosuna yeni bir ürün ekleyen bir SQL sorgusu yazınız.

```sql
INSERT INTO Products (productName, supplierID, categoryID, price, stock)
VALUES ('Yeni Ürün', 1, 2, 29.99, 100);
```

1. “USA” ülkesindeki tüm müşterilerin “contactTitle” alanını “Sales Manager” olarak güncelleyen bir SQL sorgusu yazınız.

```sql
UPDATE Customers
SET contactTitle = 'Sales Manager'WHERE country = 'USA';
```

1. 2020 yılından önce yapılmış tüm siparişleri silen bir SQL sorgusu yazınız.

```sql
DELETE FROM Orders
WHERE orderDate < '2020-01-01';
```

1. “Customers” tablosundan siparişi olmayan müşterileri silen bir SQL sorgusu yazınız.

```sql
DELETE FROM Customers
WHERE customerID NOT IN (SELECT DISTINCT customerID FROM Orders);
```

1. “Products” tablosundaki tüm ürünlerin fiyatını %10 artıran bir SQL sorgusu yazınız.

```sql
UPDATE Products
SET price = price * 1.10;
```

### Tablo İşlemleri Soruları

1. Öğrenciler için bir tablo oluşturan bir SQL sorgusu yazınız. Tablo, öğrenci numarası (primary key), ad, soyad, doğum tarihi ve bölüm içermelidir.

```sql
CREATE TABLE Students (
    student_id INT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    birth_date DATE,
    department VARCHAR(100)
);
```

1. “Orders” tablosuna bir “status” sütunu ekleyen ve varsayılan değerini “Pending” yapan bir SQL sorgusu yazınız.

```sql
ALTER TABLE Orders
ADD status VARCHAR(20) DEFAULT 'Pending';
```

1. “Products” tablosundaki “description” sütununu silen bir SQL sorgusu yazınız.

```sql
ALTER TABLE Products
DROP COLUMN description;
```

1. “Customers” tablosuna e-posta adresi için bir UNIQUE kısıtlaması ekleyen bir SQL sorgusu yazınız.

```sql
ALTER TABLE Customers
ADD email VARCHAR(100) UNIQUE;
```

1. “Students” tablosunda, yaş için “15 ile 30 arasında olmalı” şeklinde bir CHECK kısıtlaması ekleyen bir SQL sorgusu yazınız.

```sql
ALTER TABLE Students
ADD CONSTRAINT chk_age CHECK (age BETWEEN 15 AND 30);
```

# 🧪 Uygulama Soruları - Bölüm 2

### VIEW Soruları

1. “Orders” ve “Customers” tablolarını birleştiren ve müşteri adı, sipariş tarihi ve toplam sipariş tutarını gösteren “OrderSummary” adlı bir VIEW oluşturunuz.

```sql
CREATE VIEW OrderSummary ASSELECT c.customerName, o.orderDate, SUM(od.quantity * p.price) as total_amount
FROM Orders o
JOIN Customers c ON o.customerID = c.customerID
JOIN OrderDetails od ON o.orderID = od.orderID
JOIN Products p ON od.productID = p.productID
GROUP BY o.orderID, c.customerName, o.orderDate;
```

1. “Products” tablosundaki stok miktarı 10’dan az olan ürünleri gösteren “LowStockProducts” adlı bir VIEW oluşturunuz.

```sql
CREATE VIEW LowStockProducts ASSELECT * FROM Products WHERE stock < 10;
```

1. “OrderDetails” VIEW’ini güncelleyerek, sipariş durumunu ekleyen bir SQL sorgusu yazınız.

```sql
ALTER VIEW OrderDetails ASSELECT o.orderID, c.customerName, p.productName, od.quantity, p.price, o.status
FROM Orders o
JOIN Customers c ON o.customerID = c.customerID
JOIN OrderDetails od ON o.orderID = od.orderID
JOIN Products p ON od.productID = p.productID;
```

1. “CustomerInfo” VIEW’ini silen bir SQL sorgusu yazınız.

```sql
DROP VIEW IF EXISTS CustomerInfo;
```

1. Hangi VIEW özelliği, performansı artırmak için kullanılır? (A: Indexed Views, B: Materialized Views, C: Simple Views)

Cevap: B: Materialized Views

### Stored Procedure Soruları

1. Müşteri ID’si parametre olarak alan ve o müşterinin siparişlerini listeleyen bir stored procedure yazınız.

```sql
DELIMITER //CREATE PROCEDURE 
GetCustomerOrders(IN customer_id INT)
BEGIN    SELECT * FROM Orders WHERE customerID = customer_id;
END //DELIMITER ;
```

1. Ürün fiyatını belirli bir yüzde oranında artıran bir stored procedure yazınız. Ürün ID ve artış oranı parametre olarak alınmalıdır.

```sql
DELIMITER //CREATE PROCEDURE 
IncreaseProductPrice(IN product_id INT, IN increase_percentage DECIMAL(5,2))
BEGIN    UPDATE Products
    SET price = price * (1 + increase_percentage/100)
    WHERE productID = product_id;
END //DELIMITER ;
```

1. Belirli bir tarih aralığındaki sipariş sayısını hesaplayan ve OUT parametresi ile döndüren bir stored procedure yazınız.

```sql
DELIMITER //
CREATE PROCEDURE GetOrderCountInDateRange(IN start_date DATE, IN end_date DATE, OUT order_count INT)
BEGIN    SELECT COUNT(*) INTO order_count
    FROM Orders
    WHERE orderDate BETWEEN start_date AND end_date;
END //
DELIMITER ;
```

1. Aşağıdaki prosedür kodundaki hatayı bulunuz:
    
    ```sql
    CREATE PROCEDURE GetTotalPrice(orderID INT)
    BEGIN    DECLARE total DECIMAL(10,2);
        SELECT SUM(quantity * price) FROM OrderDetails WHERE orderID = orderID;
        RETURN total;
    END;
    ```
    
- `orderID = orderID` yerine parametre adını kullanmalı: `orderID = order_id`
- `RETURN` yerine `INTO` ve `OUT` parametre kullanmalı

Düzeltilmiş kod:

```sql
CREATE PROCEDURE GetTotalPrice(IN order_id INT, OUT total DECIMAL(10,2))
BEGIN    SELECT SUM(quantity * price) INTO total
    FROM OrderDetails
    WHERE orderID = order_id;
END;
```

1. Bir stored procedure içinde döngü oluşturmak için hangi kontrol yapısı kullanılır?

Cevap: WHILE, LOOP veya REPEAT kontrol yapıları kullanılır.

### Trigger Soruları

1. “Orders” tablosuna yeni bir sipariş eklendiğinde, “Products” tablosundaki ilgili ürünün stok miktarını azaltan bir trigger yazınız.

```sql
DELIMITER //
CREATE TRIGGER after_order_insert
AFTER INSERT ON OrderDetails
FOR EACH ROWBEGIN    UPDATE Products
    SET stock = stock - NEW.quantity
    WHERE productID = NEW.productID;
END //
DELIMITER ;
```

1. “Employees” tablosundaki bir çalışan silinmeden önce, çalışan bilgilerini “EmployeeArchive” tablosuna aktaran bir trigger yazınız.

```sql
DELIMITER //
CREATE TRIGGER before_employee_delete
BEFORE DELETE ON Employees
FOR EACH ROWBEGIN    INSERT INTO EmployeeArchive
    SELECT * FROM Employees WHERE employeeID = OLD.employeeID;
END //
DELIMITER ;
```

1. “Customers” tablosunda bir müşteri güncellendiğinde, değişiklikleri loglamak için “CustomerLogs” tablosuna kaydeden bir trigger yazınız.

```sql
DELIMITER //
CREATE TRIGGER after_customer_update
AFTER UPDATE ON Customers
FOR EACH ROWBEGIN    INSERT INTO CustomerLogs(customerID, action, actionDate)
    VALUES(NEW.customerID, 'UPDATE', NOW());
END //
DELIMITER ;
```

1. Aşağıdaki trigger kodundaki hatayı bulunuz:
    
    ```sql
    CREATE TRIGGER update_product
    AFTER UPDATE ON Products
    FOR EACH ROWBEGIN    IF NEW.price < 0 THEN        SET NEW.price = 0;
        END IF;
    END;
    ```
    
- `AFTER UPDATE` triggerında `NEW.price` değiştirilemez, bu işlem yalnızca `BEFORE UPDATE` triggerında yapılabilir.

Düzeltilmiş kod:

```sql
CREATE TRIGGER update_product
BEFORE UPDATE ON Products
FOR EACH ROWBEGIN    IF NEW.price < 0 THEN        SET NEW.price = 0;
    END IF;
END;
```

1. Bir tablodaki değişiklikleri takip etmek için hangi tür trigger kullanılmalıdır? (A: BEFORE, B: AFTER, C: INSTEAD OF)

Cevap: B: AFTER

### Fonksiyon Soruları

1. İki sayıyı parametre olarak alan ve aralarındaki farkın mutlak değerini döndüren bir fonksiyon yazınız.

```sql
DELIMITER //
CREATE FUNCTION AbsoluteDifference(num1 INT, num2 INT)
RETURNS INTDETERMINISTIC
BEGIN    RETURN ABS(num1 - num2);
END //DELIMITER ;
```

1. Bir müşteri ID’sini parametre olarak alan ve o müşterinin toplam sipariş tutarını hesaplayan bir fonksiyon yazınız.

```sql
DELIMITER //
CREATE FUNCTION GetCustomerTotalAmount(customer_id INT)
RETURNS DECIMAL(10,2)
READS SQL DATABEGIN    DECLARE total DECIMAL(10,2);
    SELECT SUM(od.quantity * p.price) INTO total
    FROM Orders o
    JOIN OrderDetails od ON o.orderID = od.orderID
    JOIN Products p ON od.productID = p.productID
    WHERE o.customerID = customer_id;
    RETURN IFNULL(total, 0);
END //DELIMITER ;
```

1. Bir metni parametre olarak alan ve metindeki kelime sayısını hesaplayan bir fonksiyon yazınız.

```sql
DELIMITER //
CREATE FUNCTION CountWords(text VARCHAR(1000))
RETURNS INTDETERMINISTIC
BEGIN    DECLARE word_count INT DEFAULT 0;
    DECLARE i INT DEFAULT 1;
    DECLARE state INT DEFAULT 0;
    WHILE i <= LENGTH(text) DO
        IF SUBSTRING(text, i, 1) = ' ' THEN            SET state = 0;
        ELSEIF state = 0 THEN            SET state = 1;
            SET word_count = word_count + 1;
        END IF;
        SET i = i + 1;
    END WHILE;
    RETURN word_count;
END //
DELIMITER ;
```

1. Aşağıdaki fonksiyon kodundaki hatayı bulunuz:
    
    ```sql
    CREATE FUNCTION CalculateTax(price DECIMAL(10,2))
    RETURNS DECIMAL(10,2)
    BEGIN    DECLARE taxRate DECIMAL(4,2);
        SELECT rate INTO taxRate FROM TaxRates WHERE country = 'USA';
        RETURN price * taxRate;
    END;
    ```
    
- Ülke parametresi tanımlanmamış
- TaxRates tablosuna sorgu güvenli değil, rate null olabilir

Düzeltilmiş kod:

```sql
CREATE FUNCTION CalculateTax(price DECIMAL(10,2), country VARCHAR(50))
RETURNS DECIMAL(10,2)
READS SQL DATABEGIN    DECLARE taxRate DECIMAL(4,2) DEFAULT 0;
    SELECT rate INTO taxRate
    FROM TaxRates
    WHERE country = country
    LIMIT 1;
    IF taxRate IS NULL THEN SET taxRate = 0; END IF;
    RETURN price * taxRate;
END;
```

1. Fonksiyonlar ile prosedürler arasındaki temel fark nedir?

Cevap: Fonksiyonlar mutlaka bir değer döndürür ve SELECT sorgularında kullanılabilir. Prosedürler değer döndürmek zorunda değildir ve giriş, çıkış parametreleri alabilir.

### Normalizasyon Sorula

1. Aşağıdaki tabloyu 1NF'ye dönüştürünüz:
    
    
    | öğrenciID | ad | dersler |
    | --- | --- | --- |
    | 1 | Ali | Matematik, Fizik |
    | 2 | Ayşe | Kimya, Biyoloji, Fizik |

**Öğrenciler Tablosu:**

| öğrenciID | ad |
| --- | --- |
| 1 | Ali |
| 2 | Ayşe |

**Öğrenci Dersleri Tablosu:**

| öğrenciID | ders |
| --- | --- |
| 1 | Matematik |
| 1 | Fizik |
| 2 | Kimya |
| 2 | Biyoloji |
| 2 | Fizik |
1. Aşağıdaki 1NF tabloyu 2NF'ye dönüştürünüz:
    
    
    | siparişID | ürünID | müşteriID | ürünFiyatı | müşteriAdresi |
    | --- | --- | --- | --- | --- |
    | 1 | 101 | 1 | 50 | İstanbul |
    | 1 | 102 | 1 | 25 | İstanbul |
    | 2 | 101 | 2 | 50 | Ankara |

**Siparişler Tablosu:**

| siparişID | müşteriID | müşteriAdresi |
| --- | --- | --- |
| 1 | 1 | İstanbul |
| 2 | 2 | Ankara |

**Sipariş Detayları Tablosu:**

| siparişID | ürünID | ürünFiyatı |
| --- | --- | --- |
| 1 | 101 | 50 |
| 1 | 102 | 25 |
| 2 | 101 | 50 |

**Ürünler Tablosu:**

| ürünID | ürünFiyatı |
| --- | --- |
| 101 | 50 |
| 102 | 25 |
1. Aşağıdaki 2NF tabloyu 3NF'ye dönüştürünüz:
    
    
    | öğrenciID | adSoyad | bölümID | bölümAdı | bölümBaşkanı |
    | --- | --- | --- | --- | --- |
    | 1 | Ali Yılmaz | 10 | Bilgisayar Müh. | Prof. Ahmet |
    | 2 | Ayşe Demir | 20 | Elektrik Müh. | Prof. Mehmet |
    | 3 | Can Öztürk | 10 | Bilgisayar Müh. | Prof. Ahmet |

**Öğrenciler Tablosu:**

| öğrenciID | adSoyad | bölümID |
| --- | --- | --- |
| 1 | Ali Yılmaz | 10 |
| 2 | Ayşe Demir | 20 |
| 3 | Can Öztürk | 10 |

**Bölümler Tablosu:**

| bölümID | bölümAdı | bölümBaşkanı |
| --- | --- | --- |
| 10 | Bilgisayar Müh. | Prof. Ahmet |
| 20 | Elektrik Müh. | Prof. Mehmet |
1. Veritabanı normalizasyonunun amacı nedir?

Cevap: Veritabanı normalizasyonunun amacı veri tekrarını azaltmak, veri bütünlüğünü sağlamak ve daha etkili bir veri modeli oluşturmaktır.

1. İkinci Normal Form (2NF) için doğru olan ifade hangisidir?
A) Her sütun atomik değerler içermelidir
B) Anahtar olmayan her sütun, anahtar sütunların tamamına tam bağımlı olmalıdır
C) Anahtar olmayan sütunlar arasında geçişli bağımlılık olmamalıdır

Cevap: B) Anahtar olmayan her sütun, anahtar sütunların tamamına tam bağımlı olmalıdır 1. Aşağıdaki tabloyu 1NF'ye dönüştürünüz:

| öğrenciID | ad | dersler |
| --- | --- | --- |
| 1 | Ali | Matematik, Fizik |
| 2 | Ayşe | Kimya, Biyoloji, Fizik |

**Öğrenciler Tablosu:**

| öğrenciID | ad |
| --- | --- |
| 1 | Ali |
| 2 | Ayşe |

**Öğrenci Dersleri Tablosu:**

| öğrenciID | ders |
| --- | --- |
| 1 | Matematik |
| 1 | Fizik |
| 2 | Kimya |
| 2 | Biyoloji |
| 2 | Fizik |
1. Aşağıdaki 1NF tabloyu 2NF'ye dönüştürünüz:
    
    
    | siparişID | ürünID | müşteriID | ürünFiyatı | müşteriAdresi |
    | --- | --- | --- | --- | --- |
    | 1 | 101 | 1 | 50 | İstanbul |
    | 1 | 102 | 1 | 25 | İstanbul |
    | 2 | 101 | 2 | 50 | Ankara |

**Siparişler Tablosu:**

| siparişID | müşteriID | müşteriAdresi |
| --- | --- | --- |
| 1 | 1 | İstanbul |
| 2 | 2 | Ankara |

**Sipariş Detayları Tablosu:**

| siparişID | ürünID | ürünFiyatı |
| --- | --- | --- |
| 1 | 101 | 50 |
| 1 | 102 | 25 |
| 2 | 101 | 50 |

**Ürünler Tablosu:**

| ürünID | ürünFiyatı |
| --- | --- |
| 101 | 50 |
| 102 | 25 |
1. Aşağıdaki 2NF tabloyu 3NF'ye dönüştürünüz:
    
    
    | öğrenciID | adSoyad | bölümID | bölümAdı | bölümBaşkanı |
    | --- | --- | --- | --- | --- |
    | 1 | Ali Yılmaz | 10 | Bilgisayar Müh. | Prof. Ahmet |
    | 2 | Ayşe Demir | 20 | Elektrik Müh. | Prof. Mehmet |
    | 3 | Can Öztürk | 10 | Bilgisayar Müh. | Prof. Ahmet |

**Öğrenciler Tablosu:**

| öğrenciID | adSoyad | bölümID |
| --- | --- | --- |
| 1 | Ali Yılmaz | 10 |
| 2 | Ayşe Demir | 20 |
| 3 | Can Öztürk | 10 |

**Bölümler Tablosu:**

| bölümID | bölümAdı | bölümBaşkanı |
| --- | --- | --- |
| 10 | Bilgisayar Müh. | Prof. Ahmet |
| 20 | Elektrik Müh. | Prof. Mehmet |
1. Veritabanı normalizasyonunun amacı nedir?

Cevap: Veritabanı normalizasyonunun amacı veri tekrarını azaltmak, veri bütünlüğünü sağlamak ve daha etkili bir veri modeli oluşturmaktır.

1. İkinci Normal Form (2NF) için doğru olan ifade hangisidir?
A) Her sütun atomik değerler içermelidir
B) Anahtar olmayan her sütun, anahtar sütunların tamamına tam bağımlı olmalıdır
C) Anahtar olmayan sütunlar arasında geçişli bağımlılık olmamalıdır

Cevap: B) Anahtar olmayan her sütun, anahtar sütunların tamamına tam bağımlı olmalıdır