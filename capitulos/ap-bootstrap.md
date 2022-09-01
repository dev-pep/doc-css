# Bootstrap

Apuntes de los aspectos más relevantes de *Bootstrap 5*. Debido a la gran cantidad de utilidades y componentes, solo se detallarán algunos elementos relevantes. Para aspectos específicos, consúltese la documentación oficial (https://getbootstrap.com/docs).

## Instalación

Para que *Bootstrap* funcione en nuestra página, se deberán incluir los estilos y los scripts necesarios. Existen varias formas de hacerlo.

### Descarga

Descargaremos y desempaquetaremos los archivos *Bootstrap*, que incluyen los estilos *CSS* y los *scripts Javascript* necesarios, y los colocaremos en una carpeta dentro del directorio público de nuestra *web* (normalmente, dentro de una carpeta ***assets***). Una vez hecho esto, incluiremos los estilos dentro de la sección `<head>`:

```html
<link rel="stylesheet" href="assets/css/bootstrap.min.css">
```

Existen varias opciones disponibles. En este caso se incluye la versión minificada del paquete completo de *Bootstrap*.

Por otro lado, se añadirán los *scripts*, al final de la sección `<body>`:

```html
<script src="assets/js/bootstrap.bundle.min.js"></script>
```

En este caso cargamos los *scripts Bootstrap* minificados, incluyendo *Popper*, que es la dependencia de *Bootstrap* para *poppers* (*tooltips*, *popovers*,...).

### *CDN*

Si queremos evitarnos la descarga, es posible acceder a los archivos en el cache de una *CDN* (*Content Delivery Network*). En este caso, a través de ***jsdelivr.net***. Así, no haría falta descargar nada, y las dos líneas indicadas anteriormente se sustuirían por:

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css"
    rel="stylesheet"
    integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js"
    integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous">
</script>
```

### Gestores de paquetes

También es posible usar gestores de paquetes, como *npm* o *yarn*.

## *Layout*

### *Breakpoints*

Los *breakpoints* permiten definir el tamaño (*span*, de 1 a 12) de una columna en función de la resolución horizontal de la pantalla o ventana. Cada resolución tiene asociado un *breakpoint*:

| *Breakpoint* | *Class infix* | Tamaño    |
| :----------- | :------------ | :-------- |
| *X-Small*    |               |   < 576px |
| *Small*      | ***sm***      |  >= 576px |
| *Medium*     | ***md***      |  >= 768px |
| *Large*      | ***lg***      |  >= 992px |
| *X-Large*    | ***xl***      | >= 1200px |
| *XX-Large*   | ***xxl***     | >= 1400px |

Por ejemplo, ara definir el ancho de columna, independiente de la resolución, se usan únicamente las clases ***col-1*** a ***col-12***, pero para definir la anchura en función de la resolución, podríamos dar múltiples clases a la columna, del tipo:

```
col-xxl-1 col-xl-2 col-lg-4 col-sm-6 col-12
```

En este caso, la columna ocupará 1 espacio a partir de ***xxl***, 2 a partir de ***xl***, etc. No tenemos por qué definir todos los *breakpoints*.

### Contenedores

Un contenedor de clase ***container*** tiene una anchura máxima definida para cada *breakpoint*, reservando cierto margen, de forma *responsive*. En cambio, uno de clase ***container-fluid*** ocupará siempre el 100% del ancho disponible. Por otro lado, un contenedor puede ser de una clase del tipo ***container-sm***, ***container-lg***, etc. Esto hará que se comporte como un ***container-fluid*** hasta llegar al *breakpoint* definido, a partir del cual se compartará como un ***container***.

```html
<div class="container">
    <!-- Contenido -->
</div>
```

Los contenedores se centran adecuadamente, aplicando los márgenes necesarios. Similarmente, las columnas tienen su *padding* (llamado *gutter*).

Estos son los tamaños que ocupa un contenedor según la resolución horizontal:

| Contenedor            | *X-Small*<br>(<576px) | *Small*<br>(>=576px) | *Medium*<br>(>=768px) | *Large*<br>(>=992px) |  *X-Large*<br>(>=1200px) | *XX-Large*<br>(>=1400px) |
| :-------------------- | :------- | :------- | :------- | :------- | :-------- | :-------- |
| ***container***       |     100% |	 540px |    720px |    960px |    1140px |    1320px |
| ***container-sm***    |     100% |	 540px |    720px |    960px |    1140px |    1320px |
| ***container-md***    |     100% |	  100% |    720px |    960px |    1140px |    1320px |
| ***container-lg***    |     100% |	  100% |     100% |    960px |    1140px |    1320px |
| ***container-xl***    |     100% |	  100% |     100% |     100% |    1140px |    1320px |
| ***container-xxl***   |     100% |	  100% |     100% |     100% |      100% |    1320px |
| ***container-fluid*** |     100% |	  100% |     100% |     100% |      100% |     100% |

### *Grid*

El sistema de rejilla (*grid*) está dividido en 12 columnas. Basado en el *flexbox CSS*. Es la característica clave de *Bootstrap*.

Dentro del contenedor tenemos filas (clase ***row***), y dentro de estas, columnas (clases ***col***). Si todas las columnas de una fila tienen como ancho simplemente ***row***, se le dará automáticamente un ancho a cada una (entre 1 y 12), dependiendo de su contenido. Dependiendo de la resolución se podrá mostrar una fila en una o más filas en pantalla.

Si a una de las columnas le asignamos un ancho (***col-5***, p.e.), las otras obtendrán anchos asignados automáticamente.

Al usar *breakpoints*, la anchura especificada se aplica **a partir** del *breakpoint* hacia arriba, hasta ***xxl***, o hasta encontrar una definición de anchura en un *breakpoint* superior.

Si en lugar de un número queremos indicar un ancho **en función del contenido**, usaremos ***auto***: ***col-md-auto***, ***col-sm-auto***, etc.

Las columnas tendrán un ancho de 12 en las resoluciones para las que no estén definidas (se apilarán una sobre otra). Si por ejemplo queremos que las columnas se apilen por debajo de ***sm***, podemos hacer algo como:

```html
<div class="container">
    <div class="row">
        <div class="col-sm">Columna 1</div>
        <div class="col-sm">Columna 2</div>
        <div class="col-sm">Columna 3</div>
    </div>
</div>
```

Es decir, con ***col-sm*** no especificamos anchos, pero indicamos anchos automáticos a partir de ***sm***, y las columnas apiladas por debajo de esa resolución.

**A las filas** se les puede dar un número de columnas que deberían tener. Esto se hace mediante las clases ***row-cols-1*** a ***row-cols-12***. También se puede configurar según *breakpoint*:

```html
<div class="row row-cols-1 row-cols-sm-2 row-cols-md-4">
    <!-- Contenido -->
</div>
```

Se pueden anidar una o más filas dentro de una columna.

Si queremos dar a las columnas, filas y/o contenedores un borde por defecto, les podemos incluir la clase ***border***.

### Alineación de columnas

Para **alinear verticalmente** las columnas dentro de una fila, existen las clases (para las **filas**) ***align-items-start***, ***align-items-center*** y ***align-items-end***. Si queremos alinear una columna individualmente, a la misma se le puede dar una clase ***align-self-start***, ***align-self-center*** o ***align-self-end***. La alineación especificada en la columna tendrá prioridad sobre la especificada en la fila. Si una columna no está alineada verticalmente, ocupará todo el alto de la fila.

En cuanto a la **alineación horizontal**, se pueden aplicar, en las **filas**, las clases ***justify-content-\****, con los sufijos ***start***, ***center***, ***end***, ***around***, ***between*** y ***evenly***.

Cuando la suma de anchos supera 12, la siguiente columna se pasa debajo (*wrapped*).

En cuanto a la **alineación horizontal del texto** que contiene una columna, podemos alinearlo con las clases ***text-start***, ***text-center*** o ***text-end***.

### Overflow

En ocasiones, el contenido de un elemento (como una columna) no cabe dentro del mismo. En ese caso, por defecto se produce un *overflow*: el contenido se derrama fuera del elemento. Para evitarlo, se puede añadir la clase ***overflow-auto*** al elemento, de tal modo que el contenido quedará dentro, y se podrá visualizar con desplazamiento (*scroll*). La otra opción es ***overflow-hidden***, que simplemente trunca la visualización del contenido al tamaño del elemento.

### Espaciado

Para definir el margen (espaciado exterior, alrededor) los objetos pueden usar las clases ***m-0*** (sin margen) a ***m-5***. De forma similar, para el *padding* (espaciado interior) se usan ***p-0*** (sin *padding*) a ***p-5***.

También es posible especificar solo los márgenes y/o *paddings* verticales (arriba, abajo) u horizontales (izquierda, derecha), insertando ***x*** o ***y*** como segundo carácter de la clase: ***mx-4***, ***py-2***, etc. Se puede ser todavía más específico, utilizando los caracteres ***t*** (*top*, arriba), ***b*** (*bottom*, abajo), ***s*** (*start*, izquierda) y ***e*** (*end*, derecha): ***me-2***, ***pt-3***, etc.

En el caso específico del *grid* (filas y columnas), aunque también se pueden usar los ajustes de margen y *padding*, es preferible por su comodidad utilizar el ajuste *gutter*. Este mecanismo establece la separación **entre columnas** de una misma fila. Lo podemos usar especificando ***g-0*** a ***g-5*** **en la fila**. El *gutter* establece entonces el *padding* para cada una de las columnas contenidas en dicha fila, y de esta forma solo hay que especificarlo en un solo lugar (la fila), y no en cada una de las columnas, una a una.

El *gutter* admite además especificación vertical u horizontal (***gx-3***, ***gy-2***, etc.).

## Componentes

### Botones

El formato típico de un botón es:

```html
<button type="button" class="btn btn-primary">Botón</button>
```

La clase ***btn*** está diseñada para etiquetas `<button>`, pero también se puede utilizar con `<a>` o `<input>`. A parte de ***btn*** se le debe dar un estilo con prefijo ***btn-*** y sufijo ***primary***, ***secondary***, ***success***, ***danger***, ***warning***, ***info***, ***light***, ***dark*** o ***link***. Si queremos que el botón sea de tipo *outline*, el prefijo será ***btn-outline-*** (exceptuando sufijo ***link***).

Si además queremos indicar tamaño, existen las clases ***btn-lg*** y ***btn-sm***.

En la etiqueta *HTML* se puede indicar ***disabled*** para deshabilitarlo.
