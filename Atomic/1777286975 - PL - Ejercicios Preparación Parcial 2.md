---
aliases:
  - PL - Ejercicios Preparación Parcial 2
tags:
"References":
cssclasses:
---
# PL - Ejercicios Preparación Parcial 2

## Lisp / CLisp

¿Qué imprime este código CLisp?

(setq X 5) 
(print X) 
(print (+ X 2))

Respuesta:
X=5
"5"
"7"

---

¿Qué imprime este código CLisp?

(setq A 2) 
(setq B 4)
(print (* A B)) 
(setq A (+ A 1)) 
(print A)

Respuesta:
A=2
B=4
"8"
A=3
"3"

---

 `print` en CLisp devuelve el valor impreso. ¿Qué salida produce?

(setq N 10) 
(setq N (+ 1 (print (+ N 5)))) 
(print N)

Respuesta:
N=10
"15", (internamente 16), N=16
"16"

Traducción con if/else y printf. Traduce al Lisp equivalente usando el frontend `trad`:

```c
int doble_o_triple(int n) { 
	if (n == 0) { return 0 ; } 
	else { printf("%d %d\n", n, n*3) ; } 
} 
//@ (doble_o_triple 4)

---

(defun doble_o_triple (n)
	(if (= n 0)
		(progn (return-from doble_o_triple 0))
		(progn (princ n)
		(princ (* n 3)))
	)
)

(doble_o_triple 4)
```

## Gramáticas Bison

Factoriza las producciones de `List` para eliminar la ambigüedad, manteniendo la misma semántica (imprimir los números separados por espacio):
```
List: NUMBER        { printf("%d", $1.value); } 
      | NUMBER List { printf("%d ", $1.value); } ;
```

```
List: NUMBER { printf("%d\n", $1.number); } R_List

R_List: // lambda   { ; }
		|  List     { ; }
```