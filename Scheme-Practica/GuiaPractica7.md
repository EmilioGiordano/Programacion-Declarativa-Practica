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
(require math)
(define (circunferencia x) (* pi(* x 2)))
```
```scheme
# Consulta
(circunferencia 5)
Output: 31.41592653589793
```
6. Escribir una función que, dada una temperatura en grados Celsius, la devuelva expresada en grados Fahrenheit. La fórmula de conversión es f = (9/5)c + 32.
```scheme
(define (temperatura x) (+ 32 (* 1.8 x)))
```
```scheme
# Consulta
(temperatura 12)
Output: 53.6
```
7. Sabiendo que: 1 pie = 12 pulgadas; 1 yarda = 3 pies; 1 pulgada = 2.54 centímetros. Definir tres funciones (yardas, pulgadas y pies), que, dado un valor en centímetros, devuelva esa longitud expresada en esas unidades. 
```scheme
(define (pulgadas x)(/ x 2.54))
(define (pies pulgada) (/ pulgada 12))
(define (yarda pies) (/ pies 3))
```
```scheme
# Consulta
; Ejemplo de uso:
(define (convertir-centimetros-a-todo x)
  (let* ((pulgadas-resultado (pulgadas x))
         (pies-resultado (pies pulgadas-resultado))
         (yardas-resultado (yarda pies-resultado)))
    (list pulgadas-resultado pies-resultado yardas-resultado)))

; Convierte 100 centímetros a pulgadas, pies y yardas:
(convertir-centimetros-a-todo 100)
Output:
'(39.37007874015748 3.2808398950131235 1.0936132983377078)
```
8. Definir "superficie", una función que dado el ancho y el largo de una habitación retorne su superficie.
```scheme
(define (superficie x y)(* x y))
```
```scheme
# Consulta
(superficie 10 10)
Output: 100
```
9.  Definir una función para ingresarle la base y la altura de un triángulo, y devuelva el valor del área.
```scheme
(areaTriangulo 12 15)
```
```scheme
# Consulta 
(areaTriangulo 12 15)
Output: 90.0
```
10. La relación entre los lados (a,b) de un triángulo y la hipotenusa viene dada por la fórmula 
a2 + b2 = h2. Definir una función para que, dadas las longitudes de los lados, calcule y 
devuelva la hipotenusa.
```scheme
(define (hipotenusa a b)(sqrt(+ (* a a)(* b b))))
```
```scheme
# Consulta
(hipotenusa 5 5)
Output: 7.0710678118654755
```
11.  El área de un triángulo cuyos lados son a, b y c se puede calcular por la fórmula:
A = sqrt(p * (p - a) * (p - b) * (p - c))
donde p = (a+b+c)/2. Definir una función para ingresarle a, b y c,  y devuelva el área del triángulo.
```scheme
(define (area-triangulo a b c)
  (let* ((p (/ (+ a b c) 2)) ; semiperímetro
         (area (sqrt (* p (- p a) (- p b) (- p c))))) area))
```
```scheme
# Consulta 
(area-triangulo 3 4 5)
Output: 6
``` 
12.   Definir una función que acepte los coeficientes a, b y c de la ecuación de primer grado a * x + b = c, y devuelva el valor de la raíz.
```scheme
(define (ecuacion-primer-grado a b c)
(/ (- c b)a ))
```
```scheme
# Consulta 
(ecuacion-primer-grado 10 2 5)
Output: 1/10
```
13.   Definir una función que acepte dos números enteros, y devuelva una lista con el cociente 
y el resto la división entera entre los dos números.
```scheme
```
```scheme
```
14.   Definir una función que, dada una cantidad de segundos, devuelva una lista con la misma 
cantidad expresada en minutos y segundos.
```scheme
```
```scheme
```  
15.   Definir una función que acepte la cantidad de varones y mujeres que hay en un recinto, y  devuelva una lista con el porcentaje de varones y mujeres.
```scheme
```
```scheme
```
16.   Utilizando las expresiones descriptas anteriormente, definir la función pasaje, que reciba  una medida en centímetros, y retorne una lista con esa medida expresada en pulgadas,  pies y yardas.
```scheme
```
```scheme
```
17.   Definir una función llamada doblar que, dada una lista de 3 números, devuelve el doble de su primera componente.
```scheme
```
```scheme
```
18.   Definir una función llamada producto_por_tres que dada una lista de 3 números devuelva otra lista con los mismos multiplicados por 3.
```scheme
```
```scheme
```
