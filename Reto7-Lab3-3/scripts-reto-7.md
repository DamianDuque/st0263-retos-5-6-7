# Scripts/comandos para reto 7/lab 3-3.

### Crear esquema spectrum_schema.

```
CREATE EXTERNAL SCHEMA spectrum_schema 
FROM DATA CATALOG 
DATABASE 'spectrum_db' 
IAM_ROLE 'arn:aws:iam::<your-account-id>:role/LabRole' 
CREATE EXTERNAL DATABASE IF NOT EXISTS;
```

### Crear tabla proveniente del esquema previamente creado.

```
create external table spectrum_schema.sales(
salesid integer,
listid integer,
sellerid integer,
buyerid integer,
eventid integer,
dateid smallint,
qtysold smallint,
pricepaid decimal(8,2),
commission decimal(8,2),
saletime timestamp)
row format delimited
fields terminated by '\t'
stored as textfile
location 's3://lab1daduquel/tickit/sales_tab/'
table properties ('numRows'='172000');
```

### Consultar todos los datos en la tabla creada.

```
select count(*) from spectrum_schema.sales;
```

### Crear tabla event2.

```
create table event2(
eventid integer not null distkey,
venueid smallint not null,
catid smallint not null,
dateid smallint not null sortkey,
eventname varchar(200),
starttime timestamp);
```

### Llenar la tabla event2 recién creada.

```
COPY event2 FROM 's3://lab1daduquel/tickit/allevents_pipe/allevents_pipe.txt'
iam_role 'arn:aws:iam::<your-account-id>:role/LabRole'
delimiter '|' timeformat 'YYYY-MM-DD HH:MI:SS' region 'us-east-1';
```

### Consulta con tablas tanto internas como externas.

```
select top 10 spectrum_schema.sales.eventid, sum(spectrum_schema.sales.pricepaid)
from spectrum_schema.sales, event2
where spectrum_schema.sales.eventid = event2.eventid
and spectrum_schema.sales.pricepaid > 30
group by spectrum_schema.sales.eventid
order by 2 desc;
```

### Query básica.

```
select * from event2 where dateid = 1833;
```