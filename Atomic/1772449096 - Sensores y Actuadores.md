---
aliases:
  - Sensores y Actuadores
tags:
"References":
cssclasses:
---
# Sensores y Actuadores

Componentes fundamentales que permiten a los dispositivos IoT interactuar con el mundo físico, recopilando datos (sensores) y ejecutando acciones (actuadores), para automatizar. Para ello, se usan las **interfaces entrada / salida de propósito general**.

## Interfaz de entrada/salida de propósito general

GPIO (General Purpose Input/Output) es un pin digital programable en un chip que puede configurarse por software como entrada para leer señales o como salida para enviar señales. 

- Entrada: el pin lee una señal digital de un componente externo.
- Salida: el pin envía una señal digital para controlar un actuador o componente.
- Programabilidad: el comportamiento del pin se define y cambia mediante software en tiempo de ejecución.

Los pines se clasifican en:
- **Digitales**: entrada/salida simple.
- **PWM**: modulación de ancho de pulso. Permiten controlar la cantidad de energía enviada a un dispositivo, útil para regular el brillo de LEDs o velocidad de los motores.
- **ADC**: conversión analógico-digital. Leen señales analógicas de sensores analógicas de sensores, convirtiéndolas en valores digitales que la placa puede procesar.
- **Comunicación**: I2C, SPI
	- I2C: pines como SCL y SDA para comunicación serie con múltiples dispositivos.
	- SPI: pines como MOSI, MISO y SCKL, para comunicación de alta velocidad.
- **Pines de alimentación (3.3V y 5.5V)**
- **Tierra (GND)**

### Pines Digitales

Funcionan como interruptores binarios que entienden dos estados: alto o bajo, representando 5V o 0V. Se configuran como entrada para leer señales de sensores y botones o como salida para enviar señales y controlar actuadores como LEDs y motores.

1. Configuración: antes de usar un pin, se le debe indicar si actuará como entrada o salida mediante comandos de programación.
2. Lectura (entrada):
	1. El pin detecta un voltaje.
	2. Si el voltaje supera un umbral, es HIGH. Si no es LOW.
3. Escritura (salida):
	1. El microcontrolador envía un voltaje a través del pin.
	2. Se programa enviando HIGH o LOW.

### PWM

Simulan una señal analógica al variar el ancho de los pulsos digitales que se envían a un dispositivo, permitiendo controlar la potencia efectiva que recibe. Alterna el ciclo de trabajo. 

**Funcionamiento**:
- Señal Digital de Alta Frecuencia: se genera un señal digital que alterna rápidamente entre un estado alto y un estado bajo a una frecuencia constante y elevada.
- Modulación del ancho de pulso: lo crucial es que el tiempo que la señal permanece en estado alto cambia, mientras que la frecuencia del ciclo completo permanece igual.
- Ciclo de Trabajo: este el porcentaje del período total del ciclo que la señal está en estado alto:
	- 50% de ciclo de trabajo: la señal está en alto la mitad del tiempo y en bajo la otra mitad.
	- 100% de ciclo de trabajo: la señal está siempre en alto.
	- 0% de ciclo de trabajo: la señal está siempre en bajo.

### Comunicación Serie Asíncrona

Los pines UART en la interfaz GPIO funcionan como un puerto de comunicación en serie simple que permite el intercambio de datos entre dos dispositivos utilizando solo dos cables.

La interfaz UART utiliza dos pines dedicados para la comunicación full-duplex:
1. Pin TX (Transmisor): envía datos en serie desde el dispositivo anfitrión.
2. Pin RX (Receptor): recibe datos en serie en el dispositivo anfitrión.

El pin TX de un dispositivo se conecta al pin RX del otro, y viceversa. Además, ambos dispositivos deben compartir una conexión a tierra común.

- **Comunicación asíncrona**: a diferencia de otros protocolos como SPI o I2C, UART es asíncrono, lo que significa que no utiliza una señal de reloj compartida para sincronizar la transmisión de datos.
- **Velocidad de Baudios**: para que la comunicación funcione, ambos dispositivos deben estar configurados para usar la misma actividad de transmisión de datos. 
- **Transmisión de Datos en Serie**: los datos se envían bit a bit a través de un solo cable para la transmisión y otro para la recepción, en lugar de en paralelo.
- **Estructura de la Transmisión**: cada paquete de datos suele incluir bits de inicio, los bits de datos propiamente dichos y bits de parada para delimitar el paquete y permitir que ambos dispositivos se sincronicen al comienzo de cada byte.

### Protocolo I2C

Es un bus de comunicaciones serie síncrono, diseñado para permitir que múltiples circuitos integrados digitales se comuniquen entre sí dentro de un sistema embebido utilizando un mínimo de cables.

**Comunicación a dos hilos**: solo requiere dos líneas de señal además de la alimentación (VCC y GND).
- SDA (Serial Data Line): línea bidireccional para la transferencia de datos.
- SCL (Serial Clock Line): línea para la señal de reloj, generada por el dispositivo maestro para sincronizar la comunicación.

**Arquitectura maestro-esclavo**: la comunicación es iniciada por un dispositivo maestro que también genera la señal de reloj. Otros dispositivos en el bus actúan como esclavos.

**Multimaestro y multiesclavo**: permite la conexión de múltiples dispositivos maestros y esclavos en el mismo bus.

**Comunicación semidúplex**: la información fluye en ambas direcciones, pero no de forma simultánea.

**Funcionamiento básico**
- **Condición de Inicio (START)**: el maestro inicia la comunicación generando una condición de inicio en el bus.
- **Direccionamiento**: el maestro envía la dirección del esclavo con el que quiere comunicarse, seguida de un bit que indica si la operación es de lectura o de escritura.
- **Reconocimiento (ACK, NACK)**: el esclavo seleccionado responde con un ACK para indicar que ha recibido la dirección correctamente y está listo para la comunicación. Si no responde, NACK.
- **Transferencia de datos**: el maestro o esclavo transmite o recibe los datos en bytes. Cada byte transmitido es seguido de un bit de reconocimiento.
- **Condición de Parada (STOP)**: el maestro finaliza la comunicación generando una condición de parada.

### Protocolo SPI

pag 63