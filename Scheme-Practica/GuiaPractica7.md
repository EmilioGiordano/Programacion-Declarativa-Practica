## Unidad 6: Introducción a Programación Funcional > Scheme


1. Escribir una función llamada "tres" que, dado cualquier valor, devuelve el número 3.
```scheme
(define (tres x) 3)   
(tres 5)
```
```scheme
# Consulta
(tres 5)
Output: 3
```

2. Escribir una función llamada triple que, dado cualquier valor x, devuelve el triple de x.
```scheme
(define (triple x) (* x 3))
(triple 5)
```
```scheme
output: 15
```
3. Función que, dado cualquier número, devuelve la mitad de este.
```scheme
(define (mitad x) (/ x 2))
```
```scheme
# Consulta
(mitad 10)
output: 5
```
4. Escribir una función que, dado cualquier valor x, devuelve el duplo de la suma de 15 + x.
```scheme
(define (duplo x) (* 2 (+ 15 x)))
```
```scheme
# Consulta
(duplo 10)
output: 50
```
5. Definir "circunferencia", que dado el radio retorne la longitud de esta.  
```scheme
```
```scheme
```
6. Escribir una función que, dada una temperatura en grados Celsius, la devuelva expresada en grados Fahrenheit. La fórmula de conversión es f = (9/5)c + 32.
```scheme
```
```scheme
```
7. Sabiendo que: 1 pie = 12 pulgadas; 1 yarda = 3 pies; 1 pulgada = 2.54 centímetros. Definir tres funciones (yardas, pulgadas y pies), que, dado un valor en centímetros, devuelva esa longitud expresada en esas unidades. 
```scheme
```
```scheme
```
8. Definir "superficie", una función que dado el ancho y el largo de una habitación retorne su superficie.
```scheme
```
```scheme
```
9.  Definir una función para ingresarle la base y la altura de un triángulo, y devuelva el valor del área.
```scheme
```
```scheme
```
10. La relación entre los lados (a,b) de un triángulo y la hipotenusa viene dada por la fórmula 
a2 + b2 = h2. Definir una función para que, dadas las longitudes de los lados, calcule y 
devuelva la hipotenusa.
```scheme
```
```scheme
```
11.  El área de un triángulo cuyos lados son a, b y c se puede calcular por la fórmula: A = sqrt(p 
* (p - a) * (p - b) * (p - c)) donde p = (a+b+c)/2. Definir una función para ingresarle a, b y c, 
y devuelva el área del triángulo.
```scheme
```
```scheme
``` 
12.  Definir una función que acepte los coeficientes a, b y c de la ecuación de primer grado a * 
x + b = c, y devuelva el valor de la raíz.
```scheme
```
```scheme
```
13.  Definir una función que acepte dos números enteros, y devuelva una lista con el cociente 
y el resto la división entera entre los dos números.
```scheme
```
```scheme
```
14.  Definir una función que, dada una cantidad de segundos, devuelva una lista con la misma 
cantidad expresada en minutos y segundos.
```scheme
```
```scheme
```  
15.  Definir una función que acepte la cantidad de varones y mujeres que hay en un recinto, y  devuelva una lista con el porcentaje de varones y mujeres.
```scheme
```
```scheme
```
16.  Utilizando las expresiones descriptas anteriormente, definir la función pasaje, que reciba  una medida en centímetros, y retorne una lista con esa medida expresada en pulgadas,  pies y yardas.
```scheme
```
```scheme
```
17.  Definir una función llamada doblar que, dada una lista de 3 números, devuelve el doble de su primera componente.
```scheme
```
```scheme
```
18.  Definir una función llamada producto_por_tres que dada una lista de 3 números devuelva otra lista con los mismos multiplicados por 3.
```scheme
```
```scheme
```