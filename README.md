# PostgreSQL ডাটাবেস কমান্ড গাইড

এই গাইডে PostgreSQL ডাটাবেসের সকল প্রয়োজনীয় কমান্ড এবং SELECT query সম্পর্কে বিস্তারিত আলোচনা করা হয়েছে। প্রতিটি কমান্ডের সাথে উদাহরণ দেওয়া হয়েছে।

---

## ১. ডাটাবেস কমান্ড (Database Commands)

### ডাটাবেস দেখা
\`\`\`sql
\l
\`\`\`
**ব্যবহার:** সার্ভারে কয়টা ডাটাবেস আছে তা দেখাবে।

### বর্তমান সংযোগ তথ্য দেখা
\`\`\`sql
\conninfo
\`\`\`
**ব্যবহার:** তুমি কোন ডাটাবেসে সংযুক্ত আছো তা দেখাবে।

### অন্য ডাটাবেসে সংযোগ
\`\`\`sql
\c databaseName
\`\`\`
**উদাহরণ:**
\`\`\`sql
\c myschool
\`\`\`
**ব্যবহার:** অন্য ডাটাবেসে সংযোগ হতে ব্যবহৃত হয়।

### নতুন ডাটাবেস তৈরি
\`\`\`sql
CREATE DATABASE databaseName;
\`\`\`
**উদাহরণ:**
\`\`\`sql
CREATE DATABASE school_db;
\`\`\`
**ব্যবহার:** নতুন ডাটাবেস তৈরি করতে ব্যবহৃত হয়।

---

## ২. টেবিল কমান্ড (Table Commands)

### সব টেবিল দেখা
\`\`\`sql
\dt
\`\`\`
**ব্যবহার:** বর্তমান ডাটাবেসে কয়টা টেবিল আছে তা দেখাবে।

### নতুন টেবিল তৈরি
\`\`\`sql
CREATE TABLE tableName (...);
\`\`\`

**উদাহরণ:**
\`\`\`sql
CREATE TABLE school_info (
  id SERIAL PRIMARY KEY,
  schoolName VARCHAR(50),
  schoolAge INT CHECK (schoolAge >= 30),
  email VARCHAR(50) UNIQUE NOT NULL,
  dob DATE,
  isActive BOOLEAN DEFAULT TRUE
);
\`\`\`

**টেবিল কলাম ব্যাখ্যা:**
- `id SERIAL PRIMARY KEY` - অটো ইনক্রিমেন্ট প্রাথমিক চাবি
- `schoolName VARCHAR(50)` - সর্বোচ্চ ৫০ অক্ষরের টেক্সট
- `schoolAge INT CHECK (schoolAge >= 30)` - পূর্ণ সংখ্যা, কমপক্ষে ৩০ হতে হবে
- `email VARCHAR(50) UNIQUE NOT NULL` - অনন্য এবং বাধ্যতামূলক ইমেইল
- `dob DATE` - তারিখ ফরম্যাট
- `isActive BOOLEAN DEFAULT TRUE` - সত্য/মিথ্যা, ডিফল্ট সত্য

### টেবিল মুছে ফেলা
\`\`\`sql
DROP TABLE tableName;
\`\`\`
**উদাহরণ:**
\`\`\`sql
DROP TABLE school_info;
\`\`\`
**ব্যবহার:** কোনো টেবিল মুছে ফেলতে ব্যবহার হয়।

---

## ৩. ডেটা ইনসার্ট কমান্ড (Data Insert Commands)

### টেবিলে ডেটা যোগ করা
\`\`\`sql
INSERT INTO tableName (column1, column2, ...) VALUES (value1, value2, ...);
\`\`\`

**উদাহরণ:**
\`\`\`sql
INSERT INTO class_info (className, email, totalStudent, passedStudent, failedStudent)
VALUES ('ClassTen1', 'classten@gmail.com', 10, 6, 2);
\`\`\`

**আরও উদাহরণ:**
\`\`\`sql
INSERT INTO students (firstName, age, country, grade)
VALUES ('রহিম', 22, 'Bangladesh', 'A');

INSERT INTO students (firstName, age, country, grade)
VALUES ('করিম', 20, 'UK', 'B');
\`\`\`

---

## ৪. টেবিল পরিবর্তন কমান্ড (ALTER TABLE Commands)

### টেবিলের নাম পরিবর্তন
\`\`\`sql
ALTER TABLE oldTableName RENAME TO newTableName;
\`\`\`
**উদাহরণ:**
\`\`\`sql
ALTER TABLE school_info RENAME TO school_details;
\`\`\`

### নতুন কলাম যোগ করা
\`\`\`sql
ALTER TABLE tableName ADD COLUMN columnName VARCHAR(20);
\`\`\`
**উদাহরণ:**
\`\`\`sql
ALTER TABLE students ADD COLUMN phone VARCHAR(11);
\`\`\`

### কলামের নাম পরিবর্তন
\`\`\`sql
ALTER TABLE tableName RENAME COLUMN oldColumn TO newColumn;
\`\`\`
**উদাহরণ:**
\`\`\`sql
ALTER TABLE students RENAME COLUMN firstName TO first_name;
\`\`\`

### কলামের ডেটা টাইপ পরিবর্তন
\`\`\`sql
ALTER TABLE tableName ALTER COLUMN columnName TYPE VARCHAR(30);
\`\`\`
**উদাহরণ:**
\`\`\`sql
ALTER TABLE students ALTER COLUMN address TYPE VARCHAR(100);
\`\`\`

### কলামে ডিফল্ট মান সেট করা
\`\`\`sql
ALTER TABLE tableName ALTER COLUMN columnName SET DEFAULT value;
\`\`\`
**উদাহরণ:**
\`\`\`sql
ALTER TABLE employee ALTER salary SET DEFAULT 20000;
\`\`\`

### ডিফল্ট মান মুছে ফেলা
\`\`\`sql
ALTER TABLE tableName ALTER COLUMN columnName DROP DEFAULT;
\`\`\`
**উদাহরণ:**
\`\`\`sql
ALTER TABLE employee ALTER salary DROP DEFAULT;
\`\`\`

### Unique Constraint যোগ করা
\`\`\`sql
ALTER TABLE tableName ADD CONSTRAINT constraintName UNIQUE(columnName);
\`\`\`
**উদাহরণ:**
\`\`\`sql
ALTER TABLE employee ADD CONSTRAINT unique_employee_email UNIQUE(email);
\`\`\`

### Constraint মুছে ফেলা
\`\`\`sql
ALTER TABLE tableName DROP CONSTRAINT constraintName;
\`\`\`
**উদাহরণ:**
\`\`\`sql
ALTER TABLE employee DROP CONSTRAINT employee_email_key;
\`\`\`

### Primary Key সেট করা
\`\`\`sql
ALTER TABLE tableName ADD CONSTRAINT constraintName PRIMARY KEY(columnName);
\`\`\`
**উদাহরণ:**
\`\`\`sql
ALTER TABLE employee ADD CONSTRAINT pk_employee_id PRIMARY KEY(id);
\`\`\`

### Primary Key মুছে ফেলা
\`\`\`sql
ALTER TABLE tableName DROP CONSTRAINT tableName_pkey;
\`\`\`
**উদাহরণ:**
\`\`\`sql
ALTER TABLE employee DROP CONSTRAINT employee_pkey;
\`\`\`

---

## ৫. SELECT কমান্ড (SELECT Commands)

### সব ডেটা দেখা
\`\`\`sql
SELECT * FROM tableName;
\`\`\`
**উদাহরণ:**
\`\`\`sql
SELECT * FROM students;
\`\`\`

### নির্দিষ্ট কলাম এবং এলিয়াস সহ ডেটা দেখা
\`\`\`sql
SELECT column1 AS "Alias1", column2 AS "Alias2" FROM tableName;
\`\`\`
**উদাহরণ:**
\`\`\`sql
SELECT first_name AS "নাম", age AS "বয়স" FROM students;
\`\`\`

### ডেটা বড় থেকে ছোট ক্রমে সাজানো (Descending)
\`\`\`sql
SELECT * FROM tableName ORDER BY columnName DESC;
\`\`\`
**উদাহরণ:**
\`\`\`sql
SELECT first_name AS "First Name", age AS "Age" FROM students ORDER BY age DESC;
\`\`\`
**ফলাফল:** সবচেয়ে বয়স্ক শিক্ষার্থী থেকে শুরু হবে।

### ডেটা ছোট থেকে বড় ক্রমে সাজানো (Ascending)
\`\`\`sql
SELECT * FROM tableName ORDER BY columnName ASC;
\`\`\`
**উদাহরণ:**
\`\`\`sql
SELECT first_name AS "First Name", age AS "Age" FROM students ORDER BY age ASC;
\`\`\`
**ফলাফল:** সবচেয়ে কম বয়স্ক শিক্ষার্থী থেকে শুরু হবে।

---

## ৬. ফিল্টারিং কমান্ড (Filtering Commands)

### Distinct - অনন্য মান খুঁজা
যদি কোনো ফিল্ডে একই ধরনের ডেটা থাকে এবং আমরা শুধু অনন্য মানগুলো দেখতে চাই:

\`\`\`sql
SELECT DISTINCT fieldName FROM tableName;
\`\`\`
**উদাহরণ:**
\`\`\`sql
SELECT DISTINCT country FROM students;
\`\`\`
**ফলাফল:** সব দেশের নাম শুধু একবার করে দেখাবে।

### সিঙ্গেল ভ্যালু ফিল্টার করা (WHERE)
একটি নির্দিষ্ট মানের ভিত্তিতে ডেটা খুঁজা:

\`\`\`sql
SELECT * FROM tableName WHERE fieldName = 'value';
\`\`\`
**উদাহরণ:**
\`\`\`sql
SELECT * FROM students WHERE student_id = 10;
\`\`\`

**আরও উদাহরণ:**
\`\`\`sql
SELECT * FROM students WHERE course = 'MERN';
\`\`\`

### অথবা কন্ডিশন (OR)
দুটি বা তার বেশি শর্তের মধ্যে যেকোনো একটি সত্য হলে:

\`\`\`sql
SELECT * FROM tableName WHERE condition1 OR condition2;
\`\`\`
**উদাহরণ:**
\`\`\`sql
SELECT * FROM students WHERE course = 'MERN' OR course = 'Full Stack';
\`\`\`
**ফলাফল:** যারা MERN অথবা Full Stack কোর্স করছে তাদের সব তথ্য।

### এবং কন্ডিশন (AND)
দুটি বা তার বেশি শর্ত সবগুলো সত্য হতে হবে:

\`\`\`sql
SELECT * FROM tableName WHERE condition1 AND condition2;
\`\`\`
**উদাহরণ:**
\`\`\`sql
SELECT * FROM students WHERE (country = 'UK') AND (grade = 'B');
\`\`\`
**ফলাফল:** যারা UK থেকে এবং গ্রেড B পেয়েছে শুধু তারা দেখাবে।

### একাধিক কন্ডিশন সহ OR এবং AND
\`\`\`sql
SELECT * FROM students WHERE (country = 'UK' OR country = 'Canada') AND (grade = 'B' OR grade = 'A');
\`\`\`
**ফলাফল:** যারা UK অথবা Canada থেকে এবং গ্রেড A অথবা B পেয়েছে।

### IN অপারেটর ব্যবহার করে (সহজ পদ্ধতি)
\`\`\`sql
SELECT * FROM tableName WHERE columnName IN (value1, value2, value3);
\`\`\`
**উদাহরণ:**
\`\`\`sql
SELECT * FROM students WHERE country IN ('UK', 'Canada') AND grade IN ('B', 'A');
\`\`\`
**ফলাফল:** একই ফলাফল কিন্তু লেখা আরও সহজ।

### নয় কন্ডিশন (NOT EQUAL)
নির্দিষ্ট মান বাদ দিয়ে বাকি সব:

\`\`\`sql
SELECT * FROM tableName WHERE columnName != 'value';
\`\`\`
**উদাহরণ:**
\`\`\`sql
SELECT * FROM students WHERE country != 'UK';
\`\`\`
**ফলাফল:** UK ছাড়া অন্য সব দেশের শিক্ষার্থী দেখাবে।

### একাধিক ফিল্ড এক্সক্লুড করা (NOT IN)
\`\`\`sql
SELECT * FROM students WHERE country NOT IN ('UK', 'USA');
\`\`\`
**ফলাফল:** UK এবং USA ছাড়া অন্য সব দেশের শিক্ষার্থী।

### বিটুইন (BETWEEN) - রেঞ্জ নির্ধারণ
নির্দিষ্ট পরিসীমার ভেতরে ডেটা খুঁজা:

\`\`\`sql
SELECT * FROM tableName WHERE columnName BETWEEN startValue AND endValue;
\`\`\`
**উদাহরণ:**
\`\`\`sql
SELECT * FROM students WHERE age BETWEEN 20 AND 25;
\`\`\`
**ফলাফল:** যারা ২০ থেকে ২৫ বছর বয়সী তারা দেখাবে (২০ এবং ২৫ উভয়ই অন্তর্ভুক্ত)।

**আরও উদাহরণ:**
\`\`\`sql
SELECT * FROM employees WHERE salary BETWEEN 20000 AND 50000;
\`\`\`

---

## ৭. সিস্টেম কমান্ড (System Commands)

### সব ব্যবহারকারী দেখা
\`\`\`sql
\du
\`\`\`
**ব্যবহার:** সার্ভারে কয়টা ব্যবহারকারী আছে তা দেখাবে।

### PostgreSQL সংস্করণ দেখা
\`\`\`sql
SELECT version();
\`\`\`
**ব্যবহার:** PostgreSQL-এর সংস্করণ দেখাবে।

### আজকের তারিখ দেখা
\`\`\`sql
SELECT current_date;
\`\`\`
**ব্যবহার:** আজকের তারিখ দেখাবে।

### স্ক্রিন পরিষ্কার করা
\`\`\`
\! cls
\`\`\`
(Windows এ)

\`\`\`
\! clear
\`\`\`
(Mac/Linux এ)
**ব্যবহার:** কমান্ড লাইন স্ক্রিন পরিষ্কার করতে।

---

## ৮. অন্য টার্মিনাল থেকে PSQL চালানো (PSQL Shell from Other Terminal)

### psql চালু করা
\`\`\`bash
psql -U postgres -d postgres
\`\`\`

**অপশন ব্যাখ্যা:**
- `-U` : কোন ব্যবহারকারী দিয়ে সংযোগ হবে
- `-d` : কোন ডাটাবেসে সংযোগ হবে

**উদাহরণ:**
\`\`\`bash
psql -U postgres -d school_db
\`\`\`

---

## ৯. PATH ত্রুটি সমাধান (PATH Error Fix)

যদি এই ত্রুটি আসে:
\`\`\`
'psql' is not recognized as the name of a cmdlet...
\`\`\`

**সমাধান:**

1. **PostgreSQL বিন ফোল্ডার খুঁজুন:**
   - `This PC` → `C:\Program Files\PostgreSQL\<version>\bin` এ যান

2. **পাথ কপি করুন**

3. **এনভায়রনমেন্ট ভ্যারিয়েবল যোগ করুন:**
   - Windows Search-এ "Environment Variables" খুঁজুন
   - → "Edit the system environment variables" ক্লিক করুন
   - → "Environment Variables" বাটন ক্লিক করুন
   - → Path → Edit → New
   - → কপি করা পাথ পেস্ট করুন
   - → OK করুন

4. **টার্মিনাল রিস্টার্ট করুন**

5. **এখন এটি কাজ করবে:**
   \`\`\`bash
   psql -U postgres
   \`\`\`

---

## ১০. কমপ্লিট প্র্যাক্টিক্যাল উদাহরণ

### উদাহরণ ১: শিক্ষার্থী টেবিল তৈরি এবং ডেটা যোগ করা

\`\`\`sql
-- টেবিল তৈরি
CREATE TABLE students (
  id SERIAL PRIMARY KEY,
  first_name VARCHAR(50) NOT NULL,
  age INT CHECK (age >= 5),
  country VARCHAR(50),
  grade VARCHAR(2),
  course VARCHAR(50)
);

-- ডেটা যোগ
INSERT INTO students (first_name, age, country, grade, course)
VALUES ('রহিম', 22, 'Bangladesh', 'A', 'MERN');

INSERT INTO students (first_name, age, country, grade, course)
VALUES ('করিম', 20, 'UK', 'B', 'Full Stack');

INSERT INTO students (first_name, age, country, grade, course)
VALUES ('সারা', 23, 'Canada', 'A', 'MERN');

INSERT INTO students (first_name, age, country, grade, course)
VALUES ('নাজমা', 21, 'USA', 'A', 'Frontend');

-- সব ডেটা দেখা
SELECT * FROM students;

-- দেশ অনুযায়ী ডেটা দেখা
SELECT DISTINCT country FROM students;

-- যারা MERN করছে তাদের দেখা
SELECT * FROM students WHERE course = 'MERN';

-- যারা A গ্রেড পেয়েছে এবং Bangladesh থেকে
SELECT * FROM students WHERE grade = 'A' AND country = 'Bangladesh';

-- বয়স অনুযায়ী সাজানো
SELECT * FROM students ORDER BY age DESC;
\`\`\`

---

## সারসংক্ষেপ

এই গাইডে আপনি শিখেছেন:
- ডাটাবেস তৈরি এবং পরিচালনা
- টেবিল তৈরি এবং সংশোধন
- ডেটা ইনসার্ট করা
- বিভিন্ন SELECT কোয়েরি ব্যবহার করা
- ফিল্টারিং এবং শর্তাধীন অনুসন্ধান
- ডেটা সাজানো এবং অনন্য মান খুঁজা

আশা করি এই গাইড আপনার PostgreSQL শেখার যাত্রায় সহায়ক হবে!
