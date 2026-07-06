---
aliases:
  - MQTT - Ejercicio 1
tags:
"References":
cssclasses:
---
# MQTT - Ejercicio 1

Es importante ser capaz de seguir un flujo para poder generalizar cualquier tipo de problema de programación de MQTT.

1. **Definición de variables globales**: `topic, frequency, flags de estado`
2. **Crear cliente**: `mqtt.Client()`
3. **Asignar callbacks + will**: `on_connect, on_message, will_set`
4. **Conectar al broker**: `client.connect(host, port, keepalive)`
5. **Iniciar bucle de red**: `client.loop_start() -> thread`
6. **on_connect**: `suscribe + pusblish identification`
7. **on_message**: `parser JSON -> actualizar estado global`
8. **Bucle principal**: `publish telemetry + time.sleep(frequency)`
9. **Desconexión**: `pusblish estado -> loop_stop -> disconnect`

---

```python
import time, threading, os, subprocess, random
import json
import paho.mqtt.client as mqtt

# 1. definición de variables globales
telemetry_topic = ""
connection_granted = False
frequency = 1.0
disconnected = False
container_Id = "Prueba"
container_host_name = os.getenv("SERIAL_NUMBER")

# 3. callbacks + will
def on_connect(client, userdata, flag, rc):
	if rc == 0:
		CONFIG_TOPIC = "/fic/containers/" + container_host_name + "/config/"
		client.suscribe(CONFIG_TOPIC)
		REQUEST_ACCESS_TOPIC = "/fic/containers/" + container_host_name + "/request_acess/"
		request_access_message = {
			"Container_id": container_id,
			"Timestamp":datetime.datetime.timestamp(datetime.datetime.now())
		}
		client.publish(REQUEST_ACCESS_TOPIC,
						payload=json.dumps(request_access_message, 
						qos=2, 
						retain=False))

def on_message(client, userdata, msg):
	global connection_granted
	global telemetry_topic
	global frequency
	
	if "config" in msg.topic:
		config_received = msg.payload.decode()
		json_config_received = json.loads(config_received)
		if json_config_received["Container_id"] == tachograph_id:
		
			try:
				if json_config_received["Authorization"] = "True":
					connection_granted=True
					telemetry_topic = json_config_received["Telemetry Topic"]
				else:
					mqtt_disconnect()
			except:
				pass
				
			try:
				if json_config_received["Disconnection"] == "True":
					mqtt_disconnect()
					telemetry_topic = json_config_received["Telemetry Topic"]
			except:
				pass 
	
			try:
				if json_config_received["Frequency"] == "True":
					mqtt_disconnect()
					telemetry_topic = json_config_received["Telemetry Topic"]
					
def connect_mqtt():
	global client
	MQTT_SERVER = os.getenv("MQTT_SERVER")
	MQTT_PORT = int(os.getenv("MQTT_PORT"))
	
	client.username_pw_set(username="fic_server", password="fic_password")
	client.on_connect = on_connect
	client.on_publish = on_publish # opt - por eso la func no está definida
	client.on_message = on_message
	
	connection_dict = {"Container_id": tachograph_id, 
						"Status": "Off - Unregulate Disconnection"}
	connection_str = json.dumps(connection_dict)
	client.will_set(SESSION_TOPIC, connection_str)
	client.connect(MQTT_SERVER, MQTT_PORT, 60)
	
def publish_telemetry(mqtt_client):
	global number_telemetries_sent
	
	current_state = {}
	current_state["Timestamp"] = data["Timestamp"]
	current_state["Container_id"] = f"Container"_id
	current_state["CO2"] = current_co2
	current_state["motor_speed"] = current_motor_speed
	current_state["location"] = {"lat": current_lat, "lon": current_lon}
	current_state["doors"] = current_door_state
	
	mqtt_client.publish(telemetry_topic, 
						payload=json.dumps(current_state),
						qos=1, 
						retain=False)
						
def mqtt_disconnect():
	global client
	global disconnected
	
	SESSION_TOPIC = "/fic/containers/" + Container_Host_Name +
	"/session/"
	disconnected_dictionary = {"Container_id": Container_id,
	"Status": "Off - Planned Disconnection",
	"Timestamp": datetime.datetime.timestamp(datetime.datetime.now())}
	json_disconnected_string = json.dumps(disconnected_dictionary)
	
	client.publish(SESSION_TOPIC, 
					payload=json_disconnected_string,
					qos=1, 
					retain=False)
	print("Disconnecting: {}".format(json_disconnected_string))
	
	client.loop_stop()
	client.disconnect()
	disconnected = True
	
def mqtt_communications():
	global client
	
	client = mqtt.Client()
	connect_mqtt()
	client.loop_start()
	
	while not disconnected and not monitor.kill_now:
		if connection_granted:
			publish_telemetry(client)
			time.sleep(frequency)
		else:
			time.sleep(frequency)
	mqtt_disconnect()
	
if __name__ == '__main__':
	try:
		t1 = threading.Thread(target=mqtt_communications, daemon=True)
		t1.start()
		t1.join()
	except Exception as e:
		print(e)
	
	
```