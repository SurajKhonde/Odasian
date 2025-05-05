**MySQL** is a relational database management system (RDBMS). It's one of the most popular open-source databases in the world. It uses SQL (Structured Query Language) to manage and query data.
#### Why use MySQL?
 1. **Structured Data**
If your application has well-defined relationships—like users, orders, transactions, etc.—MySQL is a great fit.
 2. **Reliability & Performance**
MySQL is fast, stable, and widely used in production systems—from small startups to huge companies.
 3. **Security**
Built-in user access controls and secure password handling make it safe for customer-facing applications.
4. **Integration**
MySQL works well with most backend languages (Node.js, Python, PHP, Java) and can be integrated with tools like `Sequelize`, `Prisma`, or `MySQL2` in `Node.js`
#### Summary

| Feature               | Why It Matters                           |
| --------------------- | ---------------------------------------- |
| **Structured Schema** | Perfect for predictable, related data    |
| **Fast Queries**      | Ideal for search, filtering, and reports |
| **ACID Compliant**    | Safe for handling financial transactions |
| **Widely Supported**  | Easy to host, connect, and scale         |
### Getting Started

#### How To Install and Secure `phpMyAdmin` on Ubuntu
##### Prerequisites
In order to complete this guide, you will need:

- An Ubuntu server. This server should have a non-root user with administrative privileges and a firewall configured with `ufw`. 
- A LAMP (Linux, Apache, MySQL, and PHP) stack installed on your Ubuntu server. If this is not completed yet, you can follow this guide on 
##### Step-by-Step Setup (`MySQL` + `phpMyAdmin`)
###### Step 1  Update Your Package Index
```bash
sudo apt update
sudo apt upgrade -y
```
###### LAMP Stack install
A “LAMP” stack is a group of open source software that is typically installed together in order to enable a server to host dynamic websites and web apps written in PHP. This term is an acronym which represents the **L**inux operating system with the **A**pache web server. The site data is stored in a **M**ySQL database, and dynamic content is processed by **P**HP.
**LAMP** एक acronym है:
- **L** – Linux (तुम्हारा operating system, जैसे Ubuntu)
- **A** – Apache (वेब सर्वर जो ब्राउज़र से request accept करता है)
- **M** – MySQL (डेटाबेस जहाँ data store होता है)
- **P** – PHP (server-side language जो dynamic pages generate करती है)
Ubuntu में LAMP Stack कैसे install करें?
```bash
sudo apt update
sudo apt install apache2

sudo ufw app list
Output
Available applications:
  Apache
  Apache Full
  Apache Secure
  OpenSSH
```
For now, it’s best to allow only connections on port `80`, since this is a fresh Apache installation and you don’t yet have a TLS/SSL certificate configured to allow for HTTPS traffic on your server.
To only allow traffic on port `80`, use the `Apache` profile:
```shell
sudo ufw allow in "Apache"
sudo ufw status
```

Here’s what each of these profiles mean:
- **Apache**: This profile opens only port `80` (normal, unencrypted web traffic).
- **Apache Full**: This profile opens both port `80` (normal, unencrypted web traffic) and port `443` (TLS/SSL encrypted traffic).
- **Apache Secure**: This profile opens only port `443` (TLS/SSL encrypted traffic).
अब ब्राउज़र में जाकर:  
📍 `http://localhost` या `http://your-server-ip` खोलो — अगर "`Apache2` Ubuntu Default Page" दिखे तो Apache चल रहा है।
![[Pasted image 20250505210147.png]]
##### Why is this important?
Without enabling UFW:
- Your server is **open to all** traffic.
- You can't control which ports/services are exposed.
With UFW enabled and configured:
- You only allow what’s needed (like HTTP/Apache on port 80).
- You reduce attack surface and improve system security.
##### Step 2 — Installing MySQL
Now that you have a web server up and running, you need to install the database system to be able to store and manage data for your site. MySQL is a popular database management system used within PHP environments.
Again, use `apt` to acquire and install this software:
```shell
sudo apt install mysql-server

sudo mysql
```

##### Step 3 — Installing PHP
You have Apache installed to serve your content and MySQL installed to store and manage your data. PHP is the component of our setup that will process code to display dynamic content to the final user. In addition to the `php` package, you’ll need `php-mysql`, a PHP module that allows PHP to communicate with MySQL-based databases. You’ll also need `libapache2-mod-php` to enable Apache to handle PHP files. Core PHP packages will automatically be installed as dependencies.
```shell
sudo apt install php libapache2-mod-php php-mysql
php -v
```
After this, restart the Apache web server in order for your changes to be recognized. You can do that with the following command:
```shell
sudo systemctl restart apache2
sudo systemctl status apache2
```
some choices to configure phpMyAdmin correctly. We’ll walk through these options shortly:
```shell
sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl
```
###### Creating a database in MySQL
`CREATE DATABASE mydb;`
###### Using the created database mydb
`USE mydb;`
###### Creating a table in MySQL
```sql
CREATE TABLE mytable
(
 id int unsigned NOT NULL auto_increment,
 username varchar(100) NOT NULL,
 email varchar(100) NOT NULL,
 PRIMARY KEY (id)
);
CREATE TABLE mytable will create a new table called mytable.
```
id int unsigned NOT NULL auto_increment creates the id column, this type of field will assign a unique numeric ID to each record in the table (meaning that no two rows can have the same id in this case), MySQL will automatically assign a new, unique value to the record's id field (starting with 1).
###### Inserting a row into a MySQL table
```sql
INSERT INTO mytable ( username, email )
VALUES ( "myuser", "myuser@example.com" );
```
###### Updating a row into a MySQL table
```sql
UPDATE mytable SET username="myuser" WHERE id=8
```
###### Deleting a row into a MySQL table
```sql
DELETE FROM mytable WHERE id=8
```
###### Selecting rows based on conditions in MySQL
```sql
SELECT * FROM mytable WHERE username = "myuser";
```
###### Show list of existing databases
```sql
SHOW databases;
```
###### Show tables in an existing database
```sql
SHOW tables;
```
###### Show all the fields of a table
```sql
DESCRIBE databaseName.tableName;
DESCRIBE tableName;
```
###### Creating user
First, you need to create a user and then give the user permissions on certain databases/tables. While creating the user, you also need to specify where this user can connect from.
```sql
CREATE USER 'user'@'localhost' IDENTIFIED BY 'some_password';
```
Will create a user that can only connect on the local machine where the database is hosted.
```sql
CREATE USER 'user'@'%' IDENTIFIED BY 'some_password';
```
###### Adding privileges
Grant common, basic privileges to the user for all tables of the specified database:
```sql
GRANT SELECT, INSERT, UPDATE ON databaseName.* TO 'userName'@'localhost';
// Grant all privileges to the user for all tables on all databases (attention with this):
GRANT ALL ON *.* TO 'userName'@'localhost' WITH GRANT OPTION;
```
If you must use such names, put them between back-tick `delimiters`
```sql
CREATE TABLE `table`
(
 `first name` VARCHAR(30)
);
```
A query containing the back-tick delimiters on this table might be:
```sql
SELECT `first name` FROM `table` WHERE `first name` LIKE 'a%';
```
##### Information Schema Examples

####  Data Types
###### CHAR(n)
CHAR(n) is a string of a fixed length of n characters. If it is CHARACTER SET `utf8mb4`, that means it occupies exactly 4^n bytes, regardless of what text is in it.
 Most use cases for CHAR(n) involve strings that contain English characters, hence should be CHARACTER SET ascii. (latin1 will do just as good.)
 ```sql
 country_code CHAR(2) CHARACTER SET ascii,
postal_code CHAR(6) CHARACTER SET ascii,
uuid CHAR(39) CHARACTER SET ascii, -- more discussion elsewhere
```
###### DATE, DATETIME, TIMESTAMP, YEAR, and TIME
- The `DATE` datatype comprises the date but no time component. Its format is `'YYYY-MM-DD'` with a range of '1000-01-01' to '9999-12-31'.
- The `DATETIME` type includes the time with a format of `'YYYY-MM-DD HH:MM:SS'`. It has a range from '`1000-01-01 00:00:00`' to '`9999-12-31 23:59:59`'.
- The `TIMESTAMP` type is an integer type comprising date and time with an effective range from '`1970-01-01 00:00:01`' UTC to '`2038-01-19 03:14:07`' UTC.
- The `YEAR` type represents a year and holds a range from `1901` to `2155`.
- The `TIME` type represents a time with a format of '`HH:MM:SS`' and holds a range from '`-838:59:59`' to '`838:59:59`'.
######  Why not always use `VARCHAR(255)`?
Many developers default to `VARCHAR(255)` out of habit. But:
- It **wastes space** unnecessarily.
- It doesn’t reflect **realistic limits** for many types of data.
- Choosing appropriate lengths can **improve performance and efficiency**, especially for indexing.
###### Key Guidelines
Use `CHARACTER SET ascii`** for fixed, non-Unicode strings:
These use only ASCII characters (like A-Z, 0-9) and don’t need full UTF-8 encoding.
- UUID → `CHAR(36)` or `BINARY(16)`  
    `UUIDs` look like: `123e4567-e89b-12d3-a456-426614174000`
    > `CHAR(36) CHARACTER SET ascii` — or pack into `BINARY(16)` for storage optimization.
- **country_code** → `CHAR(2)`  
    Like `'US'`, `'IN'`, `'DE'`.
