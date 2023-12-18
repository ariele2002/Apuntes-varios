# Python Apuntes

## Variables

Los nombres de variables en Python solo pueden contener valores alfanuméricos en
el rango de **(A-Z, a-z, 0-9, \_)**
como se ve también el carácter especial guion bajo o (underscore en inglés) "\_".

- No se admiten otros caracteres especiales en el nombre de las variables excepto el
  ya mencionado guion bajo o underscore en inglés "\_".
- Las variables deben **iniciar siempre** con una letra o un guion bajo, pero nunca con
  un número esto provocaría un error de sintaxis.
- Las variables que están compuestas por mas de una palabra deberán separarse con guion bajo ej: **temperatura_media**.
- Los nombres de las variables son case-sensitive, esto quiere decir que distingue entre mayúsculas y minúsculas, por lo cual las variables **nombre, Nombre** y **NOMBRE** serán tres variables distintas (ojo con esto).
  > **Mal:** `$nombre`, `nombre%`, `nombre&apellido`, `nombre-apellido`, `9gatos`
  >
  > **Bien:** `_nombre`, `nombre_apellido`, `nombreApellido`, `Joe90`, `Joe_90`

## Tipos de Datos

### Datos numéricos

En Python no existe un limite para el número máximo que podemos representar, el limite esta dado por los recursos del hardware que utilicemos.

#### Tipos de datos numéricos:

- _Enteros_: 1, 10, 38, 1985
- _Flotantes_: 2.3, 54.50, 3.141638

### Booleanos

Los booleanos son los valores de representación de verdad y deben iniciar con mayúsculas. Estos valores son importantes para los **condicionales** y los **bucles o loops**.

- _True_: (verdadero)
- _False_: (falso)

## Cadenas de Caracteres (String)

Son secuencias de caracteres encerrados entre comillas y usados para representar texto en el programa. Estas cadena pueden ir encerradas entre comillas dobles o simples.

#### Ejemplo:

```py
Nombre = "Pepe" o Nombre = 'Pepe'
```

Para determinar el tamaño o longitud de una cadena (cantidad de caracteres que posee) se utiliza la función **len()**.

```py
len("prueba")   # Retorna 6
nombre = "Anastasia"
len(nombre)    # Retorna la cantidad de caracteres en este caso 9.
```

### Estructura de un String

La estructura del string es como una matriz o arreglo de una dimensión indexada por enteros y al igual que todo arreglo comienza con el indice 0 (cero). Ej:

```py
cadena = "Probando"
# indice  01234567
```

### Indexing

Si que queremos acceder a algún carácter individual del string utilizamos el método de **indexación** cuya sintaxis es `<string>[<indice>]` Ej:

```py
"Probando"[3] nos dará como resultado 'b'
```

Si indicamos un indice que esta fuera del rango de indices del string nos dará un error: **IndexError**

```py
"Probando"[8] nos dará como resultado "IndexError"
```

### f-string

Se utiliza para poner valores dentro de un string. Ejemplo:

```py
nombre = "Pepe"
texto = f"Mi nombre es {nombre}"
print(texto)
>>> Mi nombre es Pepe
```

También para números flotantes se puede usar `{variable:,}` la `,` después del `:` es el separador de miles, puede usarse el que corresponda
según el uso de la región. También usando el `.2f` (el dos indica la cantidad de decimales o precisión), de esta manera se puede dar formato de salida a los valores.

```py
num = 1000000.5378
print(f"{num:,.2f}")
>>> 1,000,000.54
```

### Métodos de Cadenas de Caracteres

Son operaciones comunes que vienen implementadas en Python. Los métodos son parecidos a funciones pero están asociados a un elemento o valor en particular.<br>
Sintaxis: `<string>.<método>(<valores>)`<br>
Métodos mas comunes:

- `.capitalize()`: Este método retorna **una copia** del string con el primer carácter en mayúsculas y el resto en minúsculas.

```py
nombre = "roberto"
nombre.capitalize() retorna "Roberto"
```

Otros métodos muy usados:

- `.find(), .index()`: Son utilizados para búsquedas.
- `.isalnum()`: Retorna `True` si todos los caracteres son alfanuméricos.

```py
string = "Ricardo 10"
string2 = "Ricardo@gmail.com"
string.isalnum() Retorna True
string2.isalnum() Retorna False
```

