# JavaScript POO Apuntes

## Objetos
### Objeto Literal (sintaxis)
Los objetos en javaScript son una lista de pares `llave` y `valor` (key: value).
```
const user = {
    name: "Pepe",
    lastname: "Petrela",
    age: 30,
    address: {
        street: "Some street",
        city: "Some City"
    },
    hobbies: ['bushcraft', 'cooking', 'programming']
}
```
### Propiedades - Object Properties
La teoria de POO nos dice que cada objeto tiene sus propiedades, pongamos el ejemplo de un auto, tiene una marca, un modelo, un color, un año de fabricación y su velocidad máxima, estas son sus propiedades al nivel teorico. En la practica representamos estas propiedades que definen el objeto con sus respectivas `llave` y `valor`:
```
const auto = {
  marca: "Ford",
  modelo: "Falcon GT",
  color: "Rojo",
  fabricacion: 1972,
  velocidadKms: 190,
}
```
### Métodos - Methods
Los métodos son las acciones que puede hacer ese objeto y a nivel de programación estarian representadas por las funciones.
```
const auto = {
  marca: "Ford",
  modelo: "Falcon GT",
  color: "Rojo",
  fabricacion: 1972,
  velocidadKms: 190,
  encender() {
    return 'brrmmm brrrmmm trt trt trt...';
  },
  apagar() {
    return 'motor apagado...';
  }
}

console.log(auto.encender());
console.log(auto.apagar());

> brrmmm brrrmmm trt trt trt...
> motor apagado...
```
### This
La palabra clave `this` dentro del contexto de un `objeto`, pasa a tener como valor el propio objeto. De esta forma pueden obtenerse los atributos y métodos del mismo objeto. Ejemplo mostrando el contenido de `this`:
```
const auto = {
  marca: "Ford",
  modelo: "Falcon GT",
  color: "Rojo",
  fabricacion: 1972,
  velocidadKms: 190,
  encender() {
    return 'brrmmm brrrmmm trt trt trt...';
  },
  apagar() {
    return 'motor apagado...';
  },
  mostrarContenidoThis() {
    console.log(this);
  }
}

console.log(auto.encender());
auto.mostrarContenidoThis();

> brrmmm brrrmmm trt trt trt...
> {
  marca: 'Ford',
  modelo: 'Falcon GT',
  color: 'Rojo',
  fabricacion: 1972,
  velocidadKms: 190,
  encender: [Function: encender],
  apagar: [Function: apagar],
  mostrarContenidoThis: [Function: mostrarContenidoThis]
}
```
En el siguiente ejemplo, modificamos el método `mostrarContenidoThis()` del objeto `auto` para hacer más claro el consepto de `this` en el contexto de un objeto.
```
  mostrarContenidoThis() {
    console.log(this.marca);
    console.log(this.modelo);
    console.log(this.encender());
  }

console.log(auto.encender());
auto.mostrarContenidoThis();

> brrmmm brrrmmm trt trt trt...

> Ford
  Falcon GT
  brrmmm brrrmmm trt trt trt...
```
### Constructor de Objetos
Los constructores en javaScript, no son mas que funciones que nos permiten crear objetos con propidades y métodos. El nombre del constructor debe comenzar en mayúsculas. En otros lenguajes esto sería la clase. En los constructores a los métodos deben asignarsele una `function () {}` no es como en los objetos.
```
function Person() {
  this.name = ""
  this.lastname = ""
  this.age = 0
  this.showFullName = function () {
    return `${this.name} ${this.lastname}`
  }
}

user  = new Person();
user1 = new Person();
user2 = new Person();

console.log(user);

Person {
  name: '',
  lastname: '',
  age: 0,
  showFullName: [Function (anonymous)]
}
```
Como puede verse en la salida por consola, muestra un objeto `Persona` quiere decir que fue construido por este ultimo.

