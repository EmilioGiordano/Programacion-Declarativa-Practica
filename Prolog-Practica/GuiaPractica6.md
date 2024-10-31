## GUÍA DE EJERCICIOS: recursión y listas en Prolog

- [GUÍA DE EJERCICIOS: recursión y listas en Prolog](#guía-de-ejercicios-recursión-y-listas-en-prolog)
  - [Ejemplo: Factorial](#ejemplo-factorial)
  - [Ejercicio 1](#ejercicio-1)
      - [Hechos](#hechos)
      - [Predicados](#predicados)
      - [Consulta](#consulta)
  - [Ejercicio 2: MCD](#ejercicio-2-mcd)
      - [Consulta](#consulta-1)
  - [Ejercicio 3: Fibonacci](#ejercicio-3-fibonacci)
  - [Ejercicio 4: Ordenar una lista de dos elementos de menor a mayor](#ejercicio-4-ordenar-una-lista-de-dos-elementos-de-menor-a-mayor)
      - [Predicado](#predicado)
      - [Consulta](#consulta-2)
  - [Ejercicio 5: Cantidad de elementos de una lista](#ejercicio-5-cantidad-de-elementos-de-una-lista)
      - [Predicado](#predicado-1)
  - [Ejercicio 6: Cantidad de números reales de una lista](#ejercicio-6-cantidad-de-números-reales-de-una-lista)
      - [Predicado](#predicado-2)
  - [Ejercicio 7: Suma de elementos de una lista](#ejercicio-7-suma-de-elementos-de-una-lista)
      - [Predicado](#predicado-3)
  - [Ejercicio 8: Lista ordenada creciente](#ejercicio-8-lista-ordenada-creciente)
      - [Predicado](#predicado-4)
  - [Ejercicio 9:](#ejercicio-9)
  - [Ejercicio 10:](#ejercicio-10)
  - [Ejercicio 11:](#ejercicio-11)
  - [Ejercicio 12:](#ejercicio-12)
  - [Ejercicio 13:](#ejercicio-13)

### Ejemplo: Factorial 
```prolog
% Caso base: el factorial de 0 es 1.
factorial(0, 1).

% Caso recursivo: factorial de N es N 
% multiplicado por el factorial de N-1.
factorial(N, Resultado) :-
    N > 0,
    N1 is N - 1,          % Decrementamos N
    factorial(N1, R1),    % Llamada recursiva
    Resultado is N * R1.  % Calculamos el resultado
```
### Ejercicio 1
Dada una base de datos en la cual se describe una cadena de progenitores con hechos como:

##### Hechos
```prolog
progenitor_de(juan, luis).
progenitor_de(luis, maria).
progenitor_de(maria, ana).
progenitor_de(jose, hector).
```
__Escribir un predicado que relacione a una persona con un antepasado de la misma__

##### Predicados
```prolog
% Condicion de antepasados son padres
antepasado_de(Antepasado, Persona) :-
    progenitor_de(Antepasado, Persona).
% Condicion de antepasados son abuelos
    antepasado_de(Antepasado, Persona) :-
         progenitor_de(Antepasado, Intermedio),
         antepasado_de(Intermedio, Persona).
```
##### Consulta
```prolog
?- antepasado_de(juan, luis).
true
?- antepasado_de(juan, maria).
true
?- antepasado_de(juan, hector).
false
```
### Ejercicio 2: MCD
Resolver el problema de encontrar el MCD entre dos números, sabiendo que, si los números son iguales, el MCD es el mismo número, en otro caso el MCD es igual MCD entre el menor de ellos y la diferencia entre ambos
```prolog
% Caso base: si los numeros son iguales el MCD es 
% el mismo número.
% MCD: Maximo Comun Divisor
mcd(A, A, A).

% Si A es diferente de B, llama recursivamente 
% a mcd con el menor de los dos números y la
% diferencia.
mcd(A, B, MCD) :-
    A \= B,
    (A > B ->  
    	MCD1 is A - B,
        mcd(B, MCD1, MCD)
    ;   MCD1 is B - A,
        mcd(A, MCD1, MCD)
    ).
```
##### Consulta
```prolog
?- mcd(4,12, MCD)
MCD = 4
```
### Ejercicio 3: Fibonacci
Resolver el problema de encontrar el enésimo término de la sucesión de Fibonacci
```prolog
% Caso base: el primer término de Fibonacci es 0.
fibonacci(0, 0).
% Caso base: el segundo término de Fibonacci es 1.
fibonacci(1, 1).
% Caso recursivo: el enésimo término es la 
% suma de los dos anteriores.
fibonacci(N, F) :-
    N > 1,
    N1 is N - 1,    % Decrementamos N
    N2 is N - 2,    % Decrementamos N para el segundo término
    fibonacci(N1, F1),  % Llamada recursiva para N-1
    fibonacci(N2, F2),  % Llamada recursiva para N-2
    F is F1 + F2.  % Calculamos el término actual
```

| N | Resultado |
|----| ----|
| 0 | 0 |
| 1 | 1 |
| 2 | 1 |
| 3 | 2 |
| 4 | 3 |
| 5 | 5 |
| 6 | 8 |
| 7 | 13 |
| 8 | 21 |
| 9 | 34 |
| 10 | 55 |

```prolog
?- fibonacci(10, F).
F = 55
```
### Ejercicio 4: Ordenar una lista de dos elementos de menor a mayor
Predicado que relaciona una lista numérica de dos elementos con otra lista con esos dos elementos
ordenados de menor a mayor.
```prolog
 ?- acomodados( [5, 8], X).
 X = [5, 8]
 ?- acomodados( [8, 5], X).
 X = [5, 8]
```
##### Predicado
```prolog
acomodados([A,B], [A,B]) :- A =< B.
acomodados([A,B], [B,A]):- A > B.
```
##### Consulta
```prolog
acomodados( [812, 2122], X).
X = [812, 2122]
acomodados( [2122, 812], X).
X = [812, 2122]
```
### Ejercicio 5: Cantidad de elementos de una lista
Predicado que relaciona una lista con su cantidad de elementos ordenados de menor a mayor.
```prolog
?- longitud-de([a, b, c, d, e], X).
X = 5
```
##### Predicado
```prolog
longitud_de([], 0). % Caso base: la longitud de una lista vacía es 0.
longitud_de([_|Resto], N) :- 
    longitud_de(Resto, N1), % Se llama recursivamente con el resto de la lista.
    N is N1 + 1.           % Se incrementa el contador.
```

### Ejercicio 6: Cantidad de números reales de una lista
Predicado que vincula una lista de números enteros, con la cantidad de números naturales que contiene.
```prolog
?- naturales([6, -7, -4, 3, 2, 8], X).
X = 4
?- naturales([2,-1, 1, -32, 12], X).
X = 3
```
##### Predicado
```prolog
naturales([], 0).
naturales([A|B], X):- 
A >= 0, naturales(B, N1), X is N1 + 1, !;
A < 0, naturales(B, N1), X is N1.
```



### Ejercicio 7: Suma de elementos de una lista
Predicado que vincula una lista numérica, con la suma de sus elementos
```prolog
?- suma([6, 7, 4, 3, 2, 8], X).
X = 30
?- suma([6, 7, 4, 3, 2, 8, 23, 12, 3124, 1234, -1231], X).
X = 3192
```
##### Predicado
```prolog
suma([], 0).  % Caso base: La suma de una lista vacía es 0.
suma([Cabeza | Resto], Suma) :- 
    suma(Resto, SumaResto),  % Se llama recursivamente con la cola de la lista.
    Suma is Cabeza + SumaResto.  % La suma es la cabeza más la suma del resto.
```

### Ejercicio 8: Lista ordenada creciente
Predicado unario que es verdadero cuando su sujeto es una lista numérica ordenada en forma creciente.
```prolog
?- ordenada([3, 6, 8]).
YES
?- ordenada([6, 3, 8])
FAIL
```
##### Predicado
```prolog

```

### Ejercicio 9: Último elemento de una lista
Predicado que relaciona una lista cualquiera con el elemento que se encuentra en el último lugar.
```prolog
?- ultimo([a, b, c, r, f, h], X).
X = h
```

### Ejercicio 10: 
Predicado cuyos sujetos son dos listas, y que es verdadero cuando la primer lista es un subconjunto de la segunda.
```prolog
?- subconjunto([d, a, b], [m, b, f, r, d, a]).
YES
?- subconjunto([d, a, b], [m, k, f, r, d, a]).
FAIL
```

### Ejercicio 11: 
Predicado que relaciona dos listas con una tercera, formada con los elementos de ambas. (no usar el predicado append)
```prolog
?- concatenadas([d, a, b], [m, k, f, r, d, a], X).
X = [d, a, b, m, k, f, r, d, a]

CABEZA = C COLA = K
concatenadas([], X, X).
concatenadas([A|L1], Y, [A|Z]):-
concatenadas(L1, Y, Z).

concatenadas([], L, L).
concatenadas([X|A] ,Y, [X|Z]):- // Qué pasa acá?
	concatenadas(A,Y,Z).

concatenadas([], L, L).
concatenadas([C|K], L2, [C|X]):-
	concatenadas(K, L2,X).

concatenadas([d, a, b], [m, k, f, r, d, a], X).

```

### Ejercicio 12:
Predicado que relaciona una lista L1 con otra lista L2, con los mismos elementos que L1, pero rotados un lugar a la izquierda.
```prolog
?- rotada1([a, b, c, d], X).
X = [b, c, d, a]
```

### Ejercicio 13:
Predicado que relaciona una lista L1 con otra lista L2, con los mismos elementos que L1, pero rotados N lugares a la izquierda.
```prolog
?- rotadan(4, [a, b, c, d, e, f, g, h, i, j], X).
X = [e, f, g, h, i, j, a, b, c, d]
```