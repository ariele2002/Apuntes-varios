# JavaScript for React - Apuntes

## Funciones

### Funciones que Retornan Funciones y su Ejecución (Programación funcional)

Las funciones retornan valores de todo tipo de datos, pero también pueden retornar otra función, en el ejemplo veamos la salida por consola.

```
function hello() {
    return function () {
        return "Hola Mundo";
    }
}

console.log(hello());

> f () {
    return "Hola Mundo"
}
```

Para ejecutar la función que retorna se coloca otro parentesis

```
console.log(hello()())

> Hola Mundo!
```

### Default Parameters

Los parámetros por defecto son aquellos a los que se les asigna un valor en el momento de definir los parámetros de la función. Esto es muy útil cuando al llamar a la función no se le envia uno o todos sus argumentos.

```
function suma(x = 3, y = 0) {
    return x + y
}

console.log(suma(5, 4)) --> 9
console.log(suma(4)) --> 4
console.log(suma()) --> 3
```

## Objetos

Los objetos en js son definidos entre llaves `{}` y pueden contener todo tipo de datos, incluso otros objetos y también funciones.

```
const user = {
    name: 'Juan',
    lastname: 'Garompo',
    age: 30,
    address: {
        country: 'Argentina',
        city: 'Bs As',
        street: 'Petoruti Nº 325'
    },
    friends: ['Pepe', 'Garzolina', 'Jesualdo'],
    active: true,
    sendMail: function () {
        return 'Sending email...'
    }
}
```

### Acceder a los Datos del Objeto

Para acceder a los datos del objeto, se utiliza la notación de punto invocando la llave para recibir el valor asociado a esta.

```
console.log(user.name) --> Juan
console.log(user.address) --> Retorna el objeto de direcciones
console.log(user.address.city) --> Bs As
console.log(user.friends) --> Retorna el array de amigos
console.log(user.friends[0]) --> Pepe
console.log(user.active) --> true
console.log(user.sendMail) --> Retorna la función, no se ejecuta.
console.log(user.sendMail()) --> Sending email...
```

Ahora bien los datos `clave: valor` en los objetos son llamados `propiedades` y las funciones `métodos`, estos últimos se definen directamente y de forma mas corta como veremos a continuación basado en el ejemplo anterior.

```
const user = {
    name: 'Juan',
    lastname: 'Garompo',
    age: 30,
    address: {
        country: 'Argentina',
        city: 'Bs As',
        street: 'Petoruti Nº 325'
    },
    friends: ['Pepe', 'Garzolina', 'Jesualdo'],
    active: true,
    sendMail() {
        return 'Sending email...'
    }
}
```

```
console.log(user.sendMail()) --> Sending email...
```

## Shorthand Property Names

Por lo general al crear un objeto utilizando variables o constantes se hace de la siguiente manera:

```
const pName = 'laptop';
const price = 3000;

const newProduct = {
    pName: name
    price: price
}

console.log(newProduct); --> Object { pName: "laptop", price: 3000 }
```

Pero hay una forma mas facil y con menos código, poniendo solamente el nombre de las variables:

```
const pName = 'laptop';
const price = 3000;

const newProduct = {
    pName,
    price
}
console.log(newProduct); --> Object { pName: "laptop", price: 3000 }
```

## Manipulación del DOM

No es necesario el conocimiento al detalle de la manipulación del Document Object Manager, pero si el concepto, ya que los frameworks facilitan esta tarea.

```
// Manipulación del DOM
const title = document.createElement('h1');
title.innerText = "Hola Mundo desde JS!"

const button = document.createElement('button');
button.innerText = "Click";
button.addEventListener('click', function () {
    title.innerText = 'Texto actualizado con JS';
    alert('Se realizo un click!')
})

document.body.append(title);
document.body.append(button);
```

## Destructuring

Es la forma de tomar los datos de un objeto desestructurando los datos del mismo, puede ser tanto como definiendo un parametro de función como la asignación a una variable.<br>
Objeto:

```
const aUser = {
    name: 'Pepe',
    age: 30
}
```

Como parametro de una función:

```
function printInfo({name}) {
    console.log(name);
    return '<h2>Hola ' + name + '</h2>'
}

console.log(printInfo(aUser)); --> Pepe
document.body.innerHTML = printInfo(aUser); --> <h2>Hola Pepe</h2>
```