### `Object()`
El constructor `Object()` crea un objeto de forma literal y no retorna valores. Es lo mismo hacer:
```
persona = new Object()
```
que:
```
persona = {}
```
por lo que no es practico en la codificación, pero tiene métodos que nos pueden ser útiles como `.keys()` que nos retorna una array con las llaves de un objeto y `.values()` que nos retorna un array con los valores de sus atributos y métodos.
```
console.log(Object.keys(user));

> [ 'name', 'lastname', 'age', 'showFullName' ]
```
```
console.log(Object.values(user));

> [ '', '', 0, [Function (anonymous)] ]
```
### New
La palabra clave `new` es fundamental en la creación de un objeto por medio de un constructor, si se omitiera el new y se asignara directamente el constuctor, las propiedades serian asignadas al objeto global inmediatamente superior en el contexto, perdiendo el control de a donde fueron asignados los atributos del constructor. Para evitar esto ECMAScript version 5 ofrece la declaración `"use strict"` que hace que JavaScript corra en modo estricto (`strict mode`), haciendo que los atributos y métodos del constructor sean `undefined` cuando no se usa `new` produciendo un error.
```
function Person() {
  'use strict' // corre en modo estricto
  this.name = "";
  this.lastname = "";
  this.age = 0;
  this.showFullName = function() {
    return `${this.name} ${this.lastname}`;
  }
}

person1 = new Person();
console.log(person1);
// salida por consola:
Person {
  name: '',
  lastname: '',
  age: 0,
  showFullName: [Function (anonymous)]
}

person2 = Person(); // nunca se deberia hacer la asignación sin new.
console.log(person2);
// salida por consola:
TypeError: Cannot set properties of undefined (setting 'name')
```
### Prototype
Al instanciar un objeto de un constructor, este queda ligado por referencia a su constructor y toda modificación posterior a la instanciación del objeto en el constructor, se ve reflejado en sus instancias. Para modificar las propiedades del constructor se utiliza el método `.prototype`.
JavaScript es muy dinamico a la hora de modificar las propiedades de un objeto, ejemplo:
```
function Person(name, lastname) {
  'use strict'
  this.name = name;
  this.lastname = lastname;
  this.showFullName = function() {
    return `${this.name} ${this.lastname}`;
  }
}

pepe = new Person('Pepe', 'Petrela');
pepe.age = 20;
pepe.greet = function() {
  return `Hello! Im ${this.showFullName()}`;
}
console.log(pepe);

andres = new Person('Andres', 'Garsolo');
console.log(andres);

// salida por consola
Person {
  name: 'Pepe',
  lastname: 'Petrela',
  showFullName: [Function (anonymous)],
  age: 20,
  greet: [Function (anonymous)]
}
Person {
  name: 'Andres',
  lastname: 'Garsolo',
  showFullName: [Function (anonymous)]
}
```
Como puede verse en el ejemplo, hemos agregado atributos y métodos al objeto `pepe` que es una instancia de Persona, sin embargo el objeto `andres` solo tiene las propiedades del constructor.<br>
Si quisieramos que todos los objetos instanciados de Persona tuvieran las nuevas propiedades de `pepe`, Una forma seria agregarlas al constructor y la otra seria *agregarlas dinamicamente* con el método `prototipe`, ejemplo:
```
function Person(name, lastname) {
  'use strict'
  this.name = name;
  this.lastname = lastname;
  this.showFullName = function() {
    return `${this.name} ${this.lastname}`;
  }
}

pepe = new Person('Pepe', 'Petrela');
andres = new Person('Andres', 'Garsolo');

Person.prototype.age = 20;
Person.prototype.greet = function() {
  return `Hello! Im ${this.showFullName()}`;
}

console.log(pepe);
console.log(pepe.age);
console.log(andres);
console.log(andres.greet());

// salida por consola
Person {
  name: 'Pepe',
  lastname: 'Petrela',
  showFullName: [Function (anonymous)]
}
20

Person {
  name: 'Andres',
  lastname: 'Garsolo',
  showFullName: [Function (anonymous)]
}
Hello! Im Andres Garsolo
```
Al estar el objeto instanciado relacionado por referencia a su constructor, cuando modificamos a este, las nuevas propiedades estan disponibles en las instancias del constructor independientemente de cuando se hayan instanciado. Como puede verse en el ejemplo, las nuevas propiedades no se pueden ver en el objeto.
#### Cual es la utilidad de prototype?
Al ver los ejemplos, pensamos, es mas prolijo definir los atributos y métodos en el constructor desde un principio. Pero la verdadera utilidad de `prototype` es poder modificar constructores que ya vienen definidos en JavaScript o productos de terceros y adecuarlos a nuestras necesidades. Ejemplo:
```
const texto = new String("Hello");

String.prototype.greet = function (name) {
  return `${this} ${name}!`;
}

console.log(texto.greet("Andres"));

console.log("Buenas tardes".greet("Pedro"));

> Hello Andres!
> Buenas tardes Pedro!
```
## Clases (Class)
Desde ECMAScript version 6 se implementaron las `clases` que en realidad son azucar sintactico, facilita la sintaxis en la creación de objetos, tiene una sintaxis mas familiar para los que vienen de lenguajes OOP y tienen algunas ventajas y diferencias:
- `use strict` incorporado
- `.prototype` incorporado
- Las clases deben ser declaradas antes de su uso, no entran en el `Hoisting` a diferencia de funciones y variables que pueden declararse antes o despues de ser usadas.

