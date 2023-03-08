# Markdown Documentación
**Markdown:** Es la herramienta de conversión de texto-a-HTML para desarrolladores web.<br> Markdown le permite escribir usando una forma sencilla de escritura, lectura en formato de texto plano luego convirtiendolo en una estructura XHML o HTML valido.

## Sintaxis
- `#` Se utiliza como `<h1>` y el nivel sera dado por la repetición consecutiva de `#` ej:
`## <h2>`, `### <h3>` y asi hasta el nivel `<h6>` de titulos.
- `>` Se utiliza como `<blockquote>`<br>
    Ej:<br> 
    `> Este es un blockquote`
    > Este es un blockquote
- `-` Se utiliza como `<ul>`<br>
    Ej: <br>
    `- Item 1`<br>
    `- Item 2`<br>
    - Item 1
    - Item 2 <br>
- En el caso de listas ordenadas `<ol>` se utiliza el indice seguido de punto.<br>
    Ej:<br>
    `1. Item 1`<br>
    `2. Item 2`<br>
    1.  Item 1
    2.  Item 2
- Enfasis en frases: Para dar enfasis se utiliza *, para dar mas enfasis se utilizan dos ** Ej:<br>
    El siguiente texto `*tiene enfasis*`<br>
    El siguiente texto *tiene enfasis*

    El siguiente texto `**tiene enfasis más fuerte**`<br>
    El siguiente texto **tiene enfasis más fuerte**
-   Cursiva en negrita y anidada `**Texto _extremadamente_ importante**`<br>
**Texto _extremadamente_ importante**
- Subindice: `X<sub>1</sub>` <br>Resultado: X<sub>1</sub>
- Superindice: `cm<sup>2<sup>` <br>Resultado: cm<sup>2</sup>

- **Formatear código**: Se utilizan 3 comillas simples invertidas al inicio y al final del código encerrando el bloque. Algunos editores reconocen el lenguaje si agregamos la etiqueta adecuada<br>Ej:
````
```JavaScript
temp_med = temp_max - temp_min
```
````
```JavaScript
    temp_med = temp_max - temp_min
```
- `Links`: Esto es un `[ejemplo de link](http://example.com/)`<br>
<!- Resultado: Esto es un [ejemplo de link](http://example.com/)
- `Imagenes`: `![alt texto](/ruta/a_la/img.jpg "Titulo")` el titulo es opcional.