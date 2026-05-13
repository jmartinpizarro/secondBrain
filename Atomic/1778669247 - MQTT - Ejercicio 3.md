---
aliases:
  - MQTT - Ejercicio 3
tags:
"References":
cssclasses:
---
# MQTT - Ejercicio 3

---

**Ejercicio — Sistema de monitorización de temperatura (2 puntos)**

Escribir el código en Python que permita la implementación de un dispositivo IoT de monitorización de temperatura en una sala de servidores. El dispositivo se comunicará con un servidor central mediante el protocolo MQTT.

Las condiciones son las siguientes:

1. Cuando el sistema inicia, se conecta a un broker cuya dirección está disponible en una variable de entorno llamada `MQTT_SERVER` y el puerto en `MQTT_PORT`. El número de serie del dispositivo se obtiene de la variable de entorno `DEVICE_ID`. Se deben contemplar las desconexiones inesperadas.
    
2. Cuando se confirma la conexión, el dispositivo debe suscribirse al topic donde recibirá configuración, y publicar un mensaje de registro que incluya su identificador y un timestamp.
    
3. Si el servidor confirma que el dispositivo está registrado, enviará un mensaje de configuración con el topic de telemetría y la frecuencia de muestreo. El dispositivo debe actualizar su estado con esa información.
    
4. Si el servidor envía una orden de apagado, el dispositivo debe desconectarse ordenadamente.
    
5. Una vez registrado, el dispositivo publicará periódicamente la temperatura actual (variable `current_temp`) y su identificador.
    
6. Tanto en la desconexión ordenada como en la inesperada, se debe notificar el tipo de desconexión producida.
    

El bucle de comunicaciones debe ejecutarse en un hilo separado.

---

Los topics siguen esta estructura:

```
/servers/{DEVICE_ID}/register/     ← el dispositivo publica su registro
/servers/{DEVICE_ID}/config/       ← el dispositivo escucha configuración
/servers/{DEVICE_ID}/telemetry/    ← el dispositivo publica temperatura
/servers/{DEVICE_ID}/session/      ← desconexiones
```

El mensaje de registro tiene esta forma:

```json
{"device_id": "ABC123", "timestamp": 1234567890}
```

El mensaje de configuración (/config/) que llega del servidor:

```json
{"device_id": "ABC123", "Authorization": "True", "disconnect": True, "telemetry_topic": "/servers/ABC123/telemetry/", "frequency": 5.0}
```

El mensaje de telemetría:

```json
{"device_id": "ABC123", "temperature": 23.4, "timestamp": 1234567890}
```

---

```python
import os, json, datetime, time
import paho.mqtt.client as mqtt

SERIAL_NUMBER = os.getenv("DEVICE_ID")
telemetry_topic = ""
connection_granted = False
frequency = 1.0
disconnected = False

def on_connect(client, userdata, flags, rc)
	if rc == 0:
		ROUTE = "/servers/"+SERIAL_NUMBER+"/config/"
		client.subscribe(ROUTE)
		REGISTER_ROUTE = "/servers/"+SERIAL_NUMBER+"/register/"
		register_data = {"device_id": SERIAL_NUMBER,
						"timestamp": datime.datime.now() * 1000}
		client.publish(REGISTER_ROUTE, 
						payload=json.dumps(register_data), 
						qos=2, 
						retain=False)
						
		
def on_message(client, userdata, msg):
	global disconnected
	global telemetry_topic
	global frecuency
	global connection_granted
	
	if "config" in msg.topic:
		# update the client data with the response from the server
		response = msg.payload.decode()
		response = json.loads(response)
		if response["device_id"] == SERIAL_NUMBER:
			try:
				if response["Authorization"] == "True":
					frecuency = response["frecuency"]
					telemetry_topic = response["telemetry_topic"]
			except:
				pass # we should do something more serious
			if response["disconnection"] == True:
				DISCONNECTION_ROUTE = "/servers/"+SERIAL_NUMBER+"/session/" 
				disconnection_dict = {"device_id": SERIAL_NUMBER,
									  "status": "off - controlled disconnection"}
				client.publish(DISCONNECTION_ROUTE,
								payload=json.dumps(disconnection_dict),
								qos=2,
								retain=False)		
				client.loop_stop()
				client.disconnect()
				disconnected = True
		
def publish_telemetry(mqtt_client):
	current_state = {}
	current_state["device_id"] = SERIAL_NUMBER
	current_state["temperature"] = temperature
	current_state["timestamp"] = datetime.datime.now()
	
	mqtt_client.publish(telemetry_topic,
						payload=json.dumps(current_state), qos=2, retain=False)
	
def connect_mqtt():
	global client
	MQTT_SERVER = os.getenv("MQTT_SERVER")
	MQTT_PORT = int(os.getenv("MQTT_PORT", 1883))
	
	client.username_pw_set(username="fic_server", password="fic_password")
	client.on_connect = on_connect
	client.on_message = on_message
	client.on_publish = on_publish # opt - por eso la func no está definida

	will_dict = {"device_id": SERIAL_NUMBER, "status": "Off - Unregulated Disconnection"}
	connection_str = json.dumps(connection_dict)
	client.will_set("/servers/" + SERIAL_NUMBER + "/session/", will_dict)
	
	client.connect(MQTT_SERVER, MQTT_PORT, 60)

def mqtt_communications():
	global client
	client = mqtt.Client()
	connect_mqtt()
	client.loop_start()
	
	while not disconnected:
		if connection_granted:
			publish_telemetry(client)
			time.sleep(frequency)
		else:
			time.sleep(frequency)
			mqtt_disconnect() # codigo del disconnect que debería ser una funcion pero me da pereza hacerlo así
	
if __name__ == '__main__':
	try:
		t1 = threading.Thread(target=mqtt_communications, daemon=True)
		t1.start()
		t1.join()
	except Exception as e:
		print(e)
```