- **ip_address** → `CHAR(39)`  
    Long enough for IPv6: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`
- **phone** → `VARCHAR(20)`  
    To allow country codes, extensions: `+91-9876543210 ext. 123`
- **postal_code** → `VARCHAR(20)`  
    Includes codes like `'110001'`, `'90210'`, `'SW1A 1AA'`.
###### Why not simply 255?
There are two reasons to avoid the common practice of using (255) for everything.
When a complex `SELECT` needs to create temporary table (for a `subquery`, `UNION`, `GROUP` `BY`, etc), the preferred choice is to use the MEMORY engine, which puts the data in RAM. But `VARCHARs` are turned into CHAR in the process. This makes `VARCHAR(255)` CHARACTER SET `utf8mb4` take 1020 bytes. That can lead to needing to spill to disk, which is slower. In certain situations, `InnoDB` will look at the potential size of the columns in a table and decide that it will be too big, aborting a CREATE TABLE.
###### `VARCHAR` versus `TEXT`
MySQL Storage Types for Strings

|Type|Description|
|---|---|
|`CHAR(n)`|Fixed-length string. Always allocates `n` characters.|
|`VARCHAR(n)`|Variable-length string, max `n` characters.|
|`TEXT`|Variable-length string for large text, stored differently from `VARCHAR`.|
###### Key Usage Tips
 Never use `TINYTEXT`
- It's only 255 bytes max — too small for practical use.
- Rarely useful and has odd storage behavior.
Almost never use `CHAR`
- `CHAR(n)` always stores `n` characters, even if the actual content is shorter.
- For `UTF-8 (utf8mb4)`, each character can take up to 4 bytes, so:
    - `CHAR(100)` in `utf8mb4` = 400 bytes max — regardless of actual data length.
- This wastes space and slows queries (especially large datasets).
Use `CHAR` only for truly fixed-length fields, like:
- Country codes: `CHAR(2)`
- Status flags: `CHAR(1)`
And in that case, use `CHARACTER SET ascii` if you only need basic A-Z/0-9 characters (1 byte/char).

Use `VARCHAR(n)` for most cases
- Efficient and flexible
- Only stores the characters you need + 1-2 bytes for length
- `VARCHAR(n)` truncates after `n` characters (not bytes!)
###### What is "truncation"?
Truncation means cutting off extra content that exceeds a limit.
For `VARCHAR(n)`, the limit is `n` characters— not bytes. If you try to insert a string longer than `n` characters, **MySQL will either:**
1. **Cut (truncate)** it to the first `n` characters (if SQL mode allows it), or
2. **Throw an error or warning**, depending on MySQL's `sql_mode`.
Suppose we create a table:
```sql
CREATE TABLE users (
  username VARCHAR(10)
);
INSERT INTO users (username) VALUES ('abcdefghijk');
```
- `'abcdefghijk'` has 11 characters.
- `VARCHAR(10)` only allows **10 characters**.
- So:
    - If truncation is allowed, MySQL will store `'abcdefghij'` (first 10 chars).
    - If strict SQL mode is on, MySQL will reject the insert with an error or warning.
###### `INT` as AUTO_INCREMENT
Any size of `INT` may be used for `AUTO_INCREMENT. UNSIGNED` is always appropriate

###### Implicit / automatic casting
```sql
select '123' * 2; // 246

select '123ABC' * 2 // 246
select 'ABC123' * 2 // 0
```

######  Integer Types
These store whole numbers (no decimal point). You choose based on the size of numbers you'll store.

|Type|Storage|Range (Signed)|Range (Unsigned)|
|---|---|---|---|
|TINYINT|1 byte|-128 to 127|0 to 255|
|SMALLINT|2 bytes|-32,768 to 32,767|0 to 65,535|
|MEDIUMINT|3 bytes|-8M to 8M approx.|0 to 16M approx.|
|INT/INTEGER|4 bytes|-2.1B to 2.1B|0 to 4.2B|
|BIGINT|8 bytes|-9 quintillion to +9 quint.|0 to 18 quintillion approx.|

Use when:You need fast, efficient whole numbers — like IDs, counters, quantities.
#### SELECT
##### `SELECT` with `DISTINCT`
The `DISTINCT` clause after `SELECT` eliminates duplicate rows from the result set.
```sql
CREATE TABLE `car` ( `car_id` INT UNSIGNED NOT NULL PRIMARY KEY, `name` VARCHAR(20), `price` DECIMAL(8,2) ); INSERT INTO CAR (`car_id`, `name`, `price`) VALUES (1, 'Audi A1', '20000'); INSERT INTO CAR (`car_id`, `name`, `price`) VALUES (2, 'Audi A1', '15000'); INSERT INTO CAR (`car_id`, `name`, `price`) VALUES (3, 'Audi A2', '40000'); INSERT INTO CAR (`car_id`, `name`, `price`) VALUES (4, 'Audi A2', '40000'); SELECT DISTINCT `name`, `price` FROM CAR;
```

##### SELECT all columns ( * )
```sql
SELECT * FROM stack;
SELECT stack.* FROM stack JOIN Overflow ON stack.id = Overflow.id;
```
##### Why you should NOT use `SELECT *`
 ❌ Cons (Real-world issues)
1. Unnecessary Data Transfer
    - You may fetch large columns (like `VARBINARY`, `TEXT`) you don’t even use.
    - Example: Imagine a `profile_picture` field with `2MB` images. A `SELECT * FROM users` for 10 users =` 20MB` download 
2. Hidden Breakages
    - If someone drops, renames, or reorders columns, your app may break without warning.
    - With `SELECT name, email`, you get a clear error if `email` was dropped — easier to debug.
3. Slower Performance
    - MySQL has to look up all columns, even the ones you don’t use.
    - Also, if `*` includes large fields, **temp tables and joins** become slow and memory-heavy.
4. Harder to Read and Maintain
    - If you use `SELECT *`, someone reading your query has no idea what data you're actually using.
5. Joins Bring Chaos
    - If you join multiple tables and use `SELECT *`, you get overlapping column names — causing bugs.
6. You Can't Use Column Indexing Easily
    - `SELECT *` hides which fields are being filtered or ordered, making optimization difficult.
>[!Warning]
>Even though `SELECT *` is tempting (especially early on), it’s not scalable or safe. **Being explicit with your columns** improves performance, reliability, and maintainability — and makes you a more professional developer.

###### SELECT with LIKE (%)
```sql
CREATE TABLE stack
( id int AUTO_INCREMENT PRIMARY KEY, username VARCHAR(100) NOT NULL ); INSERT stack(username) VALUES ('admin'),('k admin'),('adm'),('a adm b'),('b XadmY c'), ('adm now'), ('not here');
```
"`adm`" anywhere:
```sql
SELECT * FROM stack WHERE username LIKE "%adm%";
```
Begins with "`adm`":
```sql
SELECT * FROM stack WHERE username LIKE "adm%";
```
Ends with "`adm`":
```sql
SELECT * FROM stack WHERE username LIKE "%adm";
```
Just as the `%` character in a LIKE clause matches any number of characters, the _ character matches just one character. For example,
```sql
SELECT * FROM stack WHERE username LIKE "adm_n";
```
##### SELECT with CASE or IF
```sql
SELECT st.name,
 st.percentage,
 CASE WHEN st.percentage >= 35 THEN 'Pass' ELSE 'Fail' END AS `Remark`
FROM student AS st ;
```
 Or with IF
 ```sql
 SELECT st.name, st.percentage, IF(st.percentage >= 35, 'Pass', 'Fail') AS `Remark` FROM student AS st ;
```
##### SELECT with Alias (AS)
SQL aliases are used to temporarily rename a table or a column. They are generally used to improve readability
```sql
SELECT username AS val FROM stack;
SELECT username val FROM stack;
```
##### SELECT with a `LIMIT` clause
```sql
SELECT * FROM Customers ORDER BY CustomerID LIMIT 3;
```
>[!success]
>Best Practice Always use ORDER BY when using LIMIT; otherwise the rows you will get will be unpredictable.

```sql
SELECT *
 FROM Customers
 ORDER BY CustomerID
 LIMIT 2,1;
```
`2,1` means: **skip 2 rows**, then **fetch 1 row**.
`LIMIT offset, count`
- Returns **the 3rd row** (because row count starts from 0).
Explanation: When a `LIMIT` clause contains two numbers, it is interpreted as `LIMIT` offset,count. So, in this example the query skips two records and returns one.
##### `SELECT` with `BETWEEN`
You can use `BETWEEN` clause to replace a combination of "`greater than equal` AND `less than equal`" conditions
```sql
SELECT * FROM stack WHERE id >= 2 and id <= 5;
SELECT * FROM stack WHERE id BETWEEN 2 and 5;
SELECT * FROM stack WHERE id BETWEEN 2 and 5;
```
##### `SELECT` with `WHERE`
```sql
SELECT * FROM stack WHERE username = "admin" AND password = "admin";
```
# DBMS(SQL)

[😍famous words in sql](https://www.notion.so/famous-words-in-sql-1b07af54188580c3ab75ded523aa8914?pvs=21)

This is bare minimum setup to connect with the **mysql** on your machine or **serverside**

Step-by-Step Guide to Install **MySQL** & **phpMyAdmin** on Ubuntu (Latest Version)

Step 1: Update Ubuntu Package List

```shell
sudo apt update && sudo apt upgrade -y
sudo apt install mysql-server -y
sudo systemctl status mysql
✅ If it says "active (running)", MySQL is installed successfully.
```

Step 3: Secure MySQL Installation

```shell
 //sudo mysql_secure_installation
      sudo apt install mysql-server -y
After installation, check if MySQL is running:
  sudo systemctl status mysql
```

==Step 3:== **Install phpMyAdmin**

```shell
sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl -y
```

- **Select Apache2** (Press **Space** to select, then **Enter**)

- **Configure database for phpMyAdmin with dbconfig-common?** (Choose **Yes**)

- **Set a password for phpMyAdmin** (Enter a strong password)

You'll be asked:

1. **Enable VALIDATE PASSWORD plugin?** (Choose `Y` or `N`)

2. **Set root password?** (Enter a strong password)

3. **Remove anonymous users?** (Choose `Y`)

4. **Disallow root login remotely?** (Choose `Y`)

5. **Remove test database?** (Choose `Y`)

6. **Reload privilege tables now?** (Choose `Y`)

==Step 4: Allow Remote Access (Optional)==

```shell
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

[![](DBMS(SQL)%201ad7af541885804e8eecd30e2e8af0c6/image.png)](DBMS\(SQL\)%201ad7af541885804e8eecd30e2e8af0c6/image.png)

**bind-address = 127.0.0.1**

