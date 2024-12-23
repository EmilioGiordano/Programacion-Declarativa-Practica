# 📝 Programación Declarativa
## Paradigma de Programación Lógica
### Guia de ejercicios: Decisiones en Prolog


- [Ejercicio 1: Regla _progenitor_de_](#ejercicio-1-regla-progenitor_de)
- [Ejercicio 2: Mayor o igual](#ejercicio-2-mayor-o-igual)
- [Ejercicio 3: Paridad](#ejercicio-3-paridad)
- [Ejercicio 4: Regla _cuñado_de_](#ejercicio-4-regla-cuñado_de)
- [Ejercicio 5: Múltiplo](#ejercicio-5-múltiplo)
- [Ejercicio 6: Múltiplo](#ejercicio-6-múltiplo)
- [Ejercicio 7: Longitudes de un triángulo](#ejercicio-7-longitudes-de-un-triángulo)
- [Ejercicio 8: Comisión de venta](#ejercicio-8-comisión-de-ventas)
- [Ejercicio 9: Tiempo que tarda en llenar o vaciarse un tanque de agua](#ejercicio-9-tiempo-que-tarda-en-llenar-o-vaciarse-un-tanque-de-agua)
- [Ejercicio 10: Hora un segundo despues](#ejercicio-10-hora-un-segundo-después)
- [Ejercicio 11: Categorizar jugadores](#ejercicio-11-categorizar-jugadores)
- [Más resúmenes y material de Programación Declarativa](#mas-info)

#### Ejercicio 1: regla `progenitor_de`
Se tiene una base con los siguientes hechos:
##### Hechos
```prolog
madre_de(ana, luis).
padre_de(juan, luis).
```
__Construir una regla para definir el predicado "progenitor_de__
##### Regla
```prolog
progenitor_de(P,H) :-madre_de(P,H);padre_de(P,H).
```
```prolog
?- progenitor_de(X, luis).
X = ana
X = juan
?- progenitor_de(ana, luis).
true.
?- progenitor_de(X, pedro).
X = maria ;
X = carlos.
```

#### Ejercicio 2: mayor o igual
Definir un predicado ternario "mayor_o_igual" que relaciona dos números con el mayor de ambos, o con uno de ellos si son iguales.
##### Regla
```prolog
mayor_o_igual(X,Y,Z):- 
Z is X, (X>Y);
Z is Y,  (X<Y);
(X=Y), Z = 'Iguales'.
```
##### Consulta
```prolog
?- mayor_o_igual(6,11, Mayor)
Mayor = 11
```

#### Ejercicio 3: Paridad
Definir un predicado binario "paridad" que relaciona un número con la palabra "par" si el número es par, o con la palabra "impar" de otro modo
##### Predicado binario
```prolog
paridad(Num, Par):- 
    Z is Num mod 2, Z = 0, Par = 'par';	
    Par = 'impar'.
```
##### Consulta
```prolog
?- paridad(5, Par)
Par = impar
?- paridad(10, Par)
Par = par
```

#### Ejercicio 4: Regla `cuñado_de`
Escribir una regla para "cuñado_de" dada una base como:
```prolog
esposos(ana, luis).
hermanos(maria, juan)
```
##### Regla
```prolog
esposos(maria,luis).
hermanos(maria,juan).
cuniado_de(J,L):-
esposos(M,L),
hermanos(M,J).
```
##### Consulta
```prolog
?- cuniado_de(juan, luis).
true
```
#### Ejercicio 5: Múltiplo
Preparar un predicado binario que sea verdadero cuando sus dos sujetos sean números tales que el primero es múltiplo del segundo.
##### Predicado binario
```prolog
multiplo(X,Y):- 
(X mod Y =:= 0).
```
##### Consulta
```prolog
?- multiplo(4,2)
true
```
#### Ejercicio 6: Múltiplo
Completar el predicado anterior para que sea verdadero si cualquiera de los números es
múltiplo del otro.
##### Predicado
```prolog
multiplo(X,Y):-
(X mod Y =:= 0), !;
(Y mod X =:= 0).
```
##### Consulta (con !)
```prolog
?- multiplo(2,4)
true
```
##### Consulta (sin !)
```prolog
?- multiplo(2,4)
false
```
#### Ejercicio 7: Longitudes de un triángulo
Desarrollar un predicado ternario cuyos sujetos representan las longitudes de tres segmentos, y que sea verdadero si estos tres segmentos forman triángulo. Recordar que la suma de las longitudes de dos lados cualesquiera de un triángulo siempre debe ser mayor que
la longitud del restante.
##### Predicado ternario
```prolog
longitudes(X,Y, Z) :-
	(X>0), (Y>0), (Z>0),
	(X+Y > Z), (X+Z>Y),(Y+Z>X).
```
##### Consulta
```prolog
?- longitudes(15, 12, 15).
true
?- longitudes(1, 2, 3).
false
```

### Ejercicio 8: Comisión de ventas
Un vendedor cobra una comisión del 3% sobre sus ventas, pero si vendió más de USD 50000 recibe un 1% más, además de un premio fijo de U$D 1200. Preparar un predicado que relacione el total vendido con la comisión a cobrar.
##### Predicado
```prolog
comision(TotalVendido, Comision):-
(TotalVendido > 50000) -> 
(Comision is (TotalVendido * 1.04)+ 1200);
	Comision is TotalVendido * 1.03.
```
##### Consulta
```prolog
?- comision(49000, Comision)
Comision = 50470.0
?- comision(50000, Comision)
Comision = 51500.0
```
#### Ejercicio 9: Tiempo que tarda en llenar o vaciarse un tanque de agua
A un tanque llega agua a través de una canilla, mientras que simultáneamente desagua a través de un sumidero. La capacidad del tanque es de T litros, por la canilla llegan C litros por minuto, y por el sumidero desaguan S litros por minuto. Inicialmente el tanque tiene L litros.
Desarrollar un predicado que vincule los valores T, C, S y L, con los minutos que tarda en llenarse o vaciarse el tanque.
##### Predicado
```prolog
calc(CapacidadTanque, CaudalEntrada, CaudalSalida, AguaInicial, Tiempo) :-
    AguaInicial =< CapacidadTanque,  % El nivel inicial debe ser menor o igual a la capacidad del tanque
    CaudalNeto is CaudalEntrada - CaudalSalida,  % Caudal neto (entrada - salida)
    (
        CaudalNeto > 0 -> 
        Tiempo is (CapacidadTanque - AguaInicial) / CaudalNeto;  % Si el caudal neto es positivo, se calcula el tiempo para llenarse

        CaudalNeto < 0 -> 
        Tiempo is AguaInicial / (-CaudalNeto);  % Si el caudal neto es negativo, se calcula el tiempo para vaciarse

        CaudalNeto =:= 0 -> 
        Tiempo is 0  % Si el caudal neto es cero, el tanque no se llena ni se vacía
  ).
```
##### Consulta
```prolog
?- calc(100, 3, 2, 20, Tiempo).
Tiempo = 80
```



#### Ejercicio 10: Hora un segundo después
Escribir un predicado que relacione una hora dada en horas, minutos y segundos con la hora será un segundo después.

##### Predicado
```prolog
hora_despues(Hora, Minuto, Segundo, NuevaHora, NuevoMinuto, NuevoSegundo) :-
    Segundo == 59, Minuto == 59, Hora == 23, !,  % Caso límite: 23:59:59 -> 00:00:00
    NuevaHora is 0, 
    NuevoMinuto is 0, 
    NuevoSegundo is 0.

hora_despues(Hora, Minuto, Segundo, NuevaHora, NuevoMinuto, NuevoSegundo) :-
    Segundo == 59, Minuto == 59, !,              % Caso: 12:59:59 -> 13:00:00
    NuevaHora is Hora + 1, 
    NuevoMinuto is 0, 
    NuevoSegundo is 0.

hora_despues(Hora, Minuto, Segundo, NuevaHora, NuevoMinuto, NuevoSegundo) :-
    Segundo == 59, !,                            % Caso: 12:34:59 -> 12:35:00
    NuevaHora is Hora, 
    NuevoMinuto is Minuto + 1, 
    NuevoSegundo is 0.

hora_despues(Hora, Minuto, Segundo, NuevaHora, NuevoMinuto, NuevoSegundo) :- 
    NuevoSegundo is Segundo + 1,                 % Caso general: sumar un segundo
    NuevaHora is Hora, 
    NuevoMinuto is Minuto.
```
##### Consulta
```prolog
?- hora_despues(23, 59, 59, H, M, S).
H = M, M = S, S = 0
?- hora_despues(12, 59, 59, H, M, S).
H = 13, M = S, S = 0
?- hora_despues(12, 34, 59, H, M, S).
H = 12, M = 35, S = 0
?- hora_despues(12, 34, 30, H, M, S).
H = 12, M = 34, S = 31
```

#### Ejercicio 11: Categorizar jugadores
Dados los siguientes datos sobre jugadores de basket:
```prolog
cantidad_de_dobles(juan, 15).
cantidad_de_dobles(jose, 8).
cantidad_de_dobles(pedro, 30).

cantidad_de_triples(juan, 12).
cantidad_de_triples(jose, 0).
cantidad_de_triples(pedro, 12).

cantidad_de_infracciones(juan, 4).
cantidad_de_infracciones(jose, 14).
cantidad_de_infracciones(pedro, 4).
```
que representan la cantidad de dobles, triples e infracciones de los jugadores a lo largo del campeonato, se requiere un predicado que relacione el nombre de un jugador con alguna de las siguientes categorías:
Posible NBA, cuando el jugador hizo al menos 10 triples, 30 dobles y cometió menos de 5 infracciones.
Bueno, cuando el jugador hizo al menos 20 dobles y cometió menos de 8 infracciones.
Regular, cuando el jugador hizo al menos 10 dobles y cometió menos de 12 infracciones.
Desastroso, cuando el jugador hizo menos de 10 dobles y cometió 12 o más infracciones.

##### Predicado
```prolog
estadisticas(Jugador, Categoria) :- 
    ( cantidad_de_triples(Jugador, Triples), Triples >= 10,
      cantidad_de_dobles(Jugador, Dobles), Dobles >= 30,
      cantidad_de_infracciones(Jugador, Infracciones), Infracciones < 5 ->
      Categoria = 'Posible NBA';

      cantidad_de_dobles(Jugador, Dobles), Dobles >= 20,
      cantidad_de_infracciones(Jugador, Infracciones), Infracciones < 8 ->
      Categoria = 'Bueno';

      cantidad_de_dobles(Jugador, Dobles), Dobles >= 10,
      cantidad_de_infracciones(Jugador, Infracciones), Infracciones < 12 ->
      Categoria = 'Regular';

      cantidad_de_dobles(Jugador, Dobles), Dobles < 10,
      cantidad_de_infracciones(Jugador, Infracciones), Infracciones >= 12 ->
      Categoria = 'Desastroso'
    ).
```
##### Consulta
```prolog
?- estadisticas(juan, Categoria).
Categoria = 'Regular'
?- estadisticas(pedro, Categoria).
Categoria = 'Posible NBA'
```

#### <a id="mas-info"></a>
<span style="display:none;">Firma</span>

---
✍️ **Autor:** Emilio Giordano  
🔗 Más resúmenes de Programación Declarativa en el [repositorio](https://github.com/EmilioGiordano/Programacion-Declarativa-Practica)  

---