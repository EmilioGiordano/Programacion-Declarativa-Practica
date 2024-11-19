## Programación funcional: Listas y recursión en Scheme

#### Índice
- [Función Cons](#función-cons)
- [Agregar elemento a una lista](#agregar-elemento-a-una-lista)
- [Sumatoria de una lista](#sumatoria-de-una-lista)
- [Sumatoria de dos listas](#sumatoria-de-dos-listas)
- [Eliminar elemento de la lista](#eliminar-elemento-de-la-lista)
- [Quitar todos los elementos N de una lista](#quitar-todas-las-apariciones-de-un-elemento)
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
    (display suma) 
    (sumatoria  
      (cdr lista)(+ suma (car lista)) 
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
  (if (and (null? lista)(null? lista2))
    suma
    (if (null? lista)
      (sumatoria '() (cdr lista2)(+ suma (car lista2) ) )
      (if (null? lista2)
        (sumatoria (cdr lista) '()(+ suma (car lista) ) )
        (sumatoria (cdr lista) (cdr lista2) (+ suma (+ (car lista) (car lista2))))
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

##### Quitar todas las apariciones de un elemento
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
