## Listas


##### Búsqueda recursiva:
```prolog
member(X, [X|_]).
member(X, [_|Y]):- member(X, Y).
```
`member(X, [X|_])`: verifica si el elemento X es el primer elemento de la lista. Si esto es verdadero devuelve `true`.

`member(X, [_|Y]) :- member(X, Y).`: verifica si X está en el resto de la lista Y.

##### Unión de listas / concatenación

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
