# Scripts/comandos para lab-0 (Setup).

### Configuración para activar persistencia en bucket con relación al Jupyter Notebook.

```
[
   {
   "Classification": "jupyter-s3-conf",
   "Properties": {
     "s3.persistence.enabled": "true",
     "s3.persistence.bucket": "<YOUR-BUCKET-NAME>"
     }
   }
]
```

### Conexión por SSH a instancia.

```
ssh -i <your-key-pair.pem> hadoop@<master-public-dns-name>
```

### Edición del archivo hue.ini.

```
nano /etc/hue/conf/hue.ini
```

### Reiniciar el servicio Hue.

```
systemctl restart hue.service
```



