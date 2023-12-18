# Harvard CS50’s Introduction to Programming with Python – Full University Course

## Definir main()

En Python las funciones deben definirse en el inicio del código u antes de ser invocadas, para resolver este inconveniente, se define
la función **\*main()** y se desarrolla el código dentro de esta, luego se definen las funciones que se deseen y se invoca **_main()_**
al final del programa.

```py
def main():
    hello()
    name = input("What's your name? ")
    hello(name)

def hello(to="world"):
    print(f"hello, {to}")

main()
```

## La sentencia match

Una sentencia match recibe una expresión y compara su valor con patrones sucesivos dados en uno o más bloques case. Esto es similar a grandes rasgos con una sentencia switch en C, Java o JavaScript (y muchos otros lenguajes) pero es más similar a la comparación de patrones en lenguajes como Rust o Haskell. Sólo se ejecuta el primer patrón que coincide y también es capaz de extraer componentes (elementos de una secuencia o atributos de un objeto) de un valor y ponerlos en variables.

La forma más simple compara un valor expuesto con uno o más literales:

```py
def http_error(status):
    match status:
        case 400:
            return "Bad request"
        case 404:
            return "Not found"
        case 418:
            return "I'm a teapot"
        case _:
            return "Something's wrong with the internet"
```

Observa el último bloque: el «nombre de variable» \_ funciona como un comodín y nunca fracasa la coincidencia. Si ninguno de los casos case coincide, ninguna de las ramas es ejecutada.

Se pueden combinar varios literales en un solo patrón usando | (or):

```py
case 401 | 403 | 404:
    return "Not allowed"
```

[Documentación completa](https://docs.python.org/es/dev/tutorial/controlflow.html)

## Acumuladores

En Python la sentencia corta para un acumulador es `+=` o `-=` no existe como en otro lenguajes el `i++` o `i--`

## Paradigmas de uso común

### while True:

Este paradigma es de uso común para hacer un bucle infinito hasta que se cumpla una condición determinada.

```py
while True:
    n = int(input("What's n? "))
    if n > 0:
        break

for i in range(n):
    print("meow")
```

## PIP (packages in Python)

PIP is a package manager for Python packages, or modules if you like.<br>
Note: If you have Python version 3.4 or later, PIP is included by default.<br>
Pip es el instalador de paquetes de python y se utiliza de la siguiente manera:

```
$ pip install [paquete a instalar]
```

- [pip.org/project/pip](https://pypi.org/project/pip/)
- [Documentación](https://pip.pypa.io/en/stable/)

## APIs

Ejemplo de como consumir una API REST en Python utilizando librerías y la API de iTunes:

```py
import json
import requests
import sys

if len(sys.argv) != 2:
    sys.exit()
'''
entity= el tipo de entidad que buscamos: song, musicVideo, etc...
limit= cantidad limite en los resultados de la búsqueda.
term= texto para la búsqueda
'''

response = requests.get("https://itunes.apple.com/search?entity=song&limit=25&term=" + sys.argv[1])
#print(json.dumps(response.json(), indent=2))   # Parseo de json con la librería 'json'

o = response.json()

for result in o["results"]:
    print(result["trackName"])
```

- [pypi.org/project.requests](https://pypi.org/project/requests/)
- [docs.python.org/3/library/json](https://docs.python.org/3/library/json.html)

## Unit test

Unit test es la prueba de funcionamiento de una unidad (una función dentro de un programa) y esta debe retornar un valor para poder comprobar el test.

```py
# Esta función no retorna un valor por lo cual el test no se puede realizar.
def not_tested():
    print("hello, test")

# Esta función retorna un valor por lo cual se puede efectuar el test.
def test_true():
    return 2 + 3

```

### Ejemplo de un Unit Test

Instalar **pytest:** `$ pip install pytest `, este paquete nos va a facilitar la vida a la hora de hacer un Unit Test.

Programa al que le vamos a correr el test:

```py
# calculator.py
def main():
    x = int(input("What's x? "))
    print("x squared is", square(x) )

def square(n):
    return n * n

if __name__ == "__main__":
    main()
```

Programa para el test:

```py
# test_calculator.py
from calculator import square

def test_square_positive():
    assert square(2) == 4
    assert square(3) == 9

def test_square_negative():
    assert square(-2) == 4
    assert square(-3) == 9

def test_square_zero():
    assert square(0) == 0
```

Correr el test:

```
pytest test_calculator.py
```

Este es un ejemplo simple, puede observarse en `test_calculator()` la separación en funciones para encontrar con facilidad el error si este se produce.

### Multiple tests con pytest

Si creamos una carpeta `test` (para este ejemplo y por convención) y dentro creamos un archivo sin contenido llamado `__init__.py` Python tratara esta carpeta como un paquete (packages) de forma que tomará el conjunto de estos y no solo un modulo o un archivo solo.

```
$ pytest test
```

El comando anterior realizara todos los tests posibles que se encuentren dentro de la carpeta test.

Palabras clave de esta sección: `assert` `AssertionError` `pytest`

[pytest documentation](https://docs.pytest.org)

## Files I/O

## Resources

- [youtube](https://www.youtube.com/watch?v=nLRL_NcnK-4)
- [Documentation](https://docs.python.org/)

### Ultimo visto: minuto 7:00:29 / 15:57:47
