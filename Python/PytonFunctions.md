# Python Funciones Utiles y palabras clave
## Range
La función `range()` retorna una secuencia de números, que comienzan de cero (por defecto), y se incrementan en uno (por defecto) y terminan un valor anterior al especificado. Sintaxis: `range(<inicio>,<final>,<paso>)`, tanto `inicio` como `paso` son opcionales.
```
x = range(6)
for n in x:
    print(n)

> 0
> 1
> 2
> 3
> 4
> 5

x = range(2,10,2)
for n in x:
    print(n)

> 2
> 4
> 6
> 8
```
## Enumerate
La función `enumerate()` retorna un **objeto** enumerable con la tupla `indice`, `elemento` de un `iterable`, este ultimo puede ser una lista, tupla, biblioteca, cadena de texto etc... **No modifica el iterable original**<br>
Sintaxis: `enumerate(<iterable>, start = 0)` **start**: indica el número con el cual inicia la indexación, es *opcional* y por defecto es cero. Si requiere de un inicio distinto, es buena costumbre colocar la palabra `start = <inicio>` ej: `enumerate(lista_de_compras, start = 1)`, de esta forma al indicar el start como argumento de palabra clave, evita errores si se cambiaran de lugar los argumentos en la llamada.
```
verduras = ["tomate", "espinaca", "zanahoria", "pepino"]
y = enumerate(verduras)

print(y)
>>> <enumerate object at 0x000001F01BE96D80>
```
Si convertimos el objeto enumerable en una *lista* podemos ver la tupla *indice*, *elemento*.
```
print(list(y))

[(0, 'tomate'), (1, 'espinaca'), (2, 'zanahoria'), (3, 'pepino')]
```
### Recorrer el `objeto enumerable`:
```
# Basado en el ejemplo anterior.
for index, item in y:
    print(f"Index: {index}: {item}")

# Resultado
Index: 0: tomate
Index: 1: espinaca
Index: 2: zanahoria
Index: 3: pepino
```
Si no es necesario guardarlo en una variable y economizando memoria podemos hacerlo directamente:
```
for index, item in enumerate(verduras):
    print(f"Index: {index}: {item}")

Index: 0: tomate
Index: 1: espinaca
Index: 2: zanahoria
Index: 3: pepino
```
Cambiando el indice de inicio del enumerable con `start`
```
for index, item in enumerate(verduras, start= 1):
    print(f"Index: {index}: {item}")

Index: 1: tomate
Index: 2: espinaca
Index: 3: zanahoria
Index: 4: pepino
```
**NOTA:** `enumerate()` devuelve los índices y elementos sucesivos solo cuando es necesario y no se calculan antes de tiempo. En Proyectos de Python donde se necesita tener en cuenta la eficiencia de la memoria, puede intentar usar el `enumerate()` cuando necesite recorrer grandes iterables.

## `.join()`
Retorna de un `iterable` un unico `string` sin modificar el iterable. Sintaxis: `<separador>.join(<iterable>)`.
```
verduras = ["tomate", "espinaca", "zanahoria", "pepino"]
texto = '#'.join(verduras)
print(texto)

#Resultado:
tomate#espinaca#zanahoria#pepino
```
## `all()`
La función `all()` retorna `True` si todos los items de un *iterable* son verdaderos, en otro caso retorna `False`.<br>
Si el *iterable* esta **vacío** `all()` retorna `True`.<br>
Sintaxis: `all(<iterable>)`, iterable: lista, tupla, biblioteca etc...<br>
### Ejemplos:
```
lista = [0, 1, 1]
x = all(lista)
> False  # Retorna False por que 0 se interpreta como falso y 1 como verdadero.
```
```
tupla = (0, True, False)
x = all(tupla)
> False  # Retorna False por que tanto el primer item y el tercero son falso.
```
```
myset = {0, 1, 0}
x = all(myset)
> False  # Retorna False por que tanto el primer item y el tercero son falso.
```
Ojo al piojo aca! función `all()` en las *bibliotecas* **evalua la llave no el valor.**
```
mydict = {0 : "Apple", 1 : "Orange"}
x = all(mydict)
> False  # Retorna falso por que la función all() en las bibliotecas evalua la llave no el valor.
```
```
lista = [2, 3, 5]
num = 3
if all(spot == num for spot in lista ):
    return True
else:
    return False
> False  # Por que solo el segundo elemento es verdadero.
```
## `continue`
La palabra clave (keyword) `continue` se utiliza para terminar la iteración actual en un bucle `for` (o `while`) y continua con la siguiente iteración.
```
nums = []
for num in range(10):
    if num == 3:
        continue
    nums.append(num)
print(nums)

> [0, 1, 2, 4, 5, 6, 7, 8, 9]
```
## `pass`
La declaración `pass` se utiliza cuando se requiere una instrucción sintácticamente pero no desea que se ejecute ningún comando o código.<br> Es muy común utilizarlo al armar una estructura donde mas adelante se le va a incluir el código correspondiente o en un método necesario que no vaya a hacer nada.
```
def necesito_que_este_pero_que_no_haga_nada():
    pass
```
```
for letter in 'Python': 
   if letter == 'h':
      pass
      print('This is pass block')
   print('Current Letter :', letter)

print("Good bye!")

Current Letter : P
Current Letter : y
Current Letter : t
This is pass block
Current Letter : h
Current Letter : o
Current Letter : n
Good bye!
```
