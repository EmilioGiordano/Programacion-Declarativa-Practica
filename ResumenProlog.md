# Programación lógica: Sintaxis de Prolog.

- [Hechos](#hechos)
   - [Hechos anidados o estructuras compuestas](#hechos-anidados-o-estructuras-compuestas)
- [Operadores Lógicos](#operadores-lógicos)
   - [Conjunción (AND)](#conjunción-and)
   - [Disyunción](#disyunción-or)
   - [Negación](#negación)
- [Preguntas](#preguntas)
   - [Preguntas sin variable](#preguntas-sin-variable)
   - [Preguntas con variable](#preguntas-con-variable)
- [Reglas](#reglas)
- [Expresiones](#expresiones)

## Hechos
Los hechos son afirmaciones sobre el mundo. Se utilizan para representar datos y relaciones que siempre se consideran verdaderas.
Una colección de hechos se conoce como __base de hechos__
![alt text](./img/hecho.png)
__Ejemplos de hechos:__
```prolog
hombre(carlos).
le_pertenece(maria, moneda).
padre(homero, bart).
```
#### Hechos anidados o estructuras compuestas
```prolog
actividad(juan, deportes([futbol, skate, taekwondo])).
actividad(juan, ocupaciones([estudiante])).
```
##### Consulta
```prolog
?- actividad(juan, X)
X = deportes([futbol, skate, taekwondo])
X = ocupaciones([estudiante])
```

## Operadores Lógicos
#### Conjunción (AND)
Representada por `,` (coma). Indica que ambas condiciones deben ser verdaderas.
```prolog
feliz(X) :- tieneTrabajo(X), buenaSalud(X).
```
`X es feliz` __si__ `X tieneTrabajo` __y__ `buenaSalud`

#### Disyunción (OR)
Representada por `;`. Se usa cuando alguna de las condiciones debe ser verdadera.
```prolog
contento(X) :- juega(X, futbol) ; juega(X, baloncesto).
```
`X está contento` __si__ `X juega al futbol` __o__ `X juega al baloncesto`

#### Negación
Representada por `\+`, que significa "no es cierto que".
```prolog
no_tieneHijos(X) :- \+ padre(X, _).
```
`X no tiene hijos` __si__ `no es cierto que X es padre de alguien`

## Preguntas
#### Preguntas sin variable
Su respuesta siempre es `true/false`.
Ejemplo, consderando la siguiente base de hechos:
```prolog
le_gusta(juan, pescado).
le_gusta(juan, maria).
le_gusta(maria, libro).
le_gusta(juan, libro).
le_gusta(juan, Italia).
```
Preguntas/consultas:
```prolog
?-le_gusta(juan, dinero). 
false

?-le_gusta(juan, maria). 
true
```
#### Preguntas con variable
Su respuesta es `el objeto que cumple el objetivo o false`
Preguntas/consultas:
```prolog
% Consulta: ¿Qué le gusta a juan?
?- le_gusta(juan, X)
% Respuesta: 
X = pescado
X = maria
X = libro
X = italia

% Consulta: ¿A qué le gusta maria?
?-le_gusta(X, maria).
% Respuesta: 
X = juan

% Consulta: ¿Qué le gusta a Maria & a Juan?
?-le_gusta(maria, X), le_gusta(juan, X).
% Respuesta:
X = libro.
```


## Reglas
Las reglas definen relaciones o condiciones entre hechos. Se leen como "es verdadero si...".
En Prolog, el operador `:-` se usa para expresar "si".
```prolog
hijo(X, Y) :- padre(Y, X).
abuelo(X, Z) :- padre(X, Y), padre(Y, Z).
```
`hijo(X, Y)` es verdadero si Y es padre de X.
`abuelo(X, Z)` es verdadero si X es padre de Y y Y es padre de Z.

## Expresiones
Prolog cuenta con operadores para la unificación y comparación, sea con evaluación o sea simbólica, como los siguientes:
- `X is Y %unificación con evaluación.`
- `X = Y %unificación simbólica`
- `X=:=Y %comparación con evaluación`
- `X == Y %comparación simbólica.`

```prolog
?- X is 3+5.
   X = 8

?- X = 3+5.
   X = 3+5

?- 3+5 =:= 2+6.
   yes

?- 3+5 == 2+6.
   no

?- 3+5 == 3+5.
   yes
```