Las clases en JavaScript son un conjunto de métodos que definen la estructura de un objeto (tambien un plano del objeto).
```
class Person {
  constructor(name, lastname) {
    this.name = name;
    this.lastname = lastname;
  }

  greet() {
    return `Hello ${this.name} ${this.lastname}`;
  }
  
}

const pepe = new Person("Pepe", "Petrela");
const andres = new Person("Andres", "Argelta");

console.log(pepe);
console.log(pepe.greet());
console.log(andres);
console.log(andres.greet());

Person { name: 'Pepe', lastname: 'Petrela' }
Hello Pepe Petrela
Person { name: 'Andres', lastname: 'Argelta' }
Hello Andres Argelta
```
### Clase Anonima
Las clases tambien pueden ser declaradas `anonimas` y asignandolas a una constante o variable.
```
const Person = class {
  constructor(name, lastname) {
    this.name = name;
    this.lastname = lastname;
  }

  greet() {
    return `Hello ${this.name} ${this.lastname}`;
  }
  
}
```
La clase en JavaScript es una función si vemos su tipo nos retorna `function`.
```
class Person {
  constructor(name, lastname) {
    this.name = name;
    this.lastname = lastname;
  }

  greet() {
    return `Hello ${this.name} ${this.lastname}`;
  }
  
}

console.log(typeof(Person));

> function
```
### El Constructor Retorna las Propiedades del Objeto
Como dice el titulo es el constructor el que retorna las propiedades del objeto. Si en el constructor colocamos un return con un objeto, estaria sobreescribiendo los valores del objeto. Ejemplo:
```
class Person {
  constructor(name, lastname) {
    this.name = name;
    this.lastname = lastname;

    return {x: "nuevo valor del objeto"};
  }

  greet() {
    return `Hello ${this.name} ${this.lastname}`;
  }
  
}

const pepe = new Person("Pepe", "Petrela");
console.log(pepe);

> { x: 'nuevo valor del objeto' }
```
### Prototipo de la clase
Al comprobar el prototipo nos trae el nombre de la clase.
```
console.log(Person.prototype);
> Person {}
```
## Principios de la OOP
- La OOP promueve la modularidad y reusabilidad del código.
- No hay especificaciones o documentación técnica para OOP, solo hay
una serie de principios basados en la experiencia, pepers y la investigación temprana. No hay un documento oficial que lo especifique.
- Hay un minimo de dos definiciones para establecer que un lenguaje es OOP.
    - Es la capacidad de modelar problemas basado en objetos.
        - Asociación: Objetos con la capacidad de referirse a otros objetos.
        - Agregación: Objetos con la capacidad de referir a otros objetos independientes.
        - Composición: Objetos con capacidad de referir a uno o mas objetos dependientes.
    - Soporte de algunos principios que garanticen la modularidad y la reusabilidad de código.
        - Encapsulación: Es la capacidad de concentrar código en una sola entidad, ocultando sus detalles internos.
        - Herencia: Es el mecanismo por el cual un objeto puede adquirir algunas o todas las caracteristicas de uno o mas objetos.
        - Polimorfismo: Es la capacidad de procesar objetos con distintos tipos de datos o distintas estructuras, pero al final pueden devolvernos una respuesta.

