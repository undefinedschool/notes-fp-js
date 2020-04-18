> El siguiente contenido fue elaborado por [@_nhsz](https://twitter.com/_nhsz) como guía para las clases de [undefined school](https://twitter.com/undefinedSchool)  
> Son bienvenidos los _issues_ y _PRs_ para mejorar el contenido, corregir errores, etc. 

> 👉 Si te resultó útil, **se agradece que lo compartas para que le llegue a más gente!**

# ![Notas sobre Programación Funcional con JavaScript](https://i.imgur.com/GxZsZVA.png)

## Intro 

A medida que la cantidad de líneas del código de nuestra aplicación va aumentando, debemos tener cuidado al hacer cambios y pensar a qué otras partes del código estamos afectando.

La forma más simple que conocemos para acotar el _scope_ de cierto bloque de código y construir software son las **funciones**. Nos permiten, además de reutilizar, reducir el potencial impacto de nuestros cambios. Pero aún así, razonar y entender bien qué hace cada línea de nuestras funciones puede resultar complejo y no está garantizado que no provoque efectos por fuera del scope (aka _side effects_), por ejemplo, si utilizamos variables globales.

Además, el estilo con el que solemos escribir nuestras funciones suele ser indicar las instrucciones, paso a paso, que queremos que ejecute la computadora, es decir, un modo _imperativo_: hablamos de _cómo_ hacer las cosas en lugar del _qué_ (_declarativo_).

Imaginemos que podemos estructurar nuestro código en pequeñas piezas, individuales, independientes, auto-contenidas, donde

- el resultado de la ejecución de cada pieza **depende sólo de sus inputs**
- las únicas consecuencias o **efectos provocados son sus outputs** (no hay _side effects_)
- cada una de estas piezas de código es declarativa, haciéndola más legible

Cómo podríamos lograr esto?

## Paradigma 

La programación funcional es un **paradigma de programación** que nos sirve para estructurar, organizar y controlar la complejidad de nuestro código, favoreciendo un estilo más [**_declarativo_**](https://github.com/undefinedschool/notes-fp-js#declarativo-vs-imperativo)_, utilizando expresiones y [**_funciones puras_**](https://github.com/undefinedschool/notes-fp-js#funciones-puras) para construir aplicaciones, evitando los [**_side effects_**](https://github.com/undefinedschool/notes-fp-js#side-effects) y la mutación del [**_estado**](https://github.com/undefinedschool/notes-fp-js#estado-compartido), logrando así que el código resulte...

➕ legible    
➕ declarativo  
➕ simple (sólo tenemos valores y funciones)     
➕ fácil de razonar  
➕ fácil de debuggear (cada función es una unidad con input/output definido)   
➕ fácil de testear  
➕ fácil de extender (podemos agregar funcionalidades combinando otras ya existentes)   
➕ fácil de refactorizar (nuevamente, sólo tenemos valores y funciones)   
➕ performance, si paralelizamos la ejecución de código      
➖ _side effects_  
➖ bugs    

Para esto, vamos a utilizar

- funciones pequeñas, puras: sólo dependen de sus inputs y no de otras partes del código   
- sin _side effects_: no hay consecuencias más allá del scope de la función y su output
- composición: construimos nuestra aplicación a partir de estos bloques

Usar [_funciones puras_](https://github.com/undefinedschool/notes-fp-js#funciones-puras) y [_componerlas_](https://github.com/undefinedschool/notes-fp-js#composici%C3%B3n-de-funciones) para resolver problemas más grandes son habilidades muy útiles que pueden ser utilizadas para simplificar esta complejidad.

👉 Tengamos en cuenta que **simple no significa _fácil_**: los problemas difíciles lo seguirán siendo, el paradigma funcional no va a cambiar esto, **la simplificación viene dada porque los problemas resultan más fáciles de razonar, al descomponerlos en subproblemas**. Estos problemas son mucho más sencillos de resolver de forma independiente y pueden componerse para llegar a la solución buscada.

> JavaScript no es un lenguaje de programación funcional _puro_, pero tiene soporte para algunas características del paradigma. Existen lenguajes funcionales puros que compilan a JavaScript (y pueden utilizarse en frontend), como [Elm](https://elm-lang.org/) y [PureScript](https://www.purescript.org/)

## Conceptos

### Función

![Función: un proceso que recibe determinado input y produce cierto output](https://www.thatsoftwaredude.com/images/post/166952a8-ac94-4d24-9b42-22f982096e4e.png)

Las funciones son procesos que reciben determinado _input_ y producen cierto _output_.

Utilizamos funciones principalmente para:

- _mappear_ inputs a determinados outputs: una función recibe argumentos y retorna un valor, por lo que para cada input existe un output
- procedimientos: una función puede invocarse para ejecutar una secuencia de instrucciones, conocida como procedimiento
- I/O: una función puede comunicarse con otras partes del sistema/periféricos (requests HTTP, interacción con una DB, obtener input a través de la terminal, etc)

### Aridad

Representa la cantidad de argumentos que recibe una función. Según la cantidad, una función puede ser

- _unaria_: recibe 1 argumento
- _binaria_: recibe 2 argumentos
- _ternaria_: recibe 3 argumentos
- etc...

```js
const sum = (a, b) => a + b;

const arity = sum.length;
console.log(arity) // 2

// Si utilizamos `.length` sobre una función, nos devuelve la cantidad de parámetros de la misma
```

En el ejemplo anterior, `sum` es una función _binaria_ o una función con una aridad 2 y siempre deberá ser invocada con 2 argumentos.

También existen las funciones _variádicas_: son aquellas que pueden recibir una cantidad variable de argumentos.

### Transparencia referencial

Decimos que una expresión es _referencialmente transparente_ si puede ser reemplazada por su valor, sin alterar el comportamiento del programa.

Por ejemplo, si tenemos la siguiente función

```js
const greet = () => 'Hello World!';
```

cualquier invocación de `greet()` puede ser reemplazada por el string `'Hello World!'` perfectamente, por lo tanto tiene transparencia referencial.

### Funciones First-Class

En un lenguaje de programación funcional, las funciones son [**_First-Class Citizens_**](https://github.com/undefinedschool/notes-functions-first-class) (es decir, pueden tratarse como cualquier otro valor) y JavaScript cumple con esto.

### Higher-Order Functions

Si una función acepta otras funciones como argumentos (por ejemplo, cada vez que usamos _callbacks_ en JS/Node) o retorna funciones, se dice que es una **_función de alto orden o Higher-Order Function_** (alcanza con que cumpla alguna de las 2 características).

👉 Tener en cuenta que _las funciones de alto orden son un subconjunto de las funciones de primera clase_, por lo tanto 

![First-Class Function_→ Higher-Order Function](https://i.imgur.com/RswMneW.png)

Algunos métodos de `Array`, como [`map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map), [`filter()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) y [`reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) son funciones de alto orden.

[![Higher-order functions - Part 1 of Functional Programming in JavaScript](https://img.youtube.com/vi/BMUiFMZr7vk/0.jpg)](https://www.youtube.com/watch?v=BMUiFMZr7vk)
> Ver [Higher-order functions - Part 1 of Functional Programming in JavaScript](https://www.youtube.com/watch?v=BMUiFMZr7vk)

Esta característica es la que nos va a permitir luego [componer](https://github.com/undefinedschool/notes-fp-js#composici%C3%B3n-de-funciones) funciones.

### Declarativo vs Imperativo

Cuando utilizamos un enfoque _imperativo_, definimos todos los pasos necesarios para cumplir cierta tarea. **Con un enfoque _declarativo_ en cambio, le decimos a la computadora qué hacer y que la misma se encargue de resolver los detalles**, abstrayéndonos de estos. Notemos que podemos manejar diferentes **niveles de abstracción**: JavaScript por si mismo ya es mucho más declarativo que el código máquina que termina produciendo el compilador/intérprete.

Por ejemplo, cuando estamos iterando arrays, el enfoque más imperativo sería utilizar `for` o `while` para definir los ciclos. `for...of` es más declarativo, ya que nos abstrae de ciertos detalles como la longitud, mientras que métodos como `map`, `filter` y `reduce` son más declarativos todavía, porque directamente toman el enfoque funcional.

Algunos lenguajes declarativos que ya conocemos y venimos utilizando son HTML y SQL.

### Side Effects

Decimos que una expresión o función tiene un _side effect_ si, aparte de retornar un valor, interactúa de alguna forma (lee o escribe) con un [**_estado_**](https://github.com/undefinedschool/notes-fp-js#estado-compartido) externo a la misma (es decir, cualquier otra cosa que haga aparte de retornar un valor). Por ejemplo, leer o modificar una variable global son considerados side effects.

```js
const differentEveryTime = new Date();

console.log('IO is a side effect!');
```

> Las [operaciones de I/O tienen side effects](https://www.quora.com/Why-is-it-said-that-any-I-O-operation-will-have-side-effects), porque su propósito es intercambiar información entre diferentes sistemas.

Una función que provoca side effects modifica el estado (ya sea interno de algún argumento o de una variable externa) o depende de un estado externo a su input. Una consecuencia de esto puede ser que código de otra parte del programa no esté al tanto de los cambios realizados, produciendo resultados inesperados en la ejecución o que la misma llamada a una función, en diferentes momentos pueda tener resultados diferentes. En estos casos, las funciones son _impuras_.

Los _side effects_ incluyen:

- leer/escribir de un disco (HD/SSD)
- leer/escribir de la red (request HTTP)
- leer inputs a través de la consola
- loggear info a la consola
- arrojar errores
- modificar el DOM
- mutar objetos/arrays pasados como argumentos

El paradigma funcional utiliza [funciones puras](https://github.com/undefinedschool/notes-fp-js#funciones-puras) y datos [inmutables](https://github.com/undefinedschool/notes-fp-js#inmutabilidad) para evitar los _side-effects_.

### Estado compartido

Tener estado (variables) compartido hace que nuestra aplicación se vuelva más frágil (_error-prone_), difícil de razonar y eventualmente, de debuggear, ya que puede haber otras partes del código, módulos o incluso código externo, como dependencias u otro software que use nuestra aplicación, que puedan estar modificando este estado, volviendo más complejo el seguimiento de la evolución del mismo.

Podemos tener estado compartido en

- Clases
- Variables globales
- Argumentos pasados por referencia (objetos)

Las funciones limitan los cambios realizados al estado del programa, evitando acceder a variables globales, reduciendo así los posibles [_side-effects_](https://github.com/undefinedschool/notes-fp-js#side-effects). Es por esta razón que usamos [funciones puras](https://github.com/undefinedschool/notes-fp-js#funciones-puras) en el paradigma funcional.

### Inmutabilidad

Decimos que **los datos son _inmutables_ si nunca cambian (no pueden modificarse)**. En el paradigma funcional, los datos son inmutables. Utilizar valores inmutables facilita mucho razonar sobre el código de nuestra aplicación, ya que no modificaremos accidentalmente el [estado](https://github.com/undefinedschool/notes-fp-js#estado-compartido) de la misma, por lo que es recomendable aplicar esta característica del paradigma siempre que podamos.

Las _variables_ entonces, pasan a ser _constantes_, no pueden modificarse: una vez creada una variable con cierto valor, la única forma que tenemos de modificar el mismo es creando una nueva variable con el nuevo valor. 

Por ejemplo, si queremos modificar un array, para agregar un nuevo ítem al mismo, creamos un nuevo array concatenando el array anterior con el nuevo ítem.

```js
const originalArray = [1, 2, 3];
const newArray = [...originalArray, 4];
```

> Ejemplo 1: agregar un ítem a un array sin modificar el original, utilizando [`spread operator`](https://github.com/undefinedschool/notes-es6-spread-operator)

👉 **La única forma de modificar datos es creando copias modificadas**

#### Inmutabilidad, `const` y objetos en JS

Si estamos utilizando _valores primitivos_ (`number`, `string`, `boolean`, etc), definir una variable como `const` la vuelve **inmutable**, es decir, no podemos modificar el valor de la misma (reasignar) una vez creada. 

```js
const cantModifyThis = 1;
cantModifyThis = 2;

// ❌ Uncaught TypeError: Assignment to constant variable.
```

En cambio, si estamos utilizando objetos, tengamos en cuenta que **en JavaScript, los objetos siempre se pasan por _referencia_**, es decir, si una función muta/modifica un objeto que recibe como argumento, está mutando un [estado externo](https://github.com/undefinedschool/notes-fp-js#estado-compartido) fuera de su _scope_. Los [_tipos primitivos_](https://developer.mozilla.org/en-US/docs/Glossary/Primitive) en cambio, se pasan por valor/copia.

Usar `const` en el caso de un objeto, solo impide la _reasignación_, es decir, una vez definida la variable, no podemos cambiar a qué objeto hace referencia usando el operador de asignación `=`. Pero nada nos impide modificar el objeto internamente, modificar los valores de sus propiedades/métodos o incluso agregar/eliminar alguna.

```js
const mutableData = {
  x: 1
};

// intentando reasignar
mutableData = { x: 2 };
// ❌ Uncaught TypeError: Assignment to constant variable.

// pero si modificamos una propiedad...
mutableData.x = 2;

console.log(mutableData);
// 😰 { x: 2}
```

👉 **Para evitar _mutar_ el estado, es importante tratar el input de las funciones como inmutable.**<sup id="cite_ref-2"><a href="#cite_note-2">[2]</a></sup>

> Si queremos trabajar con objetos _inmutables_ podemos utilizar el método [`Object.freeze()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze) o la librería [Immutable.js](https://immutable-js.github.io/immutable-js/)

> En el paradigma funcional, nunca deberíamos modificar un objeto directamente, sino crear uno nuevo con los cambios necesarios, a partir del original. 

Para esto, es muy útil utilizar el operador [`spread`](https://github.com/undefinedschool/notes-es6-spread-operator/) para copiar las propiedades del objeto original y modificar sólo las que cambian.

```js
const original = {
  name: 'JavaScript',
  age: 25,
  color: 'yellow'
}

const modifiedCopy = {
  ...original,
  color: 'blue'
}

console.log(original);
console.log(modifiedCopy);
```

### Funciones puras

Decimos que una función es _pura_ si 

- el valor de retorno está determinado únicamente por su input (mismo input => mismo output), sin importar cuántas veces la llamemos<sup id="cite_ref-1"><a href="#cite_note-1">[1]</a></sup> 
- es _predecible_ (por el ítem anterior)
- no modifica ningún estado interno (argumentos) ni interactúa con ningún estado externo (no leen ni modifican valores fuera de su _scope_), es decir, no provocan [_side effects_](https://github.com/undefinedschool/notes-fp-js#side-effects)
- son [_referencialmente transparentes_](https://github.com/undefinedschool/notes-fp-js#transparencia-referencial).

Es decir, dado el mismo input, retorna siempre el mismo output (es determinística). Esto hace que las funciones sean _auto-contenidas_, y _predecibles_ facilitando la [composición](https://github.com/undefinedschool/notes-fp-js#composici%C3%B3n-de-funciones) y el testeo de las mismas.

Por ejemplo, la siguiente función

```js
const sum = (a, b) => a + b;
```

es _pura_, ya que no tiene _side-effects_ y para los mismos valores de `a` y `b`, el resultado será siempre el mismo, mientras que `getId`

```js
const SECRET = 42; 

const getId = a => SECRET * a;
```

es _impura_, ya que accede a la variable global `SECRET`. Si `SECRET` fuera modificada, `getId` retornaría un valor diferente para el mismo input, por lo tanto no puede ser una función _pura_.

La siguiente función

```js
let id_count = 0;

const getId = () => ++id_count;
```

también es _impura_, por las siguientes razones:

- está accediendo a una variable por fuera de su _scope_
- crea un _side-effect_ al modificar una variable externa

#### Ejercicios

1. Cómo afectan las funciones `Array.slice()` y `Array.splice()` al array original?

a) `slice` es puro, `splice` es impuro.  
b) `slice` es impuro, `splice` es puro.  
c) ambas son puras.  
d) ambas son impuras.  

2. Justificar si `Math.random()` es una función pura o impura.
3. Justificar cuáles de las siguientes funciones son puras o no:

a)

```js
const greet = name => `Hi, ${name}`;

greet('Brianne') // 'Hi, Brianne'
```

b)

```js
window.name = 'Brianne';

const greet = () => `Hi, ${window.name}`;

greet() // "Hi, Brianne"
```

c)

```js
let greeting = '';

const greet = name => greeting = `Hi, ${name}`;

greet('Brianne');
greeting // "Hi, Brianne"
```

d)

```js
const arr = [2, 4, 6];

const doubleValues = arr => {
  for(let value of arr)  {
    value = value * 2;
  }
}

doubleValues(arr);
arr; // [4, 8, 12]

doubleValues(arr);
arr; // [8, 16, 24]
```

e) 

```js
const arr = [2, 4, 6];

const doubleValues = arr =>
  arr.map(value => value * 2);

doubleValues(arr); // [4, 8, 12]
doubleValues(arr); // [4, 8, 12]
doubleValues(arr); // [4, 8, 12]
```

f)

```js
const start = {};

const addNameToObject = (obj, val) => {
  obj.name = val;
  
  return obj;
}
```

g)

```js
const arr = [1, 2, 3, 4];

function addToArr (arr,val) {
  arr.push(val);

  return arr;
}

addToArr(arr, 5);
arr; // [1, 2, 3, 4, 5]
```

h)