```shell
bind-address = 0.0.0.0
```

**📌 When to Use** `**127.0.0.1**` **in Production**

✅ **Use** `**127.0.0.1**` **(localhost) if:**

- Your **MySQL server** and **application** (e.g., Node.js, PHP) are **on the same server**.

- You want to keep **MySQL private and prevent external access**.

- Your application only needs **local database access**.

**Example** `**config**` **for a production app using localhost MySQL:**

```shell
DB_HOST=127.0.0.1
DB_USER=myappuser
DB_PASSWORD=strongpassword
DB_NAME=mydatabase
```

**📌 When NOT to Use** `**127.0.0.1**` **in Production**

❌ **Do NOT use** `**127.0.0.1**` **if:**

- Your **application runs on a different server** than MySQL.

- You need **remote database access** from another machine.

- You're setting up a **load-balanced architecture** with multiple app servers.

🔹 **Solution: Use a Private/Internal IP Instead**

```shell
Find your server's private IP:
    ip a | grep inet
Restart MySQL:
     sudo systemctl restart mysql
Allow MySQL through the firewall:
      sudo ufw allow from 192.168.1.0/24 to any port 3306
```

**📌 Summary**

|   |   |   |
|---|---|---|
|**Scenario**|**Use** `**127.0.0.1**`**?**|**Alternative**|
|MySQL and app on the **same server**|✅ Yes|Keep MySQL private|
|MySQL on a **different server**|❌ No|Use **private/internal IP**|
|Need **remote database access**|❌ No|Allow MySQL on **private IP**|
|**Public MySQL access (Not recommended)**|❌ No|Use **SSH tunnel or VPN**|

**🚀 Best Practice for Production:**

✅ Use **127.0.0.1** if MySQL is on the same machine.

✅ Use a **private/internal IP** if MySQL is on a different server.

❌ **Never expose MySQL on a public IP (**`**0.0.0.0**`**)** unless secured with a firewall.

**Step 6: Configure Apache for phpMyAdmin**

✔ Choose "Local Unix Socket" (Recommended)

```shell
sudo phpenmod mbstring
sudo systemctl restart apache2
```

Create a symbolic link so phpMyAdmin works correctly:

```shell
sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin
```

Restart Apache:

```shell
sudo systemctl restart apache2
```

Step 7: Access phpMyAdmin

```shell
http://localhost/phpmyadmin/index.php?route=/&route=%2F&db=oneStop_apiHub&table=users
username :- phpmyadmin
Password:- Abc@123!
```

**Change MySQL Password Policy**

```shell
sudo mysql -u root -p
 //Check the current password policy settings:
SHOW VARIABLES LIKE 'validate_password%';
 //Lower the password security policy (Optional) You can set a lower security level (choose one):
    SET GLOBAL validate_password.policy = LOW;
    SET GLOBAL validate_password.length = 6;
 // ALTER USER 'root'@'localhost' IDENTIFIED BY 'NewPassword123!';

```

Choosing a MySQL Username for phpMyAdmin

```shell
phpmyadmin  
⚠️ Important Notes
    DO NOT use "root" for security reasons.
    phpmyadmin@yourdomain.com
```

🚀 look now we are setup and basic details how myphpAdmin with MySQL server setup done lets see a queries and explaition why and how engineering behind it .

**how to access Database connection in your code**

```javascript
const db = require("../config/db");
```

Creating a database in MySQL

```sql
CREATE DATABASE mydb;
//Using the created database mydb
USE mydb;
```

Creating a table in MySQL

```sql
CREATE TABLE mytable
(
 id int unsigned NOT NULL auto_increment,
 username varchar(100) NOT NULL,
 email varchar(100) NOT NULL,
 PRIMARY KEY (id)
);
```

Inserting a row into a MySQL table

```sql
INSERT INTO mytable ( username, email )
VALUES ( "myuser", "myuser@example.com" );
//The varchar a.k.a strings can be also be inserted using single quotes
INSERT INTO mytable ( username, email )
VALUES ( 'username', 'username@example.com' );
```

Updating a row into a MySQL table

```sql
UPDATE mytable SET username="myuser" WHERE id=8
```

Deleting a row into a MySQL table

```sql
DELETE FROM mytable WHERE id=8
```

Selecting rows based on conditions in MySQL

```sql
SELECT * FROM mytable WHERE username = "myuser";
SELECT * FROM leverage WHERE (created_by = ? OR created_by = '1') AND status = '1'
```

Show list of existing databases

```sql
SHOW databases;
 //Show tables in an existing database
 SHOW tables;
```

Show all the fields of a table

```sql
DESCRIBE databaseName.tableName;
 //or, if already using a database:
 DESCRIBE tableName;
```

Creating user

First, you need to create a user and then give the user permissions on certain databases/tables. While creating the  
user, you also need to specify where this user can connect from.  

```sql
// Will create a user that can only connect on the local machine where the database is hosted.
CREATE USER 'user'@'localhost' IDENTIFIED BY 'some_password';
//Will create a user that can connect from anywhere (except the local machine).
CREATE USER 'user'@'%' IDENTIFIED BY 'some_password';
```

Adding privileges

Grant common, basic privileges to the user for all tables of the specified database:

```sql
GRANT SELECT, INSERT, UPDATE ON databaseName.* TO 'userName'@'localhost';
```

Grant all privileges to the user for all tables on all databases (attention with this):

```sql
GRANT ALL ON *.* TO 'userName'@'localhost' WITH GRANT OPTION;
```

As demonstrated above, _._ targets all databases and tables, databaseName.* targets all tables of the specific database. It is also possible to specify database and table like so ==**databaseName.tableName.**==

Generally, you should try to avoid using column or table names containing spaces or using reserved words in SQL.  
For example, it's best to avoid names like  
==table== or ==first== name.

If you must use such names, put them between **back-tick ``** delimiters. For example:

```sql
CREATE TABLE `table`
(
 `first name` VARCHAR(30)
);
SELECT `first name` FROM `table` WHERE `first name` LIKE 'a%';
```

**Data Types**

CHAR(n)

CHAR(n) is a string of a fixed length of n characters. If it is CHARACTER SET ==utf8mb4==, that means it occupies exactly 4*n bytes, regardless of what text is in it.

Most use cases for CHAR(n) **involve strings that contain English characters,** hence should be CHARACTER SET ascii. (latin1 will do just as good.)

```sql
country_code CHAR(2) CHARACTER SET ascii,
postal_code CHAR(6) CHARACTER SET ascii,
uuid CHAR(39) CHARACTER SET ascii,
```

==**DATE, DATETIME, TIMESTAMP, YEAR, and TIME**==

The **DATE** datatype comprises the date but no time component. Its format is '==YYYY-MM-DD'== with a range o '==1000-01-01' to '9999-12-31=='.  
The  
==**DATETIME**== type includes the time with a format of '==YYYY-MM-DD HH:MM:SS=='. It has a range from '==1000-01-01 00:00:00' to '9999-12-31 23:59:59'.==  
The  
==**TIMESTAMP**== type is an integer type comprising date and time with an effective range from =='1970-01-01 00:00:01'UTC to '2038-01-19 03:14:07' UTC.==  
The  
==**YEAR**== type represents a year and holds a range from ==1901 to 2155.==  
The  
==**TIME**== type represents a time with a format of '**HH:MM:SS**' and holds a range from '**-838:59:59' to '838:59:59'.**

```sql
|-----------|--------------------|----------------------------------------|
| Data Type | Before MySQL 5.6.4 | as of MySQL 5.6.4                      |
|-----------|--------------------|----------------------------------------|
| YEAR      | 1 byte             | 1 byte                                                  |
| DATE      | 3 bytes                                                     |
| TIME      | 3 bytes            | 3 bytes + fractional seconds storage   |
| DATETIME  | 8 bytes            | 5 bytes + fractional seconds storage   |
| TIMESTAMP | 4 bytes            | 4 bytes + fractional seconds storage   |
|-----------|--------------------|----------------------------------------|
```

**VARCHAR(255)**

First, I will mention some common strings that are always hex, or otherwise limited to ASCII. For these, you should specify CHARACTER SET ascii (latin1 is ok) so that it will not waste space:

```sql
UUID CHAR(36) CHARACTER SET ascii -- or pack into BINARY(16)
country_code CHAR(2) CHARACTER SET ascii
ip_address CHAR(39) CHARACTER SET ascii -- or pack into BINARY(16)
phone VARCHAR(20) CHARACTER SET ascii -- probably enough to handle extension
postal_code VARCHAR(20) CHARACTER SET ascii -- (not 'zip_code') (don't know the max

city VARCHAR(100) -- This Russian town needs 91:
 Poselok Uchebnogo Khozyaystva Srednego Professionalno-Tekhnicheskoye Uchilishche Nomer Odin
country VARCHAR(50) -- probably enough
name VARCHAR(64) -- probably adequate; more than some government agencies allow
```

Why **not simply 255?** There are two reasons to avoid the common practice of using (255) for everything.

**1. Temporary Tables and MEMORY Engine Limitations**

- When MySQL needs to create a temporary table (for operations like `GROUP BY`, `ORDER BY`, `UNION`, or subqueries), it prefers the **MEMORY** storage engine for performance.

- However, **MEMORY tables store** `**VARCHAR**` **as** `**CHAR**`, which means a `VARCHAR(255) CHARACTER SET utf8mb4` (which supports up to 4 bytes per character) can take up **1020 bytes** per row.

- If this exceeds the MEMORY table row size limit (often **16KB per row**), MySQL **switches to MyISAM or InnoDB on disk**, which is significantly **slower**.

**2. InnoDB Row Size Limitations**

- InnoDB **calculates the maximum potential row size** before allowing a `CREATE TABLE`.

- Even if your data is mostly small, if a table has many `VARCHAR(255)` columns, MySQL assumes the **worst case scenario** (all columns filled to their maximum size).

- If the estimated size **exceeds 65,535 bytes** (InnoDB’s internal limit per row), the table creation **fails**.

**Best Practices Instead of Defaulting to** `**VARCHAR(255)**`

