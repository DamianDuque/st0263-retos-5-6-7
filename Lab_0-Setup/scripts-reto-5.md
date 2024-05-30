# Scripts/comandos para reto 5/lab 3-1.

### Conexión por SSH a instancia.

```
ssh -i <your-key-pair.pem> hadoop@<master-public-dns-name>
```

### Listar archivos en HDFS.

```
hdfs dfs -ls /
hdfs dfs -ls /user
hdfs dfs -ls /user/hadoop
hdfs dfs -ls /user/hadoop/datasets
```

### Instalación de Git.

```
sudo yum install git
```

### Clonación del repositorio.

```
git clone https://github.com/st0263eafit/st0263-241.git
```

### Creación de carpetas en HDFS y copia de archivos.

```
hdfs dfs -mkdir /user/hadoop/datasets
hdfs dfs -mkdir /user/hadoop/datasets/gutenberg-small
hdfs dfs -put /local-path-to-cloned-repo/* /user/hadoop/datasets/gutenberg-small
```

### Copiar archivos a Hive.

```
hdfs dfs -put /root/st0263-241/bigdata/datasets/gutenbergsmall/*.txt /user/hadoop/datasets/gutenberg-small/
```

### Copiar archivos a S3.

```
hadoop fs -put /root/st0263-241/bigdata/datasets/ s3://lab1daduquel/
```

### Copiar archivos hacia el AWS S3 vía SSH.

```
hadoop fs -put /root/st0263-241/bigdata/datasets/ s3://lab1daduquel/
```


