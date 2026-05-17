---
aliases:
  - Ejercicio Docker Compose
tags:
"References":
cssclasses:
---
# Ejercicio Docker Compose

Para favorecer el desarrollo de las funcionalidades relacionadas con el dispositivo para la
monitorización y control de almacenes de productos frescos agrícolas que se encuentran en
ubicaciones remotas se ha dedicido desarrollar un gemelo digital del mismo que se basa en la
orquestación de diversos servicios implementados mediante contenedores, que son:

1) Un contenedor que representará a la unidad de control que estará implementado en
Python, que regulará el funcionamiento del dispositivo, por un lado, se comunicará con el
sistema IoT con un message broker MQTT que estará implementado en Mosquitto. Por una
parte, se comunicará, utilizando sockets TCP, con el lector de tarjetas NFC para determinar
si alguien autorizado puede realizar la apertura de puertas. Por otra parte, se comunicará,
utilizando sockets TCP también, con un servomotor para accionar la apertura de puertas en
caso de que se haya recibido la orden de apertura presencial o remotamente.

2) Un contenedor que representará al gestor del sensor NFC que obtendrá lecturas de las
tarjetas que se acerquen al sensor. En caso de que se detecte alguna identidad, este
dispositivo se comunicará con otro contenedor que representará a la base de datos para
establecer si la identidad leída está autorizada para la apertura de puertas (esta
comunicación se realizará utilizando la librería de python para la gestión de datos en
MariaDB). En caso, de que el usuario esté autorizado, comunicará a la unidad de control la
solicitud de la apertura de la puerta. Esta comunicación se realizará utilizando los sockets
TCP.

3) Un contenedor que representará al gestor del servomotor que recibirá de la unidad de
control las órdenes de apertura y cierre de puertas utilizando sockets TCP.

4) Un contenedor que se encargará de implementar una base de datos que utilizará gestor
del sensor NFC para determinar si una identidad puede proceder a la apertura de puerta.
A partir de esta especificación, se deben elaborar los distintos ficheros docker-compose.yml
que son necesarios para la correcta orquestación de los microservicios.

Será necesario contemplar los elementos necesarios para constituir correctamente la red de
servicios, la publicación de los puertos que sea necesarios para que los distintos servicios sean
accesibles y los volúmenes necesarios para montar los componentes. Se deben incluir los
mecanismos para que los contenedores se arranquen en la secuencia correcta.

```yaml
services:
	control_unit:
		# lo primero es la build - donde está el Dockerfile
		build: ./ControlUnit
		image: controlUnit
		environment:
			- PYTHONUNBUFFERED=1
			- PORT=65431
			- MQTT_SERVER_ADDRESS=IP_PUBLICA
			- MQTT_SERVER_PORT=1883
			- DOOR_OPENEER_HOST=door_openeer
			- DOOR_OPENEER_PORT=65432
		# donde se encuentra el codigo que montará el Dockerfile
		volumes:
			- ./ControlUnit/code:/etc/usr/src/app
		networks:
			- fic_devices
		depends_on:
			door_openeer:
				condition: service_started
			
	nfc_reader:
		build: ./NFCReader
		image: nfcReader
		environment:
			- PYTHONUNBUFFERED=1
			- CONTROL_UNIT_HOST=control_unit
			- CONTROL_UNIT_PORT=65431
			- MYSQL_ROOT_PASSWORD=<root_password>
			- MYSQL_USER=<user>
			- MYSQL_PASSWORD=<password>
			- MYSQL_DATABASE=<database> 
		networks:
			- fic_devices
		depends_on:
			control_unit:
				condition: service_started
			db_service:
				condition: service_healthy
			
	door_openeer:
		build: ./DoorOpeneer
		image: doorOpeneer
		environment:
			- PYTHONUNBUFFERED=1
			- PORT=65432
		networks:
			- fic_devices
		volumes:
			- ./DoorOpeneer/code:/etc/usr/src/app
			
	db_service:
		image: mariadb:latest
		environment:
			- MYSQL_ROOT_PASSWORD=<root_password>
			- MYSQL_USER=<user>
			- MYSQL_PASSWORD=<password>
			- MYSQL_DATABASE=<database> 
		ports:
			- "3306:3306"  
		volumes:
			- ./dbservice/data:/var/lib/mysql
		networks:
			- fic_devices
		healthcheck:
			test: CMD["CMD", "healthcheck.sh", "--connect", "--innodb_initialized"]
			start_period: 10s
			interval: 10s
			timeout: 5s
			retries: 3
			
network:
	fic_devices:
		driver: bridge			
	
```
