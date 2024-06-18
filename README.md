# Apache Doris playground



```shell
docker compose up

mysql -uroot -P9030 -h127.0.0.1

ALTER SYSTEM ADD BACKEND "172.20.80.3:9050";

mysql -uadmin -P9030 -h127.0.0.1

create database demo;

use demo; 
create table mytable
(
    k1 TINYINT,
    k2 DECIMAL(10, 2) DEFAULT "10.05",    
    k3 CHAR(10) COMMENT "string column",    
    k4 INT NOT NULL DEFAULT "1" COMMENT "int column"
) 
COMMENT "my first table"
DISTRIBUTED BY HASH(k1) BUCKETS 1
PROPERTIES ('replication_num' = '1');

curl  --location-trusted -u admin: -T data.csv -H "column_separator:," http://127.0.0.1:8030/api/demo/mytable/_stream_load
```

## demo data

```shell
-- Insert with all columns specified
INSERT INTO demo.mytable (k1, k2, k3, k4) VALUES
(1, 15.25, 'sample1', 5),
(2, 30.50, 'sample2', 10),
(3, 45.75, 'sample3', 15);

-- Insert with some columns using default values
INSERT INTO demo.mytable (k1, k3) VALUES
(4, 'sample4'),
(5, 'sample5'),
(6, 'sample6');

-- Insert with all default values (only k1 must be specified)
INSERT INTO demo.mytable (k1) VALUES
(7),
(8),
(9);

-- Insert using all columns explicitly with default values
INSERT INTO demo.mytable (k1, k2, k3, k4) VALUES
(10, DEFAULT, 'sample7', DEFAULT),
(11, DEFAULT, 'sample8', DEFAULT),
(12, DEFAULT, 'sample9', DEFAULT);
```