- `.isalpha()`: Retorna True si todos los caracteres son alfabéticos.
- `.isdecimal()`: Retorna True si todos los caracteres son decimales.
- `.isdigit()`: Retorna True si todos los caracteres son dígitos.
- `.islower()`: Retorna True si todos los caracteres están en minúsculas.
- `.isupper()`: Retorna True si todos los caracteres están en mayúsculas.

Todos los métodos que comienzan en **is** retornan un booleano y son muy utilizados en los condicionales lógicos.

- `.lower()`: Retorna una **copia de la cadena** con todos sus caracteres en minúsculas.
- `.upper()`: Retorna una **copia de la cadena** con todos sus caracteres en mayúsculas.

## La Función type()

La función `type()` Retorna el tipo de un valor determinado.<br>
Sintaxis: `type(<valor o variable>)`

```py
type(35)     Retorna <class 'int'>
type(3.2)    Retorna <class 'float'>
type(True)   Retorna <class 'bool'>
type("Pepe") Retorna <class 'str'> (string)
```

## Recibiendo Datos del Usuario (input)

Para solicitar datos al usuario se utiliza la función `input()`<br>
Sintaxis: `<variable> = input(<mensaje>)`

```py
num = input("Ingrese un Número: ")
print(num)

Ejecución:
Ingrese un Número: 5
5
```

**`Advertencia:`** La función input() siempre retorna una **cadena de caracteres (string)** independientemente del tipo de dato que ingrese el usuario. Ojo al piojo, siempre hay que convertir el retorno del `input()` al tipo de dato que se requiera.<br>
Ejemplo:

```py
num = int(input("Ingrese un Número: "))
print(num)
print(type(num))

Ejecución:
Ingrese un Número: 5
5
<class 'int'>
```

## Operadores

Los **Operadores** son símbolos que denotan una operación en el programa.<br>
Los **Operandos** son valores con los cuales se ejecuta la operación.<br>
Los **Operadores** y los **Operandos** se juntan para formar una **Expresión**<br>

```py
Operador + Operando = Expresión
```

La **Expresión** es la combinación de **valores**, **variables**, y **operadores** que al ser evaluados resultan en un **valor**.<br>
Este concepto es **muy importante** en programación, se **evalúa** una **expresión** para obtener un valor final.

- Las Expresiones se evalúan de **izquierda a derecha** excepto cuando ciertos operadores de mayor "importancia o precedencia" para el orden de las operaciones al igual que en las matemáticas.

### Tipos de Operadores

#### Aritméticos

- Suma: `3 + 2` = 5 En el caso de strings concatena `"Hola" + " " + "Mundo!"` = "Hola Mundo!".
- Resta: `3 - 2` = 1
- Multiplicación: `3 * 2` = 6
- División: `4 / 2` = 2.0 En la división el resultado **siempre** es un número de coma flotante (float).
- División Entera: `5 // 3` = 1 este operador devuelve un entero **truncando** los valores decimales **no los redondea** y solo devuelve un flotante cuando los operandos son de coma flotante, pero usa el mismo procedimiento de truncar los decimales Ej: `5.0 // 3.0` = 1.0 Es muy utilizado para **Búsqueda Binaria**.
- Exponente: `2 ** 3` = 8 Puede obtenerse la raíz cuadrada aplicando la exponenciación a (1/2) Ej: `16 ** (1/2)` = 4.0 y también sigue la regla de todo número elevado a cero (0) es igual a 1 Ej: `5 ** 0` = 1
- Módulo: `5 % 2` = 1 Este operador devuelve el resto de la división, es muy utilizado para verificar si un número es par.

El orden básico de las operaciones aritméticas puede ser recordado con el acrónimo<br>**PEMDAS**

- `P`arentesis: Todas las operaciones dentro de paréntesis.
- `E`xponentes: Tienen la mayor precedencia luego de los paréntesis.
- `M`ultiplicación: Tienen la mayor precedencia luego de los exponentes.
- `D`ivisión: Tiene la mayor precedencia luego de la multiplicación.
- `A`ddition: (suma) Tiene la mayor precedencia luego de la división.
- `S`ubtraction: (resta) Tiene la mayor precedencia luego de la suma.<br>

#### Lógicos

Nos permiten trabajar con valores booleanos (**True**, **False**).

