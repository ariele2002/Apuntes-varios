# React Apuntes (Fazt, freeCodeCamp)

## Crear una app en react

```
npx create-react-app my-app  // crea la app
cd my-app  // acceder a la carpeta de la app
npm start  // ejecutar la app
```

**Nota**: Si se desea crear el proyecto en el directorio donde se esta parado, solo es necesario reemplazar el nombre del proyecto por un punto.

```
C:\proyectos\my-app> npx create-react-app .
```

Al correr la app con `npm start` se inicia el servicio en la consola, brindandonos datos de los procesos de la app e inicia en el navegador la app.

**Nota:** Si ya tuviera instalado de forma global via `npm instal -g create-react-app` desinstale el paquete usando: `npm uninstall -g create-react-app`, de esta forma se asegura que `npx` usa la versión mas actualizada.

## Estructura de Archivos

Nosotros solo trabajaremos con la carpeta `src`. Al finalizar el proyecto y al ejecutar `npm run build` se creará la carpeta `build` el contenido de esta sera el proyecto final que debe subirse al server de producción.

## Pasos a tener en cuenta antes de desarrolar

Estructura del componente:

- Identificar los elementos que componen nuestro proyecto ej: titulo, targetas, imagenes etc... identificar los patrones que se repiten, esos son los candidatos para un componente en React.

## Comenzar a desarrollar

Es recomendable borrar la carpeta `src` con todo su contenido y volver a crearla vacia al comenzar.
Pasos a seguir:

- Creamos el archivo `index.js`, que es el archivo principal de interacción de la app.
- Importamos la libreria `react`.

  _Nota_: A partir de la versión 17 de React no es necesario importar la libreria `react` para proyectos simples, pero si se importa cuando hacemos uso de Hoocks y estados y en otras condiciones.

- Importamos la libreria `react-dom/client`, para la manipulacion del DOM.
- Inicializamos una constante `root` que como valor tendra lo que devuelva el método `createRoot` de `ReactDOM` enviandole como argumento `document.getElementById('root')` que es el elemento contenedor de interfaz entre react y el documento HTML.

Ejemplo:

```JavaScript
import React from 'react';
import ReactDom from 'react-dom/client';

const root = ReactDom.createRoot(document.getElementById('root'));

root.render(<h1>Hello World</h1>);  // Renderiza la respuesta en el navegador.
```

El método `render()` envia al navegador la respuesta de nuestra app.

## Extención JSX

La extensión de React para la sintaxis de JavaScript. `JSX` = `JavaScript XML`. Nos permite describir en JavaScript cómo se verán los componentes usando una estructura similar a HTML (su estructura no necesariamente su estilo).

### Ventajas de usar JSX

- Estructura más fácil de visualizar.
- Errores y advertencias más útiles.

### Diferencias en la Sintaxis en Atributos HTML

JSX cambia la sintaxis que puede afectar a las palabras reservadas de JavaScript.

- El atributo `class` se escribe `className` ej: `<h1 className="titulo">Titulo</h1>`
- El atributo `for` se escribe `htmlFor` ej: `<label htmlFor="css">CSS</label>`
- Estilos en linea: El atributo `style` acepta un objeto JavaScript con propiedades `CSS` escritas en camelCase. Ej: en css `background-color` en jsx `backgroundColor`.

  ```JavaScript
  const myStyle = {fontFamily: 'sans-serif', backgroundColor: '#333', padding: '5px'}

  <div style={ myStyle }>Hola Mundo!</div>
  ```

  Observar en el siguiente ejemplo, que se usan dos pares de llaves `{}` el primero que nos permite escribir JavaScript en la variable y el segundo que conforma el objeto en si.

  ```JavaScript
  <div style={{backgroundColor: '#333'}}> Hola Mundo!</div>
  ```

### Estructura en JSX

Al igual que en HTML, los elementos pueden ser _anidados_ en JSX para formar estructuras más complejas. Podemos tener _elementos_ dentro de _componentes_, _componentes_ dentro de _elementos_ y _elementos_ dentro de _elementos_.

```JavaScript
<div className="Contenedor">
  <Pantalla input={input} />
  <div className="fila">
    <Boton handleClick={ agregarInput }>1</Boton>
    <Boton handleClick={ agregarInput }>2</Boton>
  </div>
</div>
```

### JavaScript en JSX

En JSX puede escribirse código JavaScript sin ningún inconveniente antes del `return` que devuelve la interfaz y dentro de esta última se escribe el código dentro de llaves `{}`

```JavaScript
function MyComponent() {
  const user = {name: "Pepe", age: 23};
  const myFunction = (age) => age + 5;

  return(
    <div>
      <h1>Nombre:{ user.name }</h1>
      <h2>Edad: { user.age }</h2>
      <h3>Edad dentro de 5 años: { myFunction(user.age)}</h3>
      <p>Prueba de calculo: { 32 * 2 }</p>
    </div>
  )
}
```

### Reglas sintacticas

- Self closing tag `/>` deben tener un espacio en blanco antes del esta: `<Component />`, `<img />`
- Punto y coma al finalizar la declaración de una arrow function. Esto es en general no solo para React.
  ```JavaScript
  const myFunction = () => { return 'Hola!'};
  ```

### Nota

La extensión `jsx` se puede usar para los módulos en React, es indistinto usar `js` o `jsx`, react los interpreta de la misma forma, pero es mas prolijo a mi forma de ver y hay varios frameworks que utilizan el `jsx` para trabajar. En mi caso prefiero usarlo.

## Componentes

Cada parte de de la estructura de nuestro proyecto puede ser un componente ej: barra de navegador, header, main etc... de esta forma pueden ser reutilizables, teniendo el código dividido en componentes mas pequeños, dividiendo el problema y no duplicando código.

**_Los componentes son funciónes que retornan una interfaz._**

El componente principal y que contiene a los demas es el `root`.

En resumen un **componente** es: Parte de la interfaz del usuario que es independiente y reusable. Es independiete por que va a tener un cierto estado y una funcionalidad especifica, ese estado y esa funcionalidad van a ser independientes. Es reusable por que una vez definido se lo puede llamar las veces que se lo necesite.

_Componentes vs Elementos_: Los componentes estan formados por elementos, los elementos son la estructura mas básica ej: div, h1, etc... y se representan en _letras minúsculas_. Toda esa combinación de estructura, presentación y lógica va a conformar un componente en React. El componente es mas complejo y los elementos son simplemente como los bloques fundamentales que lo van a componer.

Caracteristicas y sintaxis de los componentes.

- Los nombres de los componentes deben iniciar con mayúscula. De esta forma se identifica que es un componente.
- Los componentes son funciones que retornan una interfaz
- Los componentes deber retornar siempre su resultado dentro de un contenedor, el tag correspondiente en un elemento individual o dentro de un `<div>` en el caso de varios elementos o el tag que corresponda segun el contenedor y el caso.
- Invocación del Componente:
  - Puede invocarse el componente dentro de llaves `{}` y la función ej: `<div>{Componente()}</div>`
  - Usando el nombre del componente como tag `<Componente></Componente>`
  - Usando close tag que es la versión mas reducida y clara `<Componente/>`

De esta forma el componente es _reutilizable_ y puede llamarse las veces que uno desee, en el ejemplo se lo invoca de las tres formas posibles, dando el mismo resultado:

```JavaScript
function Greetings() {
    return <div>
        <h1>Esto es un componente</h1>
        <p>lorem 1234</p>
    </div>
}

root.render(
    <div>
        // Distintas formas de invocar un componente
        {Greetings()}
        <Greetings></Greetings>
        <Greetings/>
    </div>
);
```

## React DOM

Es un paquete que facilita la interacción y actualización del DOM en las aplicaciones de React.

El DOM (Document Object Model) es una representación en el navegador de todos los elementos que conforman una página o aplicación web.

## Codificando en las Interfaces

Como en el ejemplo anterior esta forma de escribir el código, su sintaxis, funciona por que realmente React no usa JavaScript, sino que utiliza el lenguaje `JSX` que es una mezcla de JavaScript y HTML por asi decirlo.<br>
Para escribir código JavaScript dentro de las interfaces, se hace entre llaves `{}`.

```JavaScript
function Greetings() {
    const married = true;
    return <h1>{married ? 'Estoy casado' : 'No estoy casado'}</h1>
}

root.render(
  <div>
    <Greetings />
  </div>
);
```

### Booleanos y objetos

Si deseamos representar un `booleano` o un `objeto` en la interfaz, esta no devolvera resultado alguno, ya que no interpretara estos valores. Para hacerlo es necesario convertirlos en `string` ejemplo:

```JavaScript
function Greetings() {
  const user = {
    firstname: "Pepe",
    lastname: "Petrela",
  };

  const verdadero = true;

  return (
    <div>
      <h1>{JSON.stringify(user)}</h1>
      <h2>{verdadero.toString()}</h2>
    </div>
  );
}
```

Mostrando los valores del objeto:

```JavaScript
function Greetings() {
  const user = {
    firstname: "Pepe",
    lastname: "Petrela",
  };

  const verdadero = true;

  return (
    <div>
      <h1>Nombre: {user.firstname} Apellido: {user.lastname}</h1>
      <h2>{verdadero.toString()}</h2>
    </div>
  );
}
```

## Fragment <> </>

