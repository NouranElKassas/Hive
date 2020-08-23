# Hive Queries
open terminal

Show all tables in hive
```show tables;```

show all the database valid in hive
```show databases;```

create a database called electricitycounter with a comment, creator name and date.
```create database electricitycounter comment 'This is my first db' with DBPROPERTIES ('creator'='Nouran','dateyy'='18-01-2020');```

show the database properties
```describe database extended electricitycounter;```

Show the electricitycounter database details
```use electricitycounter;```

create table in electricitycounter called recharge
```create table recharge (cell_no int, city string, name string,code INT, name_phone STRING, seller STRING, no_items STRING, price DOUBLE,expiryDate STRING) row format delimited fields terminated by ',';```

show tables in electricitycounter
```show tables;```

open a file recharge.input
```sudo nano recharge_input.txt``` or
```sudo gedit recharge_input.txt``` 

add sample data
```
987,eg,abc,xy1,A20,Sum,1,2000,20500110
199,uk,xyz,xy5,A21,Sum,5,3000,20500110
123,us,klm,xy3,A70,Sum,2,7000,20570130
```
save and close

select data from recharge table
```select * from recharge;```

Load the data from a file to Hive recharge table
```LOAD DATA LOCAL INPATH='PathOfTheFile/recharge_input.txt' INTO TABLE recharge;```

get the properties of recharge table
```describe recharge;```

get the properties extended of recharge table
```describe extended recharge;```

List tables in electricitycounter database
```hadoop fs -ls /user/hive/warehouse/electricitycounter.db```

create external table called recharge_extnl and will be saved as text file
```
create external table recharge_extnl (exchange string, volume int, name string) row format delimited fields terminated by ',' stored as textfile;
```
hive uses map reduce to count the number of records  in recharge table
```select count(*) from recharge;```

Select 5 rows from table recharge
```select * from recharge limit 5;```

delete table recharge_extnl if it exists
```drop table if exists recharge_extnl```

# Partition and Bucketing in Hive

Partition Static:
Creating the data then moving the data inside the table

```
create table products(code INT, name STRING, seller STRING, no_items STRING, price DOUBLE)
partitioned by(expiryDate STRING)
clustered by(seller) INTO 10 buckets
row format delimited fields terminated by ','
stored as textfile;
```
Set the partitioning not to be static
```set hive.exec.dynamic.partition.mode=nonstatic;```

Enable Partitioning in hive
```set hive.exec.dynamic.partition=true;```

Enable Bucketing un hive
```set hive.enforce.bucketing=true;```

Insert data from table to other table
```
from recharge r INSERT OVERWRITE TABLE products PARTITION(expiryDate)
select r.code,r.name_phone, r.seller, r.no_items, r.price,r.expiryDate
DISTRIBUTE by expiryDate;
```