Si un lenguaje de programación cumple con todos estos requerimientos, puede clasificarse como un lenguaje de programación orientado a objetos.
## Es JavaScript un Lenguaje OOP?
JavaScript cumple con los requerimientos para la OOP, pero no obliga a utilizarlo, en los siguientes puntos veremos como javascript cumple con estos principios y caracteristicas para que pueda ser considerado un lenguaje OOP.
### Asociación
Para asociar dos o mas objetos, se utiliza la palabra clave `.parent` que establece una asociación entre objetos. Si esta relación se elimina los objetos siguen funcionando sin problemas, ya que funcionan de manera individual y la asociación no afecta su funcionamiento.
```
class Person {
  constructor(name, lastname) {
    this.name = name;
    this.lastname = lastname;
  }
  
}

pepe = new Person("Pepe", "Petrela");
andres = new Person("Andres", "Perez");

andres.parent = pepe;

console.log(andres);
console.log(pepe);
>
Person {
  name: 'Andres',
  lastname: 'Perez',
  parent: Person { name: 'Pepe', lastname: 'Petrela' }
}
Person { name: 'Pepe', lastname: 'Petrela' }
```
### Agregación (Aggregation)
La agregación es un tipo de asociación entre uno o mas objetos, pero donde algunos objetos tienen un rol mayor al otro. El que tiene el rol mayor se determina como el contenedor de los demas objetos y las relaciones que tienen estos. El objeto que tiene el rol mayor, el que puede contener a otros es denominado `aggregate` y los objetos contenidos por el mismo son denominados `componentes`, pero aún asi cada uno de los objetos pueden tener una vida independiente.<br>
```
const company = {
  name: "La Company",
  employees: []
}

class Person {
  constructor(name, lastname) {
    this.name = name;
    this.lastname = lastname;
  }
  
}

pepe = new Person("Pepe", "Petrela");
andres = new Person("Andres", "Perez");

company.employees.push(pepe);
company.employees.push(andres);

console.log(company);
>
{
  name: 'La Company',
  employees: [
    Person { name: 'Pepe', lastname: 'Petrela' },
    Person { name: 'Andres', lastname: 'Perez' }
  ]
}
```
### Composición
La composición, es una forma de agregación pero en la cual el enlace es mucho mas fuerte y los componentes no podran tener una vida individual.
```
const Person = {
  name: "Pepe",
  lastname: "Petrela",
  address: {
    street: "Cobadonga",
    city: "Buenos Aires",
    country: "Argentina"
  }
}
```
Como vemos en el ejemplo, el componente `address` no puede tener una vida independiente por si solo cuando pertenese a otro.
## Principios OOP (Encapsulación, Herencia, Polimorfismo)
### Encapsulación
Cuando hablamos de *encapsulación*, estamos hablando de concentrar datos y funcionalidad ocultando los detalles internos.<br>
Dos Razones para el uso del encapsulamiento:
- Simplifica el uso, no sabiendo como funciona internamente, solo que funciona.
- Simplifica la gestion del cambio. Podemos cambiar el código interno, pero la salida tiene que ser la misma.