Fragment se utiliza para **cumplir** con la regla de React, de que toda interfaz debe ir contenida en una etiqueta (tag) cuando enviamos varios elementos en una interfaz, evitando etiquetas o contenedores indeseados.
Al encerrar los elementos en los tags `<>` y `</>` estos no generaran código HTML alguno.

```JavaScript
function Greetings() {
  const user = {
    firstname: "Pepe",
    lastname: "Petrela",
  };

  const verdadero = true;

  return (
    <>
      <h1>
        Nombre: {user.firstname} Apellido: {user.lastname}
      </h1>
      <h2>{verdadero.toString()}</h2>
    </>
  );
}

root.render(
  <>
    <Greetings />
    <Greetings />
    <Greetings />
  </>
);
```

## ECMASCRIPT MODULES

Como ya vimos en los _Componentes_ y sus características, estos dividen el código, su lógica y tambén pueden conformar _Componentes_ en archivos individuales, separando la lógica y ser exportados e importados, haciendo que el código sea modular y facil de mantener.

Los nombres de Módulos deben comenzar en Mayúsculas.

**Nota**: Una buena práctica que los componentes sean creados dentro de una carpeta "components".

Módulo `Sumamos.js`

```JavaScript
export function Sumamos() {
  function add(x, y) {
    return x + y;
  }
  return (
    <>
      <h1>{add(15, 30)}</h1>
    </>
  );
}
```

Principal `index.js`

```JavaScript
import React from "react";
import ReactDom from "react-dom/client";

import {Sumamos} from "./Sumamos";

const root = ReactDom.createRoot(document.getElementById("root"));

root.render(
  <>
    <Sumamos />
    <Sumamos />
    <Sumamos />
  </>
);
```

También se puede usar la sintaxis de funcion flecha en una variable en el módulo y exportarla. No se ha demostrado que tenga alguna ventaja al hacerlo asi, por lo cual las dos opciones son validas.

Módulo `Sumamos.js`

```JavaScript
export const Sumamos = () => {
  function add(x, y) {
    return x + y;
  }
  return (
    <>
      <h1>{add(15, 30)}</h1>
    </>
  );
}
```

### Exportar Varios Componentes del Módulo

Al importar separamos por coma dentro de la llave los nombres de los componentes.<br>
Módulo `Sumamos.js`

```JavaScript
export function Sumamos() {
...}

export function UserCard() {
  const user = {
    firstname: "Pepe",
    lastname: "Petrela",
  };

  return (
    <p>
      Name: {user.name} Lastname: {user.lastname}
    </p>
  );
}
```

Principal `index.js`

```JavaScript
import React from "react";
import ReactDom from "react-dom/client";

import { Sumamos, UserCard } from "./Sumamos";

const root = ReactDom.createRoot(document.getElementById("root"));

root.render(
  <>
    <Sumamos />
    <UserCard />
  </>
);
```

### Export Default

Al usar dentro del Módulo `export default` al momento de importar, debe darsele un nombre al módulo importado:

Módulo `Product.js`

```JavaScript
function Product() {
  return <h2>Product</h2>;
}

export default Product;
```

Principal `index.js`

```JavaScript
...
import Product from "./Product";

const root = ReactDom.createRoot(document.getElementById("root"));

root.render(
  <>
...
    <Product />
  </>
);
```

### Export Default e Importación de otro componente no default

En este caso debe colocarse una coma segida al nombre del Módulo y entre llaves el nombre del Componente a importar.

Módulo `Product.js`

```JavaScript
function Product() {
  return <h2>Product</h2>;
}

export function Navbar() {
  return <nav>Navbar</nav>;
}

export default Product;
```

Principal `index.js`

```JavaScript
...
import Product, {Navbar} from "./Product";

const root = ReactDom.createRoot(document.getElementById("root"));

root.render(
  <>
...
    <Product />
    <Navbar />
  </>
);
```

¿Cuando utilizar uno u otro? En realidad depende del proyecto y las circunstancias ya que dafault exporta el módulo completo y en algunos casos solo se desea importar algun/os componentes en particular.

## PROPS

Props se utiliza como _parámetro_ del _componente_ que recibira como _argumento_ los valores que se deseen al _componente_ cuando es invocado. Esta es una forma dinámica de pasar datos al componente por cada vez que es invocado.

_Los props **solo** pueden pasarse de padres a hijos_.

Módulo `EjProps.jsx`

```JavaScript
export function EjProps(props) {
    console.log(props);
    return <h2>{JSON.stringify(props)}</h2>;
}
```

Principal `index.js`

```JavaScript
...

import {EjProps} from "./EjProps";

const root = ReactDom.createRoot(document.getElementById("root"));

root.render(
  <>
    <EjProps title = "Hola Mundo"/>
    <EjProps user = {{firstname: 'Pepe', lastName: 'Pretrela'}}/>
    <EjProps f = {true}/>
    <EjProps a = {10}/>
    <EjProps xy = {10 + 5} />
  </>
);
```

Salida por consola:

```
> Object { title: "Hola Mundo" }
> Object { user: {…} }
user: Object { firstname: "Pepe", lastName: "Pretrela" }
> Object { f: true }
> Object { a: 10 }
> Object { xy: 15 }
```

Salida al Navegador:

```
{"title":"Hola Mundo"}
{"user":{"firstname":"Pepe","lastName":"Pretrela"}}
{"f":true}
{"a":10}
{"xy":15}
```

Otro Ejemplo Simple de `props`:

Módulo `EjProps.jsx`

```JavaScript
export function EjProps(props) {
    return <h2>{props.title}</h2>;
}
```

Principal `index.js`

```JavaScript
...
root.render(
  <>
    <EjProps title = "Texto 1"/>
    <EjProps title = "Texto 2"/>
    <EjProps title = "Texto 3"/>
  </>
);
...
```

Salida al Navegador:

```JavaScript
Texto 1
Texto 2
Texto 3
```

### Destructuring de Props

Props al ser un objeto se le pueden aplicar todas las propiedades y métodos que tienen los mismos. Usando destructurin del ejemplo anterior:

```JavaScript
// EjProps.jsx

export function EjProps({title}) {
    return <h2>{title}</h2>;
}
```

### Pasando Varios Parametros

Para pasar varios parámetros en el destructuring, se separan estos con una _coma_. Es buena practica en la función que recibe los argumentos poner un valor por defecto ya que si no se envia uno de los parámetros este queda como `undefined` y no se muestra en el HTML de la interfaz.

`index.js`

```JavaScript
root.render(
  <>
    <EjProps title = "Hola mundo!" user="Pepe"/>
    <EjProps title = "Hola React!" user="Juan"/>
    <EjProps title = "Hola Amigos!"/>
    <EjProps title = "Hola Compadre!"/>
  </>
);
```

`EjProps.jsx`

```JavaScript
export function EjProps({ title, user = "User" }) {
  console.log(title, user);
  return (
    <h2>
      {title} dice {user}
    </h2>
  );
}
```

Salida Navegador

```
Hola mundo! dice Pepe
Hola React! dice Juan
Hola Amigos! dice User
Hola Compadre! dice User
```

### Distintas Estructuras de Datos enviadas en Props

En este ejemplo se muestra como pasar las distintas estructura de datos a `props`:

`index.js`

```JavaScript
root.render(
  <>
    <EjProps
      name="Pepe Petrela"
      amount={3000}
      married={false}
      points={[20, 30, 50]}
      address={{ street: "Av. Garsolio 320", city: "CABA" }}
    />
  </>
);
```

`EjProps.jsx`

```JavaScript
export function EjProps({ name, amount, married, points, address }) {
  return (
    <div>
      <h1>{name}</h1>
      <h2>💵 ${amount}</h2>
      <ul>
        <li>Points: {points.join("|")}</li>
        <li>Married: {married ? "Yes ❤️" : "No 😭"}</li>
        <li>
          Address: {address.street} {address.city}
        </li>
      </ul>
    </div>
  );
}
```

### DefaultProps

Una forma de asegurarnos que en `props` recibimos el tipo de dato adecuado para la operación que va a realizar el _componente_ tenemos dos formas:

- _Parámetros por defecto_: Esto consiste inicializar el valor del parámetro con un valor por defecto en la función. De esta forma si el agrumento no es enviado al invocar el _componente_, tomara el valor por defecto.

  `DefaultProps.jsx`

  ```JavaScript
  export function Button({ text='Some text' }) {
   console.log(text);
   return <button>{text}</button>;
  }
  ```

  `index.js`

  ```JavaScript
  root.render(
    <>
      <Button text="Click me" />
      <Button text="Pay" />
      <Button />
    </>
  )
  ```

  Salida por consola:

  ```
  > Click me
  > Pay
  > Some text
  ```