✅ **Use the smallest necessary length.** If a column only ever holds two-character country codes (`US`, `GB`), use `CHAR(2)`. If names average 50 characters, use `VARCHAR(60)`, not `VARCHAR(255)`.

✅ **Know your character set.** `utf8mb4` takes up to **4 bytes per character**, while `latin1` only takes **1 byte**. This directly affects storage needs.

✅ **Consider TEXT for very long strings.** If storing long text (e.g., descriptions, comments), use `TEXT` types (`TEXT`, `MEDIUMTEXT`, `LONGTEXT`) instead of `VARCHAR(255)`.

Using `VARCHAR(255)` everywhere might seem like a "safe" choice, but in reality, **it can slow down your queries, waste memory, and cause unexpected issues**. The best practice is to **choose the right size for each column based on actual data needs**.

|   |   |   |   |   |
|---|---|---|---|---|
|**Data Type**|**Use Case**|**Pros**|**Cons**|**Best Practice**|
|`TINYTEXT`|Very small text (avoid)|Saves space|Not useful, same as `VARCHAR(255)` but worse indexing|Avoid using it|
|`TEXT`|Long, unstructured text (comments, descriptions)|No size limit in definition|Can't be indexed efficiently, slows queries|Use for long text, consider `FULLTEXT` indexing|
|`CHAR(n)`|Fixed-length data (ISO codes, hashes, Y/N flags)|Fast lookups, no fragmentation|Wastes space for variable-length text|Use for truly fixed-length data, set `CHARACTER SET ascii` when possible|
|`VARCHAR(n)`|Most general text storage (names, emails)|Efficient storage, index-friendly|Inefficient in MEMORY tables|Choose realistic `n`, avoid `VARCHAR(255)` unless necessary|

**INT as AUTO_INCREMENT**

Any size of **INT** may be used for ==AUTO_INCREMENT. UNSIGNED== is always appropriate.

1. Any INT Size Can Be Used for AUTO_INCREMENT

✅ MySQL allows TINYINT, SMALLINT, MEDIUMINT, INT, and BIGINT for AUTO_INCREMENT.  
✅ UNSIGNED is recommended for AUTO_INCREMENT because IDs never go negative, doubling the available range.  

|   |   |   |
|---|---|---|
|**Data Type**|**Signed Range**|**Unsigned Range**|
|`TINYINT`|-128 to 127|0 to 255|
|`SMALLINT`|-32,768 to 32,767|0 to 65,535|
|`MEDIUMINT`|-8,388,608 to 8,388,607|0 to 16,777,215|
|`INT`|-2,147,483,648 to 2,147,483,647|0 to 4,294,967,295|
|`BIGINT`|-9 quintillion to 9 quintillion|0 to 18 quintillion|

**Use** `**INT UNSIGNED**` **for most cases** (supports up to 4 billion IDs).

FLOAT, DOUBLE, and DECIMAL in MySQL

|   |   |   |   |   |
|---|---|---|---|---|
|**Type**|**Storage**|**Precision**|**Use Case**|**Example**|
|`FLOAT`|4 bytes|~7 digits (approximate)|Sensor data, scientific calculations|`FLOAT(7,3) → 123.456`|
|`DOUBLE`|8 bytes|~15-17 digits (approximate)|Physics, GPS coordinates, statistics|`DOUBLE(16,8) → 123.45678901`|
|`DECIMAL`|Variable (exact)|Exact, up to 65 digits|Money, financial transactions|`DECIMAL(10,2) → 99999999.99`|

**Best Practices**

✅ Use **DECIMAL** for **money/currency** (ensures precision).

✅ Use **FLOAT/DOUBLE** for **scientific or large numbers**, but expect small rounding errors.

✅ Avoid `FLOAT` or `DOUBLE` if **exact comparisons are needed** (`0.1 + 0.2 ≠ 0.3`).

**Strings in MySQL: CHAR, VARCHAR, TEXT, and BLOB**

|   |   |   |   |   |
|---|---|---|---|---|
|**Type**|**Storage**|**Max Size**|**Best For**|**Indexing**|
|`CHAR(n)`|Fixed-size|255 chars|Fixed-length codes, short strings|Fully indexable|
|`VARCHAR(n)`|Variable|65,535 chars*|Names, emails, most text fields|Fully indexable|
|`TEXT`|Variable (separate storage)|64 KB – 4 GB|Long descriptions, articles|**Limited** (first few chars only)|
|`BLOB`|Variable (binary)|64 KB – 4 GB|Images, PDFs, encrypted data|Not indexed for text search|

**Best Practices**

✅ Use `CHAR` for **fixed-length** data (like country codes, Y/N flags).

✅ Use `VARCHAR` for **general text fields** (emails, names).

✅ Use `TEXT` for **long-form content** (articles, comments).

✅ Use `BLOB` for **binary data** (images, files).

✅ Avoid `TINYTEXT`—it has little advantage over `VARCHAR(255)`.

**ENUM vs. SET in MySQL**

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    status ENUM('active', 'inactive', 'banned', 'pending') NOT NULL
);
```

MySQL offers a number of different numeric types. These can be broken down into  
Group Types  
Integer Types  
==INTEGER, INT, SMALLINT, TINYINT, MEDIUMINT, BIGINT==

Fixed Point Types ==DECIMAL, NUMERIC==

Floating Point Types ==FLOAT, DOUBLE==

Bit Value Type ==BIT==

==**Integer Types**==

[![](DBMS(SQL)%201ad7af541885804e8eecd30e2e8af0c6/image%201.png)](DBMS\(SQL\)%201ad7af541885804e8eecd30e2e8af0c6/image%201.png)

**Fixed Point Types**

Decimal

These values are stored in binary format. In a column declaration, the precision and scale should be specified.Precision represents the number of significant digits that are stored for values.

```sql
salary DECIMAL(5,2)
//5 represents the precision and 2 represents the scale. For this example,
// the range of values that can be stored in
 // this column is -999.99 to 999.99
```

This data type can store up to 65 digits.The number of bytes taken by DECIMAL(M,N) is approximately M/2.

**Floating Point Types**

==**SELECT**==

SELECT with DISTINCT

The ==**DISTINCT**== clause after ==SELECT== eliminates duplicate rows from the result set.

```sql
SELECT DISTINCT name, price FROM CAR;
```

SELECT all columns (*)

```sql
SELECT * FROM stack;
```

**Why You Should Avoid** `**SELECT ***`

❌ **Schema Changes Can Break Code**

- If a column is **added, removed, or reordered**, your application might break.

❌ **Performance Issues**

- Fetching **unnecessary columns** increases **query execution time** and **network load**.

- MySQL’s **query optimizer works better** when you specify only the needed columns.

❌ **Index Optimization is Limited**

- If you **only need indexed columns**, MySQL can **avoid reading extra data** (faster).

- `SELECT *` forces MySQL to read **all columns**, even unused ones.

Cons:

1. You are returning more data than you need. Say you add a VARBINARY column that contains 200k per row.You only need this data in one place for a single record - using SELECT * you can end up returning 2MB per 10 rows that you don't need

2. Explicit about what data is used

3. Specifying columns means you get an error when a column is removed

4. The query processor has to do some more work - figuring out what columns exist on the table

5. You can find where a column is used more easily

6. You get all columns in joins if you use SELECT *

7. You can't safely use ordinal referencing (though using ordinal references for columns is bad practice in itself)

8. In complex queries with TEXT fields, the query may be slowed down by less-optimal temp table processing

**SELECT by column name**

```sql
CREATE TABLE stack(
 id INT,
 username VARCHAR(30) NOT NULL,
 password VARCHAR(30) NOT NULL
);
INSERT INTO stack (`id`, `username`, `password`) VALUES (1, 'Foo', 'hiddenGem');
INSERT INTO stack (`id`, `username`, `password`) VALUES (2, 'Baa', 'verySecret');
```

SELECT with LIKE (%)

The `LIKE` operator is used in MySQL for pattern matching in text searches. The `%` wildcard is used to match **zero or more characters** in a string.

```sql
SELECT * FROM users WHERE name LIKE 'John%';
🔹 Finds all names that start with "John", such as:
John Johnathan Johnny
```

**2️⃣ Using** `**%**` **in Different Positions**

|   |   |   |
|---|---|---|
|**Pattern**|**Matches**|**Does Not Match**|
|`'John%'`|`John`, `Johnathan`, `Johnny`|`Mr. John`|
|`'%John'`|`Mr. John`, `Sir John`|`Johnathan`, `Johnny`|
|`'%John%'`|`John`, `Mr. John`, `Sir John`, `Johnathan`|(No exclusions)|
|`'J%n'`|`John`, `Jordan`, `Jaden`|`Jonathan`|

Example: Searching in a Table

### **Table:** `**products**`

|   |   |   |
|---|---|---|
|id|name|category|
|1|iPhone 13|Mobile|
|2|Samsung S22|Mobile|
|3|MacBook Air|Laptop|
|4|iPad Pro|Tablet|

```sql
SELECT * FROM products WHERE name LIKE '%Phone%';
```

Just as the % character in a LIKE clause matches any number of characters, the _ character matches just one character. For example,

```sql
SELECT * FROM stack WHERE username LIKE "adm_n";
+----+----------+
| id | username |
+----+----------+
| 1 | admin |
+----+----------+
```

Using `CASE` and `IF` in `SELECT` Statements

1️⃣ Using `CASE` in `SELECT`

```sql
SELECT id, name, 
  CASE 
    WHEN age < 18 THEN 'Minor'
    WHEN age BETWEEN 18 AND 65 THEN 'Adult'
    ELSE 'Senior'
  END AS age_category
FROM users;
```

Using `CASE` with Aggregation

✅ **Best for:** Grouping and conditional counting

```sql
SELECT 
  COUNT(CASE WHEN status = 'active' THEN 1 END) AS active_users,
  COUNT(CASE WHEN status = 'inactive' THEN 1 END) AS inactive_users
FROM users;

