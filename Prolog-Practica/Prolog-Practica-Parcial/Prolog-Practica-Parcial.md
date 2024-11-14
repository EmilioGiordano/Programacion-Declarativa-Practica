- [Ejercicio 1](#ejercicio-1)
    - [Base de hechos](#base-de-hechos)
- [Ejercicio 2](#ejercicio-2)
    - [Regla ternaria](#regla-ternaria)

## Ejercicio 1
Define hechos sobre los productos en un almacén, como su nombre, categoría (electronicos, ropa, alimentos), cantidad en stock y precio. Crea reglas que permitan saber qué productos están por debajo de un cierto nivel de stock o cuáles tienen un valor total (cantidad * precio) superior a un umbral.
##### Base de hechos
```prolog
producto(pepsi).
producto(coca_cola).
producto(sprite).
producto(budin).
producto(cafe).

precio(pepsi, 1600).
precio(coca_cola, 1700).
precio(sprite, 1500).
precio(budin, 1300).
precio(cafe, 3500).

stock(pepsi, 50).
stock(coca_cola, 30).
stock(sprite, 20).
stock(budin, 10).
stock(cafe, 40).

categoria(pepsi, bebida).
categoria(coca_cola, bebida).
categoria(sprite, bebida).
categoria(budin, alimento).
categoria(cafe, alimento).

% ------------ Reglas ------------ %
checkProduct(Producto, Precio, Stock, Categoria) :-
    producto(Producto),
    precio(Producto, Precio),
    stock(Producto, Stock),
 	categoria(Producto, Categoria).
 	
productoConMasDeNStock(Producto, N) :-
    stock(Producto, Stock),
    Stock >= N.


productoConMenosDeNStock(Producto, N) :-
    stock(Producto, Stock),
    Stock < N.
```

##### Consulta
```prolog
?- productoConMasDeNStock(Producto, 14).
Producto = pepsi
Producto = coca_cola
Producto = sprite
```
##### Consulta
```prolog
?- checkProduct(pepsi, Precio, Stock, Categoria)
Categoria = bebida,
Precio = 1600,
Stock = 50
% ---------------------------------------------------- %
?- checkProduct(Producto, Precio, Stock, alimento)
Precio = 1300,
Producto = budin,
Stock = 10

Precio = 3500,
Producto = cafe,
Stock = 40
```
##### Consulta
```prolog
productoConMenosDeNStock(Producto, 25)
Producto = sprite
Producto = budin
```
## Ejercicio 2
Una empresa de ventas paga a sus empleados un salario fijo de 800 pesos, mas una comisión de $ 50 por cada venta realizada, más el 8% sobre el monto total de ventas. Escribir la regla de un predicado ternario que vincule la cantidad de ventas, con el monto total de ventas y el sueldo del vendedor.

##### Regla ternaria
```prolog
montoTotal(CantidadVentas, MontoTotalVentas, SalarioFinal) :-
    SalarioFijo is 800,
    ComisionPorVenta is 50,
    PorcentajeMontoVentas is MontoTotalVentas * 0.08,
    TotalPorVentas is CantidadVentas * ComisionPorVenta,
    SalarioFinal is (SalarioFijo + TotalPorVentas + PorcentajeMontoVentas).
```
