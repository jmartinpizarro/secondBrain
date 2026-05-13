---
aliases:
  - MQTT - Ejercicio 2
tags:
"References":
cssclasses:
---
# MQTT - Ejercicio 2

En este ejercicio, el componente expone dos interfaces a la vez: HTTP (expone una API en Flask) Y MQTT (escucha dispositivos). 

Con respecto al [[1778659418 - MQTT - Ejercicio 1|MQTT - Ejercicio 1]], el Message Router no publica telemetría, solo la recibe y, como intermediario, la envía usando peticiones HTTP a la API.

```python
import os
import paho.mqtt.client as mqtt
import json
import datetime
import time

from flask import Flask, request
from flask_cors import CORS
import requests

app = Flask(__name__)

MQTT_SERVER = os.getenv("MQTT_SERVER_ADDRESS")
MQTT_PORT = int(os.getenv("MQTT_SERVER_PORT"))
API_HOST = os.getenv("HOST")
API_PORT = os.getenv("PORT")
INIT_TOPIC = "/fic/containers/+/request_access/"
client = None

def on_connect(clinet, userdata, flags, rc):
	print("Connected to subscriber with code ", rc)
	if rc == 0:
		client.subscribe(INIT_TOPIC, qos=1)
		print("Subscribed to ", INIT_TOPIC)

def register_tachograph_connection(container_id, container_hostname):
	session_id = ""
	data = {"container_id": container_id, 
			"container_hostname": container_hostname}
	# get the address and the port of the microservice to whom the
	# petition is going
	host = os.getenv('SESSIONS_MICROSERVICE_ADDRESS')
	port = os.getenv('SESSIONS_MICROSERVICE_PORT')
	
	r = requests.put('http://' + host + ':' + port + '/sessions/',
					json=data)
	if r.status_code == 201:
		complete_result = r.json()
		session_id = complete_result["session_id"]
	return session_id
	
def register_tachograph_disconnection(container_id):
	data = {"container_id": container_id}
	host = os.getenv('SESSIONS_MICROSERVICE_ADDRESS')
	port = os.getenv('SESSIONS_MICROSERVICE_PORT')
	
	r = requests.post('http://' + host + ':' + port + '/sessions/',
					  json=data)
					  
	if r.status_code == 201:
		result = r.json()
		if result["container_hostname"] != "":
			client.unsubscribe("/fic/containers/"+
								result["container_hostname"]+
								"/telemetry/")
			client.unsubscribe("/fic/containers/"+
								result["container_hostname"]+
								"/events/")
								
def store_telemetry(data):
	host = os.getenv('TELEMETRY_MICROSERVICE_ADDRESS')
	port = os.getenv('TELEMETRY_MICROSERVICE_PORT')
	r = requests.post('http://' + host + ':' + port + '/telemetry/',
						json=data)
	if r.status_code == 201:
		pass
	
```