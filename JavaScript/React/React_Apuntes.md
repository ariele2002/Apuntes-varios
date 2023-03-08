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

```
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

  ```
  const myStyle = {fontFamily: 'sans-serif', backgroundColor: '#333', padding: '5px'}

  <div style={ myStyle }>Hola Mundo!</div>
  ```

  Observar en el siguiente ejemplo, que se usan dos pares de llaves `{}` el primero que nos permite escribir JavaScript en la variable y el segundo que conforma el objeto en si.

  ```
  <div style={{backgroundColor: '#333'}}> Hola Mundo!</div>
  ```

### Estructura en JSX

Al igual que en HTML, los elementos pueden ser _anidados_ en JSX para formar estructuras más complejas. Podemos tener _elementos_ dentro de _componentes_, _componentes_ dentro de _elementos_ y _elementos_ dentro de _elementos_.

```
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

```
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
    ```
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

```
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

```
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

```
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

```
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

```
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

Como ya vimos en los _Componentes_ y sus características, estos dividen el código, su lógica y tambén pueden conformar _Componentes_ en archivos individuales, separando la lógica y ser exportados e importados, haciendo que el código sea modular y facil de mantener.<br>
\_Los nombres de Módulos deben comenzar en Mayúsculas.

**Nota**: Una buena práctica que los componentes sean creados dentro de una carpeta "components".

Módulo `Sumamos.js`

```
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

```
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

```
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

```
export function Sumamos() {
...

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

```
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

Al usar dentro del Módulo `export default` al momento de importar, debe darsele un nombre al módulo importado:<br>
Módulo `Product.js`

```
function Product() {
  return <h2>Product</h2>;
}

export default Product;
```

Principal `index.js`

```
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

En este caso debe colocarse una coma segida al nombre del Módulo y entre llaves el nombre del Componente a importar.<br>
Módulo `Product.js`

```
function Product() {
  return <h2>Product</h2>;
}

export function Navbar() {
  return <nav>Navbar</nav>;
}

export default Product;
```

Principal `index.js`

```
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

```
export function EjProps(props) {
    console.log(props);
    return <h2>{JSON.stringify(props)}</h2>;
}
```

Principal `index.js`

```
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

Otro Ejemplo Simple de `props`:<br>
Módulo `EjProps.jsx`

```
export function EjProps(props) {
    return <h2>{props.title}</h2>;
}
```

Principal `index.js`

```
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

```
Texto 1
Texto 2
Texto 3
```

### Destructuring de Props

Props al ser un objeto se le pueden aplicar todas las propiedades y métodos que tienen los mismos. Usando destructurin del ejemplo anterior:

```
// EjProps.jsx

export function EjProps({title}) {
    return <h2>{title}</h2>;
}
```

### Pasando Varios Parametros

Para pasar varios parámetros en el destructuring, se separan estos con una _coma_. Es buena practica en la función que recibe los argumentos poner un valor por defecto ya que si no se envia uno de los parámetros este queda como `undefined` y no se muestra en el HTML de la interfaz.

`index.js`

```
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

```
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

```
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

```
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

  ```
  export function Button({ text='Some text' }) {
   console.log(text);
   return <button>{text}</button>;
  }
  ```

  `index.js`

  ```
  root.render(
  <>
    <Button text="Click me" />
    <Button text="Pay" />
    <Button />
  </>
  ```

  Salida por consola:

  ```
  > Click me
  > Pay
  > Some text
  ```

