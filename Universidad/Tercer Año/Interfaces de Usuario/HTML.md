**HTML**: lenguaje de marcado para definir y estructurar contenido web. El contenido se estructura a través de etiquetas o *tags*. #html
```html
<h1>Hello World!</h1>
```

Hay dos tipos de elementos: **de bloque** y **de línea**. Los primeros son elementos estructurales que representan párrafos, listas, menús de navegación... Los segundos son contenidos dentro de elementos de bloque.

*Ejemplo de elemento de bloque*
```html
<p>Esto es un párrafo</p>
```
*Ejemplo de elemento de línea*
```html
<p>Esto es un <span>párrafo</span></p>
```

Todos los elementos tienen ciertos atributos, pero los únicos que son comunes para todas las etiquetas son el **id** y las **clases**. El id es un atributo único, mientras que un elemento puede tener `n` clases.

El propio documento suele tener una estructura intrínseca que debe de estar bien definida para poder ser validado.
```html
<!DOCTYPE html>
<html> 
<head>
<body>
```

Dentro del body, se nos permite agrupar contenedores, tanto genéricos como semánticos. Es recomendable usar siempre los **contenedores semánticos**, ya que facilita, entre otras cosas, el SEO.

Algunos de los contenedores semánticos son:
- main: contenido principal del cuerpo del documento.
- header: contenido introductorio (usualmente se introduce el nav aquí)
- footer: pie de página 
- nav: barra de navegación
- section: agrupa contenido relacionado. Generalmente tiene un encabezado asociado
- article: apartado dentro de una section
- aside: contenido no relacionado con respecto al propio documento