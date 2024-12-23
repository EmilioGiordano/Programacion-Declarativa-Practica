# 📝 Programación Declarativa
## Paradigma de Programación Lógica
### Guia de ejercicios: Recursión y Listas en Prolog

- [Ejemplo: Factorial](#ejemplo-factorial)
- [Ejercicio 1: Cadena de progenitores](#ejercicio-1-cadena-de-progenitores)
- [Ejercicio 2: MCD](#ejercicio-2-mcd)
- [Ejercicio 3: Fibonacci](#ejercicio-3-fibonacci)
- [Ejercicio 4: Ordenar una lista de dos elementos de menor a mayor](#ejercicio-4-ordenar-una-lista-de-dos-elementos-de-menor-a-mayor)
- [Ejercicio 5: Cantidad de elementos de una lista](#ejercicio-5-cantidad-de-elementos-de-una-lista)
- [Ejercicio 6: Cantidad de números reales de una lista](#ejercicio-6-cantidad-de-números-reales-de-una-lista)
- [Ejercicio 7: Suma de elementos de una lista](#ejercicio-7-suma-de-elementos-de-una-lista)
- [Ejercicio 8: Lista ordenada creciente](#ejercicio-8-lista-ordenada-creciente)
- [Ejercicio 9: Último elemento de una lista](#ejercicio-9-último-elemento-de-una-lista)
- [Ejercicio 10: Lista subconjunto de otra lista](#ejercicio-10-lista-subconjunto-de-otra-lista)
- [Ejercicio 11: Concatenación de listas(sin usar predicado append)](#ejercicio-11-concatenación-de-listassin-usar-predicado-append)
- [Ejercicio 12: Lista rotada a la izquierda](#ejercicio-12-lista-rotada-a-la-izquierda)
- [Ejercicio 13: Lista rotada a la izquierda N veces](#ejercicio-13-lista-rotada-a-la-izquierda-n-veces)
- [Más resúmenes y material de Programación Declarativa](#mas-info)

#### Ejemplo: Factorial 
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
#### Ejercicio 1: Cadena de progenitores
Dada una base de datos en la cual se describe una cadena de progenitores con hechos como:

##### Hechos
```prolog
progenitor_de(juan, luis).
progenitor_de(luis, maria).
progenitor_de(maria, ana).
progenitor_de(jose, hector).
```
__Escribir un predicado que relacione a una persona con un antepasado de la misma__

##### Predicado
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
#### Ejercicio 2: MCD
Resolver el problema de encontrar el MCD entre dos números, sabiendo que, si los números son iguales, el MCD es el mismo número, en otro caso el MCD es igual MCD entre el menor de ellos y la diferencia entre ambos
##### Predicado
```prolog
% MCD: Maximo Comun Divisor
% Caso base: si los numeros son iguales el MCD es 
% el mismo número.
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
?- mcd(4, 12, MCD)
MCD = 4
```
#### Ejercicio 3: Fibonacci
Resolver el problema de encontrar el enésimo término de la sucesión de Fibonacci
##### Predicado
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
##### Consulta
```prolog
?- fibonacci(10, F).
F = 55
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


#### Ejercicio 4: Ordenar una lista de dos elementos de menor a mayor
Predicado que relaciona una lista numérica de dos elementos con otra lista con esos dos elementos
ordenados de menor a mayor.

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
#### Ejercicio 5: Cantidad de elementos de una lista
Predicado que relaciona una lista con su cantidad de elementos ordenados de menor a mayor.

##### Predicado
```prolog
longitud_de([], 0). % Caso base: la longitud de una lista vacía es 0.
longitud_de([_|Resto], N) :- 
    longitud_de(Resto, N1), % Se llama recursivamente con el resto de la lista.
    N is N1 + 1.           % Se incrementa el contador.
```
##### Consulta
```prolog
?- longitud_de([a, b, c, d, e], X).
X = 5
```

#### Ejercicio 6: Cantidad de números reales de una lista
Predicado que vincula una lista de números enteros, con la cantidad de números naturales que contiene.

##### Predicado
```prolog
naturales([], 0).
naturales([A|B], X):- 
A >= 0, naturales(B, N1), X is N1 + 1, !;
A < 0, naturales(B, N1), X is N1.
```
##### Consulta
```prolog
?- naturales([6, -7, -4, 3, 2, 8], X).
X = 4
?- naturales([2,-1, 1, -32, 12], X).
X = 3
```

#### Ejercicio 7: Suma de elementos de una lista
Predicado que vincula una lista numérica, con la suma de sus elementos

##### Predicado
```prolog
suma([], 0).  % Caso base: La suma de una lista vacía es 0.
suma([Cabeza | Resto], Suma) :- 
    suma(Resto, SumaResto),  % Se llama recursivamente con la cola de la lista.
    Suma is Cabeza + SumaResto.  % La suma es la cabeza más la suma del resto.
```
##### Consulta
```prolog
?- suma([6, 7, 4, 3, 2, 8], X).
X = 30
?- suma([6, 7, 4, 3, 2, 8, 23, 12, 3124, 1234, -1231], X).
X = 3192
```
#### Ejercicio 8: Lista ordenada creciente
Predicado unario que es verdadero cuando su sujeto es una lista numérica ordenada en forma creciente.

```prolog
ordenada([]) :- 
    write('Lista vacía').
ordenada([_]) :- 
    write('YES').
% Regla recursiva: verifica que el primer elemento sea menor o igual que el segundo,
% luego llama recursivamente a la función con el resto de la lista.
ordenada([X, Y | Resto]) :-
    X =< Y,  % Compara el primer elemento con el segundo
    ordenada([Y | Resto]).  % Llama recursivamente con el segundo elemento y el resto de la lista
```
##### Consulta
```prolog
?- ordenada([3, 6, 8]).
YES
?- ordenada([6, 3, 8])
FAIL
```

#### Ejercicio 9: Último elemento de una lista
Predicado que relaciona una lista cualquiera con el elemento que se encuentra en el último lugar.
```prolog
?- ultimo([a, b, c, r, f, h], X).
X = h
```

### Ejercicio 10: Lista subconjunto de otra lista
Predicado cuyos sujetos son dos listas, y que es verdadero cuando la primer lista es un subconjunto de la segunda.
###### Predicado
```prolog
subconjunto([], _). % Caso base: una lista vacía siempre es subconjunto de cualquier lista.
subconjunto([X|Resto], L2) :- 
    member(X, L2), % Verifica si el primer elemento X de la primera lista está en la segunda lista.
    subconjunto(Resto, L2). % Llama recursivamente con el resto de la primera lista.
```
##### Consulta
```prolog
?- subconjunto([d, a, b], [m, b, f, r, d, a]).
YES
?- subconjunto([d, a, b], [m, k, f, r, d, a]).
FAIL
```
#### Ejercicio 11: Concatenación de listas(sin usar predicado append)
Predicado que relaciona dos listas con una tercera, formada con los elementos de ambas. (no usar el predicado append)
```prolog
concatenar([], L, L). % Caso base: si la primera lista es vacía, el resultado es la segunda lista.
concatenar([X|Resto], L, [X|Resultado]) :-
    concatenar(Resto, L, Resultado). % Caso recursivo: agrega el primer elemento de la primera lista a Resultado y llama recursivamente.
```
```prolog
?- concatenar([a1, a2, a3], [b1, b2, b3], Resultado).
Resultado = [a1, a2, a3, b1, b2, b3]
```

#### Ejercicio 12: Lista rotada a la izquierda
Predicado que relaciona una lista L1 con otra lista L2, con los mismos elementos que L1, pero rotados un lugar a la izquierda.
##### Predicado
```prolog
rotada1([X|Resto], L2) :-
    agregar_al_final(Resto, X, L2).

% Predicado auxiliar para agregar un elemento al final de una lista
agregar_al_final([], X, [X]).
agregar_al_final([Y|Resto], X, [Y|L]) :-
    agregar_al_final(Resto, X, L).
```

##### Consulta
```prolog
?- rotada1([a, b, c, d], X).
X = [b, c, d, a]
```

#### Ejercicio 13: Lista rotada a la izquierda N veces
Predicado que relaciona una lista L1 con otra lista L2, con los mismos elementos que L1, pero rotados N lugares a la izquierda.

##### Predicado
```prolog
% Caso base: rotar 0 posiciones deja la lista igual.
rotadan(0, L, L).

% Caso recursivo: si N es mayor que 0, toma el primer elemento y colócalo al final.
rotadan(N, [X|Resto], L2) :-
    N > 0,
    N1 is N - 1,
    mover_al_final(Resto, X, Ltemp), % Mueve X al final de Resto.
    rotadan(N1, Ltemp, L2).         % Llama recursivamente con N decrementado.

% Predicado auxiliar para mover un elemento al final de una lista.
mover_al_final([], X, [X]).          % Caso base: si la lista está vacía, crea una lista con el elemento X.
mover_al_final([Y|Resto], X, [Y|L]) :- % Caso recursivo: mantiene el primer elemento y sigue con el resto.
    mover_al_final(Resto, X, L).
```
##### Consulta
```prolog
?- rotadan(4, [a, b, c, d, e, f, g, h, i, j], X).
X = [e, f, g, h, i, j, a, b, c, d]
```

#### <a id="mas-info"></a>
<span style="display:none;">Firma</span>

---
✍️ **Autor:** Emilio Giordano  
🔗 Más resúmenes de Programación Declarativa en el [repositorio](https://github.com/EmilioGiordano/Programacion-Declarativa-Practica)  

---