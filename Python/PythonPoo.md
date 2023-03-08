# Python POO Programación Orientada a Objetos
La programación Orientada a objetos se define como un paradigma de la programación, una manera de programar específica, donde se organiza el código en unidades denominadas clases, de las cuales se crean objetos que se relacionan entre sí para conseguir los objetivos de las aplicaciones.

Podemos entender la programación Orientada a objetos (POO) como una forma especial de programar, más cercana a como expresaríamos las cosas en la vida real que otros tipos de programación, que permite diseñar mejor las aplicaciones, llegando a mayores cotas de complejidad, sin que el código se vuelva inmanejable.

Al programar orientado a objetos tenemos que aprender a pensar cómo resolver los problemas de una manera distinta a como se realizaba anteriormente, en la programación estructurada. Ahora tendremos que escribir nuestros programas en términos de clases, objetos, propiedades, métodos y otras cosas que explicaremos a continuación.
## Clases
Las Clases son el mapa que define un objeto y nos permite representar los atributos y la funcionalidad (métodos) del mismo.<br>
Ejemplo de clase:
```
class CuentaBancaria:
    def __init__(self, num_cuenta, nombre_titular, balance):
        self.num_cuenta = num_cuenta
        self.nombre_titular = nombre_titular
        self.balance = balance

    def generar_balance(self):
        print(self.balance)

    def depositar(self, monto):
        if monto > 0:
            self.balance += monto
```
`__init__(self, <parametros>)` Es el inicializador (constructor) de los atributos de la clase donde se define el estado del objeto y los parametros para recibir los argumentos al instanciar la clase.
## Instanciar una clase
```
mi_cuenta = CuentaBancaria("1-27938-29837", "Gervacio Perez", 56000)
mi_cuenta.balance()
>>> 56000

mi_cuenta.depositar(100)
mi_cuenta.balance()
>>> 56100
```
## Definir los Tipos de Datos en los Parámetros del Constructor
Podemos definir el tipo de dato que va recibir el párametro del constructor al recibir argumentos, de esta manera:
```
Class Item:
    def __init__(self, name: str, price: float, quantity=0 ):
```
## Validar los Argumentos Recibidos
También es una buena costumbre, validar que los argumentos recibidos sean del tipo correcto antes de asignar los valores al objeto.<br>
Esto se hace con `assert` la condición a evaluar y el mensaje del error:
```
class Item:
    __init__(self, name: str, price: float, quantity=0)
        # Corremos la validación de los argumentos recibidos.
        assert price >= 0, f"Price {price} no es mayor o igual a cero!
        assert quiantity >= 0, f"Quantity {quantity} no es mayor o igual a cero!

        # Asignar los valores al objeto self
        self.name = name
        self.price = price
        self.quantity = quantity
```  
## Variables de Clase
Las variables de clase se colocan al inicio de la clase antes del constructor `__ini__`, estas variables son de uso local de la clase y aunque pueden ser invocadas por sus instanciás y modificadas para esta ultima. Pueden ser consultadas invocando a la clase.
```
class Item:
    pay_rate = 0.8  # Tasa de pago después del 20% de descuento.

    def apply_discount(self):
        self.price *= self.pay_rate

>>> print(Item.pay_rate)
>>> 0.8

>>> print(item1.apply_discount())
>>> 80

>>> item1.pay_rate = 0.7
>>> print(item1.apply_discount())
>>> 70
```
## Lista de Objetos Instanciados de la Clase
Es bueno tener un control de las instancias realizada a la clase, podemos hacer esto acumulandolos en una lista. Cada vez que se instancia la clase, el constructor ejecuta una tarea que definimos de la siguiente manera:
```
class Item:
    all = []  # Inicializamos una lista como variable de clase
    def __init__(self, <parametros>):
        # Validaciones de variables...
        # Asignacion de del objeto...

        # Acciones a ejecutar
        Item.all.append(self) # Acumula las instancias de la clace en la variable de clase all
```
Si intentaramos ver el contenido de la lista `all` esta nos mostraria un resultado poco amigable mostrandonos la dirección de memoria del objeto: `[<__main__.Item object at 0x0000022F806F6FD0>]`, para hacerlo mas amigable utilizamos el método magico o especial `__repr__`.<br>
El método `__repr__` es un método especial utilizado dentro de una clase que representa un objeto de una clase en forma de cadena y esta puede ser formateada para obtener los datos de una forma clara y legible ej:
```
class Item:
    all = []  # Inicializamos una lista como variable de clase
    def __init__(self, <parametros>):
        # Validaciones de variables...
        # Asignacion de del objeto...

        # Acciones a ejecutar
        Item.all.append(self) # Acumula las instancias en la variable de clase all

    def __repr__(self):
        return f"Item('{self.name}', {self.price}, {self.quantity})"
```
(Este método no esta dentro del método del constructor como puede apreciarse.)<br>
Esto mostrara los datos de esta manera al invocar **print(Item.all)**<br>
`>>> [Item('Phone', 80.0, 5), Item('Laptop', 700.0, 3), Item('Cable', 10, 5), Item('Mouse', 50, 5), Item('Keyboard', 75, 5)]`
## Métodos de la Clase
### Método de Instancia
Son métodos que reciben como parametro de entrada `self`, que hace referencia al objeto que llama al método, también pueden recibir parámetros de entrada. Como primer parametro puede recibir cualquier nombre, pero por convención se utiliza `self`.
```
def metodo_instancia(self, <parametros>):
    ... código ...

>>> objeto.metodo_instancia(<argumento>)
```
Ejemplo:
```
class Operacion:
    def suma(self, a, b):
        return f"La suma de {a} + {b} = {a + b}"

>>> objeto1 = Operacion()
>>> print(objeto1.suma(3, 7))
>>> La suma de 3 + 7 = 10
```
### Método de Clase
Los métodos de clase reciben como argumento `cls`, que hace referencia a la clase. Estos métodos pueden acceder a la clase pero no a la instancia. El primer parametro puede ser cualquier nombre pero por convención es `cls`<br>
Para crear un método de clase se utiliza el decorador `@classmethod`.
```
class Operacion:
    @classmethod
    def resta(cls, a, b):
        return f"La resta de {a} - {b} = {a - b}"

>>> print(Operacion.resta(4, 3))
>>> La resta de 4 - 3 = 1
```
Los métodos de clase son utilizados comunmente para la carga de datos, instancia masiva de objetos etc...