- _PropTypes_: Es una libreria para definir el tipo y propiedades de las variables. Se instala y se invoca los métodos de la libreria. [Documentación](https://www.npmjs.com/package/prop-types)

  ```
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

```
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

```
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

```
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

```
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

En un principio React armaba sus componentes como clases, en el componente se importabla `Component` desde `react` y _exportaba_ una clase extendida a `Component` y dentro de la misma se usaba `render()` para retornar una interfaz.

```
import { Component } from "react";

export class Saludar extends Component {
  render() {
    return <h2>Hello Word!</h2>;
  }
}
```

**NOTA:** Este procedimiento hace el código mas dificil de mantener y mas engorroso, en la actualidad fue reemplazado por la programación funcional que es el mas nuevo y es el mas utilizado actualmente. Pero a nivel de aprendizaje se explica el uso, de momento en React no fue deprecado y se sigue utilizando en algunos lugares.

Antes de se utilizaban componentes de clase para poder manejar los estados, esto fue resuelto con `useState` que veremos mas adelante en _hooks_.

## Event Handlers (Manejador de Eventos, Event Listeners)

En React agregar un _event handler (event listener)_ se realiza de esta manera:

`EventHandlers.jsx`

```
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

```
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

### Formularios y Submit

En el caso de los formularios (`form`) cuando se hace el `submit` la página se refresca, después de enviar los datos. En React _nosotros vamos a tomar el control de los datos_ los procesamos y decidimos como enviarlos, por lo cual vamos a evitar que se refresque la página utilizando `preventDefault()`.

`EventHandlers.jsx`

```
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

`FetchApi.jsx`

```
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

**Esto es a modo de ejemplo hay que mejorarlo con asincronía (async/await)**

## Módulos de Terceros

No siempre hay que reinventar la rueda React tiene una gran comunidad Open Source y también soporte de sus creadores como Facebook, por lo cual hay módulos útiles que se pueden implementar facilmente en nuestro proyecto.

Aca hacemos un ejemplo utilizando un _módulo_ de terceros aplicandolo en el ejemplo anterior. Primero instalamos el _módulo_ según su documentación [Módulo de iconos](https://react-icons.github.io/react-icons/). Luego la importamos y utilizamos para poner un icono en el boton.

```
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

```
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

```
import { useState } from "react";
```

Para crear un estado debe ejecutarce la función `useState()` y como argumento el valor inicial. Esto retorna un array con la variable y la función que modifica esta ultima. ej: `const [variable, setVariable] = useState(valor_inicial)`. El nombre de la función debe llevar `set` precediendo el nombre de la variable en camelcase.

```
const [counter, setCounter] = useState(0);
```

Ejemplo de uso de `useState` en el módulo `Hooks.jsx`

```
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

```
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
    ```
    `useEffect(() => {...});
    ```
  - Se ejecuta **solo al iniciar** la app, observese que la dependencia se declara **vacia**.
    ```
    `useEffect(() => {...}, []);
    ```
  - Se ejecuta al **iniciar** la app y solo cuando el/los **estado/s declarado/s** en la dependencia se modifica/n.
    ```
    `useEffect(() => {...},[estado1, estado5]);
    ```

[Documentación React Hooks](https://reactjs.org/docs/hooks-intro.html)

## Contexto de React

Es la mejor forma de poder compartir el **estado** y **métodos** con el resto de los componentes. El _contexto_, es un _componente_ que engloba al resto de los elementos de la app, los cuales pueden acceder a los valores del contexto directamente, sin tener que pasarlo de componente a componente.

### Crear el Contexto

Siguiendo la buenas practicas, creamos una carpeta "context" y dentro creamos el módulo del contexto. En este caso para el ejemplo creamos el módulo `TaskContext.jsx`. Con el cual vamos a manejar los _estados_, los _métodos_ para modificarlos y los _datos_ que recibimos de un archivo o una API REST.

**createContext** es la libreria de React que debemos importar para crear el contexto.

```
import { createContext, useState, useEffect } from "react";
import { tasks as data } from "../data/tasks";
```

Asignamos a una variable con el nombre de nuestro módulo el retorno de la función **createContext()** y la exportamos, esta contendra el nombre de nuestro contexto y almacenara los datos de la misma.

```
export const TaskContext = createContext();
```

Creamos una función que va a _englobar_ el resto de los elementos de la app. Este sera nuestro **ContextProvider** y se exporta. Siguiendo nuestro ejemplo la nombramos `TaskContextProvider`. Esta va a recibir como argumentos en `props` los elementos de la app que representamos con `props.children` y retornaremos en el tag `<TaskContext.Provider>`

```
export function TaskContextProvider(props) {

  return (
    <TaskContext.Provider>
      {props.children}
    </TaskContext.Provider>
  );
}
```

El contexto se representa en `main.jsx` importando `TaskContextProvider` del módulo `TaskContext` y poniendo como hijo del tag `<TaskContextProvider>` a `<App/>` en el render de "root". De esta forma queda listo el contexto para compartir atributos y métodos con el resto de los componentes.

```
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

Como es un componente, comparte sus propiedades de igual manera que estos, pasando sus propiedades y métodos como valores en el tag. En este caso un objeto con estos ultimos.

**Nota**: Es una buena practica usar objetos ya que hace mucho más facil de mantener la aplicación al agregar nuevas propiedades al componente del contexto.

`TaskContext.jsx`

```
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

```
import { useState, useContext } from "react";
```

Luego importamos al módulo nuestra variable `TaskContext` a la que fue asignada el retorno de `createContext()` en el módulo `TaskContext.jsx`.

```
import { TaskContext } from "../context/TaskContext";
```

Ya teniendo disponible el `useContext` y `TaskContext` procedemos a utilizar solo las propiedades que necesite el módulo usando destructuring del retorno de `useContext(<contexto>)`, para asignarlo a una variable dentro de nuestra función `TaskForm` en el módulo.

```
const { createTask } = useContext(TaskContext);
```

De esta manera ya podemos utilizar el método del contexto `createTask` en nuestro módulo, como muestra el siguiente ejemplo:

`TaskForm.jsx`

```
function TaskForm() {...

  const handleSubmit = (e) => {
    e.preventDefault();
    createTask({ title, description });
  };
...}
```

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

```
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
```

Luego copiamos en `index.css` las siguientes linieas de código.

```
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
   ```
   import "bootstrap/dist/css/bootstrap.min.css"
   ```

## Deploy en GitHub Pages (Para proyecto creado con Vite)

Pasos a seguir:

1. Instalar paquete gh-pages `npm install gh-pages --save-dev`
2. En `package.json` se habrá instalado el nuevo paquete y debemos agregar en scripts la siguiente linea: `"deploy": "gh-pages -d dist"`
   ```
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
   ```
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
   ```
     "name": "react-taskapp-localstorage",
     "version": "0.1.0",
     "private": true,
     "homepage": "https://ariele2002.github.io/react-localstorage-tasks-test",
   ```
8. Instalamos el paquete [gh-pages](https://www.npmjs.com/package/gh-pages) : `npm i gh-pages`
9. Crear dentro de `package.json` el script `"deploy": "gh-pages -d <distribución>`:
   ```
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

```
localStorage.setItem('edad', 30);
```

### Local Storage con Arrays y Objetos

`localStorage` cuando se trata de arrys u objetos deben tratarse de forma diferente, pasandolos como un string, para esto usamos `JSON.stringify()`.

```
const taskItems = [{name: 'tarea uno'}, {name: 'tarea dos'}, {name: 'tarea tres'}];

localStorage.setItem('task', JSON.stringify(taskItems));
```

Y para recuperar los datos del storage los parseamos con `JSON.parce()`.

```
JSON.parse(localStorage.getItem('task'));
```

## If de una sola línea Mas Corto!

Esta sintaxis acorta aún mas un if de una sola linea, por ejemplo antes seria `{showCompleted ? tarea : tarea}`

```
{showCompleted && (
    <TaskTable
      tasks={taskItems}
      toggleTask={toggleTask}
      showCompleted={true}
    />
  )
}
```

## Tisp y Trucos
### Representar html embebido en un string: (OJO Leer nota antes de usar)
Si tienes un string en el cual parte de su contenido tiene código html y deseas representarlo como tal, debes incluir en el tag el atributo `dangerouslySetInnerHTML={{__html: <string>}}`. Esto es un reemplazo del DOM InnerHTML.
```
const texto = "Hola <strong>Mundo!</strong>";

<p className="text" dangerouslySetInnerHTML={{__html: texto}}></p>
```
Salida por pantalla: Hola **Mundo!**

[Documentación](https://es.reactjs.org/docs/dom-elements.html)

#### Nota:
OJO al piojo, representar directamente código html de un string que puede ser editado por el usuario u ser obtenido de alguna API REST, puede exponer a los usuarios a ataques XSS.
Por lo cual deben satizarse esos strings antes de usar la opción `dangerouslySetInnerHTML={{__html: <string>}}`. Para ello podemos instalar el paquete `dompurify`.

Instalación de dompurify y uso:
1. `npm install dompurify`
2. importar: `import DOMPurify from "dompurify";`
3. Aplicar el texto deseado: `dangerouslySetInnerHTML={{__html: DOMPurify.sanitize(texto)}}`

[npm dompurify](https://www.npmjs.com/package/dompurify)

## Recursos

Módulos:

- Módulo de iconos [react-icons](https://react-icons.github.io/react-icons/)
- Excellent intuitive React UI tools [Material UI](https://mui.com/)
- Generador de Avatar aleatorio [Robohash](https://robohash.org)
- Generador de proyectos de React, alternativa a `create-react-app` mas rapida [Vite](https://vitejs.dev/)
