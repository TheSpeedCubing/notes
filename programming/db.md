# Information

nothing here

# Installation (MySQL Server)
1. Download .deb from https://dev.mysql.com/downloads/repo/apt/

(mysql-apt-config_0.8.32-1_all.deb for instance)
```shell
dpkg -i mysql-apt-config_0.8.32-1_all.deb
apt update
apt install mysql-server
```
## file location
```
Data:
/var/lib/mysql/

Configuration:
/etc/mysql/
```

# Execute
```shell
systemctl start mysql
systemctl status mysql
systemctl stop mysql
```
default port: 3306
# Connect Authentication
```shell=
mysql
mysql -u <username>
mysql -u <username> -p<password>
```
# Create User
```sql
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```
# SQL Query - Database
## show database
```sql
SHOW DATABASES;
```
## create database
```sql
CREATE DATABASE database_name;
CREATE DATABASE IF NOT EXISTS database_name; 
```

## delete database
```sql
DROP DATABASE database_name;
```

## use database
```sql
USE database_name;
```

## select current database
```sql
SELECT DATABASE();
```

note:
```DATABASE()``` return the  database you're using.

## import .sql to database
```shell
mysql -u username -p<password> database_name < file.sql
mysql -u username -p database_name < file.sql
```
# Table
## create table
```sql
CREATE TABLE `table_name` 
(`id` INT NOT NULL , 
`name` VARCHAR(16) NOT NULL , 
);
```

# Column

## 更改Type
```
ALTER TABLE `table_name` CHANGE `column_name` `column_name` CHAR(6) NOT NULL;
```

## Attribute

### Simple Attribute
無法再分割的單位  
ex. ID
### Composite Attribute
``>=2``個其他屬性的值組成
### Derived Attribute
可經過某種計算取得的屬性
## Key Attrbute

```
Super Key
-> Candicate Key
   -> Primary Key
   -> Alternate Key
```

### Super Key
符合唯一性(unique)
的關聯鍵(可以是多個column)  

### Candicate Key
符合唯一性(unique)  
符合最小性(column數最少)   
的關聯鍵  


### Primary Key

Candicate key中最有識別性的關聯鍵  

表中放底線   
NOT NULL  
不能重複
每個table只能有一個Primary Key。

是一種index  

```sql
ALTER TABLE `table_name` ADD PRIMARY KEY(`column_name`);
```

### Alternate Key
非Primary Key的Candicate Key

### Foreign Key
用來建立資料表的關係, FK值必須要與另一張表的PK相同, 
可以重複                            

## 約束 (Constraint)

### Foreign Key
### Primary Key
### Check
### Unique
### Not Null

## Index
索引, 查詢效率較高, 
資料大小儘量固定, 越小越好。
```sql
ALTER TABLE `table_name` ADD INDEX(`column_name`);
```

## 關聯式資料庫種類
1 : 1  
1 : M  
M : N  

Junction Table

## 三種完整性規則

### 實體完整性 ENTITY INTEGRITY RULE
針對一張表,  
PK必須UNIQUE, NOT NULL

### 參考完整性 REFERENTIAL INTEGRITY RULE
針對多張表,  
子關聯表的PK值, 一定要存在於父關聯表的PK中  

### 值域完整性規則
針對一張表,  
同一column的資料屬性需相同  