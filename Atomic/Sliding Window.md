# Sliding Window

Los paquetes que están siendo enviados se encuentran en dicha ventana.

Los paquetes de dicha ventana **deben de ser recordados**: una vez que un paquete devuelve un ACK, dicho paquete se olvida y uno nuevo entra en la ventana.

## Repetición selectiva

El receptor **requiere de un buffer** de igual tamaño que el emisor para poder guardar paquetes y reordenarlos.

>[!bug] Problema
>- Guardar tantos temporizadores para tantos paquetes es complicado
>- Guardar tantos paquetes en el receptor no es lo mejor

### Go-Back-N

Solo hay un temporizador -> dicho temporizador está asociado con el paquete más antiguo de la ventana.

El receptor solo quiere el siguiente paquete, si el paquete no ha sido recibido, manda un ACK del paquete que está esperando.