- **and** : Solo retorna True cuando los dos operandos son verdaderos.

  |   x   |   y   | x and y |
  | :---: | :---: | :-----: |
  | True  | True  |  True   |
  | True  | False |  False  |
  | False | True  |  False  |
  | False | False |  False  |

  ```py
  (5 < 6) and ( 6 > 8) : False
    True        False  : False
  ```

- **or** : Evalúa si cualquiera de los operandos es verdadero el resultado es verdadero.

  |   x   |   y   | x or y |
  | :---: | :---: | :----: |
  | True  | True  |  True  |
  | True  | False |  True  |
  | False | True  |  True  |
  | False | False | False  |

  ```py
  (5 < 6) or ( 6 > 8) : True
    True       False  : True
  ```

- **not** : Este operador niega el valor de la expresión. -
  |x| not x|
  |:----:|:----:|
  |True|False|
  |False| True|

  ```py
  not (5 < 6) : False
  not  True   : False
  ```

El orden de prioridad cuando tenemos varios operadores lógicos en una expresión, se evalúan de esta manera: primero **not** luego **and** y finalmente **or**. Cuando tenemos varios operadores con el mismo orden de prioridad, se evalúan de izquierda a derecha.

#### De Asignación

Son utilizados para **asignar valores** a las variables del programa.

|     |       |
| :-: | :---: |
|  =  |  +=   |
| -=  | `*=`  |
| /=  | `**=` |
| //= |  %=   |

```py
Ej: variable = 10
    variable += 5 : 15
    variable /= 3 :  5.0
    variable *= 3 : 15.0
```

#### Relacionales

Son utilizados para **comparar valores** y retornan un **valor booleano**.
|||||
|:---:|:---:|:---:|:---:|
|>| mayor que|>=| mayor o igual que|
|<| menor que|<=| menor o igual que|
|==| igual que|!=| distinto que|

```py
5 > 5 : False
5 >= 5 : True
8 == 8 : True
8 != 8 : False
"hola" == "bola" : False
```

En el caso de las cadenas (strings) la comparación las hace siguiendo el orden del diccionario para evaluarlo, también el tamaño de la cadena cuenta en la evaluación.

```py
"ABC" < "A" : False
"A" < "B" : True
"C" != "D" : True
"Noris" == "Gino" : False
```

## Sentencias Condicionales

Son una **instrucción** o un **grupo** de **instrucciones** cuya ejecución depende del valor de una **condición booleana**.<br>

### Sentencia if

```py
Sintaxis:
    if <condición>:
        # código
```

Debe escribirse el if espacio la condición seguida de **:** e indentar el código debajo para que el compilador identifique que código depende del condicional y cual del programa principal.

```py
temp = 15
if temp < 25:
    print("Que frío lo pario!")
```

#### Sentencia else

Esta sentencia es para resolver que se debe hacer si no se cumple la condición y ejecutar otro código si fuera necesario.

```py
Sintaxis:
    if <condición>:
        # código si cumple la condición
    else:
        # código si no cumple la condición
# código del programa general
```

```
temp = 27
if temp < 25:
    print("Que frío lo pario!")
else:
    print("Que calor de locos!)
Ejecución:
Que calor de locos!
```

#### Sentencia elif

Permite especificar otras condiciones y como manejar esas condiciones.

```py
Sintaxis:
    if <condición1>:
        # código
    elif <condición2>:
        # código
    else:
        # código
    # código del programa general.
```

```py
temp = 15
if temp <=0:
    print("Frío que pelaaa!)
elif temp < 25:
    print("Que frío lo pario!)
else:
    print("Que calor de locos!)
```

**`Advertencia:`** Pueden haber varias sentencias **elif** en un condicional pero **solo una** sentencia **else**. La clausula else debe ser única en un condicional y que va a ser un respaldo cuando todas las otras condiciones sean falsas.

## Comentarios (comentar código)

Un comentario es un texto que se escribe en el programa para facilitar su comprensión.
La función principal de los comentarios es, describir la lógica de ciertas partes del código a otros programadores que lean el programa.
Los comentarios deben hacerse comenzando con `#`

```py
# Este es un comentario
num = 3 ** 5 # este es otro comentario
```

Para comentar código en un bloque se utiliza `'''` (tres comillas simples) al principio y al final del bloque, también puedes utilizar comillas dobles `"""`.

