# examen1-SistemasDistribuidos-ChristianDavidLopezMorcillo

Christian David Lopez Morcillo
A00312096


<b> <p ALIGN=center> EXAMEN 1 - Sistemas Distribuidos <p> </b>


1. Consigne los comandos de linux necesarios para el aprovisionamiento de los servicios solicitados.

<b> Para el balanceador de cargas: </b>

* Se escoge usar el programa Nginx balanceando cargas bajo el esquema round robin.

Primero se instala el repositorio necesario para poder instalar Ngix, esto se realiza agregando a los repositorios de yum un archivo .repo que indique la ruta para descargar nginx. El archivo se debe agregar en la ruta “/etc/yum.repos.d/” y debe tener la información:
```text
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=0
enabled=1
```

* Se realiza la instalación de Nginx usando yum y se inicia el servicio.
```sh
sudo yum install nginx
```

* Se crea el archivo /etc/nginx/nginx.conf y allí se especifica la ip de los servidores que atenderán las peticione, de la siguiente forma:
```txt
http {
    upstream webservers {
         server 192,168,131,126;
         server 192,168,131,127;
    }
    server {
        listen 8080;
        location / {
              proxy_pass http://webservers;
        }
    }
}
```
* Se inicia el servicio Nginx.
```sh
sudo service nginx start
```

<b>Para el servidor web: </b>

