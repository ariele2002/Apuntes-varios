# Python Algoritmos Utiles

## Temas importantes para ver

- Generator Comprehension (python avanzado): Ahorra RAM y CPU ej:
  ```py
  list_comprehension = [x**2 for x in range(10000)]
  generator_comprehension = (x**2 for x in range(10000))
  ```

## Strings

### Dar vuelta un string

Para dar vuelta un string solo hay que recorrer la cadena y en una variable asignarle el carácter iterado concatenado la variable.

```py
texto = "garlopa"
texto_invertido = ""

for char in texto:
    texto_invertido = char + texto_invertido

print(texto, texto_invertido)

>>> garlopa apolrag
```

### Dar vuelta un string usando slice

Las cadenas de texto son una tupla, no pueden modificarse pero pueden iterarse.

```py
# Usando slice recorremos el string de forma invertida string[<inicio>:<fin>:<paso>]
texto = "garlopa"
print(texto, texto[::-1])

>>> garlopa apolrag
```

## Números

### Números pares simple con bucle

Genera números pares hasta el 100. Aprovecha los parámetros del range, comienza en `2`, el rango es `101` (rango + 1 por que comienza en 0) y salta de a `2`.

```py
for i in range(2, 101, 2):
    print(i)
```

### Sumar dígitos de un número

Para sumar los dígitos de un número dado (que no es lo mismo que sumar hasta ese número eh!?) por ej: 32 es 3 + 2 = 5

```py
sum_digits(123)

def sum_digits(numero):
    suma = 0
    while numero > 0:
        suma += numero % 10 # Resto de la división (3, 2, 1) secuencia (12,3 - 1,2 - 0,1)
        numero //= 10 # división entera o sea sin los decimales (12, 1, 0) secuencia (12,3 - 1,2 - 0,1)

    return suma
```

### Números primos

Los números primos son los números enteros mayores a 1 y que solo pueden dividirse por 1 o por ellos mismos en una división entera `(if num % n == 0)`

```py
def is_prime(num):
    if num <= 1:
        return False

    for n in range(2, int((num**0.5) +1)):
        if num % n == 0:
            return False

    return True

def l_p_numbers(num):
    return [n for n in range(2, num +1) if is_prime(n)]

num = int(input("Enter a number: "))
print(l_p_numbers(num))
```

utilizo `int(num**0.5)` como límite superior en el bucle for dentro de la función `is_prime(num)`. **Esto se debe a una propiedad de los números primos que nos permite optimizar el algoritmo de comprobación de primos**.

**La propiedad es la siguiente**: si un número `n` no es primo, al menos uno de sus factores primos será **menor o igual que la raíz cuadrada de** `n`.

Entonces, en lugar de verificar todos los números hasta `n` para determinar si es primo, podemos verificar solo los números hasta la raíz cuadrada de `n`. **Si no encontramos ningún factor primo en ese rango, entonces `n` es primo**.

Por ejemplo, si queremos comprobar si `17` es primo, solo necesitamos comprobar los números desde `2` hasta la raíz cuadrada de `17`, es decir, hasta `4.25`, redondeado hacia arriba, sería `5`. Si no encontramos ningún divisor en este rango, concluimos que `17` es primo.

### Rotación de items de una Lista

```py
# Rotación de elementos: Escribe una función que tome una lista y un número entero como entrada, y devuelva una nueva lista con los elementos rotados hacia la derecha el número de veces especificado.

def r_elements(items, n):
    n = n % len(items) #  para manejar rotaciones mayores que la longitud de la lista
    return items[-n:] + items[:-n]

items = [1, 2, 3, 4, 5]
n = 4

print(r_elements(items, n))
```

## Loops

- Recordar cortar los loops con `break` cuando hayan cumplido su función en una búsqueda y no dejar que siga iterando.

## Listas (arrays), tupla, conjuntos etc

### Elementos en común entre dos listas en una nueva lista

Se crea una nueva lista con el constructor `list()` y se le asigna el resultado de la **intersección** del los dos **conjuntos** de las listas anteriores
para<br> eliminar duplicados con el constructor `set()` y poder usar la intersección `&` ya que la lista no es un hasheable y no puede usarse como **conjuntos** <br>
con las mismas. Ej: `list(set(A) & set(B))`

