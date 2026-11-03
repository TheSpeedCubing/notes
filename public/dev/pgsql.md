---
date: 2025-03-31 20:21:00
slug: 66af17b8
title: PostgreSQL
---

# PostgreSQL

## install

### apt
```
sudo apt install postgresql-client
```

### repostitory configuration
https://wiki.postgresql.org/wiki/Apt

## connect

connect
```
psql -u <user>
```
```
psql -u <user> -d <database>
```
```
-h <host>
-p <port>
```

## commands
commands
```
\l   # list all databases
\c <database>   # connect to database
\dt  # display all tables
```
```sql
CREATE DATABASE database_name;
```
```sql
DROP DATABASE database_name;
```

## pg_dump
dump a database
```
pg_dump -u <user> -d <database> -f <backup_file>.sql
```
```
-h <host>
-p <port>
```

import .sql
```
psql -u <user> -d <database> -W < file.sql
```
```
-h <host>
-p <port>
```
