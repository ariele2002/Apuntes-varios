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
### Enums
Es un ficture de TypeScript, no pertenece a JavaScript. Los `enums` nos permiten definir un conjunto de constantes con nombre.