Como asignación a una variable:

```
function printInfo(user) {
    const {name, age} = user;
    console.log(name, age);
    return '<h2>Hola ' + name + '</h2>'
}

console.log(printInfo(aUser)); --> Pepe 30
document.body.innerHTML = printInfo(aUser); --> <h2>Hola Pepe</h2>
```

## Funciones Anonimas (Sin nombre)

Es común utilizar las funciones sin nombre, por practicidad o ahorrando código, también son muy utilizadas en los eventos del DOM.

```
console.log(function () {
    return 'Texto de prueba';
}())
```

Observar en el ejemplo anterior que al ser llamada de esta manera el console.log() imprime la funcíon y no la ejecuta, por lo cual se agrega el `()` al final, para que la ejecute.

Desde un Event Listener del DOM:

```
const button = document.createElement('button');
button.innerText = 'Click me!'
button.addEventListener('click', function () {
    alert('Clicked!');
});

document.body.append(button);
```

## Arrow Functions

En las ultimas versiones de JavaScript se puede usar esta sintaxis donde no se escrible la sentencia `function` y se agrega una flecha despues de los paréntesis `() =>`. Ej:

```
const button = document.createElement('button');
button.innerText = 'Click me!'
button.addEventListener('click', () => {
    alert('Clicked!');
});

document.body.append(button);
```

## Inline Arrow Functions

En las Arrow functions el espacio luego de la flecha lo interpreta como un `return` implicito, por lo cual se pueden hacer definiciones como las siguientes:

```
const showNumber = () => 23;
const showBoolean = () => true;
const showArray = () => [1, 2, 3];

console.log(showNumber());  --> 23
console.log(showBoolean()); --> true
console.log(showArray());   --> [1, 2, 3]
```

Pero ojo al piojo! Cuando se trata de retornar un `Objeto` ya que este se define entre llaves `{}` y el arrow function puede interpretar estas como parte de la función, por lo cual el `objeto` a retornar debe ir entre paréntesis `()`:

```
const showObject = () => ({name: 'Pepe', age: 30});
console.log(showObject());  --> Object { name: "Pepe", age: 30 }
```

## Returns en Funciones

Dado que el `return` termina con la ejecución de una función, puede hacernos mas eficiente la escritura de código, aprovechando esta caracteristica, Ejemplo evitando poner un `else`:

```
const button = document.createElement('button');
button.innerText = 'Click me!'

const isAutorized = true;

button.addEventListener('click', () => {
    if (isAutorized) {
        return alert('Esta autorizado!');
    }

    return alert('No esta autorizado!');

});

document.body.append(button);
```

## String Literals

