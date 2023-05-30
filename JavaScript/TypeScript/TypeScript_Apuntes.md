# Apuntes TypeScript

## Instalación

```
npm i -g typescript
```

Comprobar que se instalo viendo su versión:

```
tsc -v
```

## Transpilar un archivo TypeScript:

```
tsc archivo.ts
```

Esto creara un archivo JavaScript con compatibilidad con la mayoria de navegadores.

Luego para ejecutar nuestro archivo `.js` tipeamos:

```
node archivo.js
```

También podemos hacerlo en usa sola linea:

```
tsc archivo.ts && node archivo.js
```

Por lo general el archivo resultante tiene que ir en un directorio diferente y lo hacemos de la siguiente manera:

```
tsc --outDir dist archivo.ts && node idst/archivo.js
```

Si no existiera el directorio indicado este sera creado al transpilar, en este caso `dist` y ejecutamos al final en este ejemplo.

## Utilizando Watch, transpilar automaticamente

Para transpilar automaticamente a medida que se realicen modificaciónes utilizamos `watch` de esta manera:

```
tsc --outDir dist archivo.ts --watch
```

Para ver mas comandos utiliza:

```
tsc --help
```

También la pagina oficial de [TypeScript](https://www.typescriptlang.org/)

## Estructura de Proyectos
Por convención el proyecto debe crearse en la carpeta `src` donde colocaremos nuestro archivo `ts` y luego ejecutaresmos `tsc --init` que creara un archivo `tsconfig.json` en nuestra carpeta raiz, con los parámetros para nuestro proyecto.

## tsconfig.json
Este archivo tiene los parámetros de configuración de nuestro proyecto, en el cual debemos descomentar y/o modificar los parámetros que necesitemos.

En este caso para seguir con el ejemplo, descomentaremos y modificaremos con nuestro directorio donde queremos se coloquen los archivos transpilados:
```json
"outDir": "./dist",
```
También descomentamos y modificamos la carpeta donde estaran nuestros archivos `ts` que seran transpilados:
```json
"rootDir": "./src",
```
En `"target"` puedes indicar a la versión de JavaScript que deseas compilar, si borras el contenido y presionas `ctrl + spacebar` te aprareceran todas las versiones que puedes colocar. en nuestro caso pondremos `"ES6"`:
```json
"target": "ES6",
```
Una vez terminada la configuración de nuestro proyecto y teniendo definidas las carpetas de transpilación, de archivos fuentes y versión de JavaScript a compilar solo debemos ejecutar:
```
tsc
```
Para que se transpilen nuestros archivos.

## Tipos Basicos de TS
TypeScrip esta fuertemente tipado a diferencia de JavaScript en el cual la asignación de distintos tipos a una variable esta permitido y puede generar inconsitencias y errores al momento de ejecución o mantenimiento. Por el contrario en TypeScript el tipado evita estos inconvenientes advirtiendonos en tiempo de edición y/o ejecución del código.

Lista de tipos basicos:
```typescript
// Basic types
let myTypeString: string = "Hello world";
let myTypeNumber: number = 32;
let myTypeBoolean: boolean = true;
let myTypeAny: any = "cualquier cosa" // no recomendado solo caso extremo.

// Array
let arrNumber: number[] = [1, 2, 3];
let arrString: string[] = ["pera", "banana", "manzana"];
let arrAny: any[] = ["pera", 32, false]; // no recomendado solo caso extremo.

// Tuple
let tuplePlayers: [string, number, boolean] = ["Pepe", 2, true];
// Tuple Array
let players: [number, string][];

players = [
    [1, "Pepe"],
    [2, "Jacinto"],
    [3, "Cacaroto"],
];
```
**Nota:** El tipo `any` no debe utilizarse solo en casos extremos, por que este tipo echaria por tierra el fuerte tipado de TypeScript.

## Inferencia de Tipos
En TypeScript se asigna el tipo del valor inicial de la variable, o sea toma el `tipo` del valor con el cual se inicializo esa variable.

Ejemplo:
```typescript
let variable1;          // Es tipo any ya que no se asigno ningún valor.
let variable2:string;   // Es de tipo string, se indico el tipo aunque no valor.
let variable3 = true;   // Es de tipo boolean, no se indico el tipo pero si el valor.
```

## Composición de Tipos
La composición de tipos se utiliza para cuando queremos definir una variable que acepte mas de un tipo.
### Unions
En la composición de tipos utilizamos unions cuando queremos asignar mas de un tipo a una variable y se hace de la siguiente manera:
```ts
let variable: string | number | null;

variable = "Pepe";
variable = 333;
variable = null;
variable = false; // ERROR en este caso no va a aceptar un tipo no definido.
```
### Enums y Objects
Es un ficture de TypeScript, no pertenece a JavaScript. Los `enums` nos permiten definir un conjunto de constantes con nombre. Estos pueden ser string o numericos.
```typescript
// Enum
enum Roles {
  User = "USER",
  Admin = "ADMIN",
  SuperAdmin = "SUPER_ADMIN",
}

console.log(Roles.SuperAdmin);
```
Los objetos no necesitan descripción según lo que ya sabemos sobre los mismos.
```typescript
// Objects

const Objeto = {
  User: "Pepe",
  Age: 30,
  Name: "Pepe Garolpo",
  Active: true,
};

console.log(Objeto.Name);
```
### Type Assertion
Cuando deseamos tipar un valor que estamos recibiendo por ejemplo API REST o fuera de nuestra aplicación, podemos hacerlo de estas dos maneras:
```typescript
// Type Assertion

let channel: any = 'Dato exterior'; // Simula el dato recibido

// Método 1
let channelStr1 = <string>channel;
const myCanvas1 = <HTMLCanvasElement>document.getElementById('main');

// Método 2
let channelStr2 = channel as string;
const myCanvas2 = document.getElementById('main') as HTMLCanvasElement;
```
El método utilizado sera el que se use por norma en el equipo de trabajo.

## Funciones
Las funciones en TypeScript toman el tipado de la función según lo que esta retorne, si no se le declara el tipo y lo hace por la inferencia de tipo:
```typescript
function printStr() { // type: void por inferencia de tipo (no retorna información)
    console.log('Hello world!');
}

function getNumber() { // Type: number por inferencia de tipo
    return Math.floor(Math.random() * 100);
}

printStr();
console.log(getNumber());
```
Pueden declararse de esa forma o declarando el tipo, según las normas del lugar de trabajo, el tipo se declara como en el ejemplo:
```typescript
function printStr():void { 
    console.log('Hello world!');
}

function getNumber(): number {
    return Math.floor(Math.random() * 100);
}

printStr();
console.log(getNumber());
```
### Parámetros
Si la función recibe argumentos, el tipado se declara en los parámetros de la función:
```typescript
function userNick(user:string, id: number):void {
    console.log(`Nickname: ${user}-${id}`);
}

userNick('Pepe',30456);
```
El tipado en los parámetros de la función siguen las mismas reglas del tipado de variables, pudiendo ser tan complejas como sea necesario.
```typescript
function printPosition(position:{lat:number, long?:number | string}):void {
    console.log(`Latitude & longitude are: LAT: ${position.lat} LONG: ${position.long}`);
}

printPosition({lat: 33, long: 55});
```
## Interface vs Clases
### Introducción
|Interface| Clases|
|---|---|
|Solo existen en tiempo de compilación.|Existen en tiempo de compilación y durante el tiempo de ejecución.|
|Solo se usan para verificación de tipos.| Podemos inicializar propiedades e implementar métodos.|
||Crear instancias de dicha clase.|

Lo más recomendable es que empecemos a trabajar con una _interface_ y si vemos por ejemplo que necesitamos inicializar una propiedad, en ese caso utilizaremos una _clase_.

En resumen, las _interfaces_ estaran disponible para nosotros, para asegurarnos que trabajamos con los tipos correctos, estarán disponibles en tiempo de desarrollo y cuando se transpilan a Javascript, dejan de existir sin generar ningun peso al bond del final.
## ¿Que es una interface?
La _interface_ es un contrato de código.

La _interface_ define la "forma" de la _data_, con la que vamos a trabajar, es una especie de molde.

Para definir una _interface_ en TypeScript, debemos utilizar la palabra reservada `interface` y el nombre de la misma:
```typescript
interface Book {
    id: number;
    title: string;
    author: string;
    coAuthor?: string;
    isLoan?: (id: number) => void
}
```
Una vez declarada la interface podemos realizar operaciones usandola como tipo para las mismas:
```typescript
// variable
const book: Book = {
  id: 1,
  title: "White House",
  author: "John Pear",
};
// array
const books: Book[] = [];
// función retorna tipo Book
function getBook(): Book {
  return { id: 1, title: "White House", author: "John Pear" };
}

const myBook = getBook();
// función recibe atributo Book y retorna Book
function createBook(book: Book): Book {
  return book;
}

const newBook: Book = {
  id: 1,
  title: 'White House',
  author: 'John Pear',
  coAuthor: 'Daril Spike',
}

createBook(newBook);
```
Debe observarse que las propiedades `coAuthor` y `isLoan` están declaradas como condicionales, si no fuera de este modo nos mostraria el error en tiempo de edición.
### Extender una Interface
La razón principal por la que se extiende una interfaz en TypeScript es para crear una nueva interfaz que herede las propiedades y métodos de una interfaz existente, pero que también tenga su propio conjunto de propiedades y métodos adicionales. Al extender una interfaz, se pueden definir nuevas propiedades y métodos, reutilizando al mismo tiempo la funcionalidad que ya está definida en la interfaz original.

La extensión de interfaces en TypeScript es útil cuando se quiere agregar o modificar las especificaciones de una interfaz existente sin tener que reescribir todo su contenido. Además, esto permite un mejor mantenimiento del código, ya que cuando se actualiza la interfaz base, todas las interfaces que la extienden también se actualizan automáticamente.  
```typescript
interface Person {
  id: number;
  name: string;
}

interface Employee extends Person {
  dept: string;
}

interface Customer extends Person {
  country: string;
}

const newEmployee: Employee = {
  id: 1,
  name: "Peter Carter",
  dept: "HHRR",
};

const newCustomer: Customer = {
  id: 1,
  name: "Arnaldus Poster",
  country: "Italy",
};
```
## Clases
En TypeScript, una clase es una estructura de programación orientada a objetos que se utiliza para definir un conjunto de atributos y métodos que representan un objeto. Para declarar una clase en TypeScript , utiliza la sintaxis `class`, seguida del nombre de la clase y el cuerpo de la misma. Por ejemplo, aquí hay una definición básica de una clase en TypeScript:
```typescript
class Employee {
  // Atrubutos o estados
  id: number;
  name: string;
  dept: string;

  // Constructor
  constructor(id: number, name: string, dept: string) {
    this.id = id;
    this.name = name;
    this.dept = dept;
    this.showInfo();
  }

  // Métodos
  showInfo(): void {
    console.log(`Name: ${this.name} dept: ${this.dept}`);
  }
}
```
En el ejemplo anterior , la clase se llama `Employee` y tiene las propiedades `id`, `name` y `dept`, inicializadas en el constructor, y un método `showInfo` que muestra el valor de algunas propiedades, una vez que se instancia la clase. Si quieres crear una instancia de la clase, simplemente llama al constructor y proporciona los argumentos necesarios. Por ejemplo:
```typescript
// Instancia de la clase Employee
const emp = new Employee(1, 'Pepe', 'Contrataciones');
```
Es importante tener en cuenta que TypeScript es un lenguaje de programación que se basa en JavaScript, por lo que muchas de las características de las clases en TypeScript son similares a las de las clases en JavaScript. Sin embargo, TypeScript agrega funcionalidades adicionales a las clases, como tipos de datos estáticos y decoradores, que no están disponibles en JavaScript.
### Access Control Keywords
Los modificadores de acceso en TypeScript son `public`, `private` y `protected`. Estos modificadores se utilizan para controlar el acceso a las propiedades y métodos de una clase.
- `public`: Se utiliza como modificador de acceso para controlar el acceso a los miembros (métodos y propiedades) de una clase desde fuera de la clase. Si un miembro de la clase se declara como público, entonces es accesible desde cualquier lugar fuera de la clase, es decir, se pueden acceder a esos miembros desde cualquier parte del código donde se tenga acceso a la instancia de la clase.

  Por defecto, todos los miembros de una clase en TypeScript son públicos, lo que significa que se pueden acceder desde cualquier lugar de la aplicación.

- `private`: Indica que la propiedad o método solo se puede acceder dentro de la misma clase en la que está definida. Esto se aplica tanto durante la compilación como en el código JavaScript resultante. No se puede acceder a una propiedad private fuera de la clase, _ni siquiera a través de la instancia de la clase_.

- `protected`: Se utiliza como un modificador de acceso para miembros de una clase. Un miembro declarado como protegido solo puede ser accedido desde dentro de la clase en la que fue declarado o _desde una subclase_. Esto significa que no puede ser accedido desde fuera de la clase o sin haber heredado la clase.
```typescript
class Employee {
  // Atrubutos o estados
  private id: number;
  private name: string;
  private dept: string;

  // Constructor
  constructor(id: number, name: string, dept: string) {
    this.id = id;
    this.name = name;
    this.dept = dept;
    this.showInfo();
  }

  // Métodos
  private showInfo(): void {
    console.log(`Name: ${this.name} dept: ${this.dept}`);
  }
}

  // Instancia de la clase Employee
  const emp = new Employee(1, 'Pepe', 'Contrataciones');
  // Acceder a una propiedad de la clase
  console.log(emp.name); // Esto provocará un error ya que no se puede acceder a una propiedad privada.
```
En este caso al instanciar la clase `Employee` mostrara los datos utilizando el método `showInfo()`, por que el constructor es un método público que tiene acceso al método privado `showInfo()` pero el siguiente código provocaria un error al intentar acceder al método privado fuera de la clase:
```typescript
console.log(emp.showInfo()); // Error al intentar acceder al método privado de la clase.
```
### Modificador Readonly
En TypeScript, `readonly` es un modificador que se puede usar en la declaración de un atributo para indicar que su valor no debe ser cambiado una vez que se ha inicializado.

Cuando se utiliza la palabra clave `readonly` antes de la declaración de una propiedad, solo se permite asignar un valor a esa propiedad en el constructor o en la definición del objeto. Si se intenta asignar un valor a la propiedad en cualquier otro lugar, se producirá un error en tiempo de compilación. Esto permite asegurar que ciertos valores se establezcan solo una vez y no sean modificados accidentalmente en el futuro. Por ejemplo:
```typescript
class Employee {
  // Atrubutos o estados
  private readonly id: number;
  private name: string;
  private dept: string;
...
}
```
### Automatic Properties
**Nota**: Puede que este termino y el de "Asignación automatica" no sean los correctos.

Podemos hacer nuestro código mas limpio evitando re-definiciones de atributos, inicializando los mismos en el constructor de esta manera sobre el ejemplo de clase anterior:
```typescript
class Employee {

  // Constructor
  constructor(private readonly id: number, private name: string, private dept: string) {
    
    this.showInfo();
  }

  // Métodos
  private showInfo(): void {
    console.log(`Name: ${this.name} dept: ${this.dept}`);
  }
}

  // Instancia de la clase Employee
  const emp = new Employee(1, 'Pepe', 'Contrataciones');
```
### Extender una Clase
En TypeScript, puedes extender una clase utilizando la sintaxis de la palabra clave `extends` seguida del nombre de la clase base que deseas extender. Al extender una clase, la clase hija hereda todos los miembros (miembros de instancia y de clase) de la clase base, y también puede agregar nuevos miembros o anular los miembros de la clase base según se necesite.

Aquí hay un ejemplo de cómo se extiende una clase en TypeScript:
```typescript
class Person {
  constructor(protected readonly id: number, protected name: string) {}
  protected greet(): void {
    console.log(`Hello ${this.name}`);
  }
}

class Employee extends Person {
  // Constructor
  constructor(id: number, name: string, private dept: string) {
    super(id, name);
    this.greet();
    this.showInfo();
  }

  // Métodos
  private showInfo(): void {
    console.log(`Name: ${this.name} Department: ${this.dept}`);
  }
}

// Instancia de la clase Employee
const emp = new Employee(1, "Pepe", "Contrataciones");
```
A tener en cuenta:
- La sentencia `super()` siempre tiene que estar antes de cualquier declaración `this`.
- Observar en `super()` y en el `constructor()` de la clase hija, como se declaran los atributos heredados de la clase padre.
- Observar el uso del Access Control Keyword `protected` que hace accesible los atributos y métodos de la clase padre a la clase hija.

## Namespaces y Modulos
Continuara...