### Métodos Estaticos
Los métodos estaticos se definen con el decorador `@staticmethod` y no reciben argumento implícito como los métodos de instancia y de clase.<br>
Este método no puede acceder al contexto **dinámico** (es cuando se estan creando las instancias), es decir a los objetos. Este método solo se puede utilizar en el contexto **estático** (es cuando se esta definiendo la clase).
```
class Operacion:
    @staticmethod
    def multiplica(a, b):
        return f"La multipicación de {a} * {b} = {a - b}"

>>> print(Operacion.multiplica(4, 3))  # llamada a travez de una clase
>>> La multiplicaión de 4 * 3 = 12

op1 = Operacion()
>>> print(op1.multiplica(4, 3))  # llamada a travez de una instancia.
>>> La multiplicaión de 4 * 3 = 12

```
### Diferencias Entre Métodos de Clase y Estaticos
Métodos de Clase:
- Es un método que esta vinculado a la clase y no al objeto.
- Tiene acceso al estado de la clase.
- Puede modificar el estado de la clase y este se aplicara a todas las instancias de la clase
- Se utilizan para crear métodos de fabrica, estos métodos de fabrica devuelven un objeto de clase.

Métodos Estaticos:
- Es un método que esta vinculado a la clase y no al objeto.
- No puede acceder ni modificar el estado de la clase.
- Se utilizan para crear funciones de utilidad.
- Son métodos que toman argumentos y funcionan sobre esos argumentos, mientras que los métodos de clase deben tener la clase como parametro.<br>
**`Observaciones:`** Lo conveniente de los métodos de clase y estaticos, es que **se puede invocar al método sin necesidad de instanciar objetos**.<br> Los objetos instanciados pueden ejecutar los métodos de clase y estaticos, pero esto rara vez puede verse y generan confucíon, no siendo una buena practica. **Evitar hacerlo**.

