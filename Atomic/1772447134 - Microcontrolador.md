---
aliases:
  - Microcontrolador
tags:
"References":
cssclasses:
---
# Microcontrolador

**Microcontrolador**: circuito integrado programable, capaz de ejecutar las órdenes grabadas en su memoria. Está compuesto de varios bloques funcionales que cumplen una tarea específica. Un microcontrolador incluye en su interior las tres principales unidades funcionales de una computadora:
- CPU
- Memoria
- Periféricos de entrada/salida

Algunos controladores pueden utilizar palabras de cuatro bits y funcionan a velocidad de reloj con frecuencias tan bajas como 4kHz, con un consumo de baja potencia (microwatts o mW). Por lo general, tendrá la capacidad de mantenerse a la espera de un evento como pulsar un botón o de otra interrupción, lo que reduce incluso aún más el consumo de energía.

#### Placas básicas

- **Arduino UNO**: la placa más conocida de la familia Arduino.
- **Raspberry Pi**: un microcontrolador de bajo coste. Se programa en lenguajes como MicroPython y C++.
- **ESP32**: populares por su capacidad de conectividad Wi-Fi y Bluetooth. Perfectas para IoT.

#### Placas Intermedias y Avanzadas

Se busca más potencia de procesamiento, más periféricos y mayor escalabilidad, estas placas son una buena opción para proyectos más complejos.
- **STM32 (ARM Cortex M)**: con un mayor rendimiento y eficiencia energética, las placas basadas en los microcontroladores STM32 son ideales para aplicaciones avanzadas.
- **Placas FPGA**: proporcionan una mayor de velocidad y flexibilidad, siendo la opción preferida para aplicaciones que requieren un alto grado de paralelismo y personalización.

#### Lenguajes de programación

- Entorno de desarrollo de Arduino (IDE): ideal para principiantes, este IDE es fácil de usar y se basa en una versión simplificada de C++.
- MicroPython: permite programar controladores con el lenguaje Python, lo que simplifica el proceso y es ideal para principiantes.
- C y C++: lenguajes de programación más potentes y versátiles, utilizados para proyectos más avanzados y de alto rendimiento.
- Lenguaje ensamblador (ASM): permite controlar directamente el microcontrolador. Más complejo de usar.

## Microcontroladores en producción

- Coste elevado: precio por unidad es demasiado alto para la producción en masa, ya que se paga por componentes que no se usarán en el producto final.
- Tamaño no optimizado: el tamaño de la placa no es compacto y no está diseñado para ajustarse a las dimensiones específicas del producto final.
- Falta de robustez: no tiene las protecciones adecuadas contra condiciones industriales como el ruido eléctrico, los golpes o las temperaturas extremas.

**Placas de producción**: diseños personalizados y optimizados para la fabricación en masa. El objetivo es reducir costos, tamaño y consumo de energía mientras se aumenta la durabilidad y fiabilidad.
- Diseño personalizado
- Microcontrolador dedicado
- Optimización de recursos
- Fabricación y pruebas
- Integración de periféricos: los periféricos se integran directamente en el PCB, en lugar de usar módulos externos.

## Arduino

Plataforma de desarrollo de electrónica de hardware y software libres que incorpora un microcontrolador reprogramable. Permite a los usuarios crear objetos electrónicos interactivos, como robots o sistemas domóticos, conectando el mundo físico con el virtual.

Las placas incluyen:
- Microcontrolador
- Pines de Entrada/Salida
- Puerto USB
- Conector de alimentación
- Botón de reinicio

### Beneficios de Arduino

- Bajo costo
- Facilidad de uso
- Gran comunidad con muchos recursos
- Versatilidad para una gran variedad de proyectos
- Es open-source

## Raspberry Pi

Ordenador de placa única de bajo coste y tamaño reducido.
- Formato compacto
- Bajo costo
- Conectividad verśatil
- Pines GPIO: pines de entrada/salida que permiten interactuar y controlar componentes electrónicos externos, como sensores y LEDs. 
- Sistemas Operativo: basado en una versión de Linux optimizada para la placa, aunque también puede ejecutar otras versiones de Linux y versiones adaptadas a Windows.

Las diferencias clave entre modelos radican en:
- Potencia de procesamiento
- Cantidad y tipo de RAM
- Conectividad

Uso de **procesadores ARM** (*Advanced RISC Machines*) son una familia de unidades centrales que usan la ISA de RISC.

## ESP32

Sistemas electrónicos de bajo costo que integran un potente microcontrolador, ofreciendo Wi-Fi, Bluetooth y un procesador de doble núcleo. Permite programar dispositivos inteligentes usando sensores y actuadores; es una alternativa popular a Arduino.

Además de C++, MicroPython y otros, también se usa *Espressif IoT Development Framework (ESP-IDF)*

- SDK autosuficiente
- Lenguajes de programación
- Conectividad
- Sistema Operativo en Tiempo Real (RTOS): permite aplicaciones multitarea
