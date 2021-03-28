# Sin título

## Selectores

Los nombres de selectores, por convenio, deberían estar formados por letras minúsculas y guiones (***-***) únicamente.

### Selector de elemento

```css
p { color: red; }
```

### Selector de clase

```css
.unaclase { color: red; }
```

### Selector de ID

```css
#idname { color: red; }
```

Selecciona un elemento concreto. En el ejemplo estaríamos seleccionando un elemento con un atributo `id="idname"`.

### Especificidad (*specificity*) de selectores

El selector más específico tiene preferencia. Ante dos selectores en conflicto con la misma especificidad, tiene preferencia el que está declarado más tarde.

Especificidad, en orden ascendente:
- Elemento.
- Clase.
- *ID*.
- Estilos *inline*.

### Clase vs *ID*

A parte de tener distinta especificidad, las clases se usan en contextos distintos a los selectores *ID*.

El *ID*, está pensado para ser usado en un solo elemento *HTML* (aunque se puede usar en más de uno). En cambio, las clases están pensadas para ser usadas en un conjunto de elementos.

## Pseudoselectores

Consisten en un selector (de cualquier tipo), dos puntos (***:***) y una información adicional.

Incluyen los distintos estados, como `:hover`, `:visited`, etc.

Por otro lado, en una jerarquía de elementos, podríamos declarar:

```css
li:first-child { color: red; }
li:last-child { color: blue; }
```

En este caso, si tuviéramos varios elementos `<li>` en el mismo nivel, dentro de otro elemento (como `<ul>`), los estilos se aplicarían solo al primero y último de los hijos `<li>`, respectivamente. Para aplicarlo a cualquier otro hijo, definiendo el orden, debemos usar la función `nth-child()`:

```css
li:nth-child(4) { color: red; }
```

En este caso, se aplicaría al cuarto elemento.

El selector `li:only-child` se aplicaría solo a los elementos `<li>` que fuesen hijos únicos.

## Selectores avanzados

Incluye los *combinators*:
- Elementos adyacentes (***+***).
- Elementos adyacentes, que además compartan el mismo padre (***~***).
- Elemento descendiente (espacio).
- Elemento hijo (***>***).

Por ejemplo, `ul li` es un selector que se refiere a cualquier elemento `<li>` que esté dentro de un elemento `<ul>`, aunque no tiene por qué ser un hijo inmediato. Sin embargo, `ul > li` se refiere a los elementos `<li>` cuyo padre inmediato es `<ul>`.

Las reglas de especificidad en *combinators* se complican bastante.

## Selectores de atributos

Tienen la forma `<etiqueta>[atributo=valor]`, y seleccionan la etiqueta especificada, pero solo si tienen el valor deseado para el atributo indicado.

```css
h2[class=especial] { color: red; }
```

No es necesario indicar los valores entrecomillados. Los valores no deberían contener espacios, ya que eso les da un significado especial, pero si aún así queremos tratar esos espacios como caracteres normales, se puede entrecomillar el valor, o indicar el espacio *escaped* (incluso ambas cosas).

Si en lugar de ***=*** usamos el operador ***^=***, estamos indicando "empieza por". ***$=*** indica "termina en". Y ***\*=*** indica "contiene".

Algunos atributos *HTML* (como `class`) admiten una serie de valores separados por espacio. En el caso de `class`, sería un modo de dar varias clases a un elemento.

```html
<h1 class="titulo titulo-pagina titulo1">Esto es un título</h1>
```

En este caso, si queremos seleccionar todos los elementos `<h1>` que pertenezcan a la clase ***titulo-pagina***, podemos hacerlo:

```css
h1[class~=titulo-pagina] { color: red; }
```

Otro ejemplo es el operador ***|=***. En este caso, especifica todas las clases que empiezan por el valor especificado (incluyendo ese valor tal cual), o por ese valor seguido de guión (***-***). Por ejemplo:

```css
h1[class|=titulo] { color: red; }
```

En este caso, entrarían las clases ***titulo***, ***titulo-5***, o ***titulo-5a33e***, pero no ***titulo5a33e***.

Recordemos que los selectores de atributos pueden usar cualquier atributo (aunque aquí lo hayamos hecho con ***class***).