- _PropTypes_: Es una libreria para definir el tipo y propiedades de las variables. Se instala y se invoca los métodos de la libreria. [Documentación](https://www.npmjs.com/package/prop-types)

  ```JavaScript
  import PropTypes from "prop-types"; // ES6
  export function Button({ text }) {
  console.log(text);
  return <button>{text}</button>;
  }

  Button.PropTypes = {
    text: PropTypes.string.isRequired,
  };

  Button.defaultProps = {
    text: "Some text",
  };
  ```

## Estilos de Componentes

### Estilos en linea

Para aplicar estilos a un elemento en línea, se utiliza el atributo `style` al que se debe asignar un _objeto_ conteniendo las propiedades de estilo, teniendo como _llave_ el nombre del atributo y el _valor_ debe ser un string `style={{color: "#FFF"}}`.

A tener en cuenta:

- Los nombres de _atributos_ que estan separados por un guión deben nombrarse en **camelcase** ej: `font-size` como `fontSize`.
- El valor debe ser siempre un string (cadena de texto). Ej: `fontSize: "20px"`.
- Los estilos en linea **no son recomendados** por motivos de organización, legibilidad y mantenimiento, pero es bueno saber este este concepto es posible de aplicar.

También es posible contener las propiedades de estilo en una variable que luego se asigna a `style` como se vera en el ejemplo:

`Task.jsx`

```JavaScript
export function TaskCard() {
  const styleContainer = {
    backgroundColor: "#202020",
    color: "#fff",
    padding: "20px",
    textAlign: "center",
  };

  return (
    <div style={styleContainer}>
      <h2 style={{ fontSize: "40px", fontFamily: "sans-serif" }}>
        Mi primer tarea
      </h2>
      <p style={{ fontFamily: "cursive" }}>Tarea realizada</p>
    </div>
  );
}
```

### Estilos Utilizando Archivos CSS

Para utilizar las hojas de estilo en un archivo CSS en React, este debe ser importado solo con la sentencia `import` y el path al archivo, ej: `import "./archivo.css"`.

Para asignarle al elemento su _clase_ correspondiente normalmente se utiliza `class="nombre_clase"` pero en React se utiliza `className` en su lugar, ej: `className="nombre_clase"`.

`Task.jsx`

```JavaScript
import "./task.css";

export function TaskCard() {
  return (
    <div className="container">
      <h2 className="title">Mi primer tarea</h2>
      <p className="sub-title">Tarea realizada</p>
    </div>
  );
}
```

`task.css`

```CSS
.container {
    padding: 20px;
    background-color: #202020;
    color: #fff;
    text-align: center;
}

.title {
    font-size: 40px;
    font-family: sans-serif;
}

.sub-title {
    font-family: cursive;
}
```

### Codificación en los estilos

Al igual que se puede utilizar lógica dentro de las interfaces, también se utiliza para los estilos:

`Task.jsx`

```JavaScript
import "./task.css";

export function TaskCard({ ready }) {
  return (
    <div className="container">
      <h2 className="title">Mi primer tarea</h2>
      <p className="sub-title">
        <span className={ready ? "bg--green" : "bg--red"}>
          {ready ? "Tarea realizada" : "Tarea no realizada"}
        </span>
      </p>
    </div>
  );
}
```

## Tipos de Componentes

### Componente de Clase

En versiones anteriores de React (anteriores 16.8) no podiamos hacer componentes funcionales, sus componentes se hacian mediante clases. En el componente se importabla `Component` desde `react`, _exportaba_ una clase extendida a `Component` y dentro de la misma se usaba `render(){}` para retornar una interfaz. Antes de se utilizaban componentes de clase para poder manejar los estados, esto fue resuelto con `useState` que veremos mas adelante en _hooks_.

```JavaScript
import { Component } from "react";

export class Saludar extends Component {
  render() {
    return <h2>Hello Word!</h2>;
  }
}
```

**NOTA:** Este procedimiento hace el código mas dificil de mantener y mas engorroso, en la actualidad fue reemplazado por la programación funcional que es el mas nuevo y es el mas utilizado actualmente. Pero a nivel de aprendizaje se explica el uso, de momento en React no fue deprecado y estas son las claves del equipo de React con respecto a los componentes de clase:

- No hay planes para eliminar las clases de React.
- No hay prisa para migrar a los Hooks.
- Pretendemos que Hooks cubran todos los casos de uso existentes para las clases, pero seguiremos soportando los componentes de clase en un futuro previsible.

### Componente de Clase Definición y uso

El Componente de Clase es una clase de ES6 (JavaScript Moderno) que retorna un elemento JSX.
La _estructura_ del Componente de Clase tiene _métodos_ y _estado_, el método es una función asociada a un componente que puede acceder y usar su estado.

#### Carácteristicas

- Debe extender React.Component.
- Deben tener un método `render()` para retornar un elemento JSX.
- Pueden recibir `props` si es necesario.

El método `render()` retorna la estructura del componente en JSX. Reemplaza al `return` de los componentes funcionales. Es el único método obligatorio para un componente de clase en React.

```JavaScript
class NombreComponente extends React.Component {
  render() {
    return <p>Mi Componente</p>
  }
}
```

#### This en componentes de clase

`this` se refiere al componente actual.

```JavaScript
class NombreComponente extends React.Component {
  render() {
    return <p>{this.props.texto}</p>
  }
}
```

#### Constructor

Es el método utilizado para inicializar el _estado_ de un componente de React. El método se llama automaticamente cuando creamos un componente e inicializa los valores del estado del mismo.

```JavaScript
class NombreComponente extends React.Component {

  constructor() {
    super();
    this.state = {completada: true};
  }

  render() {
    return <p>{this.props.texto}</p>
  }
}
```

Debe llamar a `super()` para heredar todas las funciones de su componente _padre_ (React.Component).

**props**: Si el componente tiene un método **consturctor** y recibe `props`, deben ser pasados al **constructor** y a **super()**.

```JavaScript
class NombreComponente extends React.Component {

  constructor(props) {
    super(props);
  }

  render() {
    return <p>{this.props.texto}</p>
  }
}
```

#### Estado en el Constructor

El objeto `state` (estado) se inicializa en el constructor. Ese objeto puede tener varias propiedades separadas por coma.

```JavaScript
class NombreComponente extends React.Component {

  constructor(props) {
    super(props);
    this.state = {
      completada: true,
      color: 'azul',
      prioridad: 1,
    };
  }

  render() {
    return <p>{this.props.texto}</p>
  }
}
```

#### Acceder al Estado

Para acceder al estado se utiliza la siguiente sintaxis: `this.state.propiedad`

```JavaScript
...
render() {
  return <p>{this.state.completada}</p>
}
```

#### Actualizar Estado

Para actualizar una o más propiedades del objeto `state`, se llama a `this.state.setState()` y se pasan como argumento un objeto con las propiedades que se van a actualizar y sus nuevos valores.

#### Métodos de Ciclo de Vida

Son métodos especiales de React usados para realizar operaciones con componentes en momentos específicos de su vida en el DOM.

[Documentación](https://es.reactjs.org/docs/state-and-lifecycle.html)

## Event Handlers (Manejador de Eventos, Event Listeners)

En React agregar un _event handler (event listener)_ se realiza de esta manera:

`EventHandlers.jsx`

```JavaScript
export function ButtonEJ({ text }) {
  return (
    <button
      onClick={() => {
        console.log("Cliked!");
      }}
    >
      {text}
    </button>
  );
}
```

Salida por consola

```
> Clicked!
```

Es una buena practica hacer una función por separado con el nombre handlerEventoCapturado ej: `handlerClick`, que contenga la lógica para tal evento, haciendo el código mas legible y facil de mantener.

`EventHandlers.jsx`

```JavaScript
export function ButtonEJ({ text }) {
  const handlerClick = () => {
    console.log("Clicked!");
  };
  const handlerChange = (e) => {
    console.log(e.target.value);
  };
  return (
    <>
      <button onClick={handlerClick}>{text}</button>
      <input type="text" onChange={handlerChange} />
    </>
  );
}
```

Salida por consola

```
> Clicked
> P
> Pr
> Pru
...
```

**Nota**: Cuando la función se pasa como un `props` a un Componente, en el evento debe llamarse a una función que lo ejecute `onClick={() => myfunction(<argumento>)}`. ** Revisar esto ultimo, no siempre es asi**.

### Formularios y Submit

En el caso de los formularios (`form`) cuando se hace el `submit` la página se refresca, después de enviar los datos. En React _nosotros vamos a tomar el control de los datos_ los procesamos y decidimos como enviarlos, por lo cual vamos a evitar que se refresque la página utilizando `preventDefault()`.

`EventHandlers.jsx`

```JavaScript
export function ButtonEJ({ text }) {

  const handlerSubmit = (e) => {
    e.preventDefault();
    console.log("enviado...");
  };

  return (
    <>
      <form onSubmit={handlerSubmit}>
        <button>Enviar</button>
      </form>
    </>
  );
}
```

[Lista de Eventos Documentación](https://www.w3schools.com/jsref/dom_obj_event.asp)

## Fetch() API

En React es muy comun consumir una REST API, ya que en el fron end no se suelen tener datos, estos se solicitan al back end o a una REST API.

### Ejemplo simple:

`FetchApi.jsx`

```JavaScript
export const Posts = () => {
  return (
    <button
      onClick={() => {
        fetch("https://jsonplaceholder.typicode.com/posts")
          .then((response) => response.json())
          .then((data) => console.log(data))
          .catch(error => console.error(error));
      }}
    >
      Traer datos
    </button>
  );
};
```

### Ejemplo con Async/ Await en un useEffect():

```JavaScript
const [characters, setCharacters] = useState([]);

useEffect(() => {
  async function fetchData() {
    try {
      const response = await fetch("https://rickandmortyapi.com/api/character");
      const data = await response.json();
      setCharacters(data.results);
    } catch(err) {
      console.log(err)
    }
  }
  fetchData();
}, []);
```

**Nota**: Ver la sección de manejo de errores, Error Boundary y Suspense.

## Módulos de Terceros

No siempre hay que reinventar la rueda React tiene una gran comunidad Open Source y también soporte de sus creadores como Facebook, por lo cual hay módulos útiles que se pueden implementar facilmente en nuestro proyecto.

Aca hacemos un ejemplo utilizando un _módulo_ de terceros aplicandolo en el ejemplo anterior. Primero instalamos el _módulo_ según su documentación [Módulo de iconos](https://react-icons.github.io/react-icons/). Luego la importamos y utilizamos para poner un icono en el boton.

```JavaScript
import {VscGlobe} from "react-icons/vsc"

export const Posts = () => {
  return (
    <button
      onClick={() => {
        fetch("https://jsonplaceholder.typicode.com/posts")
          .then((response) => response.json())
          .then((data) => console.log(data))
          .catch(error => console.error(error));
      }}
    >
      <VscGlobe/>Traer datos
    </button>
  );
};
```

## Arrays

En React es muy común utilizar los métodos de array como `map()`,`sort()`,`find()`,`reduce()`, etc. Es preciso tener en cuenta que cuando se generan listas de elementos en React, estos necesitan una propiedad `key={valor que no se repita}` en cada uno de los elementos padres que contienen al resto de elementos, como se vera en el ejemplo.

```JavaScript
export function Users() {
  const users = [
    {
      id: 1,
      name: "Pepe Garzolo",
      image: "https://robohash.org/user1",
    },
    {
      id: 2,
      name: "Armando Estebanquito",
      image: "https://robohash.org/user2",
    },
    {
      id: 3,
      name: "Sirope Ulobolob",
      image: "https://robohash.org/user3",
    },
  ];

  return users.map((user, i) => {
    return (
      <div key={i}>
        <h2>{user.name} id: {user.id}</h2>
        <img src={user.image} alt={`User ${user.id}`} />
      </div>
    );
  });
}
```

## Hooks de React

Los hooks son tan solo funciones que nos provee React para añadir funcionalidad extra a nuestra aplicación. Son funciones especiales que te permiten trabajar con estados en componentes funcionales y otros aspectos de React.

### useState

En React para cambiar un estado, no se realiza como solemos hacerlo en javascript. Para cambiar un estado y tener una variable que cambie en el transcurso del ciclo de vida de la app, se utiliza el hook `useState` que debe importarse de `react`.

```JavaScript
import { useState } from "react";
```

Para crear un estado debe ejecutarce la función `useState()` y como argumento el valor inicial. Esto retorna un array con la variable y la función que modifica esta ultima. ej: `const [variable, setVariable] = useState(valor_inicial)`. El nombre de la función debe llevar `set` precediendo el nombre de la variable en camelcase.

```JavaScript
const [counter, setCounter] = useState(0);
```

Ejemplo de uso de `useState` en el módulo `Hooks.jsx`

```JavaScript
import { useState } from "react";

export function Counter() {
  const [counter, setCounter] = useState(0);
  return (
    <div>
      <h2>Counter: {counter}</h2>
      <button
        onClick={() => {
          setCounter(counter + 1);
        }}
      >
        Incrementar
      </button>
      <button
        onClick={() => {
          setCounter(counter - 1);
        }}
      >
        decrementar
      </button>
      <button
        onClick={() => {
          setCounter(0);
        }}
      >
        Reiniciar
      </button>
    </div>
  );
}
```

Ejemplo con input:

```JavaScript
import { useState } from "react";

export function Message() {
  const [message, setMessage] = useState("");

  return (
    <div>
        <input type="text" onChange={e => setMessage(e.target.value)} />
        <button onClick={() => alert(message) }>Ver mensaje</button>
    </div>
  );
}
```

Al cambiar el estado que representamos en el render, React solo modifica en el DOM el valor del estado, sin recargar el resto de los elementos.

### useEffect

¿Por que se llama useEffect?: Vimos que el efecto principal de React es mostrar HTML en el DOM.

Se llama useEffect por que estamos haciendo un efecto secundario. Queremos que React haga algo distinto de mostrar HTML.

useEffect en acción: useEffect nos permite crear un puente entre React y el navegador. Ejemplo: El efecto primario de React es un `render` los efectos secundarios `useEffect` (Network, geolocalización, ¿internet disponible?, etc...) que generan un cambio de estado que React puede volver a renderizar.

#### Sintaxis

Primero debe ser importado desde 'react': `import { useState, useEffect } from 'react';`

useEffect recibe como argumento una función y opcionalmente separado por una coma un array con la/s dependencia/s: `useEffect(<función>, [<dependencia>]);`

### ¿Cuando se ejecuta useEffect?

- ¿En que momento se ejecuta?: Se ejecuta despues que React haya actualizado el DOM (renderizado).
- ¿Cuando se ejecuta?: Una vez que la app _se ejecuta por primera vez_ y
  _cada vez que se modifica un estado_, esto va a depender de como se declare la _dependencia_.
  - Se ejecuta **al iniciar** la app y cada vez que se **modifica** un estado:
    ```JavaScript
    useEffect(() => {...});
    ```
  - Se ejecuta **solo al iniciar** la app, observese que la dependencia se declara **vacia**.
    ```JavaScript
    `useEffect(() => {...}, []);
    ```
  - Se ejecuta al **iniciar** la app y solo cuando el/los **estado/s declarado/s** en la dependencia se modifica/n.
    ```JavaScript
    useEffect(() => {...},[estado1, estado5]);
    ```

### Custom Hooks

Un custom hook es una es una simple función que nos permite reutilizar un hook, en otros componentes aplicando DRY (Don't Repeat Yourself). Esto puede aplicarse a cualquier hook de React.

Sintaxis: Por norma el nombre de la función debe comenzar con `use` ej: `useMyFunction`

Ejemplo de función custom Hook:

```JavaScript
function useActive(initialState = false) {
  const [active, setActive] = useState(initialState);

  const handleToggle = () => {
    setActive(!active);
  };
  const handleTrue = () => {
    setActive(true);
  };
  const handleFalse = () => {
    setActive(false);
  };

  return [active, { handleToggle, handleTrue, handleFalse }];
}
```

Llamado desde el componente `ShowInfo`:

```JavaScript
function ShowInfo() {
  const [active, { handleToggle }] = useActive(false);

  return (
    <div>
      <button onClick={() => handleToggle()}>Show/hide</button>
      {active && (<h2>"Información que estaba oculta!"</h2>)}
    </div>
  );
}
```

llamado desde el Componente App:

```JavaScript
function App() {

  const [active, { handleToggle, handleTrue, handleFalse }] = useActive();

  return (
    <div className="App">
      <h1>Custom Hook</h1>
      <h2>{active.toString()}</h2>
      <button onClick={handleToggle}>Toggle</button>
      <button onClick={handleTrue}>True</button>
      <button onClick={handleFalse}>False</button>
      <ShowInfo />
    </div>
  );
}
```

En este ejemplo cada componente llama a `useActive` y mantiene cada uno su estado independiente del otro, llamando al custom hook y utilizando los métodos que necesitan del mismo.

[Documentación React Hooks](https://reactjs.org/docs/hooks-intro.html)

## Manejo de errores con Error Boundary

En React, un error boundary es un componente que se utiliza para manejar errores que ocurren durante la renderización o el ciclo de vida de otros componentes secundarios. Los errores que ocurren en un componente hijo normalmente propagan hacia arriba en la jerarquía de componentes hasta que son capturados por un error boundary. Una vez capturados, el error boundary puede renderizar una vista de error en lugar del componente secundario que falló.

Para utilizar un error boundary en React, se puede crear un componente que extienda la clase `React.Component` y definir los métodos `componentDidCatch(error, info)` y `render()`. El método `componentDidCatch` se invoca cuando un error es lanzado por un componente hijo y proporciona información sobre el error y su ubicación en la jerarquía de componentes. El método `render` debe retornar un elemento React que muestre una vista de error adecuada.

Por ejemplo, se podría crear un error boundary como sigue:

```JavaScript
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  componentDidCatch(error, info) {
    this.setState({ hasError: true });
    console.error(error, info);
  }

  render() {
    if (this.state.hasError) {
      return <h1>Ha ocurrido un error.</h1>;
    }
    return this.props.children;
  }
}
```

Este componente se puede utilizar para envolver otros componentes y capturar errores en su descendencia. Por ejemplo, se podría utilizar así:

```JavaScript
<ErrorBoundary>
  <MiComponente />
</ErrorBoundary>
```

Si `MiComponente` lanza un error, el error será capturado por el error boundary y se mostrará la vista de error definida en `render`.

Otro ejemplo de Error Boundary con dos métodos de captura de error:

```JavaScript
import { Component } from "react";

class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = {
      tieneError: false,
      mensajeError: "",
    };
  }

  static getDerivedStateFromError(error) {
    // Método 1
    return { tieneError: true, mensajeError: error.message };
  }

  componentDidCatch(error) {
    // Método 2
    // ambos sirven por igual
    // return { tieneError: true, mensajeError: error.message };
    console.log("Component did catch: ", error.message);
  }

  render() {
    if (this.state.tieneError) {
      // UI de Emergencia
      return (
        <div>
          <h2>Hubo un Error:</h2>
          <p>{this.state.mensajeError}</p>
          <button onClick={() => (window.location.href = "/")}>
            Recargar la página{" "}
          </button>
        </div>
      );
    }
    return this.props.children;
  }
}
```

### Nota:

Aunque los error boundaries pueden capturar la mayoría de los errores que ocurren en sus componentes secundarios, hay ciertos tipos de errores que no pueden ser capturados por ellos. Algunos de estos errores son:

- Errores en el manejo de eventos: si se produce un error en un manejador de eventos como `onClick`, `onKeyDown`, etc., este no será capturado por un error boundary.

- Errores en los componentes que se montan fuera del árbol de React: si se monta un componente fuera del árbol de React (por ejemplo, mediante el uso de `ReactDOM.createPortal`), los errores que ocurren en ese componente no se propagarán hacia arriba en la jerarquía de componentes y no podrán ser capturados por un error boundary.

- Errores en los componentes que se montan durante la fase de inicialización: si un componente falla durante la fase de inicialización, antes de que se monte en el DOM, el error no se propagará hacia arriba en la jerarquía de componentes y no podrá ser capturado por un error boundary.

- Errores en los componentes que utilizan `setTimeout` o `setInterval`: si un componente utiliza `setTimeout` o `setInterval` para programar una función, cualquier error que se produzca en esa función no se propagará hacia arriba en la jerarquía de componentes y no podrá ser capturado por un error boundary.

En general, los error boundaries son una herramienta muy útil para manejar errores en la jerarquía de componentes de React, pero es importante recordar que no pueden capturar todos los errores.

Es importante tener en cuenta que los error boundaries solo capturan errores en la descendencia del componente que los contiene, por lo que es posible que se necesiten varios error boundaries en la jerarquía de componentes para cubrir todo el árbol.
_Es recomendable solo colorar Error Boundary para los Componentes que podrian generar conflicto y no en todo el arbol en Componentes que hacen un renderizado simple._

## Contexto de React

Es la mejor forma de poder compartir el **estado** y **métodos** con el resto de los componentes. El _contexto_, es un _componente_ que engloba al resto de los elementos de la app, los cuales pueden acceder a los valores del contexto directamente, sin tener que pasarlo de componente a componente.

### **Antes de usar Context**

Context se usa principalmente cuando algunos datos tienen que ser accesibles por muchos componentes en diferentes niveles de anidamiento. Aplícalo con moderación porque hace que la reutilización de componentes sea más difícil.

Si solo deseas evitar pasar algunos props a través de muchos niveles, la [composición de componentes](https://es.reactjs.org/docs/components-and-props.html) suele ser una solución más simple que Context.

### Crear el Contexto

Siguiendo la buenas practicas, creamos una carpeta "context" y dentro creamos el módulo del contexto. En este caso para el ejemplo creamos el módulo `TaskContext.jsx`. Con el cual vamos a manejar los _estados_, los _métodos_ para modificarlos y los _datos_ que recibimos de un archivo o una API REST.

**createContext** es la libreria de React que debemos importar para crear el contexto.

```JavaScript
import { createContext, useState, useEffect } from "react";
import { tasks as data } from "../data/tasks";
```

Asignamos a una variable con el nombre de nuestro módulo el retorno de la función **createContext()** y la exportamos, esta contendra el nombre de nuestro contexto y almacenara los datos de la misma.

```JavaScript
export const TaskContext = createContext();
```

Creamos una función que va a _englobar_ el resto de los elementos de la app. Este sera nuestro **ContextProvider** y se exporta. Siguiendo nuestro ejemplo la nombramos `TaskContextProvider`. Esta va a recibir como argumentos en `props` los elementos de la app que representamos con `props.children` y retornaremos en el tag `<TaskContext.Provider>`

```JavaScript
export function TaskContextProvider(props) {

  return (
    <TaskContext.Provider>
      {props.children}
    </TaskContext.Provider>
  );
}
```

El contexto se representa en `main.jsx` importando `TaskContextProvider` del módulo `TaskContext` y poniendo como hijo del tag `<TaskContextProvider>` a `<App/>` en el render de "root". De esta forma queda listo el contexto para compartir atributos y métodos con el resto de los componentes.

```JavaScript
import {TaskContextProvider} from './context/TaskContext'

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <TaskContextProvider>
      <App/>
    </TaskContextProvider>
  </React.StrictMode>
);
```

### Compartiendo Propiedades del Contexto

Como es un componente, comparte sus propiedades de igual manera que estos, pasando sus propiedades y métodos como valores en el tag por medio del atributo **`value={}`**. En este caso un objeto con estos ultimos.

**Nota**: Es una buena practica usar objetos ya que hace mucho más facil de mantener la aplicación al agregar nuevas propiedades al componente del contexto.

`TaskContext.jsx`

```JavaScript
import { createContext, useState, useEffect } from "react";

