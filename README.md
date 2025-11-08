# PostgreSQL Commands Guide

## Database Commands

* `\l` : সার্ভারে কয়টা database আছে তা দেখাবে।
* `\conninfo` : তুমি কোন database-এ connected আছো তা দেখাবে।
* `\c databaseName` : অন্য database-এ connect হতে ব্যবহার হয়।
* `CREATE DATABASE databaseName;` : নতুন database তৈরি করতে ব্যবহৃত হয়।

## Table Commands

* `\dt` : বর্তমান database-এ কয়টা table আছে তা দেখাবে।
* `CREATE TABLE tableName (...);` : নতুন table তৈরি করতে ব্যবহৃত হয়।
  উদাহরণ:

  ```sql
  CREATE TABLE school_info (
    id SERIAL PRIMARY KEY,
    schoolName VARCHAR(50),
    schoolAge INT CHECK (schoolAge >= 30),
    email VARCHAR(50) UNIQUE NOT NULL,
    dob DATE,
    isActive BOOLEAN DEFAULT TRUE
  );
  ```
* `DROP TABLE tableName;` : কোনো table মুছে ফেলতে ব্যবহার হয়।
* `SELECT * FROM tableName;` : table-এর সব ডেটা দেখতে।



## Data Insert Command

* `INSERT INTO tableName (column1, column2, ...) VALUES (value1, value2, ...);` : Table-এ ডেটা যোগ।
  উদাহরণ:

  ```sql
  INSERT INTO class_info (className, email, totalStudent, passedStudent, failedStudent)
  VALUES ('ClassTen1', 'classten@gmail.com', 10, 6, 2);
  ```


## Alter Table Commands

* `ALTER TABLE oldTableName RENAME TO newTableName;` : Table-এর নাম পরিবর্তন।
* `ALTER TABLE tableName ADD COLUMN columnName VARCHAR(20);` : নতুন column যোগ।
* `ALTER TABLE tableName RENAME COLUMN oldColumn TO newColumn;` : Column-এর নাম পরিবর্তন।
* `ALTER TABLE tableName ALTER COLUMN columnName TYPE VARCHAR(30);` : Column-এর data type পরিবর্তন।
* `ALTER TABLE employee ALTER salary SET DEFAULT 20000;` : কোনো field-এ default value সেট করা।
* `ALTER TABLE employee ALTER salary DROP DEFAULT;` : কোনো field-এর default value মুছে ফেলা।
* `ALTER TABLE employee ADD CONSTRAINT unique_employee_email UNIQUE(email);` : কোনো field-এ unique constraint যোগ করা (এখানে `unique_employee_email` হলো constraint নাম)।
* `ALTER TABLE employee DROP CONSTRAINT employee_email_key;` : email-এর unique constraint মুছে ফেলা।
* `ALTER TABLE employee ADD CONSTRAINT pk_employee_id PRIMARY KEY(id);` : কোনো field-কে primary key বানানো (এখানে `pk_employee_id` হলো primary key constraint নাম)।
* `ALTER TABLE employee DROP CONSTRAINT employee_pkey;` : primary key constraint মুছে ফেলা।

## SELECT Commands

### ১️⃣ সব ডেটা দেখা
```sql
SELECT * FROM students;
```
**ব্যাখ্যা:** কোনো টেবিলের সব ডেটা দেখতে।

---

### ২️⃣ নির্দিষ্ট ফিল্ড ও এলিয়াস সহ দেখা
```sql
SELECT first_name AS "First Name", age AS "Age" FROM students;
```
**ব্যাখ্যা:** নির্দিষ্ট কলাম বেছে নিয়ে এলিয়াস (Alias) ব্যবহার করে সুন্দরভাবে দেখা।

---

### ৩️⃣ ডেটা বড় থেকে ছোট (Descending) ক্রমে সাজানো
```sql
SELECT first_name AS "First Name", age AS "Age" FROM students ORDER BY age DESC;
```
**DESC মানে:** বড় থেকে ছোট।

---

### ৪️⃣ ডেটা ছোট থেকে বড় (Ascending) ক্রমে সাজানো
```sql
SELECT first_name AS "First Name", age AS "Age" FROM students ORDER BY age ASC;
```
**ASC মানে:** ছোট থেকে বড়।

---

