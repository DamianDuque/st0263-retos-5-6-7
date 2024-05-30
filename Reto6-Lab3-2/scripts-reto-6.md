# Scripts/comandos para reto 6/lab 3-2.

### Query usando datos de HDI.

```
SELECT * FROM "labs-db"."hdi" limit 10;
```

### Query usando datos de Tickit.

```
SELECT * FROM "tickit-db"."sales_tab" limit 10;
```

### Crear tabla externa HDI_db en Hive.

```
CREATE EXTERNAL TABLE HDI_db (id INT, country STRING, hdi FLOAT, lifeex INT,
mysch INT, eysch INT, gni INT)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION 's3://etrujilloc-datasets/onu2/hdi/';
```

### Conexión a beeline.

```
beeline
```

```
!connect jdbc:hive2://ec2-44-213-113-211.compute-1.amazonaws.com:10000/lab2-db
```

### Crear tabla externa HDI_Beeline_db en Beeline.

```
CREATE EXTERNAL TABLE HDI_Beeline_db (id INT, country STRING, hdi FLOAT, lifeex INT,
mysch INT, eysch INT, gni INT)
 ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE LOCATION '/user/hadoop/datasets/onu2/hdi/';
```

### Crear tabla HDI en Hive.

```
CREATE TABLE HDI (id INT, country STRING, hdi FLOAT, lifeex INT,
mysch INT, eysch INT, gni INT) 
ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE;
```

### Describir base de datos HDI_Beeline_db.

```
describe hdi_beeline_db;
```

### Mostrar tablas almacenadas.

```
show tables;
```

### Query a HDI en Hive.

```
select country, gni from hdi where gni > 1500;
```

### Crear tabla externa EXPO en Hive.

```
CREATE EXTERNAL TABLE EXPO (country STRING, expct FLOAT) 
ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' 
STORED AS TEXTFILE 
LOCATION 's3://lab1daduquel1/onu2/_export/';
```

### Join entre HDI y EXPO en Hive.

```
select hdi.country, gni, expct from hdi join expo on (hdi.country = expo.country) where gni > 2000;
```

### Crear tabla docs en Hive.

```
CREATE EXTERNAL TABLE docs (line STRING) 
STORED AS TEXTFILE 
LOCATION 's3://daduquel/datasets/gutenberg-small/';
```

### Ordenado por palabra de mayor a menor ocurrencia.

```
SELECT word, count(1) AS count FROM (SELECT explode(split(line,' ')) AS word FROM docs) w 
GROUP BY word 
ORDER BY word DESC LIMIT 10;
```

### Ordenado por palabra de menor a mayor ocurrencia.

```
SELECT word, count(1) AS count FROM (SELECT explode(split(line,' ')) AS word FROM docs) w 
GROUP BY word 
ORDER BY count DESC LIMIT 10;
```
