# ogg_single_replication
Este repositorio corresponde al caso de uso de replicación simple, unidireccional, utilizando Golden Gate.

## Requisitos
Se necesita tener instalado Docker.

Además, para ejecutar este proyecto se necesitan las credenciales de un usuario de AWS con permisos para gestionar:

- VPC
- EC2
- RDS (Oracle y Postgresql)

La ejecución tiene un coste muy pequeño en AWS.

## ¿Cómo lo ejecuto?
Para ejecutarlo, primero hay que construir la imagen Docker utilizando el siguiente comando:

```
docker build . --no-cache -t ogg_single_replication
```

Una vez construida la imagen, ejecutamos:
```
docker run -it --rm -e KEY_ID=<AWS_KEY_ID> -e SECRET_ID=<AWS_SECRET_ID> --entrypoint /bin/bash ogg_single_replication
```

sustituyendo <AWS_KEY_ID> y <AWS_SECRET_ID> por el valor correspondiente de las credenciales de AWS.

Al ejecutar el comando se accede al terminal del contenedor, y tenemos que ejecutar:

``` 
sh build.sh
```

Con este script lanzamos la ejecución de Terraform que creará todo el entorno necesario en AWS. Una vez creado, para realizar 
la replicación, tenemos que seguir los pasos marcados en el post.

El script tarda unos 15 minutos en crear toda la infraestructura

## ¿Cómo destruyo el entorno?
Desde la misma terminal del contenedor Docker, lanzamos:

```
sh destroy.sh
```

Con este script se lanza el comando de Terraform para destruir la infraestructura creada.