```py
'''
Este es un bloque de comentario
en varios renglones, se inicia y
finaliza con tres comillas simples.
'''

"""
Este es un bloque de comentario
en varios renglones, se inicia y
finaliza con tres comillas dobles.
"""
```

## Listas

Es una **estructura de datos** utilizada para almacenar múltiples valores en secuencia.
Los valores son almacenados en **secuencias ordenadas** cada uno de los elementos tiene su propia secuencia mediante un índice (**index**).

```py
lista = [1, 2, "peras", True, 3.4]
```

### Características

- Secuencia ordenada de valores.
- Puede contener valores de cualquier tipo.
- Puede contener valores de distintos tipos.
- Cada posición en la lista está asociada a un entero llamado **índice**.
- Es **mutable**. Puede ser modificada.

### Acceder a un elemento

Para acceder a un elemento de la lista, usamos su índice correspondiente.<br>
Sintaxis: `<lista>[<índice>]`

```py
lista = ["perro", "Juan", 3, True]
# índice:   0        1    2    3

print(lista[0])
$ perro

print(lista[1])
$ Juan

```

Las cadenas de texto (**strings**) se comportan como listas se puede acceder a cada uno de los elementos por medio de su indice.

```py
cadena = "murciélago"
print(cadena[2])

$ r
```

A diferencia de de las **listas** un **string** no es mutable por lo cual cuando se quiera cambiar alguno de sus valores generara un error.

```py
lista = ["banana", "pera", "manzana"]
cadena = "Comer"

lista[1] = "uva"
print(lista)
$ ['banana', 'uva', 'manzana']

cadena[0] = "P"
$ TypeError: 'str' object does not support item assignment

```

### Slice o Rebanada

Se puede acceder a varios elementos descartando otros tomando una porción (slice) de una lista (creando una nueva sin modificar la existente) y se usa la siguiente sintaxis:<br>
`lista[<indice_inicial> : <indice_final>]` donde el **indice_inicial** es `inclusivo` y el **indice_final** es `exclusivo`.<br>
**Nota:** Cuando usamos slice el indicar **un _indice fuera del rango_ no genera _error_**.

```py
fruta = ["banana", "pera", "manzana", "coco"]
    index:  0         1        2         3
print(fruta[1:3])
$ ['pera', 'manzana']
```

Dejando el primer valor o el ultimo o ambos vacíos se pueden establecer rangos como:

- `lista[:3]` desde el inicio de la lista, hasta el indice indicado
- `lista[2:]` desde el indice indicado al final de la lista.
- `lista[:]` toda la lista (no me parece practico pero no esta mal mencionarlo)

#### Paso o Pass

El paso se utiliza para pasar de algunos elementos, su sintaxis es `lista[<idice_inicio>:<inidice_final>:<paso>]`

```py
frutas = ["pera", "banana", "manzana", "uva", "melon", "sandia"]
print(frutas[1:5:2])
$ ['banana', 'uva']

print(frutas[::2])
$ ['pera', 'manzana', 'melon']

print(frutas[0:6:3])
$ ['pera', 'uva']
```

### Indice negativo

El indice negativo se utiliza para seleccionar un elemento desde el final de la cadena y de esta hacia la izquierda, donde el indice `[-1]` pertenece al ultimo elemento de la cadena.

```py
fruta = ["banana", "pera", "manzana", "coco"]

print(fruta[-1])
$ coco

print(fruta[-2])
$ manzana

print(fruta[1:-2])
$ ['pera']

print(fruta[-3:-1])
$ ['pera', 'manzana']
```

### Métodos para operar con listas

- `append()` agrega un elemento al final de la lista `<lista>.append(<elemento>)`
  ```
  nums = [1, 2, 3, 4]
  nums.append(5)
  print(nums)
  >>> [1, 2, 3, 4, 5]
  ```
- `insert()` Inserta un elemento en un índice especifico `<lista>.insert(<índice>, <elemento>)`
  ```
  nums = [1, 2, 3, 4, 5]
  nums.insert(0, 6)
  print(nums)
  >>> [6, 1, 2, 3, 4, 5]
  ```
- `remove()` Elimina un elemento, este método nos permite eliminar la primera ocurrencia del elemento especificado en los paréntesis: `<lista>.remove(<elemento>)`
  ```py
  nums = [1, 2, 3, 4, 5, 4]
  nums.remove(4)
  print(nums)
  >>> [1, 2, 3, 5, 4]
  ```
  Si intentamos remover un valor que no existe en la lista nos dará un **ERROR**
