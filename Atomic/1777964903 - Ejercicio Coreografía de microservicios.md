---
aliases:
  - Ejercicio Coreografía de microservicios
tags:
"References":
cssclasses:
---
# Ejercicio Coreografía de microservicios

Los componentes de plataforma en nube que son necesarios para gestionar los servicios
requeridos para la solución IoT relativa a las estaciones metereológicas son los siguientes:

1) Un servicio que implemente el protocolo MQTT necesario para recibir información
desde los dispositivos. Se utilizará un mosquitto que será gestionado mediante un
contenedor.

2) Un Message Router que será el componente encargado de interactuar con el Mosquitto
para recibir los mensajes procedentes de las estaciones de riego y meteorológicas y será
el encargado de enviar mensajes a los mismos. Este componente expondrá mediante su
API REST algunas funcionalidades para el envío de configuraciones y comandos a los
distintos dispositivos.

3) Un microservicio implementado en Python sobre Flask para registrar los comandos que
se envíen a cada uno de los dispositivos y que realice su envío a los mismos utilizando
los servicios de Message Router a partir de su API REST.

4) Un servicio de base de datos MySQL o María DB que se utilizará para almacenar la
información requerida por el microservicio de gestión de comandos

**A) Elaborar el/los ficheros docker-compose.yaml que será necesario para coreorgafíar
todos los servicios que se han indicado anteriormente. Se deberán implementar el patrón
de diseño de microservicios de bases de datos separadas y deberá facilitar el
escalado/desescalado de los mismos en caso de que sea necesario. Será necesario
contemplar los elementos necesarios para constituir correctamente la red de servicios, la
publicación de los puertos que sea necesarios para que los distintos servicios sean accesibles y los volúmenes necesarios para montar los componentes.**

```yaml
services:
	mosquitto:
		build: ./mosquitto
		ports:
			- "1883:1883"
		volumes:
			- "./mosquitto/code/mosquitto.conf:/etc/mosquitto/mosquitto.conf"
	
	message_router:
		build: ./message_route
		image: message_router
		ports: 
			- "5000:5000"
		environment:
			- PYTHONUNBUFFERED: 1 
			- MQTT_HOST=mosquitto
			- MQTT_PORT=1883
			- MESSAGE_ROUTER_PORT=5000
			- COMMANDS_MICROSERVICES_HOST=commmands_microservice
			- COMMANDS_MICROSERVICES_PORT=5001
		volumes:
			- "./message_router/code:/etc/usr/src/app"
		depends_on:
			- mosquitto
			- commands_microservice
			  
	commands_microservice:
		build: ./commands_microservice
		image: commands_microservice
		ports:
			- "5001:5001"
		environment:
			- PYTHONUNBUFFERED=1
			- COMMANDS_MICROSERVICE_PORT=5001
			- MESSAGE_ROUTER_HOST=message_router
			- MESSAGE_ROUTER_PORT=5000
			- DBHOST=commands_db
			- DBUSER=fic_db_user
			- DBPASSWORD=secret1234
			- DBDATABASE=fic_data
		depends_on:
			- commands_db
			  
	commands_db:
		build: ./microservices/telemetry_microservice/dbservice
		environment:
			- MARIADB_ROOT_PASSWORD=<password>
			  
	
```

**B) Elaborar los ficheros Dockerfile correspondientes al contenedor necesario para
desplegar el servicio de Message-Router y el microservicio de comandos.**

*Se añade también el de MQTT por amor al arte*

```Dockerfile
FROM debian:bullseye-slim

RUN apt update && apt upgrade -y

RUN apt install mosquitto mosquitto-clients -y

RUN touch /etc/mosquitto/passwd
RUN mosquitto_passwd -b /etc/mosquitto/passwd fic_server fic_password

CMD ["/usr/sbin/mosquitto", "-c", "/etc/mosquitto/mosquitto.conf"]
```

*Message Router*

```Dockerfile
FROM python:3-12

COPY ./code /etc/usr/src/app
WORKDIR /etc/usr/src/app
RUN pip install -r requirements.txt
CMD ["python", "-u", "main.py"]
```

*Microservicio de comandos*
*API*

```Dockerfile
FROM python:3-12

COPY ./code /etc/usr/src/app
WORKDIR /etc/usr/src/app
RUN pip install -r requirements.txt
CMD ["python", "-u", "main.py"]
```

*DB*

```Dockerfile
FROM mariadb:latest
ADD init.sql /docker-entrypoint-initdb.d/ddl.sql
```

