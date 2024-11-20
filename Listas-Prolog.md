## Listas
#### Índice
- [Suma de todos los elementos una listas](#suma-de-todos-los-elementos-una-listas)
- [Suma de todos los elementos de dos listas](#suma-de-todos-los-elementos-de-dos-listas)
- [Búsqueda recursiva](#búsqueda-recursiva)
- [Unión/concatenación de listas](#uniónconcatenación-de-listas)
- [Longitud de una lista](#longitud-de-una-lista)
- [Concatenar dos listas y devolver una tercera.](#concatenar-dos-listas-y-devolver-una-tercera)
##### Suma de todos los elementos una listas
```prolog
sumatoria([], 0).   
sumatoria([Cabeza | Resto], Suma) :-  
    sumatoria(Resto, SumaResto), 
    Suma is Cabeza + SumaResto.
```
Consulta
```prolog
?-sumatoria([1, 2, 3], Resultado).
Resultado = 6
```
##### Suma de todos los elementos de dos listas
```prolog
% Caso base
suma([], [], 0).   
% Caso con segunda lista vacía
suma([Cabeza1 | Resto1], [], Suma) :-  
    suma(Resto1, [], SumaResto), 
    Suma is Cabeza1 + SumaResto.

% Caso con primera lista vacía
suma([], [Cabeza2 | Resto2], Suma) :-  
    suma([], Resto2, SumaResto), 
    Suma is Cabeza2 + SumaResto.

% Caso con ambas listas con elementos
suma([Cabeza1 | Resto1], [Cabeza2 | Resto2], Suma) :-  
    suma(Resto1, Resto2, SumaResto), 
    Suma is Cabeza1 + Cabeza2 + SumaResto.
```
Consulta
```prolog
?- suma([1, 2, 3], [1, 2, 3], Resultado).
Resultado = 12
```
##### Búsqueda recursiva
```prolog
member(X, [X|_]).
member(X, [_|Y]):- member(X, Y).
```
`member(X, [X|_])`: verifica si el elemento X es el primer elemento de la lista. Si esto es verdadero devuelve `true`.

`member(X, [_|Y]) :- member(X, Y).`: verifica si X está en el resto de la lista Y.

##### Unión/concatenación de listas 

```prolog
concatenar([], L, L). % Caso base: concatenar una lista vacía con L da como resultado L.
concatenar([X|Resto], L, [X|Resultado]) :- 
    concatenar(Resto, L, Resultado). % Caso recursivo: agrega el primer elemento de la primera lista a Resultado y llama recursivamente.
```

```prolog
concatenar([1, a], [4, 5, 6], Resultado).
Resultado = [1, a, 4, 5, 6]
```

##### Longitud de una lista

```prolog
longitud([], 0).
longitud([_|B], X):- longitud(B, N1), X is N1 + 1.
```
```prolog
longitud([1,2, [a]], A)
A = 3
```
##### Concatenar dos listas y devolver una tercera.
```prolog
concatenar([], L, L). % Caso base: si la primera lista es vacía, el resultado es la segunda lista.
concatenar([X|Resto], L, [X|Resultado]) :-
    concatenar(Resto, L, Resultado). % Caso recursivo: agrega el primer elemento de la primera lista a Resultado y llama recursivamente.
```
```prolog
?- concatenar([a1, a2, a3], [b1, b2, b3], Resultado).
Resultado = [a1, a2, a3, b1, b2, b3]
```