import { tasks as data } from "../data/tasks";

export const TaskContext = createContext();

export function TaskContextProvider(props) {
  const [tasks, setTasks] = useState([]);

  useEffect(() => {...
  }, []);

  function createTask(task) {...
  }

  function deleteTask(taskId) {...
  }

  return (
    <TaskContext.Provider
      value={{
        tasks,
        createTask,
        deleteTask,
      }}
    >
      {props.children}
    </TaskContext.Provider>
  );
}
```

### Usando las Propiedades del Contexto en los Módulos

Para usar las propiedades del contexto en un módulo, tenemos que importar desde `react` el método `useContext`. En este caso para nuestro ejemplo usamos el módulo `TaskForm.jsx`.

```JavaScript
import { useState, useContext } from "react";
```

Luego importamos al módulo nuestra variable `TaskContext` a la que fue asignada el retorno de `createContext()` en el módulo `TaskContext.jsx`.

```JavaScript
import { TaskContext } from "../context/TaskContext";
```

Ya teniendo disponible el `useContext` y `TaskContext` procedemos a utilizar solo las propiedades que necesite el módulo usando destructuring del retorno de `useContext(<contexto>)`, para asignarlo a una variable dentro de nuestra función `TaskForm` en el módulo.

```JavaScript
const { createTask } = useContext(TaskContext);
```

De esta manera ya podemos utilizar el método del contexto `createTask` en nuestro módulo, como muestra el siguiente ejemplo:

`TaskForm.jsx`

```JavaScript
function TaskForm() {...

  const handleSubmit = (e) => {
    e.preventDefault();
    createTask({ title, description });
  };
...}
```

**Advertencias**

- La llamada de `useContext()` en un componente no es afectada por los proveedores devueltos desde el mismo componente. El `<Context.Provider>` correspondiente necesita estar arriba del componente que hace la llamada de `useContext()`.
- React **rerenderiza automáticamente** todos los hijos que usen un contexto particular empezando desde el proveedor que recibe un `value` diferente. Los valores anteriores y los siguientes son comparados con `Object.is`. Saltarse el rerenderizado con `memo` no evita que los hijos reciban valores de contexto frescos de arriba.
- Si tu sistema de compilación produce módulos duplicados en la salida (lo cual puede pasar si usas enlaces simbólicos), esto puede romper el contexto. Pasar algo a través del contexto solo funciona si `SomeContext` que usas para proporcionar el contexto y `SomeContext` que usas para leerlo son exactamente el mismo objeto, como está determinado por la comparación `===`.

## React Route V6

Para utilizar React Router v6 es necesario instalar `react-router-dom` como una dependencia adicional de `reac-router`. `react-router-dom` es un paquete que proporciona enlaces (`<Link>`) y otras utilidades para trabajar con React Router en aplicaciones web.
**Nota:** No se en que situaciones se instala `react-router` hasta ahora funciona solo con `react-router-dom`.

Para instalar tanto `react-router` como `react-router-dom` en tu proyecto, puedes ejecutar el siguiente comando:

```
npm install react-router react-router-dom
```

Una vez que React Router v6 esté instalado, puedes comenzar a usarlo en tu proyecto. Para ello, primero importa los componentes necesarios:

```JavaScript
import { BrowserRouter, Routes, Route } from "react-router-dom";
```

En este ejemplo, estamos importando los componentes `BrowserRouter`, `Routes` y `Route`. El componente `BrowserRouter` es necesario para crear un objeto de enrutamiento que funcione en una aplicación React. `Routes` es el componente que contiene las rutas definidas para la aplicación y `Route` es el componente que define una ruta específica.

Luego, envuelve tu aplicación en el componente `BrowserRouter` y define tus rutas utilizando el componente Routes. Por ejemplo:

`App.jsx`

```JavaScript
import { BrowserRouter, Routes, Route} from "react-router-dom";