Es la forma de incluir valores y código dentro de un string sin la nececidad de concatenar las expresiones y el texto. La sintaxis es la siguiente; Se encierra el texto entre las comillas simples inclinadas a la izquierda ( _`_ ) y las expresiones dentro de ${}.

```
prueba = `El valor es: ${variable} siempre y cuando se cumpla ${variable > 5 ? variable + 2: variable = 0} en esta ocación`
```

```
// String literals
const background = 'blue';
const color = 'white';
const isAutorized = false;

const button = document.createElement('button');
button.innerText = `${isAutorized ? 'Click me!': "Don't click me"}`
button.style = `background: ${isAutorized ? background: 'red'}; color: ${color};`

button.addEventListener('click', () => {
    if (isAutorized) {
        return alert('Esta autorizado!');
    }

    return alert('No esta autorizado!');

});

document.body.append(button);
```

## Array Methods

Por lo general para recorrer un array se usa un bucle `for` pero en React casi no se utilizan, en su lugar se utilizan los _array methods_.<br>
Estos métodos de array requieren de una función (callback) que se ejecutara por cada elemento del array recorrido enviando el elemento como argumento de dicha función. Es recomendable _nombrar el array en plural_ asi puede nombrarse el parámetro de la función en _singular_, para mayor claridad.<br>

### `forEach()`

El método `forEach()` trabajaria como el bucle `for` y no retorna valor alguno, por lo cual las operaciones deben hacerse dentro de la función callback, Ej. asignarle a una variable o array el valor de la operación.<br> **Nota:** en React se usa `map()` en su lugar, por que se ajusta al paradigma de progamación funcional, retornando un nuevo array sin modificar el actual.

#### Definición y Uso

- El método `forEach()` ejecuta una función por cada elemento en el array.
- El método `forEach()` _NO_ se ejecuta en los elementos vacios del array.

#### Sintaxis

`array.forEach(function(currentValue, index, arr), thisValue)`

#### Parámetros

- `function()`: _Requerido_, función que corre por cada elemento del array.
- `currentValue`: _Requerido_, contiene el valor del elemento actual.
- `index`: _Opcional_, contiene ell indice del elemento actual.
- `arr`: _Opcional_, contiene el array donde pertenece el elemento actual.
- `thisValue`: _Opcional_, Por defecto su valor es `undefined`. Es un valor pasado a la función como `this`.

#### Valor que Retorna

- `undefined`

#### Nota:

- `forEach()` en el DOM _NO_ funciona con HTMLCollection por eso se usa for, pero si funciona con los NodeList.
- _No es bueno_ usar `forEach` en código async await (ver bien por que).

#### Ejemplos

```
const numbers = [1, 2, 3, , 5, 6, , 8, 9, 10];

numbers.forEach((number) => {
    console.log(number);
});

console.log(numbers);

Salida a consola:
1
2
3
5
6
8
9
10
Array(10) [ 1, 2, 3, <1 empty slot>, 5, 6, <1 empty slot>, 8, 9, 10 ]
```

```
const names = ['Pepe', 'Jesualdo', 'Anastacia', 'Peperino'];

names.forEach((name) => {
    console.log(`Hola ${name}!`);
});

console.log(names);

Salida a consola:
Hola Pepe!
Hola Jesualdo!
Hola Anastacia!
Hola Peperino!
Array(4) [ "Pepe", "Jesualdo", "Anastacia", "Peperino" ]
```

### `map()`

Crea un nuevo array llamando a una función por cada elemento del array.

#### Definición y Uso

- Crea un nuevo array llamando a una función por cada elemento del array.
- Ejecuta una función una vez para cada elemento de un array.
- _NO_ ejecuta la función para elementos vacíos.
- _NO_ cambia el array original.

#### Sintaxis

`array.map(function(currentValue, index, arr), thisValue)`

#### Parámetros

- `function()`: _Requerido_, función que corre por cada elemento del array.
- `currentValue`: _Requerido_, contiene el valor del elemento actual.
- `index`: _Opcional_, contiene ell indice del elemento actual.
- `arr`: _Opcional_, contiene el array donde pertenece el elemento actual.
- `thisValue`: _Opcional_, Por defecto su valor es `undefined`. Es un valor pasado a la función como `this`.

#### Valor que Retorna

- Un Array, con el resultado de la función por cada elemento del array.

#### Ejemplos

```
const numbers = [0, 1, 2, 3, 4, 5];

const newArr = numbers.map((number) => {
    return number * 2
});

console.log(newArr);

> Array(6) [ 0, 2, 4, 6, 8, 10 ]
```

```
const names = ['Pepe', 'Juan', 'Ana', 'Gervacio'];

const helloNames = names.map((name) => {
    return `Hello ${name}`;
});

console.log(names);
console.log(helloNames);

> Array(4) [ "Pepe", "Juan", "Ana", "Gervacio" ]
> Array(4) [ "Hello Pepe", "Hello Juan", "Hello Ana", "Hello Gervacio" ]
```

### `find()`

Retorna el primer elemento que cumpla con la condición en la función que llama por cada elemento del array.

#### Definición y Uso

- Retorna el primer elemento que cumpla con la condición indicada.
- Ejecuta una función una vez para cada elemento de un array.
- _NO_ ejecuta la función para elementos vacíos.
- _NO_ cambia el array original.

#### Sintaxis

`array.find(function(currentValue, index, arr),thisValue)`

#### Parámetros

- `function()`: _Requerido_, función que corre por cada elemento del array.
- `currentValue`: _Requerido_, contiene el valor del elemento actual.
- `index`: _Opcional_, contiene ell indice del elemento actual.
- `arr`: _Opcional_, contiene el array donde pertenece el elemento actual.
- `thisValue`: _Opcional_, Por defecto su valor es `undefined`. Es un valor pasado a la función como `this`.

#### Valor que Retorna

- Un valor, del primer elemento que pase el test. En otro caso retorna `undefined`.

#### Ejemplos

```
const names = ['Pepe', 'Juan', 'Ana', 'Gervacio', 'Aurelio'];

const findName = names.find((name) => {
    if (name[0] === 'A') {
        return name;
    }
});

console.log(findName);

> Ana
```

### `filter()`

El método filter() crea un nuevo arreglo con los elementos que pasen el test que provee la función.

#### Definición y Uso

- Crea un nuevo array lleno con los elementos que pasen el test propuesto por la función.
- _NO_ ejecuta la función en los elementos vacíos.
- _NO_ modifica el array original.

#### Sintaxis

`array.filter(function(currentValue, index, arr), thisValue)`

#### Parámetros

- `function()`: _Requerido_, función que corre por cada elemento del array.
- `currentValue`: _Requerido_, contiene el valor del elemento actual.
- `index`: _Opcional_, contiene ell indice del elemento actual.
- `arr`: _Opcional_, contiene el array donde pertenece el elemento actual.
- `thisValue`: _Opcional_, Por defecto su valor es `undefined`. Es un valor pasado a la función como `this`.

#### Valor que Retorna

- Un array, con los elementos que pasaron el test propuesto por la función, si ningún elemento pasa el test, retorna un array vacío.

#### Ejemplos

```
const names = ['Pepe', 'Juan', 'Ana', 'Gervacio', 'Aurelio'];

const filteredArray = names.filter((name) => {
    if (name[0] === 'A') {
        return name;
    }
});

console.log(names);
console.log(filteredArray);

> Array(5) [ "Pepe", "Juan", "Ana", "Gervacio", "Aurelio" ]
> Array [ "Ana", "Aurelio" ]
```

### `concat()`

El método concat(), concatena dos o mas arrays retornando el resultado creando un nuevo array.

#### Definición y Uso

- Concatena dos o mas arrays
- Retorna un nuevo array conteniendo los arrays concatenados.
- _NO_ modifica los arrays originales.

#### Sintaxis

`array1.concat(array2, array3, ..., arrayX)`

#### Parámetros

- `array1,...` _Requerido_, los arrays que se van a concatenar.

#### Valor que Retorna

- Un Array, con el contenido de los arrays concatenados.

#### Ejemplos

```
const names = ['Pepe', 'Juan', 'Ana', 'Gervacio', 'Aurelio'];
const newNames = ['Alonso', 'Eustaquio', 'Petrelo'];

concatNames = names.concat(newNames);

console.log(names);
console.log(newNames);
console.log(concatNames);

> Array(5) [ "Pepe", "Juan", "Ana", "Gervacio", "Aurelio" ]
> Array(3) [ "Alonso", "Eustaquio", "Petrelo" ]
> Array(8) [ "Pepe", "Juan", "Ana", "Gervacio", "Aurelio", "Alonso", "Eustaquio", "Petrelo" ]
```

### `reduce()`

Reduce toma las propiedades de un objeto y permite reducirlas a un solo valor.

#### Definición y Uso

- El método ejecuta una función (callback) de reducción por cada elemento del array.
- El método retorna un solo valor: el acumulador resultante de la función.
- El método no ejecuta la función en los elementos vacíos del array.
- El método no cambia el array original.

#### Nota

En el primer callback, no hay ningún valor devuelto del callback anterior. Normalmente, el elemento de matriz 0 se utiliza como valor inicial y la iteración comienza a partir del elemento de matriz 1. Si se proporciona un valor inicial, se utiliza y la iteración comienza desde el elemento de matriz 0.

#### Sintaxis

`array.reduce(function(total, currentValue, currentIndex, arr), initialValue)`

#### Parámetros

- `function()`: _Requerido_, la función que corre por cada elemento del array.
- `total`: _Requerido_, es el acumulador que retorna `reduce()`.
- `currentValue`: _Requerido_, contiene el valor del elemento actual.
- `currentIndex`: _Opcional_, es el indice del elemento actual.
- `arr`: _Opcional_, es el array original.
- `initialValue`: _Opcional_ (a revisar por que no me parece), es el valor inicial con el que empieza `total`, puede inicializarse con la estructura de datos que se necesite ej: [], {}, etc...

#### Valor que Retorna

- El acumulado resultante de la ultima llamada de la función.

#### Ejemplos

```
import { students } from './data/data_samples.mjs'

// Retorna la sumatoria de las edades
const result = students.reduce((total, student) => total + student.age, 0);
console.log(result);

> 106
```

En este caso queremos obtener un array con cada una de la habilidades de de los desarrolladores sin que se repitan, veremos cada paso para llegar a ese resultado.<br>
En esta etapa nos retorna un array con las habilidades de cada desarrollador:

```
import { students, developers } from './data/data_samples.mjs'

const result = developers.reduce((allSkills, developer) => {
  return [...allSkills, developer.skills];
},[]);

console.log(result);
>
[
  [ 'HTML', 'CSS', 'JavaScript', 'React', 'Redux', 'NodeJS' ],
  [ 'HTML', 'CSS', 'JavaScript', 'React', 'Redux', 'NodeJS' ],
  [ 'HTML', 'CSS', 'JavaScript', 'React', 'Redux', 'NodeJS' ]
]
```

Utilizamos el spread operator `...` para acumular todas las habilidades en un solo array:

```
const result = developers.reduce((allSkills, developer) => {
  return [...allSkills, ...developer.skills];
},[]);

console.log(result);
>
[
  'HTML',       'CSS',
  'JavaScript', 'React',
  'Redux',      'NodeJS',
  'HTML',       'CSS',
  'JavaScript', 'React',
  'Redux',      'NodeJS',
  'HTML',       'CSS',
  'JavaScript', 'React',
  'Redux',      'NodeJS'
]
```

En el siguiente paso para que no se repitan las habilidades utilizamos el objeto `Set()` (un conjunto) que nos retorna una colección de valores que _no pueden repetirse_ solo puede haber una ocurrencia de cada valor.

```
const result = developers.reduce((allSkills, developer) => {
  return new Set([...allSkills, ...developer.skills]);
},[]);

console.log(result);

> Set(6) { 'HTML', 'CSS', 'JavaScript', 'React', 'Redux', 'NodeJS' }
```

Como puede apreciarse, nos retorna un _objeto Set_, para convertirlo nuevamente a un array utilizamos `Array.from()` que nos retorna un nuevo array de un _iterable_.

```
const result = developers.reduce((allSkills, developer) => {
  return Array.from(new Set([...allSkills, ...developer.skills]));
},[]);

console.log(result);

> [ 'HTML', 'CSS', 'JavaScript', 'React', 'Redux', 'NodeJS' ]
```

### `sort()`

El metodo `sort()` nos permite ordenar un array, MODIFICANDO EL ARRAY ORIGINAL OJO AL PIOJO!!.<br>
Cuando se utiliza solamente `sort()` este ordena el array como si todos sus elementos fueran texto y el orden es de diccionario, donde los numeros son primeros, luego mayúsculas, luego minúsculas y despues por el valor de la letra en la secuencia de abecedario.<br>
Ejemplo:

```
const frutaNros = ['duraznitos', 'banana', 40, 'durazno', 150, 'anana', 50, 'coco', 'Pera', 'manzana', 100];

console.log(frutaNros.sort());
>
[
  100,          150,
  40,           50,
  'Pera',       'anana',
  'banana',     'coco',
  'duraznitos', 'durazno',
  'manzana'
]
```

Para hacer un sort de números utilizamos esta sintaxis: `array.sort(function(<primer_valor>, <segundo_valor>) { primer_valor - segundo_valor});`<br>
Ejemplo con la llamada simple y con callback:

```
const numeros = [100, 200, 1000, 2000, 5000, 101]

console.log(numeros.sort());
> [ 100, 1000, 101, 200, 2000, 5000 ]

console.log(numeros.sort((a, b) => a - b));
> [ 100, 101, 200, 1000, 2000, 5000 ]
```

Ordenando el objeto students por edad:

```
import { students, developers, points } from './data/data_samples.mjs'

students.sort((a, b) => a.age - b.age);
console.log(students);
>
[
  { name: 'John', lastname: 'Doe', age: 20, course: 'Web Development' },
  { name: 'Ryan', lastname: 'Ray', age: 20, course: 'Web Development' },
  {
    name: 'Jane',
    lastname: 'Doe',
    age: 21,
    course: 'Financial Management'
  },
  { name: 'Jack', lastname: 'Doe', age: 22, course: 'Accounting' },
  { name: 'Jill', lastname: 'Doe', age: 23, course: 'Marketing' }
]
```

### `some()`

El método `some()` retorna un booleano (`true` o `false`) si algún elemento del array cumple con la condición del callback.

#### Definición y Uso

- Chequea si algún elemento del array pasa el test del callback.
- Ejecuta el callback una vez por cada elemento del array.
- Retorna `true` (y detiene la ejecución) si el callback retorna `true` en algún elemento del array.
- Retorna `false` si el callback retorna `false` en todos los elementos del array.
- El método no se ejecuta en los elementos vacios del array.
- El método no cambia el array original.

#### Sintaxis

`array.some(function(value, index, arr), this)`

#### Párametros

- `function()`: _Requerido_, callback que se ejecuta por cada elemento del array.
- `value`: _Requerido_, el valor del elemento actual del array.
- `index`: _Opcional_, el indice actual del array.
- `arr`: _Opcional_, el array original.
- `this`: _Opcional_, Por defecto su valor es `undefined`. Es un valor pasado a la función como `this`.

#### Valor de Retorno

- Un booleano, `true` si algun elemento del array pasa el test y `false` si ningun elemento pasa el test.

#### Ejemplos

```
import { students } from './data/data_samples.mjs'

const result = students.some(student => student.age > 20);

console.log(result);

> true
```

```
const result = students.some(student => student.name === `John`);

console.log(result);

> true
```

### `every()`

El método `every()` funciona a la inversa que `some()`, retornando `true` si todos los elementos del array pasan el test del callback o `false` si alguno o todos los elementos no pasan el test.

```
import { students } from './data/data_samples.mjs'

const result = students.every(student => student.age >= 20);

console.log(result);

> true
```

### Combinación de Métodos de Arrays

Se pueden combinar los métodos según se necesiten para llegar a un resultado determinado, la combinación toma el retorno del método anterior.

#### Ejemplo

```
import { students } from './data/data_samples.mjs'

// retorna un array con el nombre completo y la edad
const result = students.map(({name, lastname, age}) => ({
  student: `${name} ${lastname}`,
  age
}))
    // retorna array con los que tienen edad mayor a 20 años
  .filter(student => student.age > 20)
  // retorna array ordenado por edad de menor a mayor.
  .sort((a, b) => a.age - b.age)
  // retorna la suma de las edades.
  .reduce((total, student) => total + student.age, 0);

console.log(result);

> 66
```

### Nota

Cuando en el `callback` solo hay un parametro se pueden omitir los paréntesis `()`, al igual que las llaves de la función si su única linea de código es un `return`

```
import {students} from './data/sample_data.mjs';

const fullName = students.map(student => student.name +' '+ student.lastname);

console.log(fullName);

> Array(5) [ "Jill Doe", "John Doe", "Jack Doe", "Ryan Ray", "Jane Doe" ]
```

### Referencias Sobre Arrays

- [MDN Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [Fast Web Arrays](https://faztweb.com/contenido/javascript-arrays-replit)

## Spread Operator

El operador de _propagación_ de JavaScript (`...`) nos permite copiar rápidamente todo o parte de una matriz u objeto existente en otra matriz u objeto.

### Ejemplo Concatenación de Arrays:

```
const names = ['Pepe', 'Juan', 'Ana', 'Gervacio', 'Aurelio'];
const newNames = ['Alonso', 'Eustaquio', 'Petrelo'];

const moreNames = [...names, ...newNames];

console.log(moreNames);

> Array(8) [ "Pepe", "Juan", "Ana", "Gervacio", "Aurelio", "Alonso", "Eustaquio", "Petrelo" ]
```

### Ejemplo Concatenación de Objetos:

```
const user = {
    name: 'Pepe',
    lastname: 'Pumbate'
}
const address = {
    street: 'Ayacucho 318 P 3 D 8',
    city: 'Buenos Aries'
}
const userInfo = {...user, ... address};

console.log(userInfo);

> Object { name: "Pepe", lastname: "Pumbate", street: "Ayacucho 318 P 3 D 8", city: "Buenos Aries" }
```

### Ejemplo Modificación de Objeto:

Obsérvese en este ejemplo, que al utilizar el spread operator (`...`) al concatenar en un nuevo `objeto` con otros `objetos`, actualizará en las `claves` que tengan en común el `valor` del último `objeto` que conincida con su `clave`. También agregará la/s `clave: valor` nueva/s que presenten los `objetos` concatenados.

```
const user = {
    name: 'Pepe',
    lastname: 'Pumbate',
    address: {
        street: 'Ayacucho 318 P 3 D 8',
        city: 'Buenos Aries'
    }
}
const newAddress = {
    address: {
        street: 'Independencia 341 1er Piso',
        city: 'CABA'
    }
}
const userState = {state: true};

const userUpdated = {... user, ...newAddress, ...userState};

console.log(userUpdated);
console.log(userUpdated.address);
console.log(userUpdated.state);

> Object { name: "Pepe", lastname: "Pumbate", address: {…}, state: true }
> Object { street: "Independencia 341 1er Piso", city: "CABA" }
> true
```

### Ejemplo con Destructuring:

```
const numbers = [1, 2, 3, 4, 5];

const [uno, dos, ...rest] = numbers;

console.log(uno, dos, rest);

> 1 2 > Array(3) [ 3, 4, 5 ]
```

## Ecmascript Modules

Es el concepto de JavaScript para separar un proyecto en varios modulos, haciendo una esctructura del proyecto facil de mantener y administrar.

### Activando la propiedad de modulo en el HTML

Activar la propiedad de modulo: En el documento html, debe declararse en la carga del script la propiedad `type="module"`. Esto activara las propiedades `import` y `export` para los módulos.

```
<script type= "module" src="./index.js"></script>
```

### El módulo y la exportación

El modulo puede exportar sus funciones y atributos con cualquier extructura de datos, solo debe declarar la sentencia `export` delante de los mismos.<br>
Cuando se desea exportar un método o atributo por defecto se utiliza `export default <propiedadDelModulo>`, de esta manera al ser importado el módulo y sin declarar una propiedad especifica, exporta por defecto la propiedad declarada. **Nota:** La propiedad por defecto no se exportara cuando se definan propiedades individuales en la importación.

```
// exampleModule.js

export function add(x=0, y=0) {
    return x + y;
}

export function multiply(x=0, y=0) {
    return x * y;
}

export const points = [1, 2, 3, 4, 5];
export const text = "Enviado desde el módulo";

export default text;
```

### Importación de Modulos

Para importar propiedades de un modulo se declara `import` y la destructuración de las propiedades que se requieran seguido de `from` y la ruta del módulo.

```
// index.js

import {add, multiply, points, text} from './modules/exampleModule.js';

console.log(add(20, 5));
console.log(multiply(2, 3));
console.log(points);
console.log(text);

> 25
> 6
> Array(5) [ 1, 2, 3, 4, 5 ]
> Enviado desde el módulo
```

Importar por defecto: Cuando solo se importa el módulo, este solo pondrá a disposición las propiedades que exporta por defecto.

```
// index.js

import example from './modules/exampleModule.js';

console.log(example);

> Enviado desde el módulo
```

### Extension .js .mjs

El estándar es que los módulos y su invocación utilizen la extención `.js` o `mjs` (modulo.js, Pepito.js, etc...), de otra manera los navegadores emitiran un `error`, por que están basados en el estandar de javaScript. Esto lo aclaro, por que los frameworks por facilidad de desarrollo o experiencia de desarrollo no lo utilizan, pero estos ultimos tienen propiedades para que funcionen sin inconvenientes. En javaScript puro no funciona sin la extensión `.js` o `mjs`.

## Optional Chaining

Es muy utilizado cuando se reciben datos del backend o algún servicio y no se tiene la certeza de si existe un elemento, el siguiente ejemplo nos devuelve un error del navegador y corta la ejecución del programa:

```
const user = {
    name: 'Juancho',
    address: {
        street: 'Ayacucho 318 P3 D8',
        city: 'Buenos Aires'
    },
}

console.log(user.location.city);

> Uncaught TypeError: user.location is undefined
```

Para evitar esto se utiliza el signo de pregunta `?` a la derecha del elemento en cuestion.

```
console.log(user.location?.city);

> undefined
```

De esta forma retorna `undefined` como valor, pero no genera un error en el navegador y no corta la ejecución del programa.

## Async Await (Promesas y Asincronia)

Async Await: Es una forma de manejer las promesas.<br>

### Promise

Para conocer en detalle el funcionamiento de `async` y `await` repasemos que es el objeto promesa.<br>
`Promise`: Es un objeto de javascript que nos permite manejar el código asincrono. Ejemplo:

```
function getData() {
    return new Promise((resolve, reject) => {
        if (data.length === 0) {
            reject(new Error('Data is empty'));
        }
        setTimeout(() => {  // simulamos asincronia
            resolve(data);
        }, 2000);
    });
}

getData()
    .then((response) => console.log(response))
    .catch((err) => console.log(err.message));

> Array(4) [ {…}, {…}, {…}, {…} ] // luego de 2 segundos retorna data.
> Data is empty  // Si data esta vacio.
```

Ejemplo con DOM y `fetch()` que ya maneja el objeto `Promise`

```
const ul = document.createElement('ul');

fetch('https://jsonplaceholder.typicode.com/posts')
.then((response) => {
    return response.json();
}).then((data) => {
    console.log(data);
    data.forEach((post) => {
        const li = document.createElement('li');
        li.innerText = post.title;
        ul.append(li);
    });
    document.body.append(ul);
});
console.log('Linea 2')

> Linea 2
> Array(100) [ {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, … ]
```

Como puede observarse "Linea 2" se ejecuta primero mientras `promise` espera la respuesta del servicio, cuando este retorna los datos, se ejecuta.

### Async Await

Async Await, es una forma de manejar las promesas, con una sintaxis mas limpia y clara. Veamos el ejemplo anterior usando `async` y `await`

```
async function loadData() {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts');
    const data = await response.json();
    console.log(data);

    const ul = document.createElement('ul');

    data.forEach((post) => {
        const li = document.createElement('li');
        li.innerText = post.title;
        ul.append(li);
    });

    document.body.append(ul);
}

loadData();

> Linea 2
> Array(100) [ {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, … ]
```

Como puede verse es una sintaxis mas clara, pero el código asincrono debe ir dentro de una `función` precedida de `async` y cada proceso asincrono debe ir precedido de `await`, que solo puede ser usado dentro de un bloque `async`.

### Top Level Await

En JavaScript Ecmascript 2022 como nueva caracteristica, incorpora `Top Level Await`, esto permite usar el `await` sin incorporarlo dentro de un bloque `async` Ejemplo:

```
const response = await fetch('https://jsonplaceholder.typicode.com/posts');
const data = await response.json();
const ul = document.createElement('ul');

console.log(data);

data.forEach((post) => {
    const li = document.createElement('li');
    li.innerText = post.title;
    ul.append(li);
});

document.body.append(ul);

console.log('Linea 2');

> Array(100) [ {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, … ]
> Linea 2
```

## Tips and Tricks

- _Condicional mas simple:_ 
  En algunas ocaciones uno debe hacer expresiones con operadores lógicos que evaluen varios valores, generando lineas de código extensas o poco legibles:
  ```
  let a =  8;
  ( a !== 0 && a !== 5 && a !== 3 )
  // true
  ```
  Esto puede simplificarse de la siguiente forma:
  ```
  let a = 8;
  (![0, 5, 3].includes(a))
  // true
  ```
- _Total de caracteres que suman los valores de un array:_
  ```
  const array = ["pepe", "toronja",2, "30", true];
  const suma = array.join('').length;
  console.log(suma);
  // array.join('') retorna un string "pepetoronja230true"
  // el .length retorna 18
  ```
- _Extraer valores de un array:_ Se pueden extraer valores de un array en el orden que estan en el misma y asignarlas a variables de esta forma.
  ```
    const names = ['Pepe', 'Anastacia', 'Garzolo'];
    const [primero, segundo] = names;
    
    console.log(primero, segundo);

    // Salida por consola:
    Pepe Anastacia
  ```