- `in` Verifica si un elemento esta en la lista `<elemento> in <lista>`

  ```py
  lista = [1, 2, "Pepe", 4, 5]
  "Pepe" in lista
  >>> True
  ```

  Devuelve un booleano que puede usarse en un condicional:

  ```py
  if "Pepe" in lista:
      print("Pepe se encuentra en la lista!")
  else:
      print("Nadie sabe donde esta Pepe")

  >>> "Pepe esta en la lista!"
  ```

- `index()` Retorna el índice de la primera ocurrencia del elemento en la lista. Si no se encuentra el elemento, ocurre un error. `<lista>.index(<elemento>)`
  ```py
  nombre = ["Ana", "Juan", "Francisco","Juan"]
  nombre.index("juan")
  >>> 1
  ```

### Cambiar valores en una lista

Para cambiar un valor en una lista se utiliza la siguiente sintaxis: `<lista>[<índice>] = <nuevo_valor>`

```py
nums = [1, 2, 3, 4]
nums[2] = 6
print(nums)
>>> [1, 2, 6, 4]
```

### Métodos de las Listas

Sintaxis: `<lista>.<método>(<parámetros>)`<br>
Métodos importantes:

- `.count(<elemento>)` Permite contar las veces que se repite el elemento indicado.
- `.extend(<lista>)` Nos permite extender una lista agregándole los elementos de otra lista.
- `.pop()` Elimina y retorna un elemento de la lista.
- `.reverse()` Reversa el orden actual de la lista.
- `.sort()` Ordena la lista en un orden especifico.

## Tuplas (Tuples)

Es una estructura de datos **inmutable** que contiene una secuencia **ordenada** de elementos.

```py
tuple = (1, 2, "Pepe", 3.5, True)
```

### Características

- Secuencia **ordenada** de valores.
- Puede contener valores de cualquier tipo de datos.
- Puede contener valores de distintos tipos de datos.
- Cada posición en la tupla se identifica con un entero denominado **índice**.
- Es **inmutable**. No puede ser modificada.
  Para acceder a sus elementos se hace de la misma forma que con las listas.

```py
letras = ("A", "B", "C")

letras[0]
>>> 'A'
letras[1]
>>> 'B'
letras[2]
>>> 'C'
```

Para encontrar un elemento se utiliza `in` al igual que en las listas.

```py
tupla = (1, 2, "Pepe", 4, 5)
"Pepe" in tupla
>>> True
```

Devuelve un booleano que puede usarse en un condicional:

```py
if "Pepe" in tupla:
    print("Pepe se encuentra en la tupla!")
else:
    print("Nadie sabe donde esta Pepe")

>>> "Pepe esta en la tupla!"
```

`index()` Retorna el índice de la primera ocurrencia del elemento en la tupla. Si no se encuentra el elemento, ocurre un error. `<tupla>.index(<elemento>)`

```py
nombre = ("Ana", "Juan", "Francisco","Juan")
nombre.index("juan")
>>> 1
```

`count()` Nos muestra el número de ocurrencias de un elemento en la tupla. `<tupla>.count(<elemento>)`

```py
tupla = (1, 2, 3, 4, 5, 6, 4, 7, 8, 4)
tupla.count(4)
>>> 3
```

## Diccionarios

Es una colección de **pares clave valor**.<br>
Ejemplo de diccionario: `{"A": 45, "B": 30}` "A" = clave : 45 = valor.

### Características:

- Colección de pares Clave-Valor.
- Las claves deben ser **únicas e inmutables**.
- Los valores asociados pueden ser de cualquier tipo.
- La clave se usa para acceder a su valor asociado.
- Los pares clave-valor pueden ser modificados, añadidos y eliminados.
  Por lo tanto los diccionarios son un tipo de estructura de datos **mutable**.

Para acceder a los valores del diccionario, se utiliza la siguiente sintaxis `<diccionario>[<clave>]`

```py
edades = {"Pepe": 23, "Anastasia": 45}
edades["Pepe"]
>>> 23
edades["Anastasia"]
>>> 45
```

Otra opción es utilizando el método `get()`

```py
edades.get("Pepe")
>>> 23
```

