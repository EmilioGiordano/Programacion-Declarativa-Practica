Programación funcional – Decisiones y recursión 
1. Definir una función que reciba un número y devuelva verdadero si el mismo es par

```scheme
(define (esPar x)
  (if (= (remainder x 2) 0)
      "El número es par"
      "El número es impar"))
```
`(remainder x 2)`: Calcula el residuo de dividir x por 2.
`(= (remainder x 2) 0)`: Compara si el resultado de remainder x 2 es igual a 0. Esta expresión devolverá #t (verdadero) si el residuo es 0 y #f (falso) si no lo es

```prolog
(esPar 12) 
(esPar 7)
```

2. Definir una función que acepta un número y devuelve verdadero si dicho número es divisible  por seis. 

```scheme
(define (divisiblePorSeis x)   
  (= (remainder x 6) 0))
```
```scheme
(divisiblePorSeis 13)
Output:#f
(divisiblePorSeis 12)
Output:#t
```

3. Definir una función que reciba dos números y devuelva el mayor de ambos.
```scheme
(define (mayor x y) (if (> x y) x y))
```
```scheme
(mayor 10 5)
Output: 10
```
4. Definir una función que reciba dos números y devuelva verdadero si el segundo es múltiplo del primero. 
```scheme
(define (multiplo x y)
  (= (remainder x y) 0))
```
`(remainder x y)` devuelve el valor del residuo que queda después de dividir x entre y.
###### 10 / 5 = 2. Residuo 0. Es multiplo
###### 10 / 3 = 3. Residuo 1. No es multiplo

5. Definir una función que reciba dos números y devuelva verdadero si alguno de ellos es  múltiplo del otro. 

```scheme
(define (multiplo x y)
    (or(= (remainder x y) 0)
    (= (remainder y x) 0)))
```

```scheme
(multiplo 5 10)
Output: #t
(multiplo 10 5)
Output: #t
(multiplo 10 3)
Output: #f
(multiplo 3 10)
Output: #f
```

6. Definir una función que reciba tres números y devuelva verdadero si los tres números son  iguales. 
```scheme
(define (iguales x y z)
  (and
    (= x y)
    (= x z)
    (= z y)
  ))
```
```scheme
(iguales 10 10 10)
Output: #t
(iguales 101 10 10)
Output: #f
```

7. Definir una función que acepta tres números y devuelva verdadero si dos de ellos sin iguales.
```scheme
(define (iguales x y z)
  (or
    (= x y)
    (= x z)
    (= z y)
  ))
```
```scheme
(iguales 10 11 11)
Output: #t
(iguales 11 12 13)
Output: #f
```

8. En una fábrica, la eficiencia de una máquina se calcula en función de las piezas producidas, por una parte, y de las piezas defectuosas por la otra.
__Las condiciones son las siguientes:__ 
- Producción mínima: 1000 piezas. 
- Máximo de piezas defectuosas: 20 
El puntaje asignado a la máquina se calcula como sigue: 
- Puntaje 1: si no cumple con ninguna de las condiciones. 
- Puntaje 2: si cumple sólo con la segunda. 
- Puntaje 3: si cumple sólo con la primera. 
- Puntaje 4: si cumple con ambas. 
Definir una función que acepte la cantidad de piezas producidas y defectuosas y devuelva el  puntaje que corresponda. 



```scheme
(define (puntaje piezasProducidas piezasDefectuosas)
  (cond 
    [(and(> piezasProducidas 1000)(< piezasDefectuosas 20)) "Puntaje 4."]
    [(> piezasProducidas 1000) "Puntaje 3."]
    [(< piezasDefectuosas 20) "Puntaje 2."]
    [else "Puntaje 1."]
  )
)
```

```scheme
(puntaje 1000 20)
Output: "Puntaje 1."
(puntaje 1000 19)
Output: "Puntaje 2."
(puntaje 1001 20)
Output: "Puntaje 3."
(puntaje 1001 19)
Output: "Puntaje 4."
```

#### 9. ¿Elemento pertenece a una lista? 
Escribir una función que acepte un elemento y una lista, y devuelva verdadero si el elemento  pertenece a la lista. 
```scheme
(define 
  (pertenece elemento  lista)
    (if (null? lista)                 
        #f                             
        (if (= (car lista) elemento )          
            #t                        
            (pertenece elemento  (cdr lista))
        )
    )
)
```
`(null? lista)`: Verifica si la lista está vacía. 
`(car lista)`: Devuelve el primer elemento de la lista.
`(cdr lista)`: Devuelve la lista sin el primer elemento, es decir, el resto de la lista.
`(= (car lista) elemento)`: Compara el primer elemento de la lista con el elemento que estamos buscando.
- __Si son iguales__, devuelve #t (verdadero), lo que significa que el elemento sí pertenece a la lista.
- __Si no son iguales__, la función se llama recursivamente para continuar buscando el elemento en el resto de la lista: (pertenece elemento (cdr lista)).


```scheme
(pertenece 3 '(5 4 7))
```

El símbolo `'`(apóstrofe) antes de un paréntesis en '(5 4 7) se usa en Racket (y otros lenguajes de la familia Lisp) para crear una lista literal. Esto significa que estás indicando al intérprete que no debe evaluar el contenido de la lista, sino que debe considerarlo como una lista literal de elementos.

##### Flujo:
__Primera llamada__:
- (pertenece 3 '(5 4 7)): La lista no está vacía, el primer elemento 5 no es igual a 3.
- Se llama recursivamente con el resto de la lista: (pertenece 3 '(4 7)).

__Segunda llamada__:
- (pertenece 3 '(4 7)): La lista no está vacía, el primer elemento 4 no es igual a 3.
- Se llama recursivamente con el resto de la lista: (pertenece 3 '(7)).

__Tercera llamada__: 
- (pertenece 3 '(7)): La lista no está vacía, el primer elemento 7 no es igual a 3.
- Se llama recursivamente con el resto de la lista: (pertenece 3 '()).

__Cuarta llamada__: 
- (pertenece 3 '()): La lista está vacía, por lo que devuelve #f

#### Extra: Sumar elementos de una Lista. 
```scheme
(define (sumarLista lista)
  (if (null? lista)                   ; Verificamos si la lista está vacía
      0                               ; Si es vacía, la suma es 0
      (+ (car lista)                  ; Si no está vacía, sumamos el primer elemento (car)
         (sumarLista (cdr lista)))))  ; y llamamos recursivamente con el resto de la lista (cdr)
```

```scheme
(sumarLista '(-23 12 23))
```


#### 10. Cantidad de elementos de una Lista. 
Escribir una función que acepte una lista y devuelva la cantidad de elementos de esa lista.

Alternativa 1:
```scheme
(define (cantidad lista) (length lista))
```
```scheme
(define (cantidad lista contador)
  (if (null? lista)
  (display contador)
  (cantidad (cdr lista) (+ contador 1))))
```
```scheme
(cantidad '(1 2 3 4 5 6  8 9) 0)
Output: 8
```
#### 11. Sumatoria de una lista.
Escribir una función que acepte una lista numérica y devuelva la sumatoria de la misma. 

```scheme
(define (sumar lst) 
  		(apply + lst))
```
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
(sumatoria '(-1000 233 1500 ) 0)
Output: 733
```
