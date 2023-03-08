# Manipulación del DOM Apuntes
## ¿Que es DOM?
El HTML DOM (Document Object Model) es un estándar sobre cómo obtener, cambiar, agregar o eliminar elementos HTML. Cuando una página web es cargada, el navegador crea un DOM en forma de un árbol de objetos, cada uno con sus propiedades, atributos, métodos y estos pueden ser enteramente manipulados por javascript.
<h3 style="text-align: center">The HTML DOM Tree of Objects</h3>
<p style="text-align: center">
<img src="https://www.w3schools.com/js/pic_htmltree.gif" alt="DOM tree" caption="The HTML DOM Tree of Objects">
</p>

Con el modelo de objetos, JavaScript obtiene toda la potencia que necesita para crear HTML dinámico:
- JavaScript puede cambiar todos los *elementos* HTML de la página.
- JavaScript puede cambiar todos los *atributos* HTML de la página.
- JavaScript puede cambiar todos los *estilos* CSS en la página.
- JavaScript puede eliminar los *elementos* y *atributos* existentes en el HTML.
- JavaScript puede añadir nuevos *elementos* y *atributos* HTML.
- JavaScript puede *reaccionar* a todos los *eventos* HTML existentes.
- JavaScript puede crear nuevos *eventos* HTML en la página.

## Seleccionar Elementos del DOM
Para seleccionar elementos del DOM tenemos distintos métodos que se aplican al `document`.
### `.getElementById()`
Selecciona el elemento por su `id`, recordemos que el id debe ser unico e irrepetible para cada elemento. Retorna una referencia al objeto Element, o null si un elemento con el `id` especificado no se encuentra en el documento.
```
const title = document.getElementById('main-heading');
console.log(title);

> <h1 id="main-heading">
```
### `.getElementByClassName()`
Retorna un objecto similar a un array de los elementos hijos que tengan todos los nombres de clase indicados. Cuando es llamado sobre el objeto `document` , la busqueda se realiza en todo el `document`, incluido el `nodo raíz`. También puedes llamar `getElementsByClassName()` sobre cualquier elemento; en ese caso retornara sólo los elementos hijos del elemento raíz indicado que contengan los nombres de clase indicados.
#### Sintaxis
`<elementoRaiz>.getElementsByClassName('<clase>')`, si se busca por mas de una `clase` deben separarse por espacio.
```
const listItems = document.getElementByClassName('list-item');
console.log(listItems);

> HTMLCollection { 0: li.list-items, 1: li.list-items, 2: li.list-items, 3: li.list-items, 4: li.list-items, length: 5 }
```
### `.getElementByTagName()`
Devuelve una lista de elementos que tienen un `tag name` determinado. Se explora el árbol por debajo del elemento dado, excluyendo el propio elemento.<br>
#### Sintaxis
`<elementoRaiz>.getElementByTagName('<tagName>')`, si se utiliza `'*'` que representa todos los elementos, eso mismo es lo que va a retornar.
```
const byTagName = document.getElementsByTagName('li');
console.log(byTagName);

> HTMLCollection { 0: li.list-items, 1: li.list-items, 2: li.list-items, 3: li.list-items, 4: li.list-items, length: 5 }
```
### `.querySelector()`
Devuelve el *primer* elemento del documento (utilizando un recorrido primero en profundidad pre ordenado de los nodos del documento) que coincida con el grupo especificado de selectores. (solo el primero que encuentre ojo al piojo).
#### Sintaxis
`<ElementoRaiz>.querySelector(<uno-o-mas-selectores-CSS>)`
```
const elemento = document.querySelector(".miClase");
```
#### Ejemplo más útil
Los Selectores pueden ser muy útiles como se demostrará en el siguiente ejemplo. Aquí, será retornado el primer elemento `<input name="login" />` dentro de `<div class="user-panel main">`.
```
const elemento = document.querySelector("div.user-panel.main input[name='login']");
```
### `.querySelectorAll()`
El método querySelectorAll() de un Document devuelve una NodeList estática (no viva) que representa una lista de elementos del documento que coinciden con el grupo de selectores indicados.
#### Sintaxis
`<elementoRaiz>.querySelectorAll('<uno-o-mas-selectores-CSS>)`
```
const containers = document.querySelectorAll('div');
console.log(containers);

> NodeList [ div.container, div]
0: <div class="container">​
1: <div>
length: 2
<prototype>: NodeListPrototype { item: item(), keys: keys(), values: values(), … }
```
## Dar Estilos a los Elementos
Para dar estilo a los elementos se utiliza `<elemento>.style.<atributo> = <valor>`, cuando el atributo esta separado por `-` se utiliza camelcase ej: `font-size` es `fontSize`.
```
const title = document.querySelector('#main-heading');
title.style.color = 'red';

console.log(title);
> <h1 id="main-heading" style="color: red;">
```
Varios elementos de una NodeList:
```
const listItems = document.querySelectorAll('.list-items');

// Forma tradicional
for(let i=0; i < listItems.length; i++) {
    listItems[i].style.fontSize = '2rem';
}

// Usando array methods
listItems.forEach(item => item.style.fontSize = '2rem');

console.log(listItems);

> 0: <li class="list-items" style="font-size: 2rem;">​
  1: <li class="list-items" style="font-size: 2rem;">...
```
## Crear, Agregar y Modificar Elementos
### `.createElement('<element>)`
Crea el elemento especificado en el argumento:
```
const ul = document.querySelector('ul');
const li = document.createElement('li');
```
### Agregar elemento
Es tan simple como agregar un elemento en un objeto, en este caso en el NoneList.
```
ul.append(li);
```
### Modificando el texto `.innerText`
```
li.innerText = 'X-Men`;
```
### Modificando Atributos y Clases
#### Atributos
`.setAttribute('<atributo>', '<valor>')`: Establece el valor de un atributo en el elemento indicado. Si el atributo ya existe, el valor es actualizado, en caso contrario, el nuevo atributo es añadido con el nombre y valor indicado.
```
li.setAttribute('id', 'main-heading');
console.log(li);

