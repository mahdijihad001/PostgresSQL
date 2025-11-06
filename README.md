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

## Alter Table Commands

* `ALTER TABLE oldTableName RENAME TO newTableName;` : Table-এর নাম পরিবর্তন।
* `ALTER TABLE tableName ADD COLUMN columnName VARCHAR(20);` : নতুন column যোগ।
* `ALTER TABLE tableName RENAME COLUMN oldColumn TO newColumn;` : Column-এর নাম পরিবর্তন।
* `ALTER TABLE tableName ALTER COLUMN columnName TYPE VARCHAR(30);` : Column-এর data type পরিবর্তন।

## Data Insert Command

* `INSERT INTO tableName (column1, column2, ...) VALUES (value1, value2, ...);` : Table-এ ডেটা যোগ।
  উদাহরণ:

  ```sql
  INSERT INTO class_info (className, email, totalStudent, passedStudent, failedStudent)
  VALUES ('ClassTen1', 'classten@gmail.com', 10, 6, 2);
  ```

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