**Modificar, Agregar:** `<diccionario>[<clave>] = <nuevo_valor>` en este caso si la clave es nueva se agregará un nuevo par clave-valor al diccionario, si ya existiera se cambiara el valor de la clave ya existente.

```py
edades = {"Pepe": 23, "Anastasia": 45}
edades["Ana"] = 36
edades["Pepe"] = 18
>>> {"Pepe": 18, "Anastasia": 45, "Ana": 36}
```

**Remover:** Sintaxis: "`del <diccionario>[<clave>]`".

```py
del edades["Ana"]
>>> {"Pepe": 18, "Anastasia": 45}
```

Comprobar la existencia de un elemento: `<clave> in <diccionario>`

## Documentación

python.org -> documentation -> python Docs -> funciones Built-in: información sobre las funciones que ya vienen incorporadas.

## Ciclos

Es una _estructura de control_ en programación que permite _ejecutar_ una o varias líneas de código _múltiples veces_.
**Iteración:** Es una repetición de un cierto grupo de instrucciones, una repetición del bucle o ciclo.

### For

Lo utilizamos cuando sabemos con antelación **cuantas veces** debemos repetir ciertas instrucciones.

```py
Sintaxis:
for <variable> in range(<inicio>, <fin>, <paso>):
    # Código

for i in range(4):
    print(i)
>>> imprime i 4 veces con los valores: 0 1 2 3.
```

`<variable>` en este caso es una variable de control del bucle.
Características:

- Variable que puede ser utilizada en el código que se va a repetir.
- Se actualiza automáticamente antes de cada iteración. Se actualiza con los valores devueltos por la función range.
- Debe tener un nombre descriptivo.

`range`: devuelve una secuencia de entero que nosotros especificamos.Cuando especificamos un solo valor lo toma como el **final** de la secuencia y por defecto el numero inicial va a ser **cero**.<br>
`paso`: Opcional, se agrega esta opción cuando se desea que incremente en mas de 1 a ..n.

```py
range(4) --> 0, 1, 2, 3
```

### Iterar sobre iterables (ciclos sobre iterables)

Los iterables son datos, estructuras o variables que pueden retornar sus elementos uno a la vez, estos pueden iterarse con bucles.

- Cadenas de caracteres.
- Listas
- Tuplas
- Diccionarios
- Otros...

Sintaxis:

```py
for <var> in <iterable>:
    # Código

for char in "Loops":
    # Código
    iteration índice char (Ejemplo del paso de la iteración)
        1       0    'L'
        2       1    'o'
        3       2    'o'
        4       3    'p'
        5       4    's'
```

Iterar sobre diccionarios: En estos casos el valor de la variable en la iteración es
la llave del diccionario.<br>
`.values()`: Si se desea iterar sobre los valores se debe usar esta función.<br>
`.items()`: Si se desea iterar sobre el par llave-valor se utiliza esta función y se agrega una variable mas; pueden usarse individualmente dentro del código.

```py
letras = {"a": 1, "b": 2}
for letra in letras:
    print(letra) # imprime la llave: 'a' 'b'

for valor in letras.values():
    print(valor) # imprime los valores: 1 2

for clave, valor in letras.items():
    print(clave, valor) # imprime el par 'a' 1 'b' 2
```

### While

- Es un ciclo que continúa **mientras** una condición es **verdadera (True)** y se detiene cuando es **falsa (False)**.
- **Iteraciones**: Un ciclo while **no tiene** un número fijo o predeterminado de iteraciones, por los cual se utiliza cuando no se sabe la cantidad exactas de interacciones.
- Los ciclos while **no actualizan** la(s) variable(s) de control automáticamente. Las variales de control deben ser actualizadas explicitamente en el cuerpo del while con linea de código, de lo contrario produce un bucle infinito asi que **Mucho ojo con esto**.
- **Sintaxis:**

  ```py
  while <condición>:
      # bloque de código
  ```

  Ejemplo:

  ```py
  x = 20  # Variable de control

  while x < 35:
      print(x)
      x += 3  # Actualización de la variable de control
  ```

- **While True:** Se utiliza cuando se quiere realizar un número indeterminado de secuencias, donde no posee una variable de control, sino un condicional que al cumplirse corta el bucle por medio de un `break` o un `return` según la necesidad.

Ejemplo:

```py
while True:
    x = int(input("Ingrese un número par: "))

    if x % 2 == 0:
        print(f"El numero {x} es par")
        break
```