//🔹 Counts users based on their status without using multiple WHERE clauses.
```

SELECT with Alias (AS)

SQL aliases are used to temporarily rename a table or a column. They are generally used to improve readability.

```sql
SELECT username AS val FROM stack;
SELECT username val FROM stack;
```

SELECT with a **LIMIT** clause

```sql
SELECT *
 FROM Customers
 ORDER BY CustomerID
 LIMIT 3;
```

Best Practice: Always Use `ORDER BY` with `LIMIT`

When using `LIMIT`, MySQL **does not guarantee** which rows you get **unless** you specify `ORDER BY`. Without ordering, MySQL might return **random or inconsistent** results depending on how rows are stored or indexed.

🔴 Problem: Unpredictable Results Without `ORDER BY`

```sql
SELECT * FROM users LIMIT 5;
❌ Issues:
Unclear order – Are these the newest users? Oldest? Random?
Results may change on repeated queries, even if data doesn’t change.
```

**✅ Solution: Use** `**ORDER BY**`

```sql
      SELECT * FROM users ORDER BY created_at DESC LIMIT 5;
🔹 Guaranteed: The 5 most recent users (assuming created_at stores timestamps).
// Getting the Top 3 Highest Salaries
      SELECT name, salary FROM employees ORDER BY salary DESC LIMIT 3;
//Pagination (Using LIMIT with OFFSET)
      SELECT * FROM products ORDER BY price ASC LIMIT 10 OFFSET 20;
```

Using `BETWEEN` in `SELECT` (MySQL Best Practices)

```sql
SELECT * FROM products WHERE price BETWEEN 100 AND 500;
//🔹 Returns all products with prices from 100 to 500 (inclusive).
//🔹 Equivalent to:
SELECT * FROM products WHERE price >= 100 AND price <= 500;
 // BETWEEN with Dates
 SELECT * FROM orders WHERE order_date BETWEEN '2024-01-01' AND '2024-02-01';
// BETWEEN with Text (Alphabetical Ranges)
  SELECT * FROM customers WHERE last_name BETWEEN 'A' AND 'M';
// Using NOT BETWEEN
SELECT * FROM products WHERE price NOT BETWEEN 100 AND 500;
```

`BETWEEN` with `ORDER BY` and `LIMIT`

```sql
SELECT * FROM employees 
WHERE salary BETWEEN 3000 AND 7000 
ORDER BY salary DESC 
LIMIT 5;
//🔹 Returns the top 5 highest-paid employees within the 3000-7000 salary range.
```

**SELECT with WHERE**

```sql
SELECT * FROM stack WHERE username = "admin" AND password = "admin";
```

**Backticks**

There are many examples where **backticks** are used inside a query but for many it's still unclear when or where to use backticks ` `.

**NULL**

- Data not yet known - such as end_date, rating

- Optional data - such as middle_initial (though that might be better as the empty string)

- 0/0 - The result of certain computations, such as zero divided by zero.

- NULL is not equal to "" (blank string) or 0 (in case of integer).

- others?

### `**LIMIT**` **and** `**OFFSET**` **Relationship in MySQL**

In MySQL, `LIMIT` and `OFFSET` work together for **pagination**—retrieving a subset of records from a larger dataset.

```sql
SELECT * FROM table_name LIMIT limit_value OFFSET offset_value;

SELECT * FROM employees LIMIT 5 OFFSET 5;
SELECT * FROM products ORDER BY id LIMIT 10 OFFSET 0;
```

==**LIMIT**== clause with one argument

SELECT * FROM users ==ORDER BY== id ==ASC== ==LIMIT== 2

When two arguments are used in a ==**LIMIT**== clause:

the **first** argument represents the row from which the result set rows will be presented – this number is often mentioned as an **offset**, since it represents the row previous to the initial row of the constrained result set. This allows the argument to receive 0 as value and thus taking into consideration the first row of the nonconstrained result set.  
the  
**second** argument specifies the maximum number of rows to be returned in the result set (similarly to the one argument's example).

```sql
SELECT * FROM users ORDER BY id ASC LIMIT 2, 3
SELECT * FROM users ORDER BY id ASC LIMIT 0, 2
SELECT * FROM users ORDER BY id ASC LIMIT 2
```

Notice that in this alternative syntax the arguments have their positions switched:  
the  
**first** argument represents the number of rows to be returned in the result set;  
the  
**second** argument represents the offset.

**Creating databases**

Create a DATABASE. Note that the shortened word SCHEMA can be used as a synonym.

```sql
CREATE DATABASE Baseball;
//If the database already exists, 
     CREATE DATABASE IF NOT EXISTS Baseball;
     
 //Drop
 DROP DATABASE IF EXISTS Baseball; -- Drops a database if it exists, avoids Error 1008
DROP DATABASE xyz; -- If xyz does not exist, ERROR 1008 will occur
```

**INSERT**

```sql
INSERT INTO `table_name`
 (`index_field`, `other_field_1`, `other_field_2`)
 VALUES
 ('index_value', 'insert_value', 'other_value')
 ON DUPLICATE KEY UPDATE
 `other_field_1` = 'update_value',
 `other_field_2` = VALUES(`other_field_2`);
```

To insert data into a MySQL database, you use the `INSERT INTO` statement. Here's the basic syntax:

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
//example
INSERT INTO employees (id, name, position, salary)
VALUES (1, 'John Doe', 'Software Engineer', 75000);
//insert multiple rowws
INSERT INTO employees (id, name, position, salary)
VALUES 
(2, 'Jane Smith', 'Project Manager', 90000),
(3, 'Alice Brown', 'Designer', 65000);
```

Using `?` in MySQL Prepared Statements

Instead of inserting values directly, you use `?` as a placeholder and provide actual values later.

**Why Use** `**?**` **or** `**%s**` **Instead of Direct Values?**

✅ **Prevents SQL Injection**

✅ **Improves Performance** (Prepared statements can be cached and reused)

✅ **More Readable Code**

==**DELETE**==

```sql
DELETE [LOW_PRIORITY] [IGNORE] FROM table_name 
WHERE condition 
ORDER BY expression 
LIMIT number_rows;
```

**🔹 Parameter Details**

|   |   |
|---|---|
|Parameter|Description|
|**LOW_PRIORITY**|Delays the deletion until there are no read operations on the table. Used mainly for MyISAM tables.|
|**IGNORE**|Ignores errors (like foreign key violations) that occur during deletion.|
|**table_name**|The table from which records will be deleted.|
|**WHERE condition**|Specifies which records to delete. If omitted, **all records** will be deleted!|
|**ORDER BY expression**|Deletes records in a specific order (useful with `LIMIT`).|
|**LIMIT number_rows**|Specifies how many rows to delete.|

Delete Specific Records

```sql
DELETE FROM employees WHERE department = 'Sales';
// Delete with LIMIT
DELETE FROM orders WHERE status = 'Pending' ORDER BY order_date LIMIT 5;
//Delete All Records 
DELETE FROM employees;
//⚠️ Better Alternative: Use TRUNCATE for faster performance:
TRUNCATE TABLE employees;
```

**🔹 Difference Between DELETE & TRUNCATE**

|   |   |   |
|---|---|---|
|Feature|DELETE|TRUNCATE|
|Uses WHERE Clause?|✅ Yes|❌ No|
|Removes Specific Rows?|✅ Yes|❌ No (removes all rows)|
|Logs Individual Deletions?|✅ Yes|❌ No|
|Can Be Rolled Back?|✅ Yes (if using `BEGIN TRANSACTION`)|❌ No|
|Resets AUTO_INCREMENT?|❌ No|✅ Yes|

**UPDATE**

```sql
UPDATE table_name 
SET column1 = value1, column2 = value2, ...
WHERE condition
ORDER BY column
LIMIT number;
```

- `**SET**` → Specifies which columns to update.

- `**WHERE**` → Specifies which rows to update (⚠️ Omitting it updates **ALL rows**).

- `**ORDER BY**` → Updates records in a specific order.

- `**LIMIT**` → Restricts the number of rows to update.

🔸 Using `Promise.all()` to Update Multiple Records

```sql
const mysql = require('mysql2/promise');

async function updateSalaries() {
    const connection = await mysql.createConnection({
        host: 'localhost',
        user: 'root',
        password: '',
        database: 'company'
    });

    // List of employees to update
    const updates = [
        { id: 1, salary: 75000 },
        { id: 2, salary: 80000 },
        { id: 3, salary: 85000 }
    ];

    // Create an array of update promises
    const updateQueries = updates.map(emp => 
        connection.execute("UPDATE employees SET salary = ? WHERE id = ?", [emp.salary, emp.id])
    );

    // Execute all updates in parallel
    await Promise.all(updateQueries);

    console.log("Salaries updated successfully!");
    await connection.end();
}

updateSalaries().catch(console.error);
```

ORDER BY

`SELECT ... FROM ... WHERE ... GROUP BY ... HAVING ... ORDER BY ... LIMIT ... OFFSET ...`

**🔸 Breakdown:**

1. `**SELECT ...**` → Specifies which columns to return.

2. `**FROM ...**` → Specifies the table to query.

3. `**WHERE ...**` → Filters rows **before** grouping.

4. `**GROUP BY ...**` → Groups rows based on a column.

5. `**HAVING ...**` → Filters groups **after** grouping.

6. `**ORDER BY ...**` → Sorts the result.

7. `**LIMIT ... OFFSET ...**` → Limits results and supports pagination.

```sql
SELECT department, COUNT(*) AS total_employees
FROM employees
WHERE salary > 50000
GROUP BY department
HAVING total_employees > 5
ORDER BY total_employees DESC
LIMIT 10 OFFSET 20;
```

**Group By**

The `**GROUP BY**` clause in MySQL is used to group rows that have the **same values** in specified columns and apply **aggregate functions** like `COUNT()`, `SUM()`, `AVG()`, etc., to each group.

- It groups rows **with the same value** in a column.

- It is **always used with aggregate functions** like:
    
    - `COUNT()` → Counts rows per group.
    
    - `SUM()` → Adds up values per group.
    
    - `AVG()` → Finds the average per group.
    
    - `MAX()` / `MIN()` → Finds max/min per group.