import "./App.css";
import Home from "./pages/Home";
import Characters from "./pages/Characters";
import Games from "./pages/Games";
import Credits from "./pages/Credits";
import NotFound from "./pages/NotFound";
import Header from "./components/Header";

function App() {
  return (
    <BrowserRouter className="App">

      <Header />

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/characters" element={<Characters />} />
        <Route path="/games" element={<Games />} />
        <Route path="/credits" element={<Credits />} />
        <Route path="*" element={<NotFound />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

_Nota:_ Como veran en el código importo los componentes de `./pages` esto es asi por que son páginas completas formadas por componentes y `Header` es importado de `./components` por que es un componente reutilizable. Esto es a modo de organizar mi código, no es obligatorio para que funcione.

### Page Not Found

Cuando se implementa `BrouserRouter` al invocar rutas que no existen en el navegador, dara como resultado una página vacia, para capturar una ruta inexistente y llevar al usuario a una página que le indique dicho error, se utiliza la siguiente ruta:

```JavaScript
<Route path="*" element={<NotFound />} />
```

Creando una ruta al componente apropiado para dicho error, en este ejemplo usamos nuestro propio componente `<NotFound>`, con la información que deseemos mostrar.

### NavLink

Al ingresar en el navegador la ruta, la página se recarga y obviamente tampoco es el método que va a utilizar el usuario normalmente. Por ese motivo creamos una navegación atravez de los _NavLinks_ que ademas de darle al usuario una forma de navegar en nuestra aplicación, hace que las páginas _no se recargen continuamente_.

**Importante:** No deben usarse los links ej: `<a href="/users">` esto funciona pero hace que la página se recargue. Deben usarse los _NavLinks_, excepto para enlaces externos a la aplicación.

#### NavLink vs Link

La principal diferencia entre `NavLink` y `Link` en `react-router-dom` es que `NavLink` está diseñado específicamente para resaltar el enlace como activo. Esto es útil para construir un menú de navegación en el que el usuario necesita saber en qué página se encuentra actualmente. `Link`, por otro lado, simplemente proporciona una forma de enlazar a otra ubicación en la aplicación.

Además, `NavLink` también acepta una prop llamada activeClassName, que se utiliza para especificar la clase que se debe aplicar al enlace activo. Mientras que Link no tiene esta prop. Ej:

```JavaScript
<li><NavLink to="/" className={(data) => console.log(data)}>Home</NavLink></li>
```

En este caso en `data` recibe un objeto:

```JavaScript
Object { isActive: true, isPending: false }
```

El cual podemos desestructurar y usar sus datos, por ej:

```JavaScript
<li>
  <NavLink to="/" className={({isActive}) => isActive ? 'link-active' : '' }>
    Home
  </NavLink>
</li>
```

En resumen, si necesita resaltar los enlaces activos en su aplicación, debe usar NavLink, de lo contrario, Link es una opción más adecuada funcionara como una etiqueta `<a href>` pero sin que refresque la página.

`Header.jsx`

```JavaScript
import { NavLink } from 'react-router-dom';
import "../styles/Header.css";
import logo from "../img/react.svg";

function Header() {
  return (
    <header className="header">
      <img src={logo} alt="Rick and Morty Logo" />
      <nav>
        <ul>
          <li>
            <NavLink to="/">Home</NavLink>
          </li>
          <li>
            <NavLink to="/characters">Character</NavLink>
          </li>
          <li>
            <NavLink to="/games">Games</NavLink>
          </li>
          <li>
            <NavLink to="/credits">Credits</NavLink>
          </li>
        </ul>
      </nav>
    </header>
  );
}

export default Header;
```

### Params

Los params (parametros) en `react-router-dom` nos son de utilidad para pasar argumentos al componente por medio de las rutas.

En la ruta se agrega el parametro precedido por `:` ej: `/<ruta>/:parametro`.

```JavaScript
<Route path="/user/:userId" element={<UserPage />} />
```

En el componente importamos el hook `useParams` de `react-router-dom` y utilizando este hook obtenemos un objeto con el/los parametro/s enviado/s ej:

```JavaScript
import { useParams } from "react-router-dom";

const UserPage = () => {
  const { userId } = useParams();

  return (
    <div>
      <h1>User: {userId}</h1>
    </div>
  );
};

export default UserPage;
```

**Nota:** Multiples parametros se separan por `/` en la ruta ej:

```JavaScript
<Route path="/user/:userId/:userName" element={<UserPage />} />
...
const params = useParams();
console.log(params);
...
localhos:5173/user/10/Alberto
...
> Object { userId: "10", userName: "Alberto" }
```

### Navigate

Se utiliza para redireccionar a una página de una ruta que ya hemos creado y una vez
redirigido, no deja retornar con el historial hacia atras. Se suele utilizar para redirigir a la página de final de seción o logout.

```JavaScript
import { BrowserRouter, Routes, Route, Navigate } from "react-router-dom";
...
<Route path="/moreusers" element={<Navigate to="/users" />} />
```

La propiedad `replace` es opcional e indica que la nueva ruta debe reemplazar la actual en el historial de la sesión en lugar de agregar una nueva entrada. Esto es útil, por ejemplo, cuando deseas evitar que un usuario haga clic en el botón "Atrás" y vuelva a la página anterior después de haber navegado a la nueva ruta.

```JavaScript
<Route path="/moreusers" element={<Navigate replace to="/users" />} />
```

**Es importante notar** que en la última versión de `react-router-dom` se utiliza el _hook_ `useNavigate` en lugar de `Navigate`. Por lo tanto, el uso de `Navigate` no será posible en futuras versiones de la biblioteca.

### useNavigate

El _hook_ `useNavigate` es una función proporcionada por la librería `react-router-dom` en React. Devuelve una función que permite navegar programáticamente mediante el cambio de URL y la renderización del componente correspondiente. Para usar `useNavigate` puedes importarlo de la siguiente manera:

```JavaScript
import { useNavigate } from 'react-router-dom';
```

Una vez importado, puedes usarlo en tu componente de esta manera:

```JavaScript
function MyComponent() {
  const navigate = useNavigate();

  function handleClick() {
    navigate('/ruta'); // Navegar a una ruta específica
  }

  return (
    <button onClick={handleClick}>Navegar a la ruta</button>
  );
}
```

_Nota:_ Es importante tener la librería react-router-dom instalada y configurada correctamente en tu proyecto antes de utilizar el useNavigate hook.

### Subcomponentes

Podemos renderizar _subcomponentes_ dentro del componente principal agregando rutas secundarias ej: ruta principal: `/dashboard` subruta: `/dashboard/welcome`.
De esta manera podemos anidar subcomponentes en renderizados mas complejos ej: `/dashboard/welcom/status/etc...`.

```JavaScript
import { useNavigate, Routes, Route, Link } from "react-router-dom";

function Dashboard() {
  const navigate = useNavigate();

  const handleClick = () => {
    navigate("/");
  };

  return (
    <div>
      <h1>Dashboar</h1>
      <button onClick={handleClick}>Logout</button>
      <Link to="welcome">Say Welcome</Link>

      <Routes>
        {/*ruta secundaria*/}
        <Route path="welcome" element={<p>Welcome!!!</p>} />
      </Routes>
    </div>
  );
}

export default Dashboard;
```

Esto renderizará el componente declarado en `element` dentro del componente principal, ahora bien, para que esto ocurra debemos hacer un cambio en la ruta que nos lleva al componente principal:

```JavaScript
<Route path="/dashboard/*" element={<Dashboard />} />
```

Al agregar el `/*` estamos diciendo que tome todas las rutas despues de `/dashboard/` si no lo hicieramos, saldría por nuestra página de error por defecto al no encontrar la ruta.

**NOTA:** Esta no es la mejor forma de distribuir nuestas rutas, haciendolo dentro de cada componente, para eso utilizaremos una buena practica que se vera en la siguiente sección _Subroutes_.

### Subroutes

En React Router, las subrutas (sub routes) son rutas que están anidadas dentro de otras rutas. Las subrutas son útiles para crear rutas jerárquicas en una aplicación y para permitir la navegación dentro de componentes anidados.

Veamos el ejemplo anterior usando sub routes:
`App.jsx`

```JavaScript
...
        <Route path="/moreusers" element={<Navigate replace to="/users" />} />
        <Route path="/dashboard/*" element={<Dashboard />}>
          <Route path="welcome" element={<p>Welcome!!!</p>} />
          <Route path="goodbye" element={<p>Good Bye!!!</p>} />
        </Route>
        <Route path="*" element={<NotFound />} />
...
```

Como se puede observar la ruta `<Route>` de `dashboard` ahora tiene una etiqueta de cierre `</Route>` y dentro las sub routes para ese componente `<Dashboard>`, es obvio que el `element` de las sub routes es simple para el ejemplo, pero pueden tratarse de componentes con distintos niveles de complegidad.

Ahora bien, si lo probamos así, los `element` de las sub routes no serán renderizados, por la simple razón que en el componente no esta definido el lugar donde debe ser renderizado.
Para esto `react-router-dom` cuenta con el componente `Outlet` que debe importarse en este caso a `<Dashboar>`.

`Dashboard.jsx`

```JavaScript
import { useNavigate, Link, Outlet } from "react-router-dom";

function Dashboard() {
  const navigate = useNavigate();

  const handleClick = () => {
    navigate("/");
  };

  return (
    <div>
      <h1>Dashboar</h1>
      <button onClick={handleClick}>Logout</button>
      <br />
      <Link to="welcome">Say Welcome</Link>
      <br />
      <Link to="goodbye">Say Good Bye</Link>

      <Outlet />

    </div>
  );
}

export default Dashboard;
```

El `element` de la sub route sera renderizado en la posición en que se coloque `<Outlet>`.
Esta es la forma en la que se ordenan las sub routes y pueden anidarse en sub routes de sub rutes de sub routes etc... según la necesidad de la aplicación.

### Rutas Protegidas

Podemos protejer nuestras rutas de accesos indebidos o comprobando permisos aca dejo un ejemplo de como podria hacerse esto, por medio de un modulo y su llamada desde los `Route` tanto para subrutas con mismo acceso como para rutas individuales.

`ProtectedRoutes.jsx`

```JavaScript
import { Navigate, Outlet } from "react-router-dom";

function ProtectedRoutes({ isAllowed, children, redirectTo="/landing" }) {
  if (!isAllowed) {
    return <Navigate to={redirectTo} />;
  }

  return children ? children : <Outlet />;
}

export default ProtectedRoutes;
```
Puede verse en `ProtectedRoutes` que si recibe sub rutas, este renderizará con `<Outlet />` y si recibe una ruta individual, renderizará con `children`. La `prop` `redirectTo` recibe un valor por defecto y también nos es util para enviarle la ruta de redirección apropiada para cada caso.

`App.jsx`

```JavaScript
// Ejemplo para sub rutas mismo nivel de permiso.
  <Route element={<ProtectedRoutes isAllowed={!!user} />}>
    <Route path="/home" element={<Home />} />
    <Route path="/dashboard" element={<Dashboard />} />
  </Route>
// Ejemplo para rutas individuales
  <Route
    path="/analytic"
    element={
      <ProtectedRoutes
        isAllowed={!!user && user.permissions.includes("analize")}
        redirectTo="/home"
      >
        <Analytic />
      </ProtectedRoutes>
    }
  />
  <Route
    path="/admin"
    element={
      <ProtectedRoutes
        isAllowed={!!user && user.roles.includes("admin")}
        redirectTo="/home"
      >
        <Admin />
      </ProtectedRoutes>
    }
  />
```

## React Redux Toolkit
Una vez creado el proyecto en React, instalamos las librerias redux y redux-toolkit esta ultima nos va a facilitar la vida con redux.
```JavaScript
npm install @reduxjs/toolkit react-redux
```
Una vez instalas las librerias hay que crear el `store`, siguiendo la documentación y la estructura que nos indica, creamos el archivo en `/src/app/store.js` y copiamos la configuración del store.
```JavaScript
import { configureStore } from '@reduxjs/toolkit'

export const store = configureStore({
  reducer: {},
})
```
El store nos retornara un `objeto` con el estado. 
Esto es como crear un `useState()` fuera de la plicación que podra compartirse con los distintos componentes.

Luego importamos el `Provider` en nuestro archivo `index.jsx` (`main.jsx` en vite js) para armar el contexto, encerrando el componente que va a compartir el estado que agregaremos como una propiedad del `Provider`.

`main.jsx`
```JavaScript
import React from "react";
import ReactDOM from "react-dom/client";
import { Provider } from "react-redux";
import { store } from './app/store';
import App from "./App";
import "./index.css";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>
);
```
### Create a Redux State Slice
Hasta aqui configuramos el estado, pero esta vacio. Lo siguiente que debemos crear el/os `reducer`, que son la forma de actualizar los estados y crear operaciones para alterar el estado. Piensa en el `reducer` como el `setStatus()` del `useState()`.

Para crear un `reducer` Redux Toolkit nos ofrece los `createSlice` y `createReducer` Las API usan Immer inside para permitirnos escribir una lógica de actualización "mutante" que se convierta en actualizaciones inmutables correctas.

Para crearlo seguimos la estructura de la documentación `/src/features/<grupo>/<grupoSlice.js>`. No es necesaria esta estructura y los nombres, pero es más ordenada.

`src/features/tasks/taskSlice.js`
```JavaScript
import { createSlice } from '@reduxjs/toolkit';

export const taskSlice = createSlice({
    name: 'tasks',
    initialState: [],
    reducers: {},
});

export default taskSlice.reducer;
```
**Nota:** Como puede verse la importación por default retorna el `reducer`.

Una vez tenemos nuestro `slice` hay que importarlo en nuestro `store.js`. _Hay que tener en cuenta que nuestro store requiere los reducers_, por lo cual importamos el default.
```JavaScript
import { configureStore } from "@reduxjs/toolkit";
import tasksReducer from "../features/tasks/taskSlice";

export const store = configureStore({
  reducer: {
    tasks: tasksReducer,
  },
});
```
### Utilizando el Estado
Para utilizar el estado, `react-redux` nos ofrece `useDispatch` y `useSelector`.
- `useDispatch`: Es para poder traer los datos dentro del estado . Tiene acceso a todo el estado, por lo cual podemos elegir a que parte queremos acceder.
- `useSelector`: Es para seleccionar o traer algo desde el estado.

Aqui importamos dentro del componente el acceso que deseamos del estado.

`App.jsx`
```JavaScript
import "./App.css";
import { useSelector } from 'react-redux'

function App() {

  const tasksState = useSelector(state => state.tasks);
  console.log(tasksState);

  return <div className="App">
    <h1>Hello World!</h1>
  </div>;
}

export default App;
```
Esto es a modo de ejemplo, en el cual muestra el estado por consola. Con esta sintaxis en cualquier componente dentro de la app, puede tener acceso al estado independientemente del anidamiento dentro de la app.

### List
Ejemplo de una lista usando el estado:

`TasksList.jsx`
```JavaScript
import { useSelector } from "react-redux";

function TasksList() {
  const tasks = useSelector((state) => state.tasks);

  return (
    <>
      {tasks.map((task) => (
        <div key={task.id}>
          <h3>{task.title}</h3>
          <p>{task.description}</p>
        </div>
      ))}
    </>
  );
}

export default TasksList;
```
### Create (crear un item nuevo en el estado)
Para agregar datos a nuestro _estado_ dentro de nuestro `state`, debemos declarar las correspondientes acciones en la propiedad `reducers` de nuestro `State Slice` y exportarla destructurandola del `stateSlice.actions`.

`taskSlice.js`
```JavaScript
const initialState = [... Datos iniciales...];

export const taskSlice = createSlice({
  name: "tasks",
  initialState, // esto resumiria initialState: initialState
  reducers: { // aca se declaran las funciones para modificar el estado.
    addTask: (state, action) => {
      return [...state, action.payload];
    },
  },
});

export const { addTask } = taskSlice.actions;
export default taskSlice.reducer;
``` 
Nuestra acciones tienen dos parámetros `state` y `action`, en esta última no le podemos pasar argumentos y es la que nos va a retornar `type` que es el tipo de acción y `payload` en la cual nos retorna los datos que pasamos como argumentos.
```JavaScript
  reducers: { 
    addTask: (state, action) => {
      return [...state, action.payload];
    },
  },
```
Luego de agregar las acciones en nuestro `stateSlice` debemos importar en el componente que va a utilizarlo `useDispatch` de `react-redux` y la acción de nuestro `stateSlice`.

`TaskForm.jsx`
```JavaScript
import { useDispatch } from "react-redux";
import { addTask } from "../features/tasks/taskSlice";
```
Por medio de `useDispatch` utilizaremos nuestra acción `addTask` para modificar el estado, como veremos en la función `handleSubmit`.

`TaskForm.jsx`
```JavaScript
  const dispatch = useDispatch();

  const handleChange = (e) => {
    setTask({
      ...task,
      [e.target.name]: e.target.value,
    });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    dispatch(addTask({
      ...task,
      id: uuid(),
    }));
  };
```
### Delete (borrar un item del estado)
... continuará...

[Documentación](https://redux-toolkit.js.org/)

Recurso para navegador Redux DevTools [Chrome](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd), [Fire Fox](https://addons.mozilla.org/en-US/firefox/addon/reduxdevtools/).

[Tutorial](https://www.youtube.com/watch?v=w2rAP7d6ndg&t=1395s)

## Vite

[Vite](create-react-app) es un generador de proyectos alternativo a `create-react-app` pero mucho mas rapido y con varias ventajas.

### Crear proyecto

```
npm create vite
```

Cuando se ejecute, nos pregunta el nombre del proyecto y los parametros para el mismo ej: lenguaje de programación, framewor, etc...

Una vez que termina, entramos a la carpeta del proyecto y ejecutamos `npm install` para instalar las dependencias del mismo.

Luego para correr la app ejecutamos `npm run dev` que seria el equivalente a `npm start` en React.

Cuando levante el servidor, copiamos el enlace que nos muestra en `local:` y lo pegamos en el navegador, para entrar a nuestra aplicación.

Dentro de src el archivo `main.jsx` es el equivalente en vite de `index.js` en `create-react-app`.

Para crear la versión de desarrolo utilizamos `npm run build`

## TailwindCSS

Tailwind CSS es un framework de CSS, que se parece bastante a este.
Tiene algunas clases ya creadas con nombres descriptivos, evitando que estemos nosotros mismos renombrando nuestras clases. También permite reducir el peso del código CSS cuando esta en modo produccion usando otro módulo llamado PostCSS.

En get started se encuentra la documentación para instalarlo en los distintos entornos y frameworks. En este caso describo la instalación para el framework Vite, dentro de un proyecto ya creado.

```
> npm install -D tailwindcss postcss autoprefixer
> npx tailwindcss init -p
```

El primer comando instala `tailwindcss`, `postcss` y `autoprefixer`, el segundo comando _inicializa_ tailwindcss.

Luego modificamos `tailwind.config.cjs` según el manual, solo las lineas de código indicadas.

```json
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
```

Luego copiamos en `index.css` las siguientes linieas de código.

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

**Nota**: Hay que verificar que `index.css` sea llamado desde `main.jsx`.

A continuación podemos correr nuestro poyecto.

```
npm run dev
```

[Tailwind CSS](https://tailwindcss.com/)

## Boostrap

Documentación [Boostrap](https://getbootstrap.com/)

1. Instalar boostrap `npm i bootstrap@<version>`
2. Importar en `index.js` la hoja de estilos que vamos a usar:
   ```JavaScript
   import "bootstrap/dist/css/bootstrap.min.css"
   ```

## Deploy en GitHub Pages (Para proyecto creado con Vite)

Pasos a seguir:

1. Instalar paquete gh-pages `npm install gh-pages --save-dev`
2. En `package.json` se habrá instalado el nuevo paquete y debemos agregar en scripts la siguiente linea: `"deploy": "gh-pages -d dist"`
   ```json
   "scripts": {
     "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "deploy": "gh-pages -d dist"
   },
   ```
   [gh-pages Documentación](https://www.npmjs.com/package/gh-pages)
3. Entramos a la pagina de Vite que tiene una opción para deploy de paginas estaticas en GitHub Pages. [Vite deploy en GitHub Pages Documentación](https://vitejs.dev/guide/static-deploy.html#github-pages)
4. Establecemos la propiedad `base` en `vite.config.cjs` y entre ` '//'` el nombre del repositorio.
   ```JavaScript
   export default defineConfig({
     plugins: [react()],
     base: '/react-task-example/',
   })
   ```
5. Crear la distribución por medio de `npm run build` esto creara la carpeta `dist` la cual tendra nuestro proyecto listo para el deploy.
6. Crear en GitHub un repositorio para el proyecto.
7. Vamos al proyecto e iniciamos el repositorio con `git init`
8. `git add .` Para agregar los archivos.
9. `git commit -m "first commit"` hacemos el comit al repositorio.
10. Copiamos el enlace que nos da GitHub con el enlace al repositorio en la consola `git remote add origin https://github.com/ariele2002/react-task-example.git`.
11. Ejecutamos `git push -u origin master` para subir el repositorio a GitHub. _Nota_: Observar en el VScode abajo a la izquierda si el `origin` es `main` o `master`.
12. Ir a GitHub, al repositorio, en el menú seleccionar "Actions" dentro de este seleccionar el boton "New Workflow" hacer click en el link " set up a workflow yourself" y pegar el código que dice el instructivo de _Vite_, hacer click en el boton verde "Start commit".
13. Ir al menú "Actions" de nuevo, seleccionar "Deploy static content to Pages", seleccionar "Run workflow" y ejecutar "Run Workflow", verificar antes que el branch sea el correcto.
14. **NO se si esto es necesario** por las dudas lo pongo aca: Ejecutamos `npm run deploy` para que publique nuestro proyecto.
15. Listo el pollo y pelada la gallina!

## Deploy en GitHub Pages (Para proyecto creado create-react-app)

Pasos a seguir:

1. Crear el repositorio en GitHub.
2. Ir a la consola a la carpeta del proyecto, si el proyecto no tiene git inicializado usar `git init`.
3. `git add .` Para seleccionar los archivos del proyecto.
4. `git commit -m "mensaje que se le quiere dar al primer commit"`
5. Usar el comando que muestra GitHub para idicar el repositorio remoto `git remote add origin https://github.com/ariele2002/react-localstorage-tasks-test.git`
6. Usa el comando que indica GitHub para subir el repositorio, _ojo, cambiar en el comando al branch que usa nuestro proyecto (master o main)_. `git push -u origin main`.
7. agregamos en `package.json` `homepage:` para indicarle la raiz de nuesto poyecto, ahi declaramos nuestra homepage y el repositorio:
   ```json
   {...
     "name": "react-taskapp-localstorage",
     "version": "0.1.0",
     "private": true,
     "homepage": "https://ariele2002.github.io/react-localstorage-tasks-test",
    ...}
   ```
8. Instalamos el paquete [gh-pages](https://www.npmjs.com/package/gh-pages) : `npm i gh-pages`
9. Crear dentro de `package.json` el script `"deploy": "gh-pages -d <distribución>`:
   ```json
   "scripts": {
     "start": "react-scripts start",
     "build": "react-scripts build",
     "test": "react-scripts test",
     "eject": "react-scripts eject",
     "deploy": "gh-pages -d build"
   },
   ```
10. Corremos `npm run build` para que cree la carpeta con la distribución `build`
11. Hacemos el `git add .`, `git commit -m "comentario de modificaciones"`, y subimos al repositorio de GitHub `git push origin master`
12. correr `npm run deploy` para que publique la pagina en GitHub.
13. Actualizar la pagina del repositorio y listoooo!!

## Mas Apuntes

### Local Storage

Podemos guardar datos por medio del `localStorage`, este guarda los datos en el navegador con el formato, `clave`/`valor` para crear un item dentro del local storage utilizamos la sintaxis `localStorage.setItem(<clave>, <valor>)`.

```JavaScript
localStorage.setItem('edad', 30);
```

### Local Storage con Arrays y Objetos

`localStorage` cuando se trata de arrys u objetos deben tratarse de forma diferente, pasandolos como un string, para esto usamos `JSON.stringify()`.

```JavaScript
const taskItems = [{name: 'tarea uno'}, {name: 'tarea dos'}, {name: 'tarea tres'}];

localStorage.setItem('task', JSON.stringify(taskItems));
```

Y para recuperar los datos del storage los parseamos con `JSON.parce()`.

```JavaScript
JSON.parse(localStorage.getItem('task'));
```

## If de una sola línea Mas Corto!

Esta sintaxis acorta aún mas un if de una sola linea, por ejemplo antes seria `{showCompleted ? tarea1 : tarea2}` o `{showCompleted ? tarea1 : null}` si no debe hacer nada si no se cumple.

```JavaScript
{showCompleted && (
    <TaskTable
      tasks={taskItems}
      toggleTask={toggleTask}
      showCompleted={true}
    />
  )
}
```

## Operador !!

En JavaScript, el operador `!!` se conoce como el operador de doble negación o también como el operador de coercción a booleano. Este operador toma cualquier valor o expresión y la convierte en un valor booleano, es decir, en `true` o `false`.

La expresión `!!valor` es equivalente a `Boolean(valor)`. Por ejemplo:

```JavaScript
var x = "Hola";
var y = !!x;
console.log(y); // true
```

Aquí, la expresión `!!x` convierte la cadena `"Hola"` en `true` y luego asigna ese valor a la variable `y`.

En resumen, el operador `!!` es útil para convertir cualquier valor a un valor _booleano_, lo que puede ser útil en situaciones como validación de formularios o manejo de valores de respuesta en API.

## Tips y Trucos

### Representar html embebido en un string: (OJO Leer Advertencia antes de usar)

Si tienes un string en el cual parte de su contenido tiene código html y deseas representarlo como tal, debes incluir en el tag el atributo `dangerouslySetInnerHTML={{__html: <string>}}`. Esto es un reemplazo del DOM InnerHTML.

```JavaScript
const texto = "Hola <strong>Mundo!</strong>";

<p className="text" dangerouslySetInnerHTML={{__html: texto}}></p>
```

Salida por pantalla: Hola **Mundo!**

[Documentación](https://es.reactjs.org/docs/dom-elements.html)

#### Advertencia:

**OJO al piojo**, representar directamente código html de un string que puede ser editado por el usuario u ser obtenido de alguna API REST, puede exponer a los usuarios a ataques XSS.
Por lo cual deben satizarse esos strings antes de usar la opción `dangerouslySetInnerHTML={{__html: <string>}}`. Para ello podemos instalar el paquete `dompurify`.

Instalación de dompurify y uso:

1. `npm install dompurify`
2. importar:

```JavaScript
import DOMPurify from "dompurify";
```

3. Aplicar el texto deseado:

```JavaScript
dangerouslySetInnerHTML={{__html: DOMPurify.sanitize(texto)}}
```

[npm dompurify](https://www.npmjs.com/package/dompurify)

### Evaluar una Expresión Matematica de un String

Para ello debe instalarse el paquete para JavaScript y Nodesjs [mathjs](https://mathjs.org/).

La función `evaluate(<string>)` nos retorna el resultado de la expresión.

Instalación y uso:

1. `npm install mathjs`
2. importar la función de la libreria:

```JavaScript
import { evaluate } from 'mathjs';
```

3. Ejemplo de uso:

```JavaScript
let resultado = evaluate('30 / 3 * 5 + 1')
```

resultado es 51.

[mathjs Documentación](https://mathjs.org/)

### Evaluar String Vacio y Sacar Espacios en Blanco.

El método `trim()` nos retorna un nuevo string, al que le remueve los espacios vacios tanto al principio como al final de este. Nos puede servir tanto para evaluar un string vacio, como también remover los espacios vacios en el comienzo y al final de un string.

```JavaScript
let texto = " El texto de Elnesto! ";

if (texto.trim()) { // evalua si el string esta vacio
  texto = texto.trim() // elimina los espaciós al principio y al final del string.
}

Consola> 'El texto de Elnesto!'
```

## Notas CSS

- `user-select: none` No permite seleccionar el texto, bueno para botones hechos con `<div>`
- `flex: 1 1` En el flex item hace que cada elemento tenga el mismo ancho dentro del contenedor.
- `:nth-child(3n + 1)`: Ver en la [documentación](https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-child) como intercalar color para listas.

## Recursos

Módulos y paquetes:

- Módulo de iconos [react-icons](https://react-icons.github.io/react-icons/)
- Excellent intuitive React UI tools [Material UI](https://mui.com/)
- Generador de Avatar aleatorio [Robohash](https://robohash.org)
- Generador de proyectos de React, alternativa a `create-react-app` mas rapida [Vite](https://vitejs.dev/)
- Generador de ids [uuid](https://www.npmjs.com/package/uuid)