```js
const arr = [1, 2, 3, 4];

function addToArr (arr, val) {
  const newArr = [...arr, val];

  return newArr;
}

addToArr(arr, 5);
arr; // [1, 2, 3, 4, 5]
```

### Composición de funciones

La composición consiste en simplemente utilizar el resultado de una función (_output_) como _input_ de otra función.

De esta forma, combinando 2 o más funciones simples (funciones que, en lo posible, hagan 1 sola cosa) podemos crear funciones más complejas.

Es el mecanismo que nos provee el paradigma para reutilizar y evitar la duplicación de código (DRY).

```js
const f = x => x + 1;
const g = y => y * 2;
const h = z => z ** 3; 
const number = 3;

const result = f(g(h(number)));
```

> Ejemplo 2: composición de funciones

Podemos pensar también a la composición de funciones como el hecho de ejecutar una serie de operaciones para resolver un problema más complejo.

```js
pipe(
  getPlayerName,
  getFirstName,
  properCase,
  addUserLabel,
  createUserTemplate
)([{name: 'John Bonham', score: 77}]);
```

El paradigma de programación funcional utiliza [funciones puras](https://github.com/undefinedschool/notes-fp-js#funciones-puras) como la _unidad primaria de composición_: son los bloques con los que vamos a construir nuestra aplicación.

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

### Recursión

[WIP]

Cuando una función se invoca a si misma, se la conoce como _función recursiva_.

### Closures

[WIP]

## Ejercicios

### Funciones Puras

Utilizar [funciones puras](https://github.com/undefinedschool/notes-fp-js#funciones-puras) (incluyendo las funciones auxiliares, si las hay) para resolver los siguientes problemas:

1. Agregar un ítem al final de un array, sin modificar el original (no podemos utilizar `push`).
2. Agregar un ítem al inicio de un array, sin modificar el original (no podemos utilizar `push`).
3. Eliminar el primer elemento de un array, sin modificar el original
4. Eliminar el último elemento de un array, sin modificar el original
5. Eliminar los duplicados de un array, utilizando `Array.filter()`.
6. Eliminar los duplicados de un array, utilizando `Array.reduce()`.
7. Eliminar los duplicados de un array, utilizando `Set`.
8. Chequear si una palabra es _palíndromo_sup id="cite_ref-3"><a href="#cite_note-3">[3]</a></sup>
9. Implementar la función `map()` de `Array` usando `reduce()`.
10. Implementar la función `filter()` de `Array` usando `reduce()`.

## Lectura recomendada: [Functional-Light JS - Kyle Simpson](https://github.com/getify/Functional-Light-JS)

---

<sup id="cite_note-1"><a href="#cite_ref-1">1</a></sup> Esto se que se conoce como [idempotencia](https://es.wikipedia.org/wiki/Idempotencia).

<sup id="cite_note-2"><a href="#cite_ref-2">2</a></sup> Se conoce como _mutator_ a los métodos/funciones que modifican los objetos recibidos como argumentos, y _accesor_ a las funciones que retornan un nuevo valor, basado en el input.

<sup id="cite_note-3"><a href="#cite_ref-3">3</a></sup> Un palíndromo es una palabra o frase que se lee igual para adelante y para atrás.
