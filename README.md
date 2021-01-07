# Rapsberry Pi server backups

#### Raspberry pi docker, transmision, amule, youtube-dl, filebrowser...

Usar la rapsberry como equipo hacer copias de seguridad, sincronización de archivos, al tratarse de un equipo de bajo consumo y no hay problema en dejarlos encendido continuamente.

mediante algunos script bash llamado con cron hacer copia de las base de datos, 

mediante script bash envia pin alguans pagians web y si no estan en marcha .

Le instalamos un servidor samba para compartir los archivos por la red. Tambien hemos incorpordado el servicio de filebrowser para tener acceso a los archivos a traves de un navegador web.

![title ><](captures/title.png)

Todo montado sobre docker con lo que ponerlo en marcha es cuestión de 2 minutos.,.

Partimos de una rapsberry con un sistema Raspberry Pi OS Lite instalado, habilitado el ssh y con ip fija en 192.168.1.222, y instalado docker y docker-compose en ella.

** dejo pendiente hacer un tutorial de esta primera fase si alguien lo necesita

# Previo

Necesitamos montar un disco duro sobre la raspberry para tener una capacidad de almacenaje

## Montar discos externos para almacenamiento

Tengo un disco duro formateado a ext4

PASO 1. Conocer la denominación de la partición que queremos montar

    sudo  fdisk -l

PASO 2. Conocer el punto de montaje y tipo de la unidad que vamos a montar

    ls -l /dev/disk/by-uuid

PASO 3. Crear la carpeta donde se montará nuestra partición

    sudo mkdir /media/homeDisc

PASO 4. Configurar que cada que arranquemos el sistema se monte la unidad

Para decirle a nuestro sistema que monte la unidad debemos configurar el archivo /etc/fstab.

    sudo nano /etc/fstab

Montar unidad ext4

    UUID=XXXXXXXXXXXX /media/homeDisc ext4 errors=remount-ro 0 1

cambiar permiso unidad al usuario pi

    chown pi:pi /media/homeDisc

crear mis directorios

    mkdir -p /media/homeDisc/download/youtube-dl
    mkdir -p /media/homeDisc/download/amule
    mkdir -p /media/homeDisc/download/torrent

    mkdir -p /media/homeDisc/media/musica

# clonar el repositorio y ejecutar el compose

git clone Rpi_server_backups

cd Rpi_server_backups

docker-compose up -d

para acceder a las aplicaciones hay montado un contenedor con nginx donde hay una web que no da acceso a las aplicaciones:

abrir en navegador y colocar la ip de nuestra raspberry, en mi caso:

    http://192.168.1.200


## contenedores montandos

### Docker samba

Servidor samba, compartir los archivos por la red con otros dispositivos. 

    smb://192.168.1.200

https://github.com/dperson/samba


### Docker rpi-monitor

Sistema de motorización de los recurso de nuestra raspberry, capacidad, temperatura ...

https://github.com/michaelmiklis/docker-rpi-monitor


###  Docker filebrowser

Navegador de archivos web no permite navegar y gestionar los archivos guardados en nuestro servidor

    us: 1234
    ps: 1234