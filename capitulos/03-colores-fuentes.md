# Colores y fuentes

## Colores

Para dar valor a las propiedades de color, debemos definir un color. Hay 3 formas de hacerlo: por nombre (***skyblue***), por código hexadecimal *RGB* (***#87cefa*** o ***#3f5***) o mediante la función `rgb()` (***rgb(135,206,235)***).

Para color del texto se usa la propiedad `color`. Para color de fondo, `background-color`, aunque se puede usar el *shorthand* `background`.

Esto son ejemplos válidos de establecer un fondo a través `background`:

```css
body { background: skyblue; }  /* background-color */
```

```css
body { background: url("../img/fondo.png"); }  /* background-image */
```

```css
body { background: url("http://dominio.com/img/fondo.png"); }  /* background-image */
```

### Ejemplo de *background*

Supongamos el siguiente *HTML*:

```html
<div id="ident-imagen"></div>
```

Y las siguientes definiciones de estilo:

```css
#ident-imagen {
    height: 400px;  /* altura */
    width: 70%;  /* anchura */
    background: url("../img/fondo.png");
    background-size: 50px 100px;  /* tamaño de la imagen de fondo en pantalla (width height) */
    background-repeat: repeat;
}
```

Si en `background-size` especificamos simplemente ***cover***, escalará la imagen de tal modo que cubra el contenedor (`<div>`) completo. Si queremos que lo haga, de tal modo que se escale la imagen lo máximo posible pero que se mantenga visible en su totalidad, se debe indicar ***contain***.

Para `background-repeat`, el valor por defecto es ***no-repeat***.

### Transparencia

Para indicar un color con transparencia se debe usar la función `rgba()`, que precisa cuatro argumentos, los 3 primeros para el *RGB* habitual (valores 0-255), y el cuarto para el canal alfa (0-1).

### Gradientes

Se definen con las funciones `linear-gradient()` y `radial-gradient()`.

`linear-gradient()` define un gradiente lineal, con argumentos dirección, color 1, color 2, color 3,... Para definir la dirección, se debe proporcionar un "vector": ***to right***, ***to bottom left***, etc., o mediante ángulos: ***-90deg***.

Junto a cada color podemos especificar los puntos del gradiente (en porcentaje) donde se ubica cada color, p.e. `linear-gradient(to right, red 20%, blue 45%, green 65%)`.

`radial-gradient()` es un gradiente circular. Difiere del lineal en que no tiene parámetro de dirección. El primer argumento, opcional, puede ser la forma del gradiente: hay dos posibilidades, ***ellipse*** (por defecto, según forma del contenedor) o ***circle***.

## Unidades

**Unidades absolutas:** centímetros (***cm***), milímetros (***mm***), pulgadas, etc. En cuanto a los píxeles (***px***), es una unidad que depende de la resolución (*dpi*) de la pantalla. Un píxel tiene el mismo tamaño en cualquier dispositivo, al igual que el resto de unidades absolutas.

**Unidades relativas:** porcentajes (***%***), tamaño relativo al tipo de fuente actual por defecto del elemento (***em***). Las unidades ***vh*** y ***vw*** indican un 1% del total del *viewport* donde estamos viendo la página (incluyendo los márgenes).

## Texto y fuentes

La **decoración** de texto trata de líneas sobre el texto. Se usa con la propiedad `text-decoration`, y sus posibles valores son ***none***, ***underline***, ***line-through*** y ***overline***.

En cuanto a `text-transform`, trata de la aplicación de cambios de caracteres. Los valores posibles son ***capitalize***, ***lowercase*** y ***uppercase***.

Para la alineación, tenemos `text-align`, con ***center***, ***left***, ***right*** y ***justify***.

### Fuentes

La propiedad `font-size` permite cambiar tamaño.

`font-weight` define la negrita, desde 0 (texto invisible), pasando por 400 (letra regular) hasta el número que permita la fuente.

`font-style` es para cursiva: ***normal***, ***italic*** y ***oblique*** (extra cursiva).

Para establecer la fuente o familia de fuentes, existe `font-family`. Se puede indicar la familia mediante el nombre de la misma (***Times***, ***Helvetica***, etc.). Si el nombre contiene espacios, habrá que entrecomillarlo con comillas dobles. También se puede indicar un nombre genérico de fuente: ***serif***, ***sans-serif***, ***monospace***, por ejemplo.

La manera de especificar la fuente o familia funciona de tal modo que se le pueden dar varias opciones, separadas por comas. En este caso se usará la primera opción disponible.

#### Fuentes externas

Un buen recurso es *google fonts*. Permite utilizar distintas fuentes *online*.