Como javascript es un lenguaje dinamico, o sea que el usuario podria tener acceso a cambiar propiedades del objeto directamente, tenemos tecnicas para evitar esto, cumpliendo con las normas de encapsulamiento.
El usuario podra acceder al estado del objeto por medio de métodos, para realizar las operaciónes necesarias. Ejemplo:
```
function Company(name) {
  let employees = [];
  this.name = name;

  this.getEmployees = function() {
    return employees;
  }

  this.addEmployees = function(employee) {
    employees.push(employee);
  }
}

const coca = new Company("Coca");
const pepsi = new Company("Pepsi");

console.log(coca);
console.log(pepsi);

coca.addEmployees({name: "Pepe", lastname: "Petrela"});
pepsi.addEmployees({name: "Andres", lastname: "Perez"});

console.log(coca.getEmployees());
console.log(pepsi.getEmployees());

console.log(coca.employees);
> salida por consola:
Company {
  name: 'Coca',
  getEmployees: [Function (anonymous)],
  addEmployees: [Function (anonymous)]
}
Company {
  name: 'Pepsi',
  getEmployees: [Function (anonymous)],
  addEmployees: [Function (anonymous)]
}
[ { name: 'Pepe', lastname: 'Petrela' } ]
[ { name: 'Andres', lastname: 'Perez' } ]
undefined
```
Como puede verse en el ejemplo el usuario no tiene acceso directo al atributo `employees` (puede observarse en la ultima salida de consola). Para poder ver o modificar este atributo, se vale de los métodos `getEmployees(employee)` y `addEmployees(employee)` respectivamente.
### Herencia (Inheritance)
Es la obtención de un objeto más especifico a partir de uno mas general, heredando los propiedades del general y agregando las especificaciones correspondientes, De esta forma ahorrando código y haciendo mas facil su mantenimiento.<br>
A nivel de codígo al crear la clase que hereda se le agrega `extends` y el nombre de la clase a heredar, dentro del constructor, se utiliza `super(<atributos>)` para heredar las propiedades de la clase que se hereda:
```
class Person {
  constructor(name, lastname) {
    this.name = name;
    this.lastname = lastname;
  }
}

class Programmer extends Person {
  constructor(name, lastname, language) {
    super(name, lastname);
    this.language = language;
  }
}

persona = new Person("Pepe", "Petrela");
console.log(persona);

programador = new Programmer("Andres", "Perez", "javascript");
console.log(programador);

> salida por consola:
Person { name: 'Pepe', lastname: 'Petrela' }
Programmer {
  name: 'Andres',
  lastname: 'Perez',
  language: 'javascript'
}
```
### Polimorfismo
La palabra polimorfismo significa *multiples formas*. En la POO es la habilidad de un objeto de realizar una acción de diferentes maneras, utilizando métodos iguales que se implementan de forma diferente en varias clases.
#### Sobrecarga (overloading)
La sobrecarga de funciones es la capacidad de un lenguaje de programación para crear múltiples funciones del mismo nombre con diferentes implementaciones. cuando se llama a una función sobrecargada, ejecutará una implementación específica de esa función apropiada para el contexto de la llamada.
```
class Programmer extends Person {
  constructor(name, lastname, language) {
    super(name, lastname);
    this.language = language;
  }

  dameDatos() {
    return `${super.dameDatos()} ${this.language}`;
  }
}

class Employee extends Person {
  constructor(name, lastname, employment) {
    super(name, lastname);
    this.employment = employment;
  }

    dameDatos() {
    return `${super.dameDatos()} ${this.employment}`;
  }
}

programador = new Programmer("Andres", "Perez", "javascript");
console.log(programador);
console.log(programador.poli());

empleado = new Employee("Pepe", "Petrela", "administrador");
console.log(empleado);
console.log(empleado.poli());
>
Programmer {
  name: 'Andres',
  lastname: 'Perez',
  language: 'javascript'
}
Andres Perez javascript
Employee {
  name: 'Pepe',
  lastname: 'Petrela',
  employment: 'administrador'
}
Pepe Petrela administrador
```
#### Polimorfismo Parametrico
completar...
#### Polimorfismo Subtipo
completar...