## Herencia
La **herencia** es un proceso mediante el cual se puede crear una clase **hija** que hereda de una clase **padre**, compartiendo sus métodos y atributos. Además de ello, una clase hija puede sobreescribir los métodos y atributos, o incluso definir unos nuevos.<br>
Se puede crear una clase hija con tan solo pasar como `parámetro` la clase de la cual queremos heredar.
```
class Item:
    ...code...

class Phone(Item):
    pass  # Esta sentencia es para cuando no hay código y necesita declarar un método, clase, etc.
```
De hecho podemos ver como efectivamente la clase Phone es hija de la clase Item usando `__bases__`:
```
print(Phone.__bases__)
>>> (<class '__main__.Item'>,)
```
De manera similar podemos ver que clases descienden de una clase en concreto con `__subclasses__`:
```
print(Item.__subclasses__)
>>> [<class '__main__.Phone'>]
```
La herencia nos permite respetar el principio `DRY (Don't Repeat Yourself)` que es muy aplicado en el mundo de la programación y consiste en no repetir código de manera innecesaria. Cuanto más código duplicado exista, más difícil será de modificar y más fácil será crear inconsistencias.
### Super
La función `super()` se utiliza cuando se quiere modificar un método heredado del padre tomando las propiedades de este y agregando las modificaciones particulares para el hijo. Ejemplo: clase padre `Item` clase hija `Phone`.
```
class Item:
    pay_rate = 0.8  # the pay rate after 20% discount. (variable de clase)
    all = []
    def __init__(self, name: str, price: float, quantity=0):
        # Run validations to the received arguments
        assert price >= 0, f"Price {price} is not greater or equal than zero!"
        assert quantity >= 0, f"Quantity {quantity} is not greater or equal than zero!"

        # Assign to self object
        self.name = name
        self.price = price
        self.quantity = quantity

        # Action to execute
        Item.all.append(self)  # Acumular los items instanciados de la clase.

    # Estos son metodos de instancia, funcionan cuando se instancia un objeto.
    def calculate_total_price(self):
        return self.price * self.quantity

    def apply_discount(self):
        self.price = self.price * self.pay_rate

    @classmethod  # Método de clase, estos funcionan sin necesidad de instanciar objetos.
    def instantiate_from_csv(cls):
        with open('items.csv', 'r') as f:
            reader = csv.DictReader(f)
            items = list(reader)

        for item in items:
            Item(
                name=item.get('name'),
                price=float(item.get('price')),  # Se pasan los argumentos a instanciar, Ojo de convertir los argumentos
                quantity=int(item.get('quantity'))  # en el tipo de dato correspondiente. No olvidar que csv es texto.
            )

    @staticmethod  # Los métodos estaticos funcionan como funciones comunes y no reciben el objeto por lo cual
    def is_integer(num):  # no reciben el self como primer argumento a diferencia del los otros métodos.
        # We will count out the floats that are point zero
        # For i.e: 5.0, 10.0 ( 7.5 no lo seria y retorna False.)
        if isinstance(num, float):
            # Count out the floats that are point zero.
            return num.is_integer()
        elif isinstance(num, int):
            return True
        else:
            return False

    def __repr__(self):  # Muestra el contenido de all en formato amigable.
        return f"{self.__class__.__name__}('{self.name}', {self.price}, {self.quantity})"
```
En la clase hija `Phone` agregamos un parámetro `broken_phones` propio para esta clase, esta sería la manera adecuada, con las normas de buenas costumbres de la utilización de `super()`.
```
from item import Item


class Phone(Item):

    def __init__(self, name: str, price: float, quantity=0, broken_phones=0):
        # Call to super function to have access to all attributes / methods
        super().__init__(
            name, price, quantity
        )

        # Run validations to the received arguments
        assert broken_phones >= 0, f"Broken Phones {broken_phones} is not greater or equal to zero!"

        # Assign to self objet
        self.broken_phones = broken_phones
```

## Encapsulamiento
El encapsulamiento o encapsulación en programación es un concepto relacionado con la programación orientada a objetos, y hace referencia al ocultamiento de los estados internos de una clase al exterior. Dicho de otra manera, encapsular consiste en hacer que los atributos o métodos internos a una clase no se puedan acceder ni modificar desde fuera, sino que tan solo el propio objeto pueda acceder a ellos.