> <li id="main-heading">
```
`.getAttribute('<atributo>')`: devuelve el valor del atributo especificado en el elemento. Si el atributo especificado no existe, el valor retornado puede ser tanto `null` como `""`, dado que `null` es lo que especifica la norma, algunas aplicaciones usan la especificacion anterior que retornan `""`, por lo que es recomendable comprobar con `<element>.hasAttribute('<atributo>')` antes de usar `.getAttribute()`.
```
console.log(li.getAttribute('id'));

> main-heading
```
`removeAttribute('<atributo>')`: Elimina un atributo del elemento especificado.
```
li.removeAttribute('id');
console.log(li);
```
#### Clases
`.add('clase')`: Agrega una clase al elemento, si fueran mas de una deben separarse por comas.
```
li.classList.add('list-items');
console.log(li);

> <li class="list-items" style="font-size: 2rem;">
```
`.contains('<clase>')` Retorna `true` si el elemento tiene la clase indicada o `false` en caso contrario.
```
console.log(li.classList.contains('list-items'));
> true
```
`.remove('<clase>')`: Elimina la clase indicada del elemento, eliminando el valor, pero no el atributo `class`.
```
li.classList.remove('list-items');
console.log(li);

> <li class="" style="font-size: 2rem;">
```
`.toggle('<clase>')`: *Cuando sólo hay un argumento presente:* Alterna el valor de la clase; ej., si la clase existe la elimina y devuelve `false`, si no, la añade y devuelve `true`. *Cuando el segundo argumento está presente:* Si el segundo argumento se evalúa como true, se añade la clase indicada, y si se evalúa como false, la elimina.
```
li.classList.add('list-items');
console.log(li);
li.classList.toggle('list-items');
console.log(li);
li.classList.toggle('list-items');
console.log(li);

> <li class="list-items" style="font-size: 2rem;">
> <li class="" style="font-size: 2rem;">
> <li class="list-items" style="font-size: 2rem;">
```
`.replace('<clase-vieja>','<clase-nueva'>)`: Reemplaza una clase existente por una nueva.
```
console.log(li);
li.classList.replace('list-items', 'prueba-class');
console.log(li);

> <li class="list-items" style="font-size: 2rem;">
> <li class="prueba-class" style="font-size: 2rem;">
```
## Recorrer el Arbol del DOM
Para tener un control del árbol del DOM tenemos que saber como movernos dentro del mismo y saber la relación de parentesco de los elementos.
### Recorriendo Nodos Padre
- `<elemento>.parentNode` nos retorna en nodo padre del elemento.
- `<elemento>.parentElement` nos retorna el elemento padre del elemento.
```
let ul = document.querySelector('ul');

console.log(ul.parentNode);
console.log(ul.parentElement);

> <div class="container">
> <div class="container">
```
Asi mismo podemos ver quien es el padre del padre hasta la ultima rama del árbol.
```
let ul = document.querySelector('ul');

console.log(ul.parentNode.parentNode);
console.log(ul.parentElement.parentElement);

