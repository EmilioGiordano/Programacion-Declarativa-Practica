# 📝 Programación Declarativa
## Paradigma de Programación Lógica
### Listas y recursión en Prolog
  
#### Índice
- [Crear lista a partir de base de hechos](#crear-lista-a-partir-de-base-de-hechos)
- [Suma de todos los elementos una listas](#suma-de-todos-los-elementos-una-listas)
- [Suma de todos los elementos de dos listas](#suma-de-todos-los-elementos-de-dos-listas)
- [Búsqueda recursiva](#búsqueda-recursiva)
- [Unión/concatenación de listas](#uniónconcatenación-de-listas)
- [Longitud de una lista](#longitud-de-una-lista)
- [Concatenar dos listas y devolver una tercera.](#concatenar-dos-listas-y-devolver-una-tercera)

### Crear lista a partir de base de hechos
Es importante conocer este concepto para poder aplicar todas las reglas posteriores de recursión y listas.
Teniendo una base de hechos como por ejemplo:
```prolog
% hecho(Nombre, Género, Año_de_estreno, Calificación).
movie('Inception', science_fiction, 2010, 8.8).
movie('The Godfather', drama, 1972, 9.2).
movie('Toy Story', animated, 1995, 8.3).
movie('The Dark Knight', action, 2008, 9.0).
movie('Pulp Fiction', drama, 1994, 8.9).
movie('Interstellar', science_fiction, 2014, 8.6).
movie('The Matrix', science_fiction, 1999, 8.7).
``` 
Si quisieramos operar sobre el atributo __Calificación__ de todos los hechos para, por ejemplo, calcular el promedio, debemos convertir los hechos en una lista. 
Utilizamos `findall`
```prolog
findall(Rating, movie(_, _, _, Rating), Ratings)
```
donde:
- `Rating`(singular) es el nombre que le damos al atributo/campo
- `movie` es el hecho.
- `_` son campos que no nos interesan incluir en la lista.
-  `Ratings`(plural) es el nombre de la __lista resultante__

##### Prueba
```prolog
findall(Rating, movie(_, _, _, Rating), Ratings)
Ratings = [8.8, 9.2, 8.3, 9.0, 8.9, 8.6, 8.7]
```
Obtenemos una lista con las calificaciones de las peliculas.
De esta manera, podremos aplicar reglas como Sumatoria y Longitud de una lista sobre la base de hechos definida, para luego calcular el promedio.

#### Reglas longitud y sumatoria de la lista. 
```prolog
longitud([], 0). 
longitud([_|B], X):- 
    longitud(B, N1), X is N1 + 1.
% ------------------------------- %
sumatoria([], 0).    
sumatoria([Cabeza | Resto], Suma) :-   
    sumatoria(Resto, SumaResto),  
Suma is Cabeza + SumaResto. 
```
#### Regla promedio
```prolog
promedioCalificaciones(Promedio):-
    findall(Rating, movie(_, _, _, Rating), Ratings),
    longitud(Ratings, Longitud),
    sumatoria(Ratings, Total),
    Promedio is (Total / Longitud).
```
#### Prueba
```prolog
promedioCalificaciones(Promedio)
Promedio = 8.785714285714286
```
### Suma de todos los elementos una listas
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
### Suma de todos los elementos de dos listas
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
Esta implementación permite sumar listas con diferente cantidad de elementos, incluso con una de ellas vacía.
```prolog
?- suma([1, 2, 3], [1], Resultado). % Resultado = 7
?- suma([1, 2, 3], [1, 2], Resultado). % Resultado = 9
?- suma([1, 2, 3], [1, 2, 3], Resultado). % Resultado = 12

?- suma([1], [1, 2, 3], Resultado). % Resultado = 7
?- suma([1, 2], [1, 2, 3], Resultado). % Resultado = 9
?- suma([1, 2, 3], [1, 2, 3], Resultado). % Resultado = 12

suma([1, 2, 3], [], Resultado). % Resultado = 6
suma([], [1, 2, 3], Resultado). % Resultado = 6


```
### Búsqueda recursiva
```prolog
member(X, [X|_]).
member(X, [_|Y]):- member(X, Y).
```
`member(X, [X|_])`: verifica si el elemento X es el primer elemento de la lista. Si esto es verdadero devuelve `true`.

`member(X, [_|Y]) :- member(X, Y).`: verifica si X está en el resto de la lista Y.

### Unión/concatenación de listas 

```prolog
concatenar([], L, L). % Caso base: concatenar una lista vacía con L da como resultado L.
concatenar([X|Resto], L, [X|Resultado]) :- 
    concatenar(Resto, L, Resultado). % Caso recursivo: agrega el primer elemento de la primera lista a Resultado y llama recursivamente.
```

```prolog
concatenar([1, a], [4, 5, 6], Resultado).
Resultado = [1, a, 4, 5, 6]
```

### Longitud de una lista

```prolog
longitud([], 0).
longitud([_|B], X):- longitud(B, N1), X is N1 + 1.
```
```prolog
longitud([1,2, [a]], A)
A = 3
```
### Concatenar dos listas y devolver una tercera.
```prolog
concatenar([], L, L). % Caso base: si la primera lista es vacía, el resultado es la segunda lista.
concatenar([X|Resto], L, [X|Resultado]) :-
    concatenar(Resto, L, Resultado). % Caso recursivo: agrega el primer elemento de la primera lista a Resultado y llama recursivamente.
```
```prolog
?- concatenar([a1, a2, a3], [b1, b2, b3], Resultado).
Resultado = [a1, a2, a3, b1, b2, b3]
```


---
✍️ **Autor:** Emilio Giordano  
🔗 Más resúmenes de Programación Declarativa en el [repositorio](https://github.com/EmilioGiordano/Programacion-Declarativa-Practica)  

---