Para la gente que conozca Java, le resultará un termino muy familiar, pero en Python es algo distinto. Digamos que Python por defecto no oculta los atributos y métodos de una clase al exterior. Sin embargo esto es algo que tal vez no queramos. Hay ciertos métodos o atributos que queremos que pertenezcan sólo a la clase o al objeto, y que sólo puedan ser accedidos por los mismos. Para ello podemos usar la doble `__` para nombrar a un atributo o método. Esto hará que Python los interprete como **“privados”**, de manera que no podrán ser accedidos desde el exterior.
```
class Item:
    def __init__(self, name: str)
        # Assign to self object
        self.__name = name
```
### Miembros Publicos, Protegidos y Privados
`Publicos:`  Los miembros públicos (generalmente métodos declarados en una clase) son accesibles desde fuera de la clase. El objeto de la misma clase es necesario para invocar un método público. Esta disposición de variables de instancia privadas y métodos públicos garantiza el principio de encapsulación de datos.<br>
Todos los miembros de una clase Python son públicos de forma predeterminada. Se puede acceder a cualquier miembro desde fuera del entorno de clase.<br>
`Protegidos:` Los miembros protegidos de una clase son accesibles desde dentro de la clase y también están disponibles para sus subclases. No se permite el acceso a ningún otro entorno. Esto permite que recursos específicos de la clase padre sean heredados por la clase hija.<br>
La convención de Python para proteger una variable de instancia es agregarle un prefijo `_` (subrayado único). Esto evita efectivamente que se acceda a él a menos que sea desde una subclase. De hecho, esto no impide que las variables de instancia accedan o modifiquen la instancia. Para evitar esto se usa el decorador `@property` que se ve mas adelante en la sección Getters y Setters.
```
self._name = name
```
`Privados:` Python no tiene ningún mecanismo que restrinja efectivamente el acceso a ninguna variable de instancia o método. Python prescribe una convención de prefijar el nombre de la variable / método con un guion bajo simple o doble para emular el comportamiento de los especificadores de acceso protegido y privado.<br>
El doble guion bajo `__` prefijado a una variable la convierte en privada. Da una fuerte sugerencia de no tocarlo desde fuera de la clase. Cualquier intento de hacerlo resultará en un AttributeError.
```
self.__name = name
```
`Observaciones:` Por lo que puedo ver, los métodos y atributos son siempre publicos y los guiones son por convención una advertencia para que no se acceda a ellos desde fuera de la clase.
### Setters y Getters
Los “Getters” y “Setters” se utilizan en POO para garantizar el principio de la encapsulación de datos.<br>
Claramente el getter se emplea para obtener los datos y el setter para cambiar el valor de los datos. Son decoradores y se identifican por tener un @ (como lo veremos en el ejemplo)<br>
Por lo general, estos se usan en Python:
- Si queremos añadir una lógica de validación para obtener y establecer un valor.
- Para evitar el acceso directo a un atributo de clase (un usuario externo no puede acceder directamente a las variables privadas ni modificarlas).

*Getters*: Para definir un getter se utiliza el decorador `@property`
```
@property
    # Property Decorator = Read-Only Attribute // getter
    def name(self):
        return self.__name
```
*Setters*: Para definir un setter se utiliza el decorador `@<atrributo>.setter`
```
@name.setter
# Setter
def name(self, value):
    if len(value) > 10:
        raise Exception("The name is too long!")
    else:
        self.__name = value
```
## Polimorfismo
El concepto de polimorfismo (del griego muchas formas) implica que si en una porción de código se invoca un determinado método de un objeto, podrán obtenerse distintos resultados según la clase del objeto. Esto se debe a que distintos objetos pueden tener un método con un mismo nombre, pero que realice distintas operaciones.
```
class Animal:
    def hablar(self):
        pass

class Perro(Animal):
    def hablar(self):
        print("Guau guau!")

class Gato(Animal):
    def hablar(self):
        print("Miauuuuu!")

class Golondrina(Animal):
    def hablar(self):
        print("Priiipipi pi pi!)
```
A continuación creamos un objeto de cada clase y llamamos al método `hablar()`. Podemos observar que cada animal se comporta de manera distinta al usar `hablar()`.
```
for animal in Perro(), Gato(), Golondrina():
    animal.hablar()

>>> Guau guau!
>>> Miauuuuu!
>>> Priiipipi pi pi!
```


## Notas:
`Refactor`: En el editor PyCharm click derecho y seleccionar `Refactor` sobre la variable o méthodo y lo cambia en todo el código donde se encuentre.