### ৫️⃣ অনন্য মান (Unique values) দেখা
```sql
SELECT DISTINCT fieldName FROM tableName;
```
**উদাহরণ:**
```sql
SELECT DISTINCT country FROM students;
```
**ফলাফল:** সব দেশের নাম শুধু একবার করে দেখাবে।

---

### ৬️⃣ নির্দিষ্ট মান অনুসারে ফিল্টার করা (WHERE)
```sql
SELECT * FROM tableName WHERE fieldName = 'value';
```
**উদাহরণ:**
```sql
SELECT * FROM students WHERE student_id = 10;
SELECT * FROM students WHERE course = 'MERN';
```

---

### ৭️⃣ অথবা কন্ডিশন (OR)
```sql
SELECT * FROM tableName WHERE condition1 OR condition2;
```
**উদাহরণ:**
```sql
SELECT * FROM students WHERE course = 'MERN' OR course = 'Full Stack';
```
**ফলাফল:** যারা MERN অথবা Full Stack কোর্স করছে।

---

### ৮️⃣ এবং কন্ডিশন (AND)
```sql
SELECT * FROM tableName WHERE condition1 AND condition2;
```
**উদাহরণ:**
```sql
SELECT * FROM students WHERE (country = 'UK') AND (grade = 'B');
```
**ফলাফল:** যারা UK থেকে এবং গ্রেড B পেয়েছে।

---

### ৯️⃣ একাধিক কন্ডিশন (AND + OR)
```sql
SELECT * FROM students WHERE (country = 'UK' OR country = 'Canada') AND (grade = 'B' OR grade = 'A');
```
**ফলাফল:** যারা UK অথবা Canada থেকে এবং গ্রেড A অথবা B পেয়েছে।

---

### 🔟 IN অপারেটর (সহজভাবে একাধিক মান চেক করা)
```sql
SELECT * FROM tableName WHERE columnName IN (value1, value2, value3);
```
**উদাহরণ:**
```sql
SELECT * FROM students WHERE country IN ('UK', 'Canada') AND grade IN ('B', 'A');
```
**ফলাফল:** একই ফলাফল কিন্তু লেখা আরও সহজ।

---

### ১১️⃣ NOT EQUAL (≠) কন্ডিশন
```sql
SELECT * FROM tableName WHERE columnName != 'value';
```
**উদাহরণ:**
```sql
SELECT * FROM students WHERE country != 'UK';
```
**ফলাফল:** UK ছাড়া অন্য সব দেশের শিক্ষার্থী।

---

### ১২️⃣ NOT IN — একাধিক মান বাদ দেওয়া
```sql
SELECT * FROM students WHERE country NOT IN ('UK', 'USA');
```
**ফলাফল:** UK এবং USA ছাড়া অন্য দেশের শিক্ষার্থী।

---

### ১৩️⃣ BETWEEN — রেঞ্জ নির্ধারণ করা
```sql
SELECT * FROM tableName WHERE columnName BETWEEN startValue AND endValue;
```
**উদাহরণ:**
```sql
SELECT * FROM students WHERE age BETWEEN 20 AND 25;
```
**ফলাফল:** যারা ২০ থেকে ২৫ বছর বয়সী তারা দেখাবে (২০ ও ২৫ সহ)।

**আরও উদাহরণ:**
```sql
SELECT * FROM employees WHERE salary BETWEEN 20000 AND 50000;
```

---


## System Commands

* `\du` : সার্ভারে কয়টা user আছে তা দেখাবে।
* `SELECT version();` : PostgreSQL-এর version দেখাবে।
* `SELECT current_date;` : আজকের তারিখ দেখাবে।
* `\! cls` বা `\! clear` : Command line screen পরিষ্কার করতে।

## PSQL Shell from Other Terminal

* `psql -U postgres -d postgres` : অন্য terminal থেকে psql চালানোর জন্য।

  * `-U` : কোন user দিয়ে connect হবে।
  * `-d` : কোন database-এ connect হবে।

### PATH Error Fix

যদি error আসে যেমন:

```
'psql' is not recognized as the name of a cmdlet...
```

তাহলে PostgreSQL-এর path environment variable-এ যোগ করতে হবে:

1. “This PC” → `C:\Program Files\PostgreSQL\<version>\bin` এ যাও।
2. ঐ path কপি করো।
3. Windows search-এ "Environment Variables" → Path → Edit → New → Paste path।
4. Save করে টার্মিনাল রিস্টার্ট।
5. এখন `psql -U postgres` কাজ করবে।
