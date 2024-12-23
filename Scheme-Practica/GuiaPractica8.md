Programación funcional – Decisiones y recursión 

# 📝 Programación Declarativa
## Paradigma de Programación Funcional
### Unidad 6: Decisiones y recursión 

# Índice

### Decisiones
- [1. Definir una función que reciba un número y devuelva verdadero si el mismo es par](#1-definir-una-función-que-reciba-un-número-y-devuelva-verdadero-si-el-mismo-es-par)
- [2. Número divisible por 6](#2-número-divisible-por-6)
- [3. Mayor de dos números](#3-mayor-de-dos-números)
- [4. Múltipo](#4-múltiplo)
- [5. Múltiplo](#5-múltiplo)
- [6. Tres números iguales](#6-tres-números-iguales)
- [7. Dos de tres números iguales](#7-dos-de-tres-números-iguales)
- [8. Eficiencia de una máquina](#8-eficiencia-de-una-máquina)

### Listas recursivas
- [9. ¿Elemento pertenece a una lista?](#9-¿elemento-pertenece-a-una-lista)
- [10. Cantidad de elementos de una Lista](#10-cantidad-de-elementos-de-una-lista)
- [11. Sumatoria de una lista](#11-sumatoria-de-una-lista)
- [12. Cantidad de números naturales de la lista](#12-cantidad-de-números-naturales-de-la-lista)
- [13. Numeros entre m & n](#13-numeros-entre-m--n)
- [14. Último elemento de una lista](#14-último-elemento-de-una-lista)
- [15. Concatenación de listas](#15-concatenación-de-listas)
- [16. Reemplazar átomo a por b en una lista](#16-reemplazar-átomo-a-por-b-en-una-lista)

### Decisiones
#### 1. Definir una función que reciba un número y devuelva verdadero si el mismo es par

```scheme
(define (esPar numero)
  (if (= (remainder numero 2) 0)
      "El número es par"
      "El número es impar"))
```
`(remainder x 2)`: Calcula el residuo de dividir x por 2.
`(= (remainder x 2) 0)`: Compara si el resultado de remainder x 2 es igual a 0. Esta expresión devolverá #t (verdadero) si el residuo es 0 y #f (falso) si no lo es

```prolog
(esPar 12) 
Output: "El número es par"
(esPar 7)
Output: "El número es impar"
```

#### 2. Número divisible por 6
Definir una función que acepta un número y devuelve verdadero si dicho número es divisible por seis

```scheme
(define (divisiblePorSeis numero)   
  (= (remainder numero 6) 0))
```
```scheme
(divisiblePorSeis 13)
Output:#f
(divisiblePorSeis 12)
Output:#t
```

#### 3. Mayor de dos números
Definir una función que reciba dos números y devuelva el mayor de ambos
```scheme
(define (mayor x y) 
  (if (> x y) x y)
)
```
```scheme
(mayor 10 5)
Output: 10
```
#### 4. Múltiplo
Definir una función que reciba dos números y devuelva verdadero si el segundo es múltiplo del primero
```scheme
(define (multiplo x y)
  (= (remainder x y) 0)
)
```
`(remainder x y)` devuelve el valor del resto que queda después de dividir x por y.
###### 10 / 5 = 2. Residuo 0. Es multiplo
###### 10 / 3 = 3. Residuo 1. No es multiplo

#### 5. Múltiplo 
Definir una función que reciba dos números y devuelva verdadero si alguno de ellos es  múltiplo del otro

```scheme
(define (multiplo x y)
    (or (= (remainder x y) 0)
        (= (remainder y x) 0)
    )
)
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

#### 6. Tres números iguales
Definir una función que reciba tres números y devuelva verdadero si los tres números son  iguales
```scheme
(define (iguales x y z)
  (and
    (= x y)
    (= x z)
    (= z y)
  )
)
```
```scheme
(iguales 10 10 10)
Output: #t
(iguales 101 10 10)
Output: #f
```
#### 7. Dos de tres números iguales 
Definir una función que acepta tres números y devuelva verdadero si dos de ellos sin iguales
```scheme
(define (iguales x y z)
  (or
    (= x y)
    (= x z)
    (= z y)
  )
)
```
```scheme
(iguales 10 11 11)
Output: #t
(iguales 11 12 13)
Output: #f
```

#### 8. Eficiencia de una máquina
En una fábrica, la eficiencia de una máquina se calcula en función de las piezas producidas, por una parte, y de las piezas defectuosas por la otra
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

### Listas recursivas
- Estructura de datos. 
- Almacena serie de términos u otras listas.
- Es una secuencia ordenada.
- Longitud variable.Se compone de cabeza y cola [CABEZA | COLA].
![Listas en Prog  Declarativa](https://github.com/user-attachments/assets/372dbc66-a10b-4796-9a0c-61100bd3475b)

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
(pertenece 7 '(5 4 7))
Output: #t
(pertenece 3 '(5 4 7))
Output: #f
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

#### Extra: Sumar elementos de una lista
```scheme
(define (sumarLista lista)
  (if (null? lista)                   
      0                            
      (+ (car lista)                  
         (sumarLista (cdr lista))
      )
  )
)
```

```scheme
(sumarLista '(-23 12 23))
```
#### Extra: Verificar si la lista esta vacia
```scheme
(define (verificarLista lista)
    (if (null? lista)
      "Vacia"
      "con elementos"
    )
)   
```
```scheme
(verificarLista '(1))
Output: "con elementos"
(verificarLista '(a))
Output: "con elementos"
(verificarLista '())
Output: "Vacia"
```
#### 10. Cantidad de elementos de una lista
Escribir una función que acepte una lista y devuelva la cantidad de elementos de esa lista.

```scheme
(define (cantidad lista contador)
  (if (null? lista)
    (display contador)
    (cantidad (cdr lista) (+ contador 1))
  )
)
```
```scheme
(cantidad '(1 2 3 4 5 6  8 9) 0)
Output: 8
```
__Alternativa__ (Length):
```scheme
(define (cantidad lista) (length lista))
```
#### 11. Sumatoria de una lista
Escribir una función que acepte una lista numérica y devuelva la sumatoria de la misma. 

```scheme
(define (sumar lista) 
  (apply + lista)
)
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

##### 12. Cantidad de números naturales de la lista
Escribir una función que acepte una lista de números enteros y devuelva la cantidad de
números naturales que contiene la lista.

```scheme
(define (es-natural n)
  (and (integer? n) (>= n 0))
)

(define (contar-naturales lista)
  (if (null? lista)
    0
    (+(if (es-natural (car lista) ) 1 0)
      (contar-naturales (cdr lista) )
    )
  )
)
```

```scheme
(contar-naturales '(1 -2 3 4.5 5))    ; Devuelve 3
(contar-naturales '(0 -1 2))          ; Devuelve 2
(contar-naturales '(-3 -5 -7))        ; Devuelve 0
(contar-naturales '(3.14 "texto" 2))  ; Devuelve 1
(contar-naturales '())                ; Devuelve 0
```
Alternativa utilizando __cond__
```scheme
(define (es-natural n)
  (and (integer? n) (>= n 0))
)

(define (contar-naturales lista)
  (cond
    [(null? lista) 0]
    [(es-natural (car lista))
      (+ 1 (contar-naturales (cdr lista)))
    ]
    [else (contar-naturales (cdr lista))]
  )
)
```

```scheme
(contar-naturales '(1 -2 3 4.5 5))    ; Devuelve 3
(contar-naturales '(0 -1 2))          ; Devuelve 2
(contar-naturales '(-3 -5 -7))        ; Devuelve 0
(contar-naturales '(3.14 "texto" 2))  ; Devuelve 1
(contar-naturales '())                ; Devuelve 0
```

##### 13. Numeros entre m & n
Escribir una función "esta-entre", que acepta dos números enteros "m" y "n", y devuelve la lista de los enteros mayores o iguales que "m" y menores o iguales que "n". 

```scheme
(define (esta-entre m n)
  (if (> m n)
    '()
    (cons m (esta-entre(+ m 1) n) )
  )
)
```
```scheme
(esta-entre 1 10)
Output: '(1 2 3 4 5 6 7 8 9 10)
(esta-entre 1 1)
Output: '(1)
(esta-entre 5 0)
Output: '()
```
##### 14. Último elemento de una lista
Definir una función que acepta una lista devuelve el último elemento de ésta.
```scheme
(define (ultimo lista)
  (if (null? lista)
      '()
      (if (null? (cdr lista) )
          (car lista)
          (ultimo (cdr lista) )
      )
  )
)
```
__Caso Base__: Se verifica si la lista está vacía utilizando `(null? lista)`. Si es así, devuelve la lista vacía.
__Segundo Caso Base__: Se verifica si el resto de la lista es vacío `(null? (cdr lista))`. Si esto es cierto, significa que el __primer elemento__ es el __único__ elemento de la lista, por lo que se devuelve con `(car lista)`.
__Recursión__: Si la lista tiene más de un elemento, se llama a __ultimo__ recursivamente con el resto de la lista `(cdr lista)`.
    
```scheme
(ultimo '(1 2 3 4 5))  ; Devuelve 5
(ultimo '(a b c d))    ; Devuelve d
(ultimo '(42))         ; Devuelve 42
```

##### 15. Concatenación de listas
Definir una función que acepte dos listas y devuelva una lista que sea la concatenación de éstas.

```scheme
(define (concatenar lista1 lista2) 
  (if (null? lista1) 
      lista2 
      (cons (car lista1) (concatenar (cdr lista1) lista2)) 
  ) 
)
```
```SCHEME
(concatenar '(1 2 3 4 ) '(a b c d ))
Output: '(1 2 3 4 a b c d)
```

##### 16. Reemplazar átomo a por b en una lista
Definir una función que acepta una lista y dos átomos "a" y "b", y devuelve otra lista con los elementos de la primera, pero con el átomo "a" sustituido por el "b", en su primera ocurrencia.

```scheme
(define (sustituir-primera lista a b)
  (if (null? lista)
      '()  
      (if (equal? (car lista) a)  ; Si el primer elemento es igual a a
          (cons b (cdr lista))  ; Sustituye por b y devuelve el resto de la lista.
          (cons (car lista) (sustituir-primera (cdr lista) a b))  ; Mantiene el elemento y llama recursivamente.
      )
  )
)  
```

```scheme
(sustituir-primera '(1 2 3 a 4 a) 'a 'b)  ; Devuelve '(1 2 3 b 4 a)
(sustituir-primera '(a b c d) 'a 'x)      ; Devuelve '(x b c d)
(sustituir-primera '(1 2 3) 'a 'b)        ; Devuelve '(1 2 3)
(sustituir-primera '() 'a 'b)             ; Devuelve '()
```

---
✍️ **Autor:** Emilio Giordano  
🔗 Más resúmenes de Programación Declarativa en el [repositorio](https://github.com/EmilioGiordano/Programacion-Declarativa-Practica)  

---