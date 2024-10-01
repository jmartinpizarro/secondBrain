# Envío con errores de bit

Se usa métodos de detección como el [[Checksum]]. Si se encuentra un error en el checksum, el paquete se elimina y se pide que se vuelva a enviar.

El ciclo se ve tal que así:
$$
\text{envío paquete → recibido → eliminado/aceptado → reconocimiento positivo/negativo }
$$

Los **acknowledgments** (ACKs y NAKs) son:
	- Reconocimiento positivo (ACK): pide que se envíe el siguiente paquete
	- Reconocimiento negativo (NAK): pide que se envíe el paquete anterior

>[!danger] PROBLEMA
>Este método no toma en cuenta que **puede haber un error en los paquetes de reconocimiento**. Es difícil de solucionar ya que:
>- Añadir un checksum a estos paquetes no arregla nada. Se repite la misma vulnerabilidad
>- Visión optimista del emisor: el paquete se pierde. Los datos erróneos se pierden y se hace una petición del paquete
>- Visión pesimista del emisor: el paquete se manda dos veces. *¿Es lo mismo "duplicación" que "no pérdida de datos"?* No, pero se puede solucionar si al recibirse los paquetes los vamos enumerando. **Si el paquete recibe un mensaje duplicado que ya está enumerado, lo descarta y envía un ACK positivo**. 

Estas visiones optimistas/pesimistas se pueden determinar como ACKs y NAKs respectivamente. Si va todo bien, recibimos ACK. Si algo falla, independientemente de lo que sea, recibimos un NAK.

## Seguridad de los paquetes de reconocimiento

Una comunicación sin errores se vería tal que así:
1. El emisor envía el paquete con número de secuencia **pck0**.
2. El receptor envía un **ACK** (reconocimiento) confirmando que ha recibido **pck0**.
3. El emisor envía el paquete con número de secuencia **pck1**.
4. El receptor envía un **ACK** para **pck1**.
5. Y así sucesivamente, alternando entre `pck0` y `pck1`.

Mientras que una **comunicación con errores se vería tal que así**:
1. El emisor envía el paquete **pck0**.
2. El receptor recibe **pck0** y envía el **ACK** para **pck0**.
3. El emisor envía el paquete **pck1**.
4. Por alguna razón, el **ACK** para **pck1** se pierde o no llega al emisor.
5. El emisor interpreta que **pck1** no fue recibido (porque no recibió el ACK para **pck1**), así que retransmite **pck1**.
6. Esta vez, el receptor recibe correctamente **pck1** y envía un **ACK** para **pck1**.

De esta forma, es posible eliminar el NAK.
## Eliminar el NAK

Eliminamos el NAK de nuestra lógicamente, solamente usaremos ACKs. ¿Cómo?

El truco está en que si el receptor no recibe correctamente un paquete (o lo pierde), no envía un NAK. En su lugar, reenvía el último número de secuencia que recibió correctamente.

1. Emisor envía pck0
2. Receptor recibe pck0
3. Emisor envía pck1
4. Receptor no recibe pck1, así que envía pck0 -> Emisor vuelve a enviar pck1

### Máquinas de Estados Finitas Completas 

- Emisor y receptor necesitan saber el número de paquetes para enumerarlos y comprobar si hay duplicados. 
- Como con la eliminación de un NAK solamente puede haber dos enumeraciones posibles, alternar entre ACKs y NAKs es suficiente.

>[!danger] PROBLEMA
>El espacio en la secuencia de números debe de ser finito

