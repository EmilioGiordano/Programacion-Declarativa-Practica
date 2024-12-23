# 📝 Programación Declarativa
## Paradigma de Programación Funcional
### Listas y recursión en Scheme

#### Índice
- [Función Cons](#función-cons)
- [Agregar elemento a una lista](#agregar-elemento-a-una-lista)
- [Sumatoria de una lista](#sumatoria-de-una-lista)
- [Sumatoria de dos listas](#sumatoria-de-dos-listas)
- [Eliminar elemento de la lista](#eliminar-elemento-de-la-lista)
- [Eliminar todas las apariciones de un elemento de una lista](#eliminar-todas-las-apariciones-de-un-elemento-de-una-lista)
- [Concatenar listas sin Append](#concatenar-listas-sin-append)
- [Longitud de una lista](#longitud-de-una-lista)
- [Invertir lista](#invertir-lista)


##### Función Cons
Una de las funciones más comunes que encontrará es la función «`cons`». Toma un valor y lo sitúa en el segundo argumento, una lista.
Así es exactamente como funciona «`cons`», añade un elemento a la cabeza de la lista. Puede crear una lista como sigue:

```scheme
(cons 1 '(2 3 4) )
```
El resultado es la lista `(1 2 3 4)`.


##### Agregar elemento a una lista
```scheme
(define (agregar-elemento elem lista)
  (cons elem lista))
```
```scheme
(agregar-elemento 0 '(1 2 3))
Output: '(0 1 2 3)
```

##### Sumatoria de una lista
```scheme
(define (sumatoria lista suma) 
  (if (null? lista) 
    suma
    (sumatoria  
      (cdr lista) (+ suma (car lista)) 
    ) 
  ) 
)
```
```scheme
(sumatoria '(1 2 10 ) 0) 
Output: 13
```

##### Sumatoria de dos listas
Esta resolución permite hacer la sumatoria de una lista, en caso de que la otra esté vacía, y de ambas en caso de que contengan elementos
```scheme
(define (sumatoria lista lista2 suma)
  ; Caso => ambas listas vacías, devuelve suma = 0.
  (if (and (null? lista)(null? lista2))
    suma
    ; Caso => primer lista vacía
    (if (null? lista)
      (sumatoria '() (cdr lista2) (+ suma (car lista2) ) )
      ; Caso => segunda lista vacía
      (if (null? lista2)
        (sumatoria (cdr lista) '() 
          (+ suma (car lista))
        )
        ; Caso => Ambas listas con elementos
        (sumatoria (cdr lista) (cdr lista2)
          (+ suma (+ (car lista) (car lista2)))
        )
      )
    )
  )
)
```
```scheme
(sumatoria '(2 2 2 2) '(1 3 2) 0)
Output: 14
(sumatoria '() '(1 3 2) 0)
Output: 6
(sumatoria '(1 3 2) '() 0)
Output: 6
```
##### Eliminar elemento de la lista
Utilizando `IF`
`equal?` puede ser reemplazado por un `=`
```scheme
(define (eliminar-primero elem lista) 
  (if (null? lista)
    '()
    (if (equal? elem (car lista))   ; Si el primer elemento coincide
      (cdr lista)                   ; devuelve el resto
      (cons (car lista) (eliminar-primero elem (cdr lista))) 
    )   
  )
) 
```

Utilizando `COND`
```scheme
(define (eliminar-primero elem lista)
  (cond
    ((null? lista) '())                   
    ((equal? elem (car lista)) (cdr lista)) 
    (else (cons (car lista) (eliminar-primero elem (cdr lista))))
   )
)
```
```scheme
(eliminar-primero 2 '(1 2 3 2 4))
Output: '(1 3 2 4)
```


##### Eliminar todas las apariciones de un elemento de una lista
```scheme
(define (eliminar-todos elem lista)
  (if (null? lista)
    '()
    ; Else if
    (if (= elem (car lista))
      (eliminar-todos elem (cdr lista)) 
      (cons (car lista) (eliminar-todos elem (cdr lista)))
    )
  )
)
```
Ejemplo:

Para la lista `(1 2 3 2 4)` y `elem = 2`:
- Primera llamada: `(car lista)` = 1, no coincide. Se construye `(1 ... )`.
- Segunda llamada: `(car lista) = 2`, coincide. Se ignora y se procesa (3 2 4).
- Tercera llamada: `(car lista) = 3`, no coincide. Se construye (3 ...).
- Cuarta llamada: `(car lista) = 2`, coincide. Se ignora y se procesa (4).
- Quinta llamada: `(car lista) = 4`, no coincide. Se construye (4 ...).
- Caso base: Lista vacía, se devuelve `'()`.

"Construir" significa formar una nueva lista.

Explicación: 
1. Caso base: Si la lista está vacía `(null? lista)`, retorna una lista vacía `'()`.
2. Coincidencia: Sino, si el primer elemento de la lista `(car lista)` es igual al elemento buscado `(equal? elem (car lista))`, no lo incluye y sigue procesando el resto de la lista `(eliminar-todos elem (cdr lista))`.
3. Recursión: Si no hay coincidencia, construye una nueva lista incluyendo el elemento actual `(cons (car lista) ...)` y sigue recursivamente con el resto de la lista.

Implementación utilizando `COND`
```scheme
(define (eliminar-todos elem lista)
  (cond
    ((null? lista) '())                   
    ((equal? elem (car lista)) (eliminar-todos elem (cdr lista))) 
    (else (cons (car lista) (eliminar-todos elem (cdr lista))))
  )
) 
```
```scheme
(eliminar-todos 2 '(1 2 3 2 4 2))
Output:'(1 3 4)
```


##### Concatenar listas sin Append
```scheme
(define (concatenar lista1 lista2)
  (if (null? lista1)
      lista2
      (cons (car lista1) (concatenar (cdr lista1) lista2))
  )
)
```
##### Longitud de una lista
```scheme
(define (longitud lista)
  (if (null? lista)
      0
      (+ 1 (longitud (cdr lista)))
  )
)
```
```scheme
(longitud '(A 1 2 3 2 4))
Output: 6
```
##### Invertir lista
```scheme
(define (invertir lista)
  (if (null? lista)
      '()
      (concatenar (invertir (cdr lista)) (list (car lista)))
  )
)
```

---
✍️ **Autor:** Emilio Giordano  
🔗 Más resúmenes de Programación Declarativa en el [repositorio](https://github.com/EmilioGiordano/Programacion-Declarativa-Practica)  

---