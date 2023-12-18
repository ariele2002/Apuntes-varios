# Apuntes Godot Engine

## Autoload o Singleton
Son nodos o scripts que se cargan automáticamente al iniciar el proyecto y se mantienen en memoria durante toda la ejecución. Esto tiene varias ventajas, puedes acceder a ellos desde cualquier escenario o script, sin necesidad de instanciarlos o buscarlos con get_node(). Puedes guardar información global que necesites compartir entre diferentes escenas, como el inventario del jugador, el puntaje, la vida, etc... Puedes manejar los cambios de escenas y las transiciones entre ellas desde un solo lugar.

### Crear un Autoload o Singleton
Para crearlo debes ir al paso de menú de la barra de tareas `Project` luego `Project settings` y a la pestaña `Autoload` allí en el icono de la `carpeta` puedes agregar cualquier escena o script que quieras que se cargue automaticamente al inicio.<br> 
Cada autoload debe que tener un nombre **unico** y sera el nombre del `nodo` en el árbol de escenas.<br>
El orden de los autoload determina el orden en que se cargan y se agregan en el arbol de escenas (Scene).
#### Ejemplo
Si quieres crear un `Autoload` que sea un `script` que hereda de `node` y que contenga `funciones` para cambiar de escena, guardar datos, etc... Tendrias que hacer lo siguiente:
- Crear antes una carpeta `scripts` en el raiz del proyecto para ser mas ordenados porfa!
- Crear un script vacio: Ir al `FileSystem` (margen izq abajo), seleccionar la carpeta `scripts` que creamos, `click derecho` seleccionar `Create New` y `Script`.
- En la plantilla de creación colocar los siguientes datos si no estan por defecto:
  - Language: Gdscript
  - inherits: Node
  - Template: Empty
  - Built-in Script: On
  - Path: aca cambiamos el nombre del archivo a `global.gd`
  - Hacer doble click sobre global.gd para editarlo y agregar todo lo que se necesite.
  - Ir al paso de menú de la barra de tareas `Project` luego `Project settings` y a la pestaña `Autoload` allí en el icono de la `carpeta` puedes seleccionar `global.gd`
  - En `Node Name: GLOBAL` colocar el nombre en mayusculas, esto se hace para identificar los nodos globales.
  - Seleccionar Add y listo.
  
  Ya en este punto tienes un `Autoload` llamado `GLOBAL` del cual puedes acceder desde cualquier parte del juego.
  ```py
  # global.gd
  extends Node

  var score: int
  ```
  ```py
  # prueba01.gd
  extends Node

  var my_score = GLOBAL.score
  ```
## Señales Signals
Las señales son una forma muy poderosa y sencilla de crear interacciones dinamicas y reactivas entre los elementos de nuestro juego, sin tener que escribir mucho código ni depender de variables globales.

_¿Que son las señales?:_ Las señales son eventos que se emiten cuando ocurre algo en un objeto, por ejemplo, cuando un boton es presionado, cuando una animación termine, cuando una colición ocurre, etc... Estos eventos pueden ser capturados por otros objetos que se suscriben a las señales y asi ejecutar una acción en respuesta. 

_¿Como funcionan las señales?:_ Las señales funcionan mediante dos pasos, **emitir** y **conectar**.
- Emitir: Es enviar un mensaje a todos los objetos que estan escuchando.
- Conectar: Conectar es establecer una conexión entre un objeto emisor y un objeto receptor y definir la función que se va a ejecutar cuando la acción sea emitida.

En Godot 4 podemos emitir y conectar señales de dos formas, desde el panel de señales `Panel derecho, pestaña Node, Signal` esto posterior a elegir un objeto emisor en `Panel izquierdo, Escene` seleccionando un objeto o creandolo. Ir al panel de Señales (Signals) click derecho en la señal y seleccionar `connect...` y aparecera el panel para conectarlo.

Otra forma de conectar y emitir señales, es por código.

Emisor:
```py
extends Button

signal hit(value) # Podemos pasarle cuantos parametros queramos seguidos de comas.
# signal hit -> Esto también seria valido, podemos declarar una señal sin necesidad de pasarle parametros

var damage: int # hit se refiere a un golpe, por lo tanto damage es la cantidad de daño.

func _on_body_entered(body):
	emit_signal("hit", damage) # Y aca le indicamos que emita la señal "hit" y le pasamos el valor del parámetro.
```
Receptor:
```py
var life = 10

func ready():
    enemy.hit.connect(take_damage) # Ahora cuando la señal se emita, la recibira el player y ejecutara la función take_damage

func take_damage() -> void:
    life -= 1
```