1️⃣ Count Employees per Department

```sql
SELECT department, COUNT(*) AS total_employees
FROM employees
GROUP BY department;

//Total Sales per Customer
SELECT customer_id, SUM(amount) AS total_spent
FROM orders
GROUP BY customer_id;
// Find Average Salary per Department
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

`**GROUP BY**` **with** `**HAVING**`

- `**WHERE**` **filters before grouping.**

- `**HAVING**` **filters after grouping.**

- Use `HAVING` when applying conditions to **aggregated results**.

Find Departments with More than 5 Employees

```sql
SELECT department, COUNT(*) AS total_employees
FROM employees
GROUP BY department
HAVING total_employees > 5;
👉 Groups by department, then filters to show only departments with more than 5 employees.

```

`GROUP BY` with Multiple Columns

Find Employee Count per Department and Job Title

### **Find Top-Selling Products**

```sql
SELECT product_id, SUM(quantity) AS total_sold
FROM order_items
GROUP BY product_id
ORDER BY total_sold DESC
LIMIT 10;
```

## **🚀 Summary Table**

|   |   |   |
|---|---|---|
|Feature|Example|Explanation|
|**Basic GROUP BY**|`GROUP BY department`|Groups data based on a column.|
|**With COUNT()**|`COUNT(*) AS total`|Counts rows per group.|
|**With SUM()**|`SUM(salary)`|Adds values per group.|
|**With AVG()**|`AVG(salary)`|Calculates the average per group.|
|**With HAVING**|`HAVING COUNT(*) > 5`|Filters groups based on aggregate conditions.|
|**With Multiple Columns**|`GROUP BY department, job_title`|Groups by more than one column.|
|**With ORDER BY**|`ORDER BY total DESC`|Sorts grouped results.|
|**With GROUP_CONCAT()**|`GROUP_CONCAT(name SEPARATOR ', ')`|Combines values into a string per group.|

==**GROUP BY**== with AGGREGATE functions

```sql
// COUNT() → Count Rows per Group
  SELECT department, COUNT(*) AS total_employees
   FROM employees
   GROUP BY department;
//SUM() → Sum of Values per Group
 SELECT department, SUM(salary) AS total_salary
 FROM employees
 GROUP BY department;
//AVG() → Average per Group
  SELECT department, AVG(salary) AS avg_salary
   FROM employees
   GROUP BY department;
 //MAX() and MIN() → Highest and Lowest per Group
  SELECT department, MAX(salary) AS highest_salary, MIN(salary) AS lowest_salary
   FROM employees
   GROUP BY department;