## Funciones

Las Funciones son un bloque de código reutilizable que realiza una sola tarea específica.

### Ventajas

- Reusable
- Conciso
- Legible
- Mantenible
- Comprobable

**Sintaxis**:

```py
def <function>():
    # bloque de código

# llamar a la función
<nombre_de_la_funcion>()
```

`Parámetros`: Es una **variable** que se **incluye en la definición de la función** para **representar** y **guardar** un valor que podemos pasar cuando **llamamos a la función**.<br>
`Argumentos` Es un **valor** que **asignamos** a un **parámetro** cuando llamamos a una **función**.<br>

- `Parámetros --> Definición de la función`
- `Argumentos --> Llamada a la función`

```py
def <function>(<parámetro>):
    # bloque de código

# llamar a la función
<nombre_de_la_funcion>(<argumento>)

# Ej:
def mostrar_doble(num):
    print(num * 2)
```

### Retornando valores de la función

**Propósito**: El propósito es devolver un valor al concluir las tareas de la función y esto lo hace con `return`. Cuando se ejecuta `return` la ejecución de la función se detiene inmediatamente y si hay código después de esta, no se ejecuta. Si no hubiera un `return` devuelve el valor `None`, cuando asignamos a una variable el resultado de una función.

```py
def <función>(<parámetros>):
    # bloque de código
    return <valor>

#Ej
def sumar(x, y):
    return x + y
> resultado = sumar(10, 3)
> print(resultado)
>>> 13
```

### Scope - Alcance de una variable

Es el alcance que tendrá una variable en el programa. Dónde se podrá usar. Determina a qué variables se tiene acceso en cada parte del programa.
**Scope - Alcance**:

- `Global` Son las variables definidas en el programa principal.
- `Local` Son las variables definidas en las funciones.

## Recursion

Es definir algo en términos de sí mismo.<br>
**Función Recursiva**: Es una función que se llama a sí misma.<br>
**Estructura de una función recursiva**:

- `Caso Base`: Permite que la función se detenga.
- `Caso Recursivo`: Es el que nos permite descomponer un problema en una versión mas pequeña de ese problema hasta llegar al caso base.

```py
def fibonacci(n):
    if n == 0 or n == 1: # Caso Base.
        return n
    else:
        return fibonacci(n - 1) + fibonnacci(n - 2) # Caso recursivo.
```

Esto retorna el número que se encuentra en la secuencia fibonacci que se le envía como argumento.

## Archivos

La sentencia `with` Nos permite abrir un archivo y luego cerrarlo automáticamente.
**Leer archivos:** sintaxis: `with open("<nombre_archivo.txt", "r">) as <variable>:` ej:

### Modos de Apertura de Archivos

- `r` (read - leer)
  ```py
  with open("frases_famosas.txt", "r") as archivo:
      for linea in archivo:
          print("=== Frase ===")
          print(linea)
  ```
- `w` (write - escribir) Reemplaza el contenido del archivo. Ojo al piojo!.

  ```py
  notas = {"Nora": 87,
       "Gino": 100,
       "Loretto": 67,
       "Talina": 38}

  with open("data_estudiantes.txt", 'w') as archivo:
      for nombre, nota in notas.items():
          archivo.write(nombre + " - " + str(nota) + "\n")
  ```

- `a` (append - añadir) Añade el contenido a continuación del contenido del archivo.

  ```py
  notas = {"Emily": 54,
       "Damiel": 98,
       "Julienne": 78}

  with open("data_estudiantes.txt", 'a') as archivo:
      for nombre, nota in notas.items():
          archivo.write(nombre + " - " + str(nota) + "\n")
  ```

- Agregar un `+` incluye leer. Por ejemplo, `w+` es leer y escribir.

## Importaciones

Al ir incrementándose la complejidad del programa, se deberán separar el mismo en distintos módulos y cuando vayamos
a trabajar con los mismos, tendremos un programa principal en el cual vamos a importar cada uno de esos módulos. De esta forma se puede trabajar como si los módulos estuvieran en el mismo archivo. Esto va a hacer que sea mas fácil de mantener y evita la repetición de código que puede ser reutilizado en otros programas.<br>
**Al importar módulos**: Estos se agrupan en el inicio del programa por orden de importancia y separándose los grupos por un linea en blanco. La importancia esta dada por el tipo de `import` primero los que importan módulos primitivos, luego los de funciones etc...

