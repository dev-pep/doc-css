# Introducción

Para fijar el estilo de la etiqueta `<h1>`, por ejemplo:

```css
h1 {
    color: red;
    font-size: 5em;
}
```

El primer elemento, el ***selector***, selecciona qué elemento de *HTML* estamos estilizando. En este caso, la etiqueta `<h1>`. Dentro de las llaves, las declaraciones tienen forma de propiedad y valor.

Pueden indicarse varios selectores a la vez:

```css
p, li {
    color: green;
}
```

# Primeros pasos

Hay tres formas de enlazar *CSS* en un archivo *HTML*. La más habitual es, dentro de la sección `<head>` incluir:

```html
<link rel="stylesheet" type="text/css" href="estilos.css">
```

Esto carga los estilos definidos en ***estilos.css***. El archivo debe indicarse con una ruta relativa a la ubicación del documento actual (es atributo `type` no es estrictamente necesario). El enlace al archivo sigue la ruta especificada, relativa al documento actual.

Por otro lado, se puede crear una hoja de estilo interna, incluyéndola en la sección `<style>` dentro de la sección `<head>`.

Y por último, se puede definir el estilo de cada elemento por separado (estilo *inline*), mediante el atributo `style`, al que se le dará el valor del estilo deseado. Por ejemplo:

```html
<h1 style="color: blue; background-color: yellow;">Hello</h1>
```

## Definición de estilos

Para cambiar solo cierto elementos de un tipo, y no todos ellos (por ejemplo, solo algunos elementos `<li>`), se puede especificar una clase (`class`) y definir el estilo para esa clase, y no para una etiqueta:

```html
<li>Elemento uno</li>
<li class="especial">Elemento especial</li>
```

Y en el archivo de estilos:


```css
.especial {
    color: orange;
}
```
En caso que queramos especificar el estilo de una clase (por ejemplo ***especial***), pero solo cuando pertenezca a una etiqueta concreta (por ejemplo `<li>`). En este caso usamos un *combinator* como selector:

```css
li.especial {
    color: orange;
}
```

Como siempre, se pueden combinar varios selectores.

Se puede especificar un *descendant combinator*, que es un mecanismo para definir anidamiento de etiquetas. Simplemente se especifican los selectores separados por espacio:

```css
li em {
    color: orange;
}
```

En este ejemplo, se aplicará el estilo a las etiquetas `<em>` que estén anidadas en una etiqueta `<li>`.

Para dar estilo a una etiqueta siempre que vaya justo después de otra (no anidada, sino contigua), se usa este *combinator*:

```css
h1 + p {
    color: orange;
}
```

En este caso se aplicará a los párrafos `<p>` que estén inmediatamente después de los encabezados `<h1>`.

Algunos elementos pueden estilizarse en función de su estado. Por ejemplo, un enlace puede haber sido visitado ya o no; o puede tener el puntero del ratón encima. En este caso se usan los dos puntos (***:***):

```css
a:link {
    color: orange;
}

a:visited {
    color: pink;
}

a:hover {
    text-decoration: none;
}
```

Los selectores y combinadores se pueden usar de cualquier forma deseada:

```css
article p span { ... }
h1 + ul + p { ... }
body h1 + p .especial { ... }
```

El último de los ejemplos define el estilo de las etiquetas con clase ***especial*** que estén dentro de un párrafo `<p>`, el cual esté definido justo después de un encabezado `h1` que esté dentro de la sección `<body>`.

Cuando hay conflicto entre dos estilos, se aplican las reglas de cascada (*cascade*) y especificidad (*specificity*).

```css
p { color: red; }
p { color: blue; }
```

En este caso se aplica cascada: el párrafo será de color azul (está declarado más tarde). Pero en este caso:

```css
.especial { color: red; }
p { color: blue; }
```

Si tenemos este *HTML*:

```html
<p class="especial">Texto</p>
```

El texto será rojo, porque se aplica la especificidad: una clase es más específica que una etiqueta.

Si deseamos que un atributo concreto tenga prioridad, independientemente de las normas mencionadas, añadiremos la etiqueta ***!important***:

```css
.especial {
    font-size: 15px;
    color: red;

}
p {
    font-size: 18px !important;
    color: blue;
}
```

En este caso, la etiqueta `<p class="especial">Texto</p>` pintará el texto de color rojo, pero con un tamaño de 18 píxeles.

En general, cada regla *CSS* está compuesta por un selector, y una serie de pares propiedad/valor separados por dos puntos (***:***) y terminados en punto y coma (***;***). Las propiedades y valores son *case sensitive*.

Si una propiedad es desconocida o se da un valor inválido, la declaración es inválida y es simplemente ignorada. *CSS* admite algunas funciones concretas como valores.

## *@rules*

Las *@rules* (*at rules*) especifican algunas acciones o comportamientos.

```css
@import 'estilos2.css';
```

En este caso, `@import` importa una hoja de estilo dentro de otra. Otra regla importante es `@media`, que tiene acceso al entorno y utiliza lógica condicional:

```css
body { background-color: pink; }
@media (min-width: 30em)
{
    body { background-color: blue; }
}
```

En este caso, se define un fondo rosa, pero si el navegador es más ancho de de ***30em***, el color de fondo será azul.

## *Shorthands*

Las propiedades `font`, `background`, `padding`, `border` y `margin` se denominan *shortdands* porque equivalen a varias propiedades a la vez. Por ejemplo:

```
padding: 10px 15px 15px 5px;
```

Equivale a:

```
padding-top : 10px;
padding-right : 15px;
padding-bottom : 15px;
padding-left : 5px;
```

## Comentarios

Los comentarios en *CSS* son multilínea, del estilo `/* ... */`.

## Espacio blanco

El espacio blanco (espacios, tabuladores y saltos de línea) es ignorado en *CSS*. En una declaración los espacios pueden separar valores, pero las propiedades nunca pueden contener espacio.
