## Índice
0. [Base de hechos](#base-de-hechos)
1. [Regla de sedentarismo](#regla-de-sedentarismo)
2. [Regla de peso ideal](#regla-de-peso-ideal)
3. [Regla de IMC](#regla-de-imc)
4. [Regla de personas deportistas con y sin listas](#regla-de-personas-deportistas-con-y-sin-listas)
5. [Regla de personas ultra deportistas (más de dos deportes)](#regla-de-personas-ultra-deportistasmás-de-dos-deportes)



## Ejercicio 3: Firma nutricional
Una firma nutricional muy importante, nos pide el desarrollo de un programa que permita analizar la salud en las personas.
##### Base de hechos
```prolog
persona(mariano, 20, m, caracteristica(68, 169, mediana)).
persona(leandro, 12, m, caracteristica(38, 123, mediana)).
persona(gisella, 30, f, caracteristica(59, 162, pequenia)).
persona(mara, 42, f, caracteristica(88, 195, grande)).
persona(osvaldo, 25, m, caracteristica(98, 165, grande)).
persona(tito, 20, m, caracteristicas(57, 170, pequenia)).

actividad(mariano, deportes([basket])).
actividad(mariano, ocupaciones([estudiante])).
actividad(leandro, deportes([futbol, skate, taekwondo])).
actividad(leandro, ocupaciones([estudiante])).
actividad(gisella, deportes([pilates])).
actividad(gisella, ocupaciones([amaDeCasa, maestra])).
actividad(mara, ocupaciones([abogada, profesora])).
actividad(osvaldo, ocupaciones([empleado])).
actividad(tito, deportes([gimnasio])).
actividad(tito, ocupaciones([eventos, gasista])).

enfermedad(leandro,alergias).
enfermedad(mara,diabetes).
enfermedad(leandro,alergias).
```
#### Regla de sedentarismo
1-  Indicar si la persona es sedentaria. Una persona es sedentaria cuando no practica deportes y tiene menos de dos ocupaciones.
2- Desarrollar un predicado que indique si una persona es activa. Una persona es activa cuando practica al menos un deporte o tiene mas de dos ocupaciones.

```prolog
multiplesOcupaciones(Persona) :-
    actividad(Persona, ocupaciones(Ocupaciones)),
    length(Ocupaciones, N),
    N >= 2.

haceDeporte(Persona) :-
    actividad(Persona, deportes(_)).

% Activa si hace deportes y tiene al menos dos ocupaciones
activa(Persona) :-
	haceDeporte(Persona),
	multiplesOcupaciones(Persona).
   
% Sedentaria si NO es activa
sedentaria(Persona) :-
    \+ activa(Persona).
```

##### Consulta
```prolog
?- sedentaria(gisella)
false
?- sedentaria(osvaldo)
true
```
#### Regla de peso ideal
3- Calcular el peso ideal de una persona de acuerdo a la siguiente formula:
Peso Ideal = 0.75 * (altura en cm - 150) + 50 

```prolog
altura(Persona, Altura) :-
    persona(Persona, _, _, caracteristica(_, Altura,_)).
   
pesoIdeal(Persona, P) :-
    altura(Persona, Altura),
    P is (0.75 * (Altura - 150) + 50).
```
##### Consulta
```prolog
?- pesoIdeal(osvaldo, P)
P: 61.25
```

#### Regla de IMC
4- Calcular el IMC (Indice de Masa Corporal) de una persona. El IMC se obtiene dividiendo el peso por la estatura(en metros) al cuadrado. 

```prolog
alturaEnMetros(Persona, AlturaMetros) :-
	persona(Persona, _, _, caracteristica(_, AlturaCm,_)),
    AlturaMetros is (AlturaCm / 100).

imc(Persona, IMC):-
    peso(Persona,Peso),
    alturaEnMetros(Persona,Altura),
    IMC is (Peso / (Altura * Altura)).
```
##### Consulta
```prolog
?- imc(tito, IMC)
IMC: 23.030045351473927
?- imc(osvaldo, IMC)
IMC: 35.99632690541782
```
#### Regla de personas deportistas con y sin listas
5- Averiguar quienes son las personas deportistas, o sea todas las personas que practican al menos un deporte. Diseñar dos soluciones, con y sin listas.

#### Sin listas.
```prolog
deportistasSinListas(Persona):-
    actividad(Persona, deportes(_)).
```
##### Consulta
```prolog
?- deportistasSinListas(X)
X = mariano
X = leandro
X = gisella
X = tito
```
#### Con listas.
```prolog
deportistasConListas(Persona):-
    actividad(Persona, deportes(Deportes)),
    Deportes \= [].  % Verifica que la lista de deportes no esté vacía
```
##### Consulta
deportistasConListas(X)
X = mariano
X = leandro
X = gisella
X = tito

#### Regla de personas ultra deportistas(más de dos deportes)
```prolog
ultraDeportistas(Persona):-
    actividad(Persona, deportes(Deportes)),
    length(Deportes, N),
    N > 2.
```
```prolog
?- ultraDeportistas(X)
X = leandro
```
