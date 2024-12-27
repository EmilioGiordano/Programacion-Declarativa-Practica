# 📝 Programación Declarativa
## Paradigma de Programación Lógica
### Guia de ejercicios: Secuencias en Prolog



- [Ejercicio 1: hechos](#ejercicio-1-hechos)
- [Ejercicio 2: Árbol genealógico](#ejercicio-2-árbol-genealógico)
- [Ejercicio 3: escribir consultas simples y compuestas](#ejercicio-3-escribir-consultas-simples-y-compuestas)
- [Ejercicio 4: escribir consultas](#ejercicio-4-escribir-consultas)
- [Ejercicio 5: Grados celsius a fahrenheit](#ejercicio-5-grados-celsius-a-fahrenheit)
- [Ejercicio 6: Convertir centímetros a yardas, pies y pulgadas](#ejercicio-6-convertir-centímetros-a-yardas-pies-y-pulgadas)
- [Ejercicio 7: : salario con comisiones](#ejercicio-7-salario-con-comisiones)
- [Ejercicio 8: promedio de notas](#ejercicio-8-promedio-de-notas)
- [Ejercicio 9: gasto total en sueldos](#ejercicio-9-gasto-total-en-sueldos)
- [Ejercicio 10: Calcular herencia para cada hijo](#ejercicio-10-calcular-herencia-para-cada-hijo)
- [Ejercicio 11: oferta de artículos](#ejercicio-11-oferta-de-artículos)
- [Ejercicio 12: reglas `hermano_de` y `tio_de`](#ejercicio-12-reglas-hermano_de-y-tio_de)
- [Ejercicio 13: ciudades conectadas por rutas](#ejercicio-13-ciudades-conectadas-por-rutas)
- [Más resúmenes y material de Programación Declarativa](#mas-info)

#### Ejercicio 1: hechos
Escribir las siguientes oraciones en Prolog:
- El oro es valioso.
- Isabel es mujer.
- Juan es Rey.
- Zeus es el progenitor de Hercules.
- José le presta dinero a Pedro.
##### Hechos
```prolog
es_valioso(oro). 
es_mujer(isabel).
es_rey(juan).
es_progenitor_de(zeus, hercules).
le_presta_dinero(jose, pedro).
```

#### Ejercicio 2: Árbol genealógico
Escribir en Prolog los datos relevantes, (a los efectos genealógicos), del siguiente párrafo: "La familia de Luis no es muy numerosa, sus padres, Carlos y Susana, tuvieron tres hijos: Roberto, Amalia, y Luis, de los cuales Luis es el menor. Carlos, a su vez, tiene una hermana mayor llamada Isabel, siendo ambos hijos de Ana y Guillermo. Los padres de Susana, Mercedes y Ernesto, tuvieron otra hija bastante menor que ella, a quien bautizaron con el nombre de Angélica, la que es tan bella como su nombre. Los dos hijos de Luis y su esposa Laura, llamados Federico y Carla, están estudiando letras".
__Utilizar solamente los predicados "es_progenitor_de", "es_varon" y "es_mujer".__
##### Regla
```prolog

% Definición del predicado padre
padre(X, Y) :- es_progenitor_de(X, Y), es_varon(X).
% familia carlos y susana
es_progenitor_de(carlos,roberto).
es_progenitor_de(carlos,amalia).
es_progenitor_de(carlos,luis).
es_progenitor_de(susana,roberto).
es_progenitor_de(susana,amalia).
es_progenitor_de(susana,luis).
% familia luis y laura
es_progenitor_de(luis, federico).
es_progenitor_de(luis, carla).
es_progenitor_de(laura, federico).
es_progenitor_de(laura, carla).
% familia ana y guillermo
es_progenitor_de(guillermo, carlos).
es_progenitor_de(guillermo, isabel).
es_progenitor_de(ana, carlos).
es_progenitor_de(ana, isabel).
% familia ernesto y mercedes
es_progenitor_de(ernesto, angelica).
es_progenitor_de(ernesto, susana).
es_progenitor_de(mercedes, angelica).
es_progenitor_de(mercedes, susana).
%genero
es_varon(carlos).
es_varon(roberto).
es_varon(luis).
es_varon(federico).
es_varon(guillermo).
es_varon(ernesto).
es_mujer(amalia).
es_mujer(susana).
es_mujer(laura).
es_mujer(carla).
es_mujer(mercedes).
es_mujer(angelica).
```

#### Ejercicio 3: escribir consultas simples y compuestas
Usando la base de datos generada en el problema de la familia de Luis, y con lo que se conoce hasta ahora, escribir consultas para obtener la siguiente información:
__Preguntas simples__:
##### A. ¿Es Carlos progenitor de Guillermo?

```prolog
?- es_progenitor_de(carlos, guillermo).
```
##### B. ¿Es Jorge progenitor de Gonzalo?

```prolog
?- es_progenitor_de(jorge, gonzalo).
```
##### C. ¿Es Carlos progenitor de Amalia?

```prolog
?- es_progenitor_de(carlos, amalia).
```

##### D. Usando el predicado "padre" preguntar: ¿Es Carlos padre de Roberto?

```prolog
% Definición del predicado padre
padre(X, Y) :- es_progenitor_de(X, Y), es_varon(X).
% Consulta
?- padre(carlos, roberto).
```

##### E. ¿Gonzalo es mujer?

```prolog
?- es_mujer(gonzalo)
```
##### F. ¿Alberto es varón?

```prolog
?- es_hombre(alberto)
```

__Preguntas compuestas (conjunciones):__
##### G. ¿Es cierto que Luis es progenitor de Carla, y que Carla es mujer?.

```prolog
?- es_progenitor_de(luis,carla), es_mujer(carla)
```
##### H. ¿Es cierto que Ernesto es progenitor de Carlos, y que éste es progenitor
de Luis, y a su vez Luis es progenitor de Carla?

```prolog
?- es_progenitor_de(ernesto,carlos), es_progenitor_de(carlos,luis), 
es_progenitor_de(luis,carla)
```

#### Ejercicio 4: escribir consultas
Usando la base de datos generada en el problema de la familia de Luis, y con
lo que se conoce hasta ahora, escribir consultas para obtener la siguiente
información:
##### A. ¿Federico es progenitor de alguien?

```prolog
?- es_progenitor_de(federico, Hijo).
```

#####  B. ¿Quiénes son los progenitores de Roberto?
```prolog
?- es_progenitor_de(Progenitor, roberto).
Progenitor = carlos
Progenitor = susana
```
##### C. ¿Guillermo tuvo alguna hija?
```prolog
?- es_progenitor_de(guillermo, X), es_mujer(X)
false
```
##### Caso con hijos varones y mujeres: 
```prolog
es_progenitor_de(carlos, X), es_mujer(X)
X = amalia
false
```

D. ¿Ernesto tuvo algún hijo varón?

```prolog
?- es_progenitor_de(guillermo, X), es_mujer(X)
false
```

E. ¿Roberto y Amalia tienen el mismo padre?

```prolog
?- es_progenitor_de(Padre, roberto), es_progenitor_de(Padre, amalia)
Padre = carlos
```

F. ¿Ernesto tuvo alguna hija que a su vez tenga una hija?

```prolog
es_progenitor_de(ernesto, Hija), es_progenitor_de(Hija, Nieta), es_mujer(Nieta).
Hija = susana,
Nieta = amalia
```
La hija es Susana, la hija mujer de Susana es Amalia

#### Ejercicio 5: Grados celsius a fahrenheit
Definir un predicado que relacione una temperatura expresada en grados Celsius con la misma temperatura expresada en grados Farenheit. Recordamos que F = (9/5) * C + 32

##### Regla
```prolog
% Definición del predicado celsius_a_fahrenheit
celsius_a_fahrenheit(C, F) :-
    F is (9/5) * C + 32.
```
##### Consulta
```prolog
?- celsius_a_fahrenheit(1, F).
F = 33.8
```

#### Ejercicio 6: Convertir centímetros a yardas, pies y pulgadas
Definir un predicado que relacione una longitud expresada en centímetros,
con la misma longitud expresada en pulgadas, pies y yardas. Recordamos que:
1 yarda = 3 pies
1 pie = 12 pulgadas
1 pulgada = 2.54 centímetros

##### Regla
```prolog
longitud(Cm, Pulgadas, Pies, Yardas) :-
    Pulgadas is (Cm/2.54),
    Pies is (Pulgadas/12),
    Yardas is (Pies/3).
```
##### Consulta
```prolog
?- longitud(100, Pulgadas, Pies, Yardas)
Pies = 21.166666666666668,
Pulgadas = 254.0,
Yardas = 7.055555555555556
```

#### Ejercicio 7: salario con comisiones
Una empresa de ventas paga a sus empleados un salario fijo de 800 pesos, mas una comisión de $50 por cada venta realizada, más el 8% sobre el monto total de ventas. Escribir la regla de un predicado ternario que vincule la cantidad de ventas, con el monto total de ventas y el sueldo del vendedor.
##### Regla
```prolog
sueldo(Ventas, MontoTotalVentas, Sueldo) :-
    SalarioFijo is 800,
    ComisionPorVenta is 50,
    PorcentajeComision is 0.08,
    % monto total de comisiones
    TotalComisiones is Ventas * ComisionPorVenta + MontoTotalVentas * PorcentajeComision,
    % sueldo total
    Sueldo is SalarioFijo + TotalComisiones.
```
##### Consulta
```prolog
?- sueldo(10, 2000000, Sueldo).
Sueldo = 161300.0
```

#### Ejercicio 8: promedio de notas
Definir un predicado que vincule las notas de cuatro parciales con la nota promedio.
##### Regla
```prolog
promedio(Nota1,Nota2, Nota3, Nota4, Promedio) :-
    SumaNotas is Nota1 + Nota2 + Nota3 + Nota4,
    Promedio is (SumaNotas/4).
```
##### Consulta
```prolog
?- promedio(2,2,10,3, Promedio)
Promedio = 4.25
```

#### Ejercicio 9: gasto total en sueldos
Una empresa tiene 5 gerentes, 23 empleados administrativos y 7 ordenanzas. Preparar un predicado que vincule el sueldo de cada categoría con el total que la empresa debe pagar a fin de mes.
##### Regla
```prolog
pagoFinal(SueldoGerente, SueldoAdministrativo, SueldoOrdenanza, PagoFinal):-
    SubtotalGerente is SueldoGerente * 5,
    SubtotalAdministrativo is SueldoAdministrativo * 23,
    SubtotalOrdenanza is SueldoOrdenanza * 7,
    PagoFinal is SubtotalGerente + SubtotalAdministrativo + SubtotalOrdenanza.
```

##### Consulta
```prolog
?- pagoFinal(650000, 450000, 800000, PagoFinal)
PagoFinal = 19200000
```

#### Ejercicio 10: Calcular herencia para cada hijo
Un millonario excéntrico tenía tres hijos Carlos, José' y Marta. Al morir dejó el siguiente legado: "A José le dejo 4/3 de lo que le dejo a Carlos; a Carlos le dejo 1/3 de mi fortuna y a Marta le dejo la mitad de lo que le dejo a José". Preparar un predicado que vincule la suma a repartir con lo que le toca a cada uno.
##### Regla
```prolog
herencia(HerenciaCarlos, HerenciaJose, HerenciaMarta, HerenciaTotal):-
    HerenciaCarlos is (HerenciaTotal / 3),
    HerenciaJose is (4/3) * HerenciaCarlos,
    HerenciaMarta is (1/2) * HerenciaJose.
```   
##### Consulta
```prolog
?- herencia(HerenciaCarlos, HerenciaJose, HerenciaMarta, 1000000).
HerenciaCarlos = 333333.3333333333,
HerenciaJose = 444444.4444444444,
HerenciaMarta = 222222.2222222222
```

#### Ejercicio 11: oferta de artículos
En un negocio se desea armar una oferta para fin de año combinando un artículo de bazar, uno de perfumería y uno de juguetería, con la condición de que la oferta no supere un cierto precio máximo. Para ello contamos con la __siguiente base de datos__:
```prolog
bazar(fuentes).
bazar(vasos)
bazar(juego_de_café).
perfumeria(jabones).
perfumeria(crema).
perfumeria(perfume).
perfumeria(autito).
perfumeria(muñeca).
perfumeria(oso).
precio(fuentes, 15).
precio(vasos, 12).
precio(juego_de_café, 20).
precio(jabones, 10).
precio(crema, 15).
precio(perfume, 25).
precio(autito, 10).
precio(muñeca, 15).
precio(oso, 20).
```
__Escribir una regla "oferta" que relacione tres artículos, uno de cada rubro, con el precio máximo, y que sea verdadero cuando la oferta no supere el precio máximo.__
##### Regla
```prolog
% Regla para verificar la oferta
oferta(ArticuloBazar, ArticuloPerfumeria, ArticuloJugueteria, PrecioMax) :-
    bazar(ArticuloBazar),
    perfumeria(ArticuloPerfumeria),
    jugueteria(ArticuloJugueteria),
    precio(ArticuloBazar, PrecioBazar),
    precio(ArticuloPerfumeria, PrecioPerfumeria),
    precio(ArticuloJugueteria, PrecioJugueteria),
    Total is PrecioBazar + PrecioPerfumeria + PrecioJugueteria,
    Total =< PrecioMax.
```

__Hacer una consulta para encontrar todas las ofertas de menos de $50.__
##### Consulta
```prolog
?- ofertas_bajo_cincuenta(ArticuloBazar, ArticuloPerfumeria, ArticuloJugueteria).
ArticuloBazar = fuentes,
ArticuloJugueteria = autito,
ArticuloPerfumeria = jabones

ArticuloBazar = fuentes,
ArticuloJugueteria = muneca,
ArticuloPerfumeria = jabones
...
...
```


#### Ejercicio 12: reglas `hermano_de` y `tio_de`
La siguiente es la descripción de la familia Adams:
```prolog
padre_de(homero, pericles).
padre_de(homero, merlina).
padre_de(desconocido, lucas).
padre_de(desconocido, homero).
varon(homero).
varon(lucas).
varon(cosa).
varon(pericles).
mujer(merlina).
mujer(morticia).
mujer(la-abuela).
madre(la-abuela, homero).
esposos(morticia, homero).
```
##### Usando los predicados anteriores, definir la relación `hermano_de`.
##### Regla
```prolog
hermano_de(X, Y) :-
    padre_de(Padre, X),
    padre_de(Padre, Y),
    X \= Y.
```
##### Escriba las reglas necesarias para la consulta `?- tio(Quien,merlina).`: 


##### Regla
```prolog

tio(Tio, Sobrino) :-
    hermano_de(Tio, PadreMadre),
    padre_de(PadreMadre, Sobrino),
    varón(Tio).
```
##### Consulta
```prolog
?- tio(Quien, merlina).
Quien = lucas
```

#### Ejercicio 13: ciudades conectadas por rutas
Se tiene la siguiente base de datos con ciudades vecinas y las rutas que las conectan:
```prolog
conectadas(arrecifes, san_antonio_de_areco, ruta_8).
conectadas(san_antonio_de_areco, cardales, ruta_8).
conectadas(carmen_de_areco, san_andres_de_giles, ruta_7).
conectadas(san_andres_de_giles, lujan, ruta_7).
conectadas(cardales, lujan, ruta_6).
conectadas(san_antonio_de_areco, san_andres_de_giles, ruta_41).
conectadas(san_andres_de_giles, mercedes, ruta_41).
conectadas(arrecifes, carmen_de_areco, ruta_51).
conectadas(carmen_de_areco, chivilcoy, ruta_51).
conectadas(lujan, mercedes, ruta_5).
conectadas(mercedes, chivilcoy, ruta_5).
siguiente(X, Y, Z) :- conectadas(Y, X, Z).
```

Escribir las siguientes consultas:
##### A. Están conectadas San Andrés de Giles y Mercedes?
Si, mediante la ruta 41
```prolog
% Consulta directa
?- conectadas(san_antonio_de_areco, san_andres_de_giles, Ruta)
Ruta = ruta_41
% Consultar todas las ciudades conectadas
?- conectadas(san_antonio_de_areco, Ciudad, _)
Ciudad = cardales,
Ciudad = san_andres_de_giles,
```
##### B. Chivilcoy está conectada con San Antonio de Areco?
```prolog
?- conectadas(chivilcoy, Ciudad, Ruta)
false
?- conectadas(chivilcoy, san_antonio_de_areco, Ruta)
false
?- conectadas(san_antonio_de_areco, chivilcoy, Ruta)
false
```
##### C. La ruta 51 conecta Carmen de Areco con San Andrés de Giles?
```prolog
?- conectadas(carmen_de_areco, san_andres_de_giles, ruta_51)
false
```
##### D. Con quien está conectada Luján?
```prolog
?- conectadas(lujan, Ciudad, _); conectadas(Ciudad, lujan, _).
Ciudad = mercedes
Ciudad = san_andres_de_giles
Ciudad = cardales
```
##### E. Cual es la que está conectada con San Andrés de Giles?
```prolog
?- conectadas(san_andres_de_giles, Ciudad, Ruta)
Ciudad = lujan,
Ruta = ruta_7
Ciudad = mercedes,
Ruta = ruta_41

?- conectadas(Ciudad, san_andres_de_giles, Ruta)
Ciudad = carmen_de_areco,
Ruta = ruta_7
Ciudad = san_antonio_de_areco,
Ruta = ruta_41
```
##### F. Cuales son las que están conectadas con San Andrés de Giles?
###### Predicado
```prolog
conectadas_con_san_andres_de_giles(Ciudad) :-
    conectadas(san_andres_de_giles, Ciudad, _);
    conectadas(Ciudad, san_andres_de_giles, _).
```
###### Consulta
```prolog
?- conectadas_con_san_andres_de_giles(Ciudad).
Ciudad = lujan
Ciudad = mercedes
Ciudad = carmen_de_areco
Ciudad = san_antonio_de_areco
```
IMPORTANTE: el lugar que tome Lujan como parámetro es importante para la G y H.
##### G. Que rutas llegan a Luján?
```prolog
?- conectadas(_, lujan, Ruta)
Ruta = ruta_7
Ruta = ruta_6
```
##### H. Que rutas salen de Luján?
```prolog
?- conectadas(lujan, _, Ruta)
Ruta = ruta_5
% Si nos interesa saber la/s ciudad/es:
?- conectadas(lujan, Ciudad, Ruta)
Ciudad = mercedes,
Ruta = ruta_5
```
##### I. Se puede salir de Carmen de Areco y llegar a Luján pasando por San Andrés de Giles?
```prolog
?- conectadas(carmen_de_areco, san_andres_de_giles, _), conectadas(san_andres_de_giles, lujan, _).
true
```
¿Por qué `_` devuelve true o false?
Cuando usas `_`, Prolog solo está verificando si las conexiones existen, sin preocuparse por el valor de las rutas. Si las conexiones son válidas, devuelve true. Si no lo son, devuelve false.
##### J. Que ruta llega a Chivilcoy saliendo de Luján y pasando por Mercedes?
```prolog
?- conectadas(lujan, mercedes, _), conectadas(mercedes, chivilcoy, Ruta)
Ruta = ruta_5
```

#### <a id="mas-info"></a>
<span style="display:none;">Firma</span>

---
✍️ **Autor:** Emilio Giordano  
🔗 Más resúmenes de Programación Declarativa en el [repositorio](https://github.com/EmilioGiordano/Programacion-Declarativa-Practica)  

---
