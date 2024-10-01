-.Se puede definir el contenido de este apartado en las siguientes fórmulas:

$$t\text{\scriptsize minor} = t\text{\scriptsize trans} + t\text{\scriptsize proc} + t\text{\scriptsize queue} + t\text{\scriptsize prop}$$

Donde $t\text{\scriptsize tx}$ (retardo de transmisión) es igual a:
$$t\text{\scriptsize trans} = L / R$$

Donde $t\text{\scriptsize proc}$ es igual a:
$$t\text{\scriptsize proc} = d / S$$

# ¿Cómo ocurren pérdidas de paquetes y los retrasos?

Existen cuatro principales tipos de retardos:
- Retardo de cola $t\text{\scriptsize queue}$: entre una red de varios dispositivos hay un router con una cola (*queue*), un *buffer*, que se va rellenando y que envía mensajes al canal. Si el buffer se llena y otro mensaje por enviar llega, **se produce una pérdida**. Existen [[protocolos de recuperación de pérdidas]] integrados en los router. 
- Retardo de transmisión $t\text{\scriptsize trans}$: tiempo que tarda el dispositivo en colocar el mensaje en canal ($t\text{\scriptsize tx}$). Se calcula dividiendo $L$ (tamaño de bits del mensaje) entre $R$ (ancho de banda).
- Retardo de propagación $t\text{\scriptsize prop}$: dependiente de la distancia $d$ a la que queremos enviar el mensaje y las características del medio $S$ (velocidad).
- Retardo de procesamiento $t\text{\scriptsize proc}$: el tiempo que tarda en procesar un nodo (del router) en procesar un paquete. Suele ser dado por el fabricante.


