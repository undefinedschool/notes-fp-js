> El siguiente contenido fue elaborado por [@_nhsz](https://twitter.com/_nhsz) como guía para las clases de [undefined school](https://twitter.com/undefinedSchool)  
> Son bienvenidos los _issues_ y _PRs_ para mejorar el contenido, corregir errores, etc. 

> 👉 Si te resultó útil, **se agradece que lo compartas para que le llegue a más gente!**

# ![Notas sobre Programación Funcional con JavaScript](https://i.imgur.com/GxZsZVA.png)

## Intro 

A medida que la cantidad de líneas del código de nuestra aplicación va aumentando, debemos tener cuidado al hacer cambios y pensar a qué otras partes del código estamos afectando.

La forma que conocemos para acotar el _scope_ de cierto bloque de código son las **funciones**. Nos permiten, además de reutilizar, reducir el potencial impacto de nuestros cambios. Pero aún así, razonar y entender bien qué hace cada línea de nuestras funciones puede resultar complejo y no está garantizado que no provoque efectos por fuera del scope (aka _side effects_), por ejemplo, si utilizamos variables globales.

Además, el estilo con el que solemos escribir nuestras funciones suele ser indicar las instrucciones, paso a paso, que queremos que ejecute la computadora, es decir, un modo _imperativo_: hablamos de _cómo_ hacer las cosas en lugar del _qué_ (_declarativo_).

Imaginemos que podemos estructurar nuestro código en pequeñas piezas, individuales, independientes, auto-contenidas, donde

- el resultado de la ejecución de cada pieza **depende sólo de sus inputs**
- las únicas consecuencias o **efectos provocados son sus outputs** (no hay _side effects_)
- cada una de estas piezas de código es declarativa, haciéndola más legible

Cómo podríamos lograr esto?

## Paradigma 

La programación funcional es un **paradigma de programación** que nos sirve para estructurar, organizar y controlar la complejidad de nuestro código, favoreciendo un estilo más [**_declarativo_**]()_, utilizando [**_funciones puras_**](), evitando los [**_side effects_**]() y la alteración del [**_estado compartido_**](), logrando así que el código resulte...

➕ legible    
➕ simple (sólo usamos funciones)    
➕ declarativo  
➕ fácil de razonar
➕ fácil de debuggear    
➕ fácil de testear  
➖ _side effects_  

Para esto, vamos a utilizar

- funciones pequeñas, que sólo dependen de sus inputs y no de otras partes del código   
- sin _side effects_ (no hay consecuencias más allá del scope de la función y su output)
- composición: construimos nuestra aplicación a partir de estos bloques

> JavaScript no es un lenguaje de programación funcional _puro_, pero tiene soporte para algunas características del paradigma. Existen lenguajes funcionales puros que compilan a JavaScript (y pueden utilizarse en frontend), como [Elm](https://elm-lang.org/) y [PureScript](https://www.purescript.org/)

## Conceptos

### Funciones First-Class

En un lenguaje de programación funcional, las funciones son [**_First-Class Citizens_**](https://github.com/undefinedschool/notes-functions-first-class) y JavaScript cumple con esto.

### Higher-Order Functions

Si una función acepta otras funciones como argumentos (por ejemplo, cada vez que usamos _callbacks_ en JS/Node) o retorna funciones, se dice que es una **_función de alto orden o Higher-Order Function_** (alcanza con que cumpla alguna de las 2 características).

👉 Tener en cuenta que _las funciones de alto orden son un subconjunto de las funciones de primera clase_, por lo tanto 

**_First-Class Function_ → _Higher-Order Function_**.

Algunos métodos de `Array`, como [`map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map), [`filter()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) y [`reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

[![Higher-order functions - Part 1 of Functional Programming in JavaScript](https://img.youtube.com/vi/BMUiFMZr7vk/0.jpg)](https://www.youtube.com/watch?v=BMUiFMZr7vk)
> Ver [Higher-order functions - Part 1 of Functional Programming in JavaScript](https://www.youtube.com/watch?v=BMUiFMZr7vk)

### Declarativo vs Imperativo

Cuando utilizamos un enfoque _imperativo_, definimos todos los pasos necesarios para cumplir cierta tarea. **Con un enfoque _declarativo_ en cambio, le decimos a la computadora qué hacer y que la misma se encargue de resolver los detalles**, abstrayéndonos de estos. Notemos que podemos manejar diferentes **niveles de abstracción**: JavaScript por si mismo ya es mucho más declarativo que el código máquina que termina produciendo el compilador/intérprete.

Por ejemplo, cuando estamos iterando arrays, el enfoque más imperativo sería utilizar `for` o `while` para definir los ciclos. `for...of` es más declarativo, ya que nos abstrae de ciertos detalles como la longitud, mientras que métodos como `map`, `filter` y `reduce` son más declarativos todavía, porque directamente toman el enfoque funcional.

Algunos lenguajes declarativos que ya conocemos y venimos utilizando son HTML y SQL.

### Side Effects

- Llamamos _side effect_ a la consecuencia de que una función modifique el [**_estado_**] de una aplicación de una forma que no sea retornar un nuevo valor.

### Estado compartido

Functions try to limit any changes to the state of the program and avoid changes to the global objects holding data

Functions have minimal side effects in the program

### Inmutabilidad

Decimos que **los datos son _inmutables_ si nunca cambian (no pueden modificarse)**. En el paradigma funcional, los datos son inmutables. La naturaleza _mutable_ de los datos es una gran fuente de bugs, por lo que aplicar esta característica del paradigma siempre que podamos, es recomendable.

Las _variables_ entonces, pasan a ser _constantes_, no pueden modificarse: una vez creada una variable con cierto valor, la única forma que tenemos de modificar el mismo es creando una nueva variable con el nuevo valor. 

Por ejemplo, si queremos modificar un array, para agregar un nuevo ítem al mismo, creamos un nuevo array concatenando el array anterior con el nuevo ítem.

```js
const originalArray = [1, 2, 3];
const newArray = [...originalArray, 4];
```
> Ejemplo 1: agregar un ítem a un array sin modificar el original, utilizando [`spread operator`](https://github.com/undefinedschool/notes-es6-spread-operator)

#### Inmutabilidad y `const` en JS

#### Inmutabilidad y objetos en JS

Tengamos en cuenta que **en JavaScript los objetos siempre se pasan por _referencia_**, mientras que los [_tipos primitivos_](https://developer.mozilla.org/en-US/docs/Glossary/Primitive), por valor/copia.

En el paradigma funcional, nunca deberíamos modificar un objeto directamente, sino crear uno nuevo con los cambios necesarios, a partir del original.

### Funciones puras

[WIP]

#### Ejercicio

[WIP]

Justificar cuáles de las siguientes funciones son puras o no:

### Composición de funciones

La composición consiste en simplemente utilizar el resultado de una función (_output_) como _input_ de otra función.

De esta forma, combinando funciones simples (que, en lo posible, hagan 1 sola cosa) podemos construir funcionalidades más complejas.

```js
const f = x => x + 1;
const g = y => y * 2;
const h = z => z ** 3; 
const number = 3;

const result = f(g(h(number)));
```
> Ejemplo 2: composición de funciones

#### Refactor 1: Compose

Miremos el ejemplo anterior y pensemos qué pasaría si tuviéramos que componer muchas funciones...

```js
const f = ...;
const g = ...;
const h = ...;
const i = ...;
const j = ...;
const k = ...;
const x = 3;

const result = f(g(h(i(j(k(x))))));
```

Terminaríamos con cada vez más funciones anidadas, algo que podríamos llamar _Composition Hell_ 🤔

Utilizando `reduce` o [`reduceRight`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/ReduceRight) (dependiendo del orden en el que querramos componer), podemos escribir una _función de composición_ para obtener el mismo resultado.

```js
const f = x => x + 1;
const g = y => y * 2;
const h = z => z ** 3; 
const number = 3;

const compose = (...fns) => 
  x => fns.reduceRight((acc, fn) => fn(acc), x);
  
const enhance = compose(f, g, h);

enhance(number);
```
> Ejemplo 3: función de composición

👉 Este patrón es muy común en la programación funcional y podemos implementarlo utilizando el método [`compose`](https://ramdajs.com/docs/#compose) de la librería utilitaria [Ramda](https://ramdajs.com/)

##### Refactor 2: Pipeline operator 🙌

Existe un operador (_aún en fase experimental_, por lo que necesitamos [Babel](https://alligator.io/js/pipeline-operator/) para poder utilizarlo), el [Pipeline operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Pipeline_operator) que permite escribir de forma mucho más legible la composición de funciones, utilizando el output de una expresión como input de la siguiente.

Volviendo el ejemplo original y utilizando el pipeline, podríamos reescribirlo de la forma

```js
const f = x => x + 1;
const g = y => y * 2;
const h = z => z ** 3; 
const number = 3;

3
  |> h 
  |> g 
  |> f;
```

👉 [Ver ejemplo en Codepen](https://codepen.io/nhquiroz/pen/xxwVWym)

👉 Este patrón es muy común en la programación funcional y también podemos implementarlo utilizando el método [`pipe`](https://ramdajs.com/0.19.0/docs/#pipe) de la librería utilitaria [Ramda](https://ramdajs.com/)

#### Ejercicio

Escribir las siguientes funciones  

- `scream`: recibe un string y retorna el mismo string convertido a mayúsculas
- `exclaim`: recibe un string y retorna el mismo string con un signo de exclamación (`!`) al final
- `repeat`: recibe un string y retorna el mismo string, repetido 2 veces y separado por 1 espacio

y componerlas sobre el string `'I like coffee'`, utilizando primero `scream`, luego `exclaim` y por último `repeat`.

Resolverlo de tres formas, con la composición más trivial (`f(g(x))`) y luego aplicando los refactors 1 y 2 mencionados anteriormente.

<details><summary><strong>⚡ Solución v1</strong></summary>

```js
const scream = str => str.toUpperCase();
const exclaim = str => `${str}!`;
const repeat = str => `${str} ${str}`;

const str = 'I like coffee';
const result = repeat(exclaim(scream(str)));
```

</details>

<details><summary><strong>⚡ Solución v2</strong></summary>

```js
const scream = str => str.toUpperCase();
const exclaim = str => `${str}!`;
const repeat = str => `${str} ${str}`;

const str = 'I like coffee';

const enhance =  compose(scream, explain, repeat);
enhance(str);
```

</details>


<details><summary><strong>⚡ Solución v3</strong></summary>

```js
const scream = str => str.toUpperCase();
const exclaim = str => `${str}!`;
const repeat = str => `${str} ${str}`;

const str = 'I like coffee';

str
  |> scream 
  |> exclaim 
  |> repeat;
```

</details>

### Closures

[WIP]

## Ejercicios

> **Nota:** utilizar [funciones puras]() en los ítems donde se pida implementar alguna, incluyendo las funciones auxiliares

1. Escribir una función que filtre los duplicados de un array, utilizando `Array.filter()`
2. Escribir una función que filtre los duplicados de un array, utilizando `Array.reduce()`
3. Implementar la función `map()` de `Array` usando `reduce()`
4. Implementar la función `filter()` de `Array` usando `reduce()`