`Módulos`: Un módulo es un archivo de Python que contiene definiciones y sentencias relacionados.<br>
`Importación`: Es la **sentencia** que da acceso a las funciones y constantes definidas en el módulo importado.<br>
**Sintaxis**: `import <nombre_modulo>`<br>
**Invocar funciones del módulo importado**: `<módulo>.<función>(<argumentos>)`

```py
import math
print(math.pow(9, 2))

>>> 81.0
```

**Invocar una constante**: `<modulo>.<constante>`

```py
import math
print(math.pi)

>>> 3.141592653589793
```

**Importar un módulo con un nombre alternativo**: `import <módulo> as <nombre_alternativo>`

```py
import math as matematicas
print(matematicas.pi)
```

**Importar solo un elemento especifico de un módulo**: `from <módulo> import <elemento>`

```py
from math import pow
print(pow(9, 2))
```

### Errores y Excepciones

**Error en la sintaxis del programa**: Ocurre cuando no se siguen las reglas formales para escribir código en Python.<br>
**Excepciones**: Es un error detectado durante la ejecución de un programa.<br>

`try, except`: Se utiliza para capturar errores y ejecutar linea de código en consecuencia.

```
try:
    # Intenta ejecutar este código
except:
    # Si ocurre una excepción, detente inmediatamente y ejecuta este código.
```

Ejemplo:

```
num1 = int(input("Ingrese un número: "))
num2 = int(input("Ingrese otro número: "))

try:
    resultado = num1 / num2
    print(f"{num1} / {num2} = ", resultado)
except:
    print("Alerta Excepción")
```

**Excepciones solo por un tipo de error**: Podemos decirle al `except` que actue según un tipo de error.<br>
Sintaxis: `except <tipo_de_excepción>`

```
num1 = int(input("Ingrese un número: "))
num2 = int(input("Ingrese otro número: "))

try:
    resultado = num1 / num2
    print(f"{num1} / {num2} = ", resultado)
except: ZeroDivisionError:
    print("No se puede dividir por cero")
```

**Siempre es recomendable ser especifico en las excepciones** y pueden agregarse varias clausulas `except` debajo del `try` capturando distintas excepciones y actuando en consecuencia de la excepcion capturada.<br>
**Opción para capturar el mensaje de error**: `except <tipo_de_error> as <variable>`

```
except ZeroDivisionError as e:
    print("No se puede dividir por cero Error: ", e)

>>> No se puede dividir por cero Error: division by zero
```

Clausula `else:` Si no ocurrio una excepción en `try` se ejecuta el código en `else`.

```
try:
    # Intenta ejecutar este código
except:
    # Si ocurre una excepción, detente inmediatamente y ejecuta este código.
else:
    # si no ocurre una exceptción en try ejecuta este código.
```

Ejemplo:

```
num1 = int(input("Ingrese un número: "))
num2 = int(input("Ingrese otro número: "))

try:
    resultado = num1 / num2
    print(f"{num1} / {num2} = ", resultado)
except ZeroDivisionError as e:
    print("No se puede dividir por cero Error: ", e)
else:
    print("Todo salio bien!")
```

Clausula `finally:` Se ejecuta siempre se halla encontrado o no una excepción y se utiliza generalmente para las tareas que
deben hacerse siempre como por ejemplo, cerrar un archivo.

```
try:
    # Intenta ejecutar este código
except:
    # Si ocurre una excepción, detente inmediatamente y ejecuta este código.
else:
    # si no ocurre una exceptción en try ejecuta este código.
Finally:
    # Se ejecuta siempre halla ocurrido una excepción o no.
```

## Modulos Utiles para Importar

`random`

```
import random
numero_aleatorio = random.randint(desde_inclusive, hasta_inclusive) # randint(a, b) es random de enteros.
```

`random.choice()`: Permite elegir aleatoriamente una opcion que pasamos como lista.

```
opcion = random.choice(["piedra", "papel", "tijera"])
```

## Tips

`Dos renglones en blanco`: arriba y debajo de las **funciones** y cualquier otro elemento, y lo mismo para la **llamada a la función** es lo que dicta la normas de estilo en Python.

## Documentación

- [docs.python.or](https://docs.python.org/)

## Recursos

- [Paquetes (packages)](https://pypi.org/)

```

```
