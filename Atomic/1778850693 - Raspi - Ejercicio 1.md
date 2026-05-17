---
aliases:
  - Raspi - Ejercicio 1
tags:
"References":
cssclasses:
---
# Raspi - Ejercicio 1

```python
import RPi.GPIO as GPIO
import mpu5060
import GPS
import sys, signal, time, threading, os
import json

# definimos las variables globales sin settear valores reales, solamente los sensores y actuadores que van puramente por GPIO; no por protocolos como SPI o I2C
button_pin = 0
rgb_1_red=0
rgb_1_green=0
rgb_1_blue=0
rgb_2_red=0
rgb_2_green=0
rgb_2_blue=0
should_run=False

mpu_object=None
gps_object=None
speed_registry=[]
accelerometer_state="stop"
gps_state="stop"
position_registry=[]
current_speed=0.0

def setup_devices():
	global button_pin
	global rgb_1_red
	global rgb_1_green
	global rgb_1_blue
	global rgb_2_red
	global rgb_2_green
	global rgb_2_blue
	global mpu_object
	global gps_object
	
	mpu_object = mpu6050()
	gps_object = GPS()
	
	GPIO.setmode(GPIO.BCM)
	GPIO.setwarnings(False)
	button_pin=16
	GPIO.setup(button_pin, GPIO.IN, pull_up_down=GPIO.PUD_UP)
	
	rbg_1_red=23
	GPIO.setup(rgb_1_red, GPIO.OUT)
	rbg_1_green=24
	GPIO.setup(rgb_1_green, GPIO.OUT)
	rbg_1_blue=25
	GPIO.setup(rgb_1_blue, GPIO.OUT)
	
	rbg_2_red=5
	GPIO.setup(rgb_2_red, GPIO.OUT)
	rbg_2_green=6
	GPIO.setup(rgb_2_green, GPIO.OUT)
	rbg_2_blue=13
	GPIO.setup(rgb_2_blue, GPIO.OUT)
	
def signal_handler(sig):
	GPIO.cleanup()
	sys.exit(0)
	
def button_released_callback(channel):
	global should_run
	should_run != should_run
	
def led_manager():
	pass
	
def accelometer_manager():
	pass
	
def gps_manager():
	pass
	
def start_program():
	global t1, t2, t3
	
	t1 = threading.Thread(target=led_manager, daemon=True)
	t2 = threading.Thread(target=accelometer_manager, daemon=True)
	t3 = threading.Thread(target=gps_manager, daemon=True)
	t1.start()
	t2.start()
	t3.start()
	
if __name__=='__main__':
	try:
		setup_devices()
		
		GPIO.add_event_detect(button_pin, GPIO.RISING, callback=button_released_callback, bouncetime=200)
		signal.signal(signal.SIGINT, signal_handler)
		
		start_program()
		
		while True:
			pass
	except Exception as e:
		print(e)
		sys.exit(0)
```