```py
A = ["pera", 58, "uva", True, 3, 5, 3, False, False]
B = ["banana", "uva", 3, "melon", True, True]

C = list(set(A) & set(B))
print(C)
>>> ["uva", 3, True]
```

### Eliminar elementos duplicados sin cambiar el orden

`dict.fromkeys(<lista>,<item>)` crea un diccionario en el cual las **llaves** son los **items** de la lista y como toda key no puede haber duplicados, luego se crea una **lista** con este diccionario sin alterar el orden de los elementos, si lo hiciéramos con un `set()` este alteraría el orden original de los elementos.

```py
items = ['banana', 'manzana', 'banana', 'pera', 'banana', 'pera', 'uva']
no_duplicates = list(dict.fromkeys(items)) # list({'banana': None, 'manzana': None, 'pera': None, 'uva': None})
print(no_duplicates)

['banana', 'manzana', 'pera', 'uva']
```

El constructor `dict(<key>=<argument>)` Ej:

```py
x = dict(name = "John", age = 36, country = "Norway")
```

### Eliminar elementos duplicados contiguos:

En este caso verificamos si la **nueva lista** esta vacía, agregamos el elemento o si el elemento guardado anteriormente es distinto al siguiente.
`if not new_items or item != new_items[-1]` de esta forma evitamos un error **'IndexError: list index out of range'** de nuestra nueva lista.

```py
def remove_contiguous(items):
    new_items = []
    for item in items:
        if not new_items or item != new_items[-1]:
            new_items.append(item)
    return new_items

items = ['manzana', 'banana', 'banana', 'pera', 'uva', 'banana', 'uva', 'uva', 'manzana']
print(remove_contiguous(items))

>>> ['manzana', 'banana', 'pera', 'uva', 'banana', 'uva', 'manzana']
```

### Sumar elementos por grupos

Tenemos una lista y un numero que indica el rango de elementos a sumar para devolver una nueva lista con la suma de cada grupo. Utilizamos comprensión de listas, sumamos los elementos utilizando slice de la lista con `i` como indice e `i + n` como limite de un rango que comienza en `0`, el rango es `len(nums)` y el paso es `n`.

```py
def add_by_groups(nums, n):
    return [sum(nums[i: i+n]) for i in range(0, len(nums), n)]

nums = [1, 2, 3, 4, 5, 6, 7]
n = 2
print(add_by_groups(nums, n))

>>> [3, 7, 11, 7]
```

### Intercalar dos listas

Para intercalar dos listas por comprensión vamos a utilizar el método `zip(<lista1>, <lista2>,...)` retorna un objeto iterable, este tiene las tuplas con uno de cada elemento intercalado.
Por lo cual para retornar una lista con los elementos intercalados de dos listas, primero utilizamos `zip()` y luego iteramos ese par.

```py
def interleave(l1, l2):
    return [elem for pair in zip(l1, l2) for elem in pair]

l1 = [1, 2, 3]
l2 = ['pera', 'banana', 'manzana']
print(interleave(l1, l2))

>>> [1, 'pera', 2, 'banana', 3, 'manzana']
```

Ahora bien `zip()` se detiene en el ultimo elemento de la lista mas corta dejando afuera los elementos de la lista mas larga.<br>
Si queremos que incluya todos los elementos, agregamos haciendo **slice** según que cadena sea mas larga en la siguiente función aprovechando la función anterior:

```py
def interleave_all(l1, l2):
    len_l1 = len(l1)
    len_l2 = len(l2)

    if len_l1 > len_l2:
        return interleave(l1, l2) + l1[len_l2:]
    else:
        return interleave(l1, l2) + l2[len_l1:]

items1 = [1, 2, 3, 4, 5, 6, 7]
items2 = ['pera', 'banana', 'manzana', 'uva']
print(interleave_all(l1, l2))

>>> [1, 'pera', 2, 'banana', 3, 'manzana', 4, 'uva', 5, 6, 7]
```

### Lista mas larga en una lista de listas

Simplemente se utiliza `max(<lista>, key=len)` para que tome por tamaño y no por el valor mas alto.

```py
def longest_list(items):
    return max(items, key=len)
```