> <body>
> <body>
```
El elemento final es la raiz del árbol, que es `document` y este no tiene un elemento padre que lo contenga.
```
const html = document.documentElement;

console.log(html);
console.log(html.parentNode);
console.log(html.parentElement);

> <html lang="en">
> HTMLDocument
> null
```
### Recorriendo Nodos Hijos
- `<elemento>.childNodes` nos retorna un `NodeList` en el cual toma como elemento del nodo las indentaciones y saltos de linea.
- `<elemento>.firstChild` nos retorna el primer hijo (elemento) en el NodeList.
- `<elemento>.lastChild` nos retorna el último hijo (elemento) en el NodeList.
```
let ul = document.querySelector('ul');

console.log(ul.childNodes);
console.log(ul.firstChild);
console.log(ul.lastChild);

> NodeList(11) [ #text, li.list-items, #text, li.list-items, #text, li.list-items, #text, li.list-items, #text, li.list-items, … ]
> #text "\n            "
> #text "\n            "
```
Se ve claramente que esta bien a nivel informativo pero es poco practico para trabajar. Para ello tenemos
- `<elemento>.children` nos retorna un `HTMLCollection` con los elemento HTML hijos.
- `<elemento>.firstElementChild` nos retorna el primer elemento hijo.
- `<elemento>.lastElementChild` nos retorna el último elemento hijo.
```
let ul = document.querySelector('ul');

console.log(ul.children);
console.log(ul.firstElementChild);
console.log(ul.lastElementChild);

> HTMLCollection { 0: li.list-items, 1: li.list-items, 2: li.list-items, 3: li.list-items, 4: li.list-items, length: 5 }
> <li class="list-items">
> <li class="list-items">
```
### Recorriendo Nodos Hermanos
- `<elemento>.previousElementSibling` nos retorna el elemento hermano anterior al elemento en cuestion.
- `<elemento>.nextElementSiblin` nos retorna el elemento posterior al elemento en cuestion.
```
let ul = document.querySelector('ul');

console.log(ul.previousElementSibling);
console.log(ul.nextElementSibling);

> <h1 id="main-heading">
> null
```
## Event Listeners
- Los **eventos** son las acciones que puede realizar el usuario, al realizar un evento se produce una serie de acciones.
- Los **Listeners** (oyentes o escuchadores en español) se encargan de controlar los eventos, esperan a que el evento se produzca y realiza una serie de acciones.
### `addEventListener()`
Agrega un controlador de eventos a un elemento del DOM.<br>
#### Sintaxis
`<element>.addEventListener("<event>", <function>, <useCapture>)`
Paranetros:
- `event` *Requerido*, nombre del evento, referencia: [DOM Event Object](https://www.w3schools.com/jsref/dom_obj_event.asp)
- `function` *Requerido*, función que sera llamada cuando se cumpla el evento.
- `useCapture` *Opcional*, por default tiene el valor `false`. Si su valor es `false`, el controlador se ejecuta en la fase de burbuja (bubbling)propagando el evento de forma ascendente.<br>Si su valor es `true`, el controlador se ejecutara en la fase captura (capture) propagando el evento en forma descendente.
#### Valor de retorno
`NONE`
#### Ejemplos
```
// Agrega un evento al hacer click en el boton 2 con un alert.
const buttonTwo = document.querySelector('.btn-2');

function alertBtn() {
    alert('I also love JavaScript!');
};

buttonTwo.addEventListener("click", alertBtn);
```
Ejemplo anterior con sintaxis moderna
```
document.querySelector('.btn-2').addEventListener("click", () => alert('Mismo que el anterior con sintaxis moderna'));
```
Cambiar color de forndo cuando el mouse pasa sobre el elemento.
```
const newBackgroundColor = document.querySelector('.box-3');

function changeBgColor() {
    newBackgroundColor.style.backgroundColor = 'blue';
};

newBackgroundColor.addEventListener("mouseover", changeBgColor);
```
Revelar u ocultar un elemento usando clases.
```
// Reveal Event

// Script
const revealBtn = document.querySelector('.reveal-btn');

const hiddenContent = document.querySelector('.hidden-content');

function revealContent() {
    if(hiddenContent.classList.contains('reveal-btn')) {
        hiddenContent.classList.remove('reveal-btn');
    } else {
        hiddenContent.classList.add('reveal-btn');
    }
}

revealBtn.addEventListener("click", revealContent);

// CSS
.hidden-content {
    display: none;
}

.hidden-content.reveal-btn {
    display: block;
}
```
Versión anterior pero mas corta usando función `flecha` y el método del `classList`,`toggle`.
```
// Reveal Event

const revealBtn = document.querySelector('.reveal-btn');

const hiddenContent = document.querySelector('.hidden-content');

revealBtn.addEventListener("click",() => hiddenContent.classList.toggle('reveal-btn'));
```
## Propagación de Eventos (Event Propagation)
Los eventos en javaScript no se detienen en el elemento que los disparó, si no que se *propagan*. La progapación se hará a todos sus ancestros hasta llegar al *último* nodo padre.
### Captura de Eventos
Cuando ejecuto una acción y produzco un evento (ejemplo click) se producen 3 fases para que se activen los handlers del evento:
- 1ra. *Capturing*: Captura, esta se ejecuta de forma descendente en el árbol del DOM. Buscando desde el elemento padre con mayor gerarquia descendiendo hasta localizar el elemento del DOM más profundo en el que se halla producido el evento.
- 2da. *Target*: Esta fase lo que hace es ver si el elemento del DOM más profundo en el que se halla producido el evento, tiene un listener asociado a ese evento.
- 3ra. *Bubbling* (no siempre): En esta fase se ejecuta la acción de ese evento y luego va ascendiendo por el árbol del DOM buscando si en los elementos padres hay un *listener* para ese mismo *evento*, ejecutando de forma ascendente las acciónes de dichos listeners.
- Nota: No todos los *eventos* tienen esta 3ra. fase del *Bubbling*. Para verificar si un *evento* tiene *Bubbling*, ademas de la documentación correspondiente, se puede chequear el atributo `bubbles` del evento si es `true`:
    ```
    document.querySelector("button").addEventListener("click", function(event){
    console.log(event.bubbles);
    });
    
    > true
    ```

### Event Bubbling
La propagación de forma ascendente se la llama `Event bubbling` evento burbujeante, ya que este comportamiento simula a las burbujas ascendiendo a la superficie.<br> En la sintaxis del *eventListener()*: `<element>.addEventListener("<event>", <function>, <useCapture>)` el último parámetro por defecto es `false` por lo cual el `Event bubbling` es el activo por defecto, buscando y ejecutando de forma ascendente en el árbol del DOM las acciones de los listeners asociados con ese evento. En el ejemplo se coloca este parámetro a modo demostrativo, ya que no es necesario.
```
// Event propagation Event bubbling

window.addEventListener("click", function(){
    console.log('Window');
}, false);

document.addEventListener("click", function(){
    console.log('Document');
}, false);

document.querySelector(".div2").addEventListener("click", function(){
    console.log('DIV 2');
}, false);

document.querySelector(".div1").addEventListener("click", function(){
    console.log('DIV 1');
}, false);

document.querySelector("button").addEventListener("click", function(e){
    console.log(e);
}, false);

> click { target: button, buttons: 0, clientX: 325, clientY: 223, layerX: 325, layerY: 223 }
> DIV 1
> DIV 2
> Document
> Window
```
### Event Capture
El `Event Capture` hace lo mismo que el `Event Bubbling` pero de forma *descendente*, para activarlo solo es necesario cambiar el ultimo parámetro del `<element>.addEventListener("<event>", <function>, <useCapture>)` a `true`.

### stopPropagation()
La *propagación de eventos* puede generar efectos indeseados al ejecutar las acciones de los listeners asociados al evento en la rama del DOM con relación a los padres del elemento. Para evitar esta propagación y que solo ejecute el evento relacionado al listener del elemento en cuestion se utiliza el método del evento `stopPropagation()`.<br>
Si modificamos el último procedimiento del código de ejemplo anterior tendremos el siguiente resultado:
```
document.querySelector("button").addEventListener("click", function(e){
    e.stopPropagation();
    console.log(e);
}, false);

> click { target: button, buttons: 0, clientX: 308, clientY: 222, layerX: 308, layerY: 222 }
```
El método `stopPropagation()` detendra la propagación del evento en el punto en el que sea utilizado, veamos utilizando el ejemplo mencionado anteriormente pero aplicando el método en el 3er procedimiento:
```
document.querySelector(".div2").addEventListener("click", function(e){
    e.stopPropagation();
    console.log('DIV 2');
}, false);

> click { target: button, buttons: 0, clientX: 327, clientY: 224, layerX: 327, layerY: 224 }
> DIV 1
> DIV 2
```
### preventDefault()
El método `preventDefault()` cancela el evento si este es cancelable, sin detener el resto del funcionamiento del evento, es decir, puede ser llamado de nuevo. Llamar a `preventDefault()` en cualquier momento durante la ejecución, cancela el evento, lo que significa que cualquier acción por defecto que deba producirse como resultado de este evento, no ocurrirá. Por ejemplo:
- Al hacer click en el boton "Submit", evita que envie el formulario.
    ```
    document.getElementById("myForm").addEventListener("submit", function(event){
        event.preventDefault();
    });
    ```
- Al hacer click en un link, evita que el enlace siga a la URL.
    ```
    document.getElementById("myLink").addEventListener("click", function(event) {
        event.preventDefault();
    });
    ```

No todos los eventos son cancelables y si se utiliza `preventDefault()` en un evento no cancelable, no tendra efecto alguno. Ademas de la documentación de los eventos, una forma de saber si un evento es cancelable o no, use el atributo `cancelable` del evento.
```
document.querySelector("button").addEventListener("click", function(e){
    console.log(e.cancelable);
}, false);

> true
```
El método `preventDefault()` no detiene la propagación del evento, para eso debe usar el método `stopPropagation()`.
### Ejecutar Solo Una Vez Un Evento
Para que un evento se ejecute solo una vez, al ultimo parámetro del `addEventListener()` le enviamos la clave: valor `{once: true}`.<br>
Basandonos en el ejemplo de propagación del `Event Bubbling`, modificamos el event listener de `.div2` para que se ejecute solo una vez, cuando se realicen mas clicks, el event listener de `.div2` no se ejecutará.
```
document.querySelector(".div2").addEventListener("click", function(e){
    console.log('DIV 2');
}, {once: true});

document.querySelector("button").addEventListener("click", function(e){
    console.log(e.target.innerText = 'Clicked!');
}, false);

// Primer click
> Clicked!
> DIV 1
> DIV 2
> Document
> Window

// Segundo Click
> Clicked!
> DIV 1
> Document
> Window
```
### Ventajas y Desventajas de la Propagación de Eventos
- *Desventajas*: Dado lo ya explicado en cuanto a la propagación de eventos, hay que tener en cuenta sus propiedades en nuestro diseño, para evitar efectos indeseados y errores en nuestra aplicación.
- *Ventajas*: Podemos servirnos de la propagación de eventos para optimizar nuestro código, evitando la duplicidad, haciendo un código más limpio, eficiente y que ahorre recursos, como veremos en la sección *Delegación de Eventos*.
## Delegación de Eventos (Event Delegation)
La delegación de eventos, aprovecha la propagación de eventos utilizando un event listener en el elemento padre, por lo cual se aplica por medio de la propagación a sus elementos hijos, sin tener que colocar un event listener en cada uno de ellos. De esta forma no duplica código y optimiza recursos.<br>
Pongamos el ejemplo de una lista de items o a una sección con articulos que podrian ser 5 o 10000, a los cuales queremos darle un efecto a cada uno cuando se haga un click sobre uno de ellos. En este caso colocar un event listener por cada uno, no seria práctico ni optimo.<br>
En el siguiente ejemplo aplicamos la *delegación de eventos* para una lista de deportes:
```
// Event delegation

document.querySelector('#sports').addEventListener('click', function(event){
    console.log(`${event.target.getAttribute('id')} is cliked!`);

    const target = event.target;

    // hacemos un condicional para que se aplique donde deseamos.
    if (target.matches('li')) {
        target.style.backgroundColor = 'lightgrey';
    }
});

// Si agregamos un item, tendra los mismos efectos que los anteriores.
const sports = document.querySelector('#sports');
const newSport = document.createElement('li');

newSport.innerText = 'Rugby';
newSport.setAttribute('id', 'rugby');

sports.appendChild(newSport);

// Si agregamos un item, tendra los mismos efectos que los anteriores.
const sports = document.querySelector('#sports');
const newSport = document.createElement('li');

newSport.innerText = 'Rugby';
newSport.setAttribute('id', 'rugby');

sports.appendChild(newSport);

> football is cliked!
> rugby is cliked!
> sports is cliked! // este es el contenedor y no se aplican los efectos que de los items por el condicional.
```

## Métodos Utiles
- `<element>.matches('<css_selector>')`, método devuelve `true` si un elemento coincide con un selector CSS específico, de lo contrario retorna `false`.
```
document.querySelector('ul').addEventListener('click', 
    event => console.log(event.target.matches('li')) 
);
```


## Notas al Pie
Nota: Esto es para ver el contenido en cuanto a los distintos aspectos del texto:
```
// html contenido
<li class="list-items"><span>Neo</span>
                The Matrix</li>
// Observar el contenido
const firstListItem = document.querySelector('li');

console.log(firstListItem.innerText);
console.log(firstListItem.textContent);
console.log(firstListItem.innerHTML);
```