```

## **🚀 Summary Table**

|   |   |   |
|---|---|---|
|Aggregate Function|Description|Example|
|`**COUNT(*)**`|Counts rows per group|`COUNT(*) AS total`|
|`**SUM(column)**`|Adds up values per group|`SUM(salary)`|
|`**AVG(column)**`|Finds the average per group|`AVG(salary)`|
|`**MAX(column)**`|Finds the highest value per group|`MAX(salary)`|
|`**MIN(column)**`|Finds the lowest value per group|`MIN(salary)`|
|`**HAVING**`|Filters grouped results|`HAVING COUNT(*) > 3`|
|**Multiple Columns**|Groups by multiple criteria|`GROUP BY department, job_title`|
|`**GROUP_CONCAT()**`|Combines values into a string|`GROUP_CONCAT(name)`|

**MySQL Joins**

**Types of Joins in MySQL**

There are **four main types** of joins:

1. ==**INNER JOIN**== → Returns matching rows from both tables.

2. ==**LEFT JOIN**== ==(or== ==**LEFT OUTER JOIN**====) → Returns all rows from the left table + matching rows from the right table.==

3. ==**RIGHT JOIN**== ==(or== ==**RIGHT OUTER JOIN**====)== → Returns all rows from the right table + matching rows from the left table.

4. ==**FULL JOIN**== ==(or== ==**FULL OUTER JOIN**====)== → Returns all rows from both tables (MySQL does not support this directly).

[![](DBMS(SQL)%201ad7af541885804e8eecd30e2e8af0c6/3bs7C.png)](DBMS\(SQL\)%201ad7af541885804e8eecd30e2e8af0c6/3bs7C.png)

### **📌 Employees Table (**`**employees**`**)**

|   |   |   |
|---|---|---|
|emp_id|name|dept_id|
|1|Alice|101|
|2|Bob|102|
|3|Charlie|NULL|
|4|David|101|
|5|Emma|103|

### **📌 Departments Table (**`**departments**`**)**

|   |   |
|---|---|
|dept_id|dept_name|
|101|HR|
|102|IT|
|103|Sales|
|104|Marketing|

1️⃣ **INNER JOIN**

```sql
SELECT employees.emp_id, employees.name, departments.dept_name
FROM employees
INNER JOIN departments ON employees.dept_id = departments.dept_id;
```

✔️ **Only exact matches (**`**dept_id**`**) appear in the result.**

Why Only `FROM employees` in `INNER JOIN`?

- The `FROM employees` **sets the starting point** (base table).

- The `INNER JOIN departments` **adds matching rows** from `departments`.

- The `ON employees.dept_id = departments.dept_id` **defines the condition** that links the tables.

**But Why Choose** `**FROM employees**`**?**

**I**f Employees are the Primary Data Focus

- If we primarily need employee details, `FROM employees` makes sense.

- It starts with the `employees` table.

- It looks for matching `dept_id` in `departments`.

- If a match is found, it includes the row; otherwise, it is excluded.

2️⃣ **LEFT JOIN (LEFT OUTER JOIN)**

🔹 **Returns all rows from the left table** (`employees`), even if there's no match in the right table.

A `LEFT JOIN` in MySQL returns **all records from the left table** and **matching records from the right table**. If there is **no match** in the right table, it returns `NULL` for those columns.

```sql
SELECT employees.emp_id, employees.name, departments.dept_name
FROM employees
LEFT JOIN departments ON employees.dept_id = departments.dept_id;
```

**3️⃣ RIGHT JOIN (RIGHT OUTER JOIN)**

🔹 **Returns all rows from the right table** (`departments`), even if there's no match in the left table.

```sql
SELECT employees.emp_id, employees.name, departments.dept_name
FROM employees
RIGHT JOIN departments ON employees.dept_id = departments.dept_id;
```

4️⃣ **FULL JOIN (FULL OUTER JOIN)**

Returns all rows from both tables.

✅ MySQL **does NOT support FULL JOIN**, but you can simulate it using `UNION`:

```sql
SELECT employees.emp_id, employees.name, departments.dept_name
FROM employees
LEFT JOIN departments ON employees.dept_id = departments.dept_id
UNION
SELECT employees.emp_id, employees.name, departments.dept_name
FROM employees
RIGHT JOIN departments ON employees.dept_id = departments.dept_id;
```

5️⃣ CROSS JOIN

🔹 **Returns the Cartesian product (all possible combinations) of both tables.**

```sql
SELECT [employees.name](http://employees.name/), departments.dept_name
FROM employees
CROSS JOIN departments;
```

✔️ Useful for generating all possible combinations.

✔️ Grows exponentially, so be careful with large datasets!

## **🚀 Quick Comparison Table**

|   |   |
|---|---|
|**Join Type**|**Returns**|
|**INNER JOIN**|Only matching rows from both tables|
|**LEFT JOIN**|All rows from the left table + matches from the right|
|**RIGHT JOIN**|All rows from the right table + matches from the left|
|**FULL JOIN** (Not in MySQL)|All rows from both tables (use `UNION`)|
|**CROSS JOIN**|All possible combinations (Cartesian Product)|
|**SELF JOIN**|Joins a table to itself|

## 🚀 Key Takeaways

✅ Use `INNER JOIN` for only matching rows.

✅ Use `LEFT JOIN` to keep all rows from the left table.

✅ Use `RIGHT JOIN` to keep all rows from the right table.

✅ Use `FULL JOIN` (via `UNION`) to keep everything from both tables.

✅ Use `CROSS JOIN` for all possible combinations.

✅ Use `SELF JOIN` for hierarchical relationships.

1 how to install myphpAdmin mysql in your UBUNTU machine

Let’s setup own **Projects** learn from from projects **MYSQL**

db.config.js

```sql
require("dotenv").config();
module.exports = {
  HOST: process.env.host,
  USER: process.env.user,
  PASSWORD: process.env.password,
  DB: process.env.db,
  dialect: "mysql",
  charset: "utf8mb4",
  pool: {
    max: 50,
    min: 0,
    acquire: 30000,
    idle: 10000,
  },
};
```

|   |   |
|---|---|
|**Property**|**Description**|
|`HOST`|The database **host** (e.g., `localhost` or a remote server).|
|`USER`|The database **username** (e.g., `root`).|
|`PASSWORD`|The **password** for the database user.|
|`DB`|The **database name** to connect to.|
|`dialect`|Specifies **MySQL** as the database type.|
|`charset`|Uses **utf8mb4**, which supports emojis and special characters.|
|`pool`|Connection pool settings (optimizes performance).|

What is the `pool` Configuration?

The `pool` object controls **how many connections** MySQL maintains.

|   |   |
|---|---|
|**Option**|**Description**|
|`max: 50`|Allows up to **50 concurrent connections**.|
|`min: 0`|Minimum **0 connections** (idle connections can close).|
|`acquire: 30000`|**Timeout (30s) before failing** if a connection is unavailable.|
|`idle: 10000`|If a connection is **idle for 10s, it will be released**.|

The `mysql2` package is an improved version of `mysql` for Node.js. It provides **better performance**, **async/await support**, and **faster queries**.

```sql
1️⃣ Install mysql2 if you haven't already:
```

✅ **Creates a MySQL connection using credentials from** `**dbConfig.js**`**.**

```javascript
const mysql = require('mysql2');
// Create a connection pool
const pool = mysql.createPool({
   host: dbConfig.HOST,
  user: dbConfig.USER,
  password: dbConfig.PASSWORD,
  database: dbConfig.DB,
}).promise(); // Enable promise support

Using mysql2 with promise(): This enables the await pool.execute() syntax.
```

2️⃣ Connecting to the Database

```javascript
connection.connect((error) => {
  if (error) throw error;
  console.log("Successfully connected to the database.");
```

3️⃣ Function to Create Tables

```javascript
  function createTable(query) {
    const createTableSQL = query;

    connection.query(createTableSQL, (err) => {
      if (err) {
        console.error(`Error creating table:`, err);
      } else {
        console.log(`Table created successfully`);
      }
    });
  }
```

5️⃣ Looping Through Tables to Create Them

```javascript
  table.forEach((e) => {
    const checkTableSQL = `SHOW TABLES LIKE '${e.tableName}'`;

    connection.query(checkTableSQL, (err, results) => {
      if (err) {
        console.error(`Error checking ${e.tableName} table:`, err);
      } else {
        if (results.length === 0) {
          createTable(e.query);
        } else {
          console.log(`${e.tableName} table already exists`);
          userInsert();
        }
      }
    });
  });
```

how to create tables like if we are connecting MySQL first time then we creates Automatically tables

```javascript
const { table } = require("./table.js");
exports.table = [
  {
    tableName: "users",
    query:
      "CREATE TABLE IF NOT EXISTS users (id INT AUTO_INCREMENT PRIMARY KEY,email VARCHAR(255) NULL,password VARCHAR(255) NULL,user_name VARCHAR(255) NULL,mobile_number BIGINT NULL UNIQUE,name VARCHAR(255) NULL,passport_number VARCHAR(255) NULL,passport_front VARCHAR(255) NULL,passport_back VARCHAR(255) NULL,role ENUM('Global Admin', 'Super Admin', 'Admin', 'Broker', 'Informatic Broker (IB)'),user_type ENUM('1', '2'),gender VARCHAR(255) NULL,dob VARCHAR(255) NULL,acc_no VARCHAR(255) NULL,c_acc_no VARCHAR(255) NULL,ifsc_code VARCHAR(255) NULL,bank_name VARCHAR(255) NULL,branch_name VARCHAR(255) NULL,acc_holder_name VARCHAR(255) NULL,kyc_status VARCHAR(255) NULL,passport_reason TEXT NULL,email_reason TEXT NULL,createdAt TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP, updatedAt TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP, country VARCHAR(255) NULL,country_code VARCHAR(10) NULL, otp_hash` VARCHAR(255) NULL, otp_time` VARCHAR(255) NULL,`refer_id` VARCHAR(255) NULL,`refred_by_id` VARCHAR(255) NULL,`google_auth_json` TEXT NULL DEFAULT NULL, `google_hash` VARCHAR(255) NULL DEFAULT NULL, `google_auth_json`, ADD `google_ascii` VARCHAR(255) NULL DEFAULT NULL,`enable_2fa` ENUM('Y','N') NOT NULL DEFAULT 'N',`google_auth_verify` ENUM('Y','N') NOT NULL DEFAULT 'N', is_crypto_enabled ENUM('no', 'yes') NOT NULL DEFAULT 'no',is_equity_enabled ENUM('no', 'yes') NOT NULL DEFAULT 'no',is_fx_enabled ENUM('no', 'yes') NOT NULL DEFAULT 'no',`is_contact_verified` ENUM('yes','no') NOT NULL DEFAULT 'no',`is_onboared` ENUM('Y','N') NOT NULL DEFAULT 'N');",
  },
  {
    tableName: "distributed_trade_fees",
    query:
      "CREATE TABLE IF NOT EXISTS `distributed_trade_fees` (`id` int NOT NULL AUTO_INCREMENT, `user_id` int NOT NULL,  `from_user_id` int NOT NULL,  `coin_id` int NOT NULL,  `fees_amount` decimal(10,2) NOT NULL,  `order_id` int NOT NULL,  `created_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;",
  }]
```

1. how pass random or code base query in java script

```javascript
const getUserInfo = "SELECT * FROM users WHERE id = ?";
    try {
    const [rows] = await pool.execute(getUserInfo, [userId]); 
    return rows[0]; // Return the first user
  } catch (error) {
    console.error("Error fetching user:", error);
    throw error; // Rethrow the error for handling
  }
}
const sql = `INSERT INTO user_activity (user_id, message, title) VALUES (?, ?, ?)`;
const [result] = await pool.execute(sql, [1, "User logged in", "Login"]);
console.log(result);
```

Yes, both `pool.query()` and `pool.execute()` exist in `mysql2`, but they serve slightly different purposes. Here’s the key difference:

1. `query()` vs. `execute()` in `mysql2`

|   |   |   |
|---|---|---|
|Feature|`query()`|`execute()`|
|**Query Type**|Can run both parameterized and non-parameterized queries.|Only works with parameterized queries (`?` placeholders).|
|**Prepared Statements**|Does **not** use prepared statements; sends raw SQL to MySQL.|Uses prepared statements for better security and performance.|
|**Security**|More prone to SQL injection if parameters aren’t properly escaped.|Safer as it automatically escapes and binds parameters.|
|**Performance**|Slightly slower because MySQL has to parse the query every time.|Faster for repeated queries as MySQL caches the prepared statement.|

**2. When to Use** `**query()**`

Use `query()` when:

- You **don't** have user inputs or dynamic values (e.g., static queries).

- You want to execute a query **once**, without worrying about performance.

```javascript
const [rows] = await pool.query("SELECT * FROM users");
```

**3. When to Use** `**execute()**`

Use `execute()` when:

- You **have dynamic values** (e.g., user input like `id`).

- You want to **prevent SQL injection** (it automatically escapes values).

- You need **better performance** for repeated queries.

```javascript
const [rows] = await pool.execute("SELECT * FROM users WHERE id = ?", [userId]);
```

If you are running **simple static queries**, `query()` is fine. But in most cases, `execute()` is the better choice. 🚀

In `mysql2`, the result of a query or execution is returned as an **array**, where:

- The **first element (**`**rows**`**)** contains the actual data from the database.

- The **second element (**`**fields**`**)** (optional) contains metadata about the result set (like column definitions).

```javascript
const [rows] = await pool.execute("SELECT * FROM users WHERE id = ?", [userId]);
```

Example Output from `execute()`

```javascript
const [rows] = await pool.execute("SELECT * FROM users WHERE id = ?", [1]);
console.log(rows);
//result
[
  {
    "id": 1,
    "name": "John Doe",
    "email": "john@example.com"
  }
]
Since it's an array of objects, we often return just rows[0] to get the first user.
```

```javascript
async function getUsers(req) {
  const { loginUserId, role } = req; // Extract role and user ID

  try {
    // Define the user columns to select
    const userColumns = [
      "users.id",
      "users.name",
      "users.role",
      "users.status",
      "users.user_name",
      "users.email",
      "users.user_type",
      "users.mobile_number",
      "users.createdAt",
      "users.refer_id",
      "users.refred_by_id",
      "users.user_lock",
    ];

    // Roles to exclude
    const filteredRoles = [
      "Global Admin",
      "Super Admin",
      "Broker",
      "Informatic Broker (IB)",
    ];

    let result;

    if (role === "Global Admin") {
      // Query for Global Admins
      const query = `
        SELECT DISTINCT ${userColumns.join(", ")}
        FROM users 
        WHERE role = 'admin' 
        ORDER BY id DESC
      `;

      // Execute query
      const [rows] = await pool.execute(query);
      result = rows;
    } else {
      // Query for other users, filtering out certain roles
      const usersQuery = `
        SELECT DISTINCT ${userColumns.join(", ")}
        FROM users 
        WHERE users.role NOT IN (?, ?, ?, ?) 
          AND users.refred_by_id = ? 
        ORDER BY users.id DESC
      `;

      // Execute query with parameterized values
      const [rows] = await pool.execute(usersQuery, [...filteredRoles, loginUserId]);
      result = rows;
    }

    return result;
  } catch (error) {
    console.error("Error executing query:", error.message);
    throw error;
  }
}
userColumns.join(", ") makes the code: 
✅ More maintainable
✅ More flexible
✅ More error-pro
```

```javascript
const query = `SELECT \`read\`, \`write\`, \`delete\` FROM permissions WHERE userId = ${userId}`;
```

==**\**== why?

That backslash (`\`) is an **escape character** in JavaScript **template literals** (backtick strings).  
✅ Correct Syntax for  
`UPDATE` in MySQL

```javascript
UPDATE users 
SET name = ?, mobile_number = ?, refred_by_id = ? 
WHERE id = ?;
```

`**SET**` **clause:** Specifies which columns to update.

`**WHERE**` **clause:** Ensures that only the specific user (with `id = ?`) gets updated.

🔥 Difference Between `INSERT` and `UPDATE`

|   |   |   |   |
|---|---|---|---|
|**Command**|**Purpose**|**Uses** `**VALUES**`**?**|**Uses** `**SET**`**?**|
|`INSERT`|Adds new row|✅ Yes|❌ No|
|`UPDATE`|Modifies existing row|❌ No|✅ Yes|

**What is an Alias in SQL?**

An **alias** is a temporary, short name for a **table** or **column** used within a SQL query. Aliases **do not** change actual table or column names in the database—just how they appear in the query.

✅ **1. Make Queries Shorter & More Readable**

```sql
SELECT customers.id, customers.name, customers.email FROM customers;
// with alias
SELECT c.id, c.name, c.email FROM customers AS c;

 //If you want to return column names differently:
 SELECT name AS full_name, email AS contact_email FROM users;
```

**📌 How to Use** `**FIND_IN_SET()**` **Correctly**

If `n.pair_ids` **is stored as a string** in your database,you **must ensure** `cp.id` is treated as a string inside `FIND_IN_SET()`.

```sql
FIND_IN_SET(value, comma_separated_list)
```

- `**value**` → The single value you want to find.

- `**comma_separated_list**` → A string containing comma-separated values.

- `**value**` → The single value you want to find.

- `**comma_separated_list**` → A string containing comma-separated values.

```sql
SELECT
    n.id AS credential_id,
    n.exchange,   
    cp.id AS pair_id,
    c1.symbol AS name1,
    c2.symbol AS name2
FROM exchange_credentials n
LEFT JOIN coinpair cp ON FIND_IN_SET(cp.id, n.pair_ids)
LEFT JOIN cryptocoin c1 ON c1.id = cp.coin_first_id
LEFT JOIN cryptocoin c2 ON c2.id = cp.coin_second_id
WHERE exchange IN ('Binance', 'Kraken');
```

Understanding the `LEFT JOIN` with `FIND_IN_SET()`

🔹 What’s Happening?

- `n.pair_ids` → A column in `exchange_credentials` that stores multiple `pair_id`s as a comma-separated string (e.g., `'10,20,30'`).

- `cp.id` → The `id` from the `coinpair` table.

- `FIND_IN_SET(cp.id, n.pair_ids)` checks if `cp.id` exists inside the `pair_ids` string.

⚠️ Why `FIND_IN_SET()` is NOT Recommended?

1. ❌ Poor Performance on Large Data
    
    - Does NOT use indexes (full table scan).
    
    - Slower than a normal `JOIN`.

2. ❌ Comma-Separated Values Are Bad for SQL
    
    - SQL databases are relational (use separate tables, not lists).
    
    - `FIND_IN_SET()` is a workaround, not best practice.

🚀 Best Alternative: Normalize the Database

Instead of storing `pair_ids` as a comma-separated string, create a mapping table.

✅ Create a `credential_pairs` table

```sql
sql
CopyEdit
CREATE TABLE credential_pairs (
    credential_id INT,
    pair_id INT,
    PRIMARY KEY (credential_id, pair_id)
);
```

✅ **Insert Data:**

```sql

INSERT INTO credential_pairs (credential_id, pair_id) VALUES
(1, 10), (1, 20), (1, 30),
(2, 15), (2, 25);
```

Selecting All Columns From One Table + Some Columns From Another

```sql
SELECT notifications.*, users.name 
FROM notifications 
LEFT JOIN users ON notifications.user_id = users.id;
```

**If a table has many columns,** ==**fetching unnecessary**== **data** ==**slows down queries.**==

- `notifications.*` = All columns from `notifications` table.

- `users.name` = Only `name` column from `users`.

- Better practice → Select only needed columns for better performance.

Other way Insert

```sql
const sql = "INSERT INTO coinpair SET ?";
const values = {
  coin_first_id: firstCoinId,
  coin_second_id: secondCoinId,
  current_price: price,
  stepSize,
  vendor_id: vendorId,
  is_vendor,
};
const result = await dbQueryAsync(sql, values);
```

How It Works?

- The `SET ?` syntax allows you to pass an **object (**`**values**`**)**.

- MySQL will automatically map the **keys** in the object (`coin_first_id`, `coin_second_id`, etc.) to **column names**.

- The **values** in the object (`firstCoinId`, `secondCoinId`, etc.) will be inserted into the respective columns.

**Difference Between Both Methods**

|   |   |   |
|---|---|---|
|**Method**|**Pros**|**Cons**|
|`SET ?` (Your method)|✅ Shorter and cleaner|❌ Might not work in all SQL setups|
|`VALUES (?, ?, ? ...)`|✅ More explicit and standard|❌ Slightly longer|

Both methods work, but the `VALUES (?, ?, ?)` approach is **more common** for MySQL.

**INNER JOIN = Only matching rows from both tables**

```sql
SELECT 
  cp.*, 
  fc.name AS first_coin_name, 
  sc.name AS second_coin_name, 
  fc.symbol AS first_coin_symbol, 
  sc.symbol AS second_coin_symbol
FROM coinpair cp
INNER JOIN cryptocoin fc ON cp.coin_first_id = fc.id
INNER JOIN cryptocoin sc ON cp.coin_second_id = sc.id;
```

**📢 याद रखने का सबसे आसान तरीका**

|   |   |
|---|---|
|JOIN Type|याद रखने का तरीका|
|**INNER JOIN**|"सिर्फ मैचिंग डेटा रखो, बाकी हटा दो!"|
|**LEFT JOIN**|"LEFT टेबल का पूरा डेटा रखो, Right का सिर्फ वही रखो जो मैच करे, बाकी NULL!"|

✅ How `ON` Works?

The `ON` clause is written **inside a JOIN statement** and **connects a column from the first table to a column from the second table**.

```sql
SELECT column_names 
FROM table1 
JOIN table2 
ON table1.column_name = table2.column_name;
```

- **table1** → First (Left) Table

- **table2** → Second (Right) Table

- **ON table1.column_name = table2.column_name** → This is the condition for matching the rows.

🔹 INNER JOIN with `ON`

```sql
SELECT users.id, users.name, orders.order_id, orders.product 
FROM users 
INNER JOIN orders 
ON users.id = orders.user_id;
```

1️⃣ The `WITH` Statement Starts a **CTE**

A Common Table Expression (CTE) is a temporary result set that can be referenced within a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement. It makes complex queries more readable and modular.

### **Why use** `**WITH floating_profit AS (...**`**)?**

In your query, the `WITH` statement creates a **temporary table** called `floating_profit`. This CTE calculates the **unrealized profit/loss** for users and stores it so it can be used later in the main query.

```sql
 WITH floating_profit AS (
    SELECT 
        crypto_margin_orders.user_id,         
        ROUND(SUM(CASE 
            WHEN crypto_margin_orders.order_side = 'BUY' THEN (coinpair.best_ask - crypto_margin_orders.price) * crypto_margin_orders.quantity 
            WHEN crypto_margin_orders.order_side = 'SELL' THEN (crypto_margin_orders.price - coinpair.best_bid) * crypto_margin_orders.quantity 
            ELSE 0 
        END - IFNULL(crypto_margin_orders.commission, 0)), 2) AS total_floating_profit
    FROM 
        crypto_margin_orders
    LEFT JOIN 
        coinpair ON coinpair.id = crypto_margin_orders.currency_pair 
    WHERE  
        crypto_margin_orders.status = 'open'         
    GROUP BY  
        crypto_margin_orders.user_id
),
realized_pl AS (
    SELECT 
        crypto_margin_orders.user_id,         
        ROUND(SUM(CASE 
            WHEN crypto_margin_orders.order_side = 'BUY' THEN (crypto_margin_orders.closed_price - crypto_margin_orders.price) * crypto_margin_orders.quantity 
            WHEN crypto_margin_orders.order_side = 'SELL' THEN (crypto_margin_orders.price - crypto_margin_orders.closed_price) * crypto_margin_orders.quantity 
            ELSE 0 
        END - IFNULL(crypto_margin_orders.commission, 0)), 2) AS total_realized_pl
    FROM 
        crypto_margin_orders
    WHERE  
        crypto_margin_orders.status = 'close'         
    GROUP BY  
        crypto_margin_orders.user_id
)

SELECT 
    u.id AS user_id,
    u.user_name,
    u.user_lock,
    
    -- Net quantity of open orders
    ROUND(SUM(CASE 
        WHEN co.order_side = 'BUY' AND co.status = 'open' THEN co.quantity
        WHEN co.order_side = 'SELL' AND co.status = 'open' THEN co.quantity
        ELSE 0
    END), 2) AS net_quantity_open,

    -- Net quantity of closed orders
    ROUND(SUM(CASE 
        WHEN co.order_side = 'BUY' AND co.status = 'close' THEN co.quantity
        WHEN co.order_side = 'SELL' AND co.status = 'close' THEN co.quantity
        ELSE 0
    END), 2) AS net_quantity_closed,    

    -- Realized P/L from the realized_pl CTE
    ROUND(IFNULL(rp.total_realized_pl, 0), 2) AS realized_pl,

    -- Unrealized P/L from the floating_profit CTE
    ROUND(IFNULL(fp.total_floating_profit, 0), 2) AS unrealized_pl,

    -- Total exposure for open orders
    ROUND(SUM(CASE 
        WHEN co.status = 'open' THEN co.quantity * co.price * co.leverage
        ELSE 0
    END), 2) AS total_exposure,

    -- Long exposure for open BUY orders
    ROUND(SUM(CASE 
        WHEN co.order_side = 'BUY' AND co.status = 'open' THEN co.quantity * co.price
        ELSE 0
    END), 2) AS long_exposure,    

    -- Short exposure for open SELL orders
    ROUND(SUM(CASE 
        WHEN co.order_side = 'SELL' AND co.status = 'open' THEN co.quantity * co.price
        ELSE 0
    END), 2) AS short_exposure,

    -- Max loss from the risk management table
    COALESCE(ROUND(rim.daily_auto_close, 2), '-') AS maxLoss,

    -- Total quantity bought
    ROUND(SUM(CASE 
        WHEN co.order_side = 'BUY' THEN co.quantity
        ELSE 0
    END), 2) AS total_qty_bought,

    -- Total quantity sold
    ROUND(SUM(CASE 
        WHEN co.order_side = 'SELL' THEN co.quantity
        ELSE 0
    END), 2) AS total_qty_sold

FROM 
    users u
INNER JOIN 
    crypto_margin_orders co ON u.id = co.user_id
LEFT JOIN 
    floating_profit fp ON u.id = fp.user_id
LEFT JOIN 
    realized_pl rp ON u.id = rp.user_id
LEFT JOIN 
    risk_info_management rim ON u.id = rim.target_user_id 
    AND rim.risk_info_type = 'crypto'
WHERE 
    u.role IN ('Informatic Broker (IB)', 'SubIB') ${
      role !== "Global Admin" ? `AND u.id in (${users})` : ""
    }
GROUP BY 
    u.id, u.user_name 
ORDER BY 
    u.user_name ASC LIMIT ${limit} OFFSET ${(page - 1) * limit}
```

- This part **calculates unrealized profit/loss** for each user and stores it in `floating_profit`.

- The `**ROUND(SUM(...), 2)**` ensures the values are formatted properly.

- **The CTE is like a temporary table**—we can use it later in the main query.

```sql
LEFT JOIN floating_profit fp ON u.id = fp.user_i
```