# Layout

Aquí veremos la disposición de elementos en pantalla (*layout*).

## Box (caja)

La disposición básica en caja (rectangular) tiene estos elementos:
- **Contenido:** en el centro de la caja.
- ***Padding:*** margen interior, entre el contenido y el borde.
- **Borde:** el recuadro visible.
- **Margen:** espacio exterior alrededor del borde.

En cuanto al tamaño de los elementos, se suele usar una medida absoluta para la altura, y una medida relativa para la anchura.

Para establecer las dimensiones del contenido, simplemente, se utilizan las propiedades `height` y `width`.

Para definir el *padding* podemos utilizar el *shorthand* ***padding***. Si especificamos un solo tamaño, lo utilizará para los cuatro márgenes. Si indicamos dos, el primero se usará para el margen superior e inferior, y el segundo para derecha e izquierda. Podemos establecer los cuatro márgenes en este orden: arriba, derecha, abajo, izquierda.

Mediante el *shorthand* `border` podemos definir el borde, especificando, en este orden, el tamaño, estilo y color. El tamaño puede ser cualquier medida que queramos para el grosor del borde. El estilo indica cómo se dibuja el borde, por ejemplo punteado (***dotted***), discontinuo (***dashed***), sólido (***solid***) o doble (***double***). En cuanto al color, cualquier color valdrá.

Los márgenes se pueden definir con el *shorthand* ***margin***. Funciona igual que ***padding***.

```css
.unaclase {
    height: 400px;
    width: 70%;
    padding: 10px;
    border-style: 3px solid blue;
    margin: 25px 30px;
}
```

## *Float* y *display*

La propiedad `float` cambia el flujo de elementos en la página, haciendo que el elemento esté flotando a la izquierda o derecha de la pantalla, de tal forma que el contenido va fluyendo a su lado. Posibles valores de esta propiedad son ***none***, ***left*** o ***right***. Si lo establecemos en ***inherit***, heredará el *float* del elemento padre.

La propiedad `display` cambia la forma de mostrar el elemento. Si le damos el valor ***none***, el elemento desaparece de pantalla.

Hay dos tipos principales de *display*. En el tipo bloque (*block*), el elemento reserva su propio espacio (como `<div>`), incluyendo sus márgenes, y empieza en una línea nueva; al terminar, lo siguiente empezará en otra línea nueva. El tipo *inline* fluye con el resto (como `<span>`), y no reserva un bloque de espacio para sí mismo ni inserta líneas nuevas al empezar o al terminar. Existe un modo intermedio, llamado *inline block* en el que el elemento se reserva un espacio, incluyendo sus márgenes, pero no empieza en línea nueva, ni termina insertando una línea nueva, sino que fluye como un carácter.

Valores posibles de `display` son ***inline***, ***block*** o ***inline-block***.

## *Flexbox*

Es una caja flexible. Esta compuesta por un contenedor (normalmente un contenedor `<div>`) y por los elementos que contiene, que son hijos del contenedor. Los *flexboxes* son útiles como componentes de una página: barra lateral, menú superior, pie, etc. Mucho mejor que un *float*.

Para que el contenedor sea un *flexbox*, hay que darle el valor ***flex*** a la propiedad `display` del mismo.

En un *flexbox* los elementos fluyen de forma distinta. Podemos indicar cómo queremos que lo hagan. La propiedad `flex-direction` nos permite definir la dirección. ***row*** (por defecto) hará fluir de izquierda a derecha, mientras que ***column*** lo hará de arriba a abajo. Si queremos invertir el orden, existen los valores ***row-reverse*** (derecha a izquierda) y ***column-reverse*** (abajo a arriba).

`flex-wrap` permite el *wrap* de los elementos. Valores posibles son ***wrap*** o ***no-wrap*** (por defecto). El valor ***wrap-reverse*** hace que las nuevas líneas se vayan colocando encima.

Para alineación horizontal de los objetos, existe la propiedad `justify-content`. Valores posibles son ***flex-start*** (izquierda del contenedor), ***flex-end*** (derecha), y ***center*** (centro). La alineación ***space-between*** justifica los elementos a derecha e izquierda de tal modo que el espacio entre cada uno de ellos es el mismo. De forma similar, con ***space-around***, el espacio alrededor de cada elemento es el mismo (da un aspecto más centrado).

En cuanto a la alineación vertical, existe la propiedad `align-items`. Por defecto tiene el valor ***stretch*** (estira verticalmente los elementos). Con ***center*** se centran verticalmente. Con ***flex-start*** se situarán en la parte superior, y con ***flex-end*** en la inferior.

A los elementos del contenedor se les puede dar la propiedad *CSS* `order` (por ejemplo con estilado *inline*), con un número, y quedan ordenados de la forma indicada.

Para gestionar el espacio de forma *responsive* en caso de que ampliar o reducir el tamaño del *flexbox*, se le puede dar a los elementos que lo componen las siguientes propiedades:
- `flex-basis` define la anchura mínima del elemento.
- `flex-grow` indica, al ampliarse el *flexbox*, la velocidad de ampliación de la anchura de cada elemento a partir de su anchura mínima. Si se les da el mismo número a todos, todos se ensancharán a la misma velocidad. El valor por defecto es 0 (no ensanchar).
- `flex-shrink` es la velocidad con la que el elemento se encoge durante la reducción de la caja, a partir de su anchura mínima. El valor por defecto es 1. Si se le da valor 0, el elemento no encogerá.

Existe un *shorthand* para estas propiedades: `flex`. Si se le dan tres argumentos, los toma como *grow*, *shrink* y *basis*.

Independientemente de la alineación (vertical) definida en el contenedor, cada elementos puede tener su propia alineación, que *overrides* la del contenedor (`align-items`). La propiedad del elemento es `align-self`.

## *Grid*

Disposición como en una tabla. Se activa dando a la propiedad `display` del contenedor el valor ***grid***.

Para especificar las filas se usa `grid-template-rows`, mientras que para columnas es `grid-template-columns`. Esta sería una definición de columnas:

```
grid-template-columns: 10px 50px 10px;
```

En este caso, tres columnas. Las filas funcionan igual. Existe un valor muy útil para los tamaños que es, en lugar de especificar un ancho, usar ***auto***, que reparte equitativamente el espacio disponible.

Para justificar los elementos de un *grid* horizontalmente, tenemos la propiedad `justify-content`, a la que se puede dar los valores ***center***, ***start*** o ***end***, que funciona como en los *flexboxes*. El valor ***space-evenly*** distribuye los elementos de tal modo que el espacio entre ellos es uniforme. También existe ***space-around***.

Para alinear verticalmente, existe la propiedad `align-content`. Podemos usar los valores de la alineación horizontal, que se aplicarán a las filas en lugar de a las columnas.

Los *gaps* son los huecos que hay entre los elementos. Hay *column gaps* y *row gaps*. Podemos dar el valor de los primeros mediante la propiedad `grid-column-gap` y dándole un tamaño. Para columnas, `grid-row-gap`. Con el *shorthand* `grid-gap` damos los valores de columna y fila.

Los elementos que se van encontrando en un contenedor (por ejemplo elementos `<div>` dentro de un contenedor también `<div>`), se van asignando por orden, primero los de la fila 1, luego la 2, etc. Alternativamente, se puede indicar, **para cada elemento**, qué fila(s) y/o columna(s) ocupará:


```
grid-column: 1 / 3;
grid-row: 5 / 6;
```
En este caso el elemento empieza en la primera columna (incluida) y termina en la tercera (no incluida), mientras que ocupa la línea 5 únicamente. En lugar de definir el punto final (a la derecha de la barra), se puede simplemente indicar el número de filas/columnas que ocupará el elemento con `span`. En el caso anterior, lo equivalente sería:

```
grid-column: 1 / span 2;
grid-row: 5 / span 1;
```

Existe un *shorthand* para estas propiedades: `grid-area`. Lo equivalente al ejemplo anterior sería:

```
grid-area: 5 / 1 / span 1 / span 2;
```

## Movimiento y animaciones

Supongamos que tenemos un elemento en la página que debe cambiar de color cuando pasamos el ratón por encima. Esto se puede hacer por ejemplo:

```css
#boton-id:hover {
    background: red;
}
```

Si además queremos que las propiedades del elemento (en este caso, `background`) no cambién inmediatamente, sino que lo hagan mediante una transición, deberemos definir la propiedad `transition` en ese elemento. Así que añadiremos, por ejemplo:

```css
#boton-id {
    transition: background 0.3s ease;
}
```

En este caso, definimos que las transiciones en `background` duren 0.3 segundos. Si queremos especificar milisegundos, pondremos ***300ms***. A continuación seleccionaremos uno de los posibles estilos de transición: ***ease*** y ***ease-in-out*** hacen un tipo distinto de interpolación cada una, mientras que ***linear*** lo hace lineal, por ejemplo. Como tercer argumento, indicamos el *delay* en empezar la transición (por defecto 0).

Si queremos que la transición afecte a más propiedades, las indicamos, separadas por comas. Si queremos que afecte a todas las propiedades indicaremos el valor ***all*** en lugar de esa lista.

Es posible mover, escalar y rotar elementos mediante la propiedad `transform`. A esta se le puede pasar como argumento la función `translate()` para mover, `scale()` para escalar, y `rotate()` para rotar.

`translate()` necesita una vector (x, y), es decir dos magnitudes. En cuanto a `scale()` necesita un número que multiplicará el tamaño inicial. `rotate()`, por su parte, necesita un ángulo (***-45deg***, ***90deg***, etc.).

También podemos aplicarle otras transformaciones, como `skewX()`, `skewY()`, o la función `matrix()` que permite realizar todas estas operaciones de golpe.

### Animaciones

Permite definir una animación con *keyframes*, para aplicarlas a cualquier elemento:

```css
@keyframes mi-animacion {
    0% { background: red; }
    25% { background: blue; }
    75% { background: red; }
    100% { background: black; }
}
```

En lugar de porcentajes, se puede indicar los valores ***to*** y ***from***, que indican principio y final.

Para aplicar una animación definida, a un elemento, debemos asignarla y configurarla:

```css
#mi-elemento:hover {
    animation-name: mi-animacion;
    animation-duration: 3s;  /* por defecto es 0 */
    animation-timing-function: linear;  /* diferentes estilos */
    animation-delay: 0.5s;
    animation-iteration-count: 2;  /* número de repeticiones */
    animation-direction: normal;  /* reverse, alternate, alternate-reverse */
}
```

Si en `animation-delay` especificamos un valor negativo, se saltará ese tiempo de la animación.

En `animation-iteration-count` podemos darle el valor ***infinite***.

Podemos usar el *shorthand* `animation`:

```css
#mi-elemento:hover {
    animation: mi-animacion 3s linear 0.5s 2 normal;
}
```
