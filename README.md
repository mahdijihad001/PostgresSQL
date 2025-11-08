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

* `SELECT * FROM students;` : কোনো টেবিলের সব ডেটা দেখতে।  
* `SELECT first_name AS "First Name", age AS "Age" FROM students;` : নির্দিষ্ট ফিল্ড ও এলিয়াস (Alias) সহ ডেটা দেখা।  
* `SELECT first_name AS "First Name", age AS "Age" FROM students ORDER BY age DESC;` : বয়স অনুযায়ী বড় থেকে ছোট ক্রমে সাজানো (DESC মানে: বড় থেকে ছোট)।  
* `SELECT first_name AS "First Name", age AS "Age" FROM students ORDER BY age ASC;` : বয়স অনুযায়ী ছোট থেকে বড় ক্রমে সাজানো (ASC মানে: ছোট থেকে বড়)।  
* `SELECT DISTINCT fieldName FROM tableName;` : কোনো ফিল্ডের অনন্য মান (unique values) দেখা।  
* `SELECT DISTINCT country FROM students;` : সব দেশের নাম শুধু একবার করে দেখাবে।  
* `SELECT * FROM tableName WHERE fieldName = 'value';` : নির্দিষ্ট মান অনুসারে ফিল্টার করা।  
* `SELECT * FROM students WHERE student_id = 10;` : student_id ১০ এমন রেকর্ড দেখাবে।  
* `SELECT * FROM students WHERE course = 'MERN';` : শুধুমাত্র MERN কোর্স করা শিক্ষার্থীদের দেখাবে।  
* `SELECT * FROM tableName WHERE condition1 OR condition2;` : দুটি শর্তের মধ্যে যেকোনো একটি সত্য হলে ডেটা দেখাবে।  
* `SELECT * FROM students WHERE course = 'MERN' OR course = 'Full Stack';` : যারা MERN বা Full Stack কোর্স করছে তাদের ডেটা দেখাবে।  
* `SELECT * FROM tableName WHERE condition1 AND condition2;` : দুটি শর্তই সত্য হতে হবে।  
* `SELECT * FROM students WHERE (country = 'UK') AND (grade = 'B');` : যারা UK থেকে এবং গ্রেড B পেয়েছে।  
* `SELECT * FROM students WHERE (country = 'UK' OR country = 'Canada') AND (grade = 'B' OR grade = 'A');` : যারা UK বা Canada থেকে এবং গ্রেড A বা B পেয়েছে।  
* `SELECT * FROM tableName WHERE columnName IN (value1, value2, value3);` : নির্দিষ্ট মানগুলোর মধ্যে যেকোনো একটি হলে ডেটা দেখাবে।  
* `SELECT * FROM students WHERE country IN ('UK', 'Canada') AND grade IN ('B', 'A');` : যারা UK বা Canada থেকে এবং গ্রেড A বা B পেয়েছে।  
* `SELECT * FROM tableName WHERE columnName != 'value';` : নির্দিষ্ট মান বাদ দিয়ে বাকি সব ডেটা দেখাবে।  
* `SELECT * FROM students WHERE country != 'UK';` : UK ছাড়া অন্য সব দেশের শিক্ষার্থী।  
* `SELECT * FROM students WHERE country NOT IN ('UK', 'USA');` : UK ও USA ছাড়া অন্য দেশের শিক্ষার্থী দেখাবে।  
* `SELECT * FROM tableName WHERE columnName BETWEEN startValue AND endValue;` : নির্দিষ্ট রেঞ্জের (পরিসীমার) মধ্যে ডেটা দেখাবে।  
* `SELECT * FROM students WHERE age BETWEEN 20 AND 25;` : ২০ থেকে ২৫ বছর বয়সী শিক্ষার্থী।  
* `SELECT * FROM employees WHERE salary BETWEEN 20000 AND 50000;` : যাদের বেতন ২০,০০০ থেকে ৫০,০০০ টাকার মধ্যে।
* `SELECT * FROM tableName WHERE fieldName LIKE 'A%';` : LIKE case-sensitive সার্চ করে — এখানে যেসব মান A দিয়ে শুরু হয় (যেমন Amin, Anik), সেগুলো দেখাবে।
* `SELECT * FROM tableName WHERE fieldName ILIKE 'A%';` : ILIKE case-insensitive সার্চ করে — এখানে A বড় হোক বা ছোট (A বা a), দুই ক্ষেত্রেই মিলে যাবে (যেমন Anik, anik)।
* `SELECT UPPER(first_name) FROM students;` : first_name কলামের সব অক্ষর বড় হরফে (Uppercase) দেখাবে। উদাহরণ: যদি নাম থাকে anik, তাহলে দেখাবে ANIK।
* `SELECT LOWER(first_name) FROM students;` : first_name কলামের সব অক্ষর ছোট হরফে (Lowercase) দেখাবে। উদাহরণ: যদি নাম থাকে ANIK, তাহলে দেখাবে anik।
* `SELECT LENGTH(first_name) FROM students;` : first_name কলামের প্রতিটি মানের অক্ষরের সংখ্যা দেখাবে। উদাহরণ: যদি নাম হয় Anik, তাহলে ফলাফল হবে 4।
* `SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM students;` : দুইটি কলাম একত্রে যোগ করে (concatenate) একটি নতুন কলাম তৈরি করবে। উদাহরণ: first_name = 'Anik' এবং last_name = 'Hasan' হলে দেখাবে Anik Hasan।

## Aggregate Functions

* `SELECT AVG(age) FROM students;` : সব age-এর গড় (average) দেখাবে।
* `SELECT MAX(age) FROM students;` : সবচেয়ে বড় age মান দেখাবে।
* `SELECT MIN(age) FROM students;` : সবচেয়ে ছোট age মান দেখাবে।
* `SELECT SUM(age) FROM students;` : সব age মান যোগফল (sum) দেখাবে।
* `SELECT COUNT(age) FROM students;` : কতজনের age আছে (non-null rows) তা গণনা করে দেখাবে।

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
