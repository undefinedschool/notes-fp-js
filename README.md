# ![Programación Funcional con JavaScript](https://i.imgur.com/Mn8UzGQ.png)

<div align="center">  
  <p align="center">
  <sub>
    Estas notas fueron elaboradas por <a href="https://twitter.com/_nhsz" target="_blank" rel="noreferrer noopener">@_nhsz</a>, como parte del contenido de los cursos de <a href="https://undefinedschool.io/" target="_blank" rel="noreferrer noopener"><strong>undefined school</strong></a>, una escuela de <strong>Desarrollo Web Full Stack JavaScript</strong>, <a href="https://github.com/undefinedschool/" target="_blank" rel="noreferrer noopener">100% Open Source</a>, con <strong>mentorías personalizadas para grupos reducidos</strong> y el foco puesto en los <strong>fundamentos</strong> y <strong>conceptos avanzados</strong> ⚡
  </sub>
  </p>
  
  <p align="center">
  <sub>
    Si te resultaron útiles, te cuento que soy muy fan del café; si querés colaborar para que no me quede dormido y siga escribiendo guías, apuntes y más <strong>contenido Open Source en español</strong>, podés invitarme uno, gracias! ❤️
  </sub>
  </p>
  
  <p align="center">
  ☕
  <code> 
  <a mp-mode="dftl" href="https://www.mercadopago.com.ar/checkout/v1/redirect?pref_id=243772354-b32a750f-2505-41c1-8e5e-9dcdb4536593" name="MP-payButton" class='blue-ar-l-rn-none'>
    <strong>Invitame 1 café!</strong>
  </a>
  </code>
  </p>
  <hr>
</div>

👉 Ver [todas las notas](https://github.com/undefinedschool/notes)

## Contenido

- [Intro](https://github.com/undefinedschool/notes-fp-js#intro)
- [Paradigma](https://github.com/undefinedschool/notes-fp-js#paradigma)
- [Conceptos](https://github.com/undefinedschool/notes-fp-js#conceptos)
  - [Función](https://github.com/undefinedschool/notes-fp-js#funci%C3%B3n)
  - [Aridad](https://github.com/undefinedschool/notes-fp-js#aridad)
  - [Transparencia referencial](https://github.com/undefinedschool/notes-fp-js#transparencia-referencial)
  - [Funciones _First-Class_](https://github.com/undefinedschool/notes-fp-js#funciones-first-class)
  - [_Higher-Order Functions_](https://github.com/undefinedschool/notes-fp-js#higher-order-functions)
  - [Declarativo vs Imperativo](https://github.com/undefinedschool/notes-fp-js#declarativo-vs-imperativo)
  - [_Side Effects_](https://github.com/undefinedschool/notes-fp-js#side-effects)
  - [Estado compartido](https://github.com/undefinedschool/notes-fp-js#estado-compartido)
  - [Inmutabilidad](https://github.com/undefinedschool/notes-fp-js#inmutabilidad)
    - [Inmutabilidad, `const` y objetos en JS](https://github.com/undefinedschool/notes-fp-js#inmutabilidad-const-y-objetos-en-js)
  - [Funciones puras](https://github.com/undefinedschool/notes-fp-js#funciones-puras)
    - [Otros beneficios de utilizar funciones puras](https://github.com/undefinedschool/notes-fp-js/blob/master/README.md#otros-beneficios-de-utilizar-funciones-puras)
    - [Ejercicios](https://github.com/undefinedschool/notes-fp-js#ejercicios)
  - [Composición de funciones](https://github.com/undefinedschool/notes-fp-js#composici%C3%B3n-de-funciones)
    - [`compose`](https://github.com/undefinedschool/notes-fp-js#compose)
    - [`pipe`](https://github.com/undefinedschool/notes-fp-js#pipe)
      - [_Pipeline operator_](https://github.com/undefinedschool/notes-fp-js#pipeline-operator)
    - [Ejercicio](https://github.com/undefinedschool/notes-fp-js#ejercicio)
  - [`reduce`](https://github.com/undefinedschool/notes-fp-js#reduce)
  - [_Point-Free Style_](https://github.com/undefinedschool/notes-fp-js#point-free-style)
  - [Recursión](https://github.com/undefinedschool/notes-fp-js#recursi%C3%B3n)
    - [Recursión y ciclos](https://github.com/undefinedschool/notes-fp-js/blob/master/README.md#recursi%C3%B3n-y-ciclos)
  - [Closures](https://github.com/undefinedschool/notes-fp-js#closures)
  - [Function Decorators](https://github.com/undefinedschool/notes-fp-js/blob/master/README.md#function-decorators)
  - [Currying]()
- [Ejercicios](https://github.com/undefinedschool/notes-fp-js#ejercicios-1)
  - [Funciones Puras](https://github.com/undefinedschool/notes-fp-js#funciones-puras-1)
  - [Higher-Order Functions](https://github.com/undefinedschool/notes-fp-js/blob/master/README.md#higher-order-functions-1)
  - [Composición de funciones](https://github.com/undefinedschool/notes-fp-js/blob/master/README.md#composici%C3%B3n-de-funciones-1)
  - [Recursión](https://github.com/undefinedschool/notes-fp-js#recursi%C3%B3n-1)
  - [Closures](https://github.com/undefinedschool/notes-fp-js#closures-1)
  - [Reduce](https://github.com/undefinedschool/notes-fp-js/blob/master/README.md#reduce-1)
- [Lecturas Recomendadas](https://github.com/undefinedschool/notes-fp-js#lecturas-recomendadas)

---

## Intro 

A medida que la cantidad de líneas del código de nuestra aplicación va aumentando, debemos tener cuidado al hacer cambios y pensar a qué otras partes del código estamos afectando.

La forma más simple que conocemos para acotar el _scope_ de cierto bloque de código y construir software son las **funciones**. Nos permiten, además de reutilizar, reducir el potencial impacto de nuestros cambios. Pero aún así, razonar y entender bien qué hace cada línea de nuestras funciones puede resultar complejo y no está garantizado que no provoque efectos por fuera del scope (aka _side effects_), por ejemplo, si utilizamos variables globales.

Además, el estilo con el que solemos escribir nuestras funciones suele ser indicar las instrucciones, paso a paso, que queremos que ejecute la computadora, es decir, un modo _imperativo_: hablamos de _cómo_ hacer las cosas en lugar del _qué_ (_declarativo_).

Imaginemos que podemos estructurar nuestro código en pequeñas piezas, individuales, independientes, auto-contenidas, donde

- el resultado de la ejecución de cada pieza **depende sólo de sus inputs**
- las únicas consecuencias o **efectos provocados son sus outputs** (no hay _side effects_)
- cada una de estas piezas de código es declarativa, haciéndola más legible

Cómo podríamos lograr esto?

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

## Paradigma 

La programación funcional es un **paradigma de programación** que nos sirve para estructurar, organizar y controlar la complejidad de nuestro código, favoreciendo un estilo más [**_declarativo_**](https://github.com/undefinedschool/notes-fp-js#declarativo-vs-imperativo)_, componiendo [**_funciones puras_**](https://github.com/undefinedschool/notes-fp-js#funciones-puras) para construir aplicaciones, evitando el uso de [**_estado compartido_**](https://github.com/undefinedschool/notes-fp-js#estado-compartido), los [**_datos mutables_**](https://github.com/undefinedschool/notes-fp-js#inmutabilidad) y los [**_side effects_**](https://github.com/undefinedschool/notes-fp-js#side-effects), logrando así que el código resulte...

➕ legible    
➕ declarativo  
➕ simple (sólo tenemos valores y funciones)     
➕ fácil de razonar  
➕ fácil de debuggear (cada función es una unidad con input/output definido)   
➕ fácil de testear, si usamos funciones puras  
➕ fácil de extender (podemos agregar funcionalidades combinando otras ya existentes)   
➕ fácil de refactorizar (nuevamente, sólo tenemos valores y funciones)   
➕ performance, si paralelizamos la ejecución de código      
➖ _side effects_  
➖ bugs    

Para esto, vamos a utilizar

- funciones pequeñas, puras: sólo dependen de sus inputs y no de otras partes del código   
- sin _side effects_: no hay consecuencias más allá del scope de la función y su output
- composición: construimos nuestra aplicación a partir de estos bloques

Nuestra aplicación estará definida en términos de una función principal. La función principal se define a partir de otras funciones, que a su vez se definen a partir de otras funciones, etc, hasta llegar a valores de tipos primitivos como `number` o `string`.

El _estado_ de nuestra aplicación fluye a través de _funciones puras_, en contraste con lo que sucede en la [_Programación Orientada a Objetos_](https://github.com/undefinedschool/notes-oop-js), donde el estado de las aplicaciones es usualmente compartido en objetos y manipulado a través de sus métodos.

Usar [_funciones puras_](https://github.com/undefinedschool/notes-fp-js#funciones-puras) y [_componerlas_](https://github.com/undefinedschool/notes-fp-js#composici%C3%B3n-de-funciones) para resolver problemas más grandes son habilidades muy útiles que pueden ser utilizadas para simplificar esta complejidad.

👉 Tengamos en cuenta que **simple no significa _fácil_**: los problemas difíciles lo seguirán siendo, el paradigma funcional no va a cambiar esto, **la simplificación viene dada porque los problemas resultan más fáciles de razonar, al descomponerlos en subproblemas**. Estos problemas son mucho más sencillos de resolver de forma independiente y pueden componerse para llegar a la solución buscada.

> JavaScript no es un lenguaje de programación funcional _puro_, pero tiene soporte para algunas características del paradigma. Existen lenguajes funcionales puros que compilan a JavaScript (y pueden utilizarse en frontend), como [Elm](https://elm-lang.org/), [ClojureScript](https://clojurescript.org/) y [PureScript](https://www.purescript.org/)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

## Conceptos

### Función

![Función: un proceso que recibe determinado input y produce cierto output](https://www.thatsoftwaredude.com/images/post/166952a8-ac94-4d24-9b42-22f982096e4e.png)

Las funciones son procesos que reciben determinado _input_ y producen cierto _output_.

Utilizamos funciones principalmente para:

- _mappear_ inputs a determinados outputs: una función recibe argumentos y retorna un valor, por lo que para cada input existe un output
- procedimientos: una función puede invocarse para ejecutar una secuencia de instrucciones, conocida como procedimiento
- I/O: una función puede comunicarse con otras partes del sistema/periféricos (requests HTTP, interacción con una DB, obtener input a través de la terminal, etc)

En el paradigma funcional, las funciones cumplen con las siguientes características:

- Son [puras](https://github.com/undefinedschool/notes-fp-js#funciones-puras)
- Usan [datos inmutables](https://github.com/undefinedschool/notes-fp-js#inmutabilidad)
- Tienen [transparencia referencial](https://github.com/undefinedschool/notes-fp-js#transparencia-referencial)
- Son de [primera clase](https://github.com/undefinedschool/notes-fp-js#funciones-first-class)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

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

👉 **Es importante respetar la aridad de las funciones cuando estamos [componiendo]()**

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

### Transparencia referencial

Decimos que una expresión es _referencialmente transparente_ si puede ser reemplazada por su valor, sin alterar el comportamiento del programa.

Por ejemplo, si tenemos la siguiente función

```js
const greet = () => 'Hello World!';
```

cualquier invocación de `greet()` puede ser reemplazada por el string `'Hello World!'` perfectamente, por lo tanto tiene transparencia referencial.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

### Funciones _First-Class_

En un lenguaje de programación funcional, las funciones son [**_First-Class Citizens_**](https://github.com/undefinedschool/notes-functions-first-class) (es decir, pueden tratarse como cualquier otro valor) y JavaScript cumple con esto.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

### _Higher-Order Functions_

Si una función acepta otras funciones como argumentos (por ejemplo, cada vez que usamos _callbacks_ en JS/Node) o retorna funciones, se dice que es una **_función de alto orden o Higher-Order Function_** (alcanza con que cumpla alguna de las 2 características).

Algunos métodos de `Array`, como [`map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map), [`filter()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) y [`reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) son funciones de alto orden.

[![Higher-order functions - Part 1 of Functional Programming in JavaScript](https://img.youtube.com/vi/BMUiFMZr7vk/0.jpg)](https://www.youtube.com/watch?v=BMUiFMZr7vk)
> Ver [Higher-order functions - Part 1 of Functional Programming in JavaScript](https://www.youtube.com/watch?v=BMUiFMZr7vk)

👉 **Esta característica es la que nos va a permitir...**

- [componer](https://github.com/undefinedschool/notes-fp-js#composici%C3%B3n-de-funciones) funciones.**
- generalizar funciones, al poder pasar funciones por parámetro (pensar por ejemplo en lo que hacen `map`, `filter` y `reduce`)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

### Declarativo vs Imperativo

Cuando utilizamos un enfoque _imperativo_, definimos todos los pasos necesarios para cumplir cierta tarea. **Con un enfoque _declarativo_ en cambio, le decimos a la computadora qué hacer y que la misma se encargue de resolver los detalles**, abstrayéndonos de estos. Notemos que podemos manejar diferentes **niveles de abstracción**: JavaScript por si mismo ya es mucho más declarativo que el código máquina que termina produciendo el compilador/intérprete.

Por ejemplo, cuando estamos iterando arrays, el enfoque más imperativo sería utilizar `for` o `while` para definir los ciclos. `for...of` es más declarativo, ya que nos abstrae de ciertos detalles como la longitud, mientras que métodos como `map`, `filter` y `reduce` son más declarativos todavía, porque directamente toman el enfoque funcional.

Algunos lenguajes declarativos que ya conocemos y venimos utilizando son HTML y SQL.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

### _Side Effects_

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

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

### Estado compartido

Tener estado (variables) compartido hace que nuestra aplicación se vuelva más frágil (_error-prone_), difícil de razonar y eventualmente, de debuggear, ya que puede haber otras partes del código, módulos o incluso código externo, como dependencias u otro software que use nuestra aplicación, que puedan estar modificando este estado, volviendo más complejo el seguimiento de la evolución del mismo.

Podemos tener estado compartido en

- Clases
- Variables globales
- Argumentos pasados por referencia (objetos)

Las funciones limitan los cambios realizados al estado del programa, evitando acceder a variables globales, reduciendo así los posibles [_side-effects_](https://github.com/undefinedschool/notes-fp-js#side-effects). Es por esta razón que usamos [funciones puras](https://github.com/undefinedschool/notes-fp-js#funciones-puras) en el paradigma funcional.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

### Inmutabilidad

Decimos que **los datos son _inmutables_ si nunca cambian (no pueden modificarse)**. En el paradigma funcional, los datos son inmutables. Utilizar valores inmutables facilita mucho razonar sobre el código de nuestra aplicación, ya que no modificaremos accidentalmente el [estado](https://github.com/undefinedschool/notes-fp-js#estado-compartido) de la misma, por lo que es recomendable aplicar esta característica del paradigma siempre que podamos.

> De ahora en más entonces, vamos a llamar _mutación_ al cambio o alteración de valores y _side effect_ al resultado de esta acción. Recordemos que, idealmente, las funciones que utilicemos deben ser [puras](https://github.com/undefinedschool/notes-fp-js#funciones-puras), es decir, que no generan ningún tipo de side effect.

Las _variables_ entonces, pasan a ser _constantes_, no pueden modificarse: una vez creada una variable con cierto valor, la única forma que tenemos de modificar el mismo es creando una nueva variable con el nuevo valor. 

Por ejemplo, si queremos modificar un array, para agregar un nuevo ítem al mismo, creamos un nuevo array concatenando el array anterior con el nuevo ítem.

```js
const originalArray = [1, 2, 3];
const newArray = [...originalArray, 4];
```

> Ejemplo: agregar un ítem a un array sin modificar el original, utilizando [`spread operator`](https://github.com/undefinedschool/notes-es6-spread-operator)

👉 **La única forma de modificar datos es creando copias modificadas**

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

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

> Si queremos trabajar con objetos _inmutables_ podemos utilizar el método [`Object.freeze()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)<sup id="cite_ref-4"><a href="#cite_note-4">[4]</a></sup> o la librería [Immer.js](https://immerjs.github.io/immer/)

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

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

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

#### Otros beneficios de utilizar funciones puras

- **Las funciones puras son más robustas**: el orden de ejecución no tienen ningún impacto en el sistema. 
- Las operaciones realizadas con funciones puras pueden ser paralelizadas.
- [**Más fáciles de testear**](https://blog.ploeh.dk/2015/05/07/functional-design-is-intrinsically-testable/) (unit tests), ya que no debemos considerar ningún contexto o estado externo, sólo el input y el output de la función.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

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

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

### Composición de funciones

El rol de una función es tomar un valor inicial y transformarlo en otro. La composición nos permite combinar funciones, para que podamos aplicar una serie de transformaciones hasta alcanzar un valor final.

**La composición consiste entonces en utilizar el resultado de una función (_output_) como argumento (_input_) de otra función**.

Podemos utilizar la composición cuando coinciden la cantidad y el tipo de retorno de una función con el tipo de argumento de otra, es decir, respetamos la [aridad](https://github.com/undefinedschool/notes-fp-js#aridad).

De esta forma, combinando 2 o más funciones simples (funciones que, en lo posible, hagan 1 sola cosa) podemos crear funciones más complejas.

Es el mecanismo que nos provee el paradigma para reutilizar y evitar la duplicación de código (DRY).

```js
const f = x => x + 1;
const g = y => y * 2;
const h = z => z ** 3; 
const number = 3;

const result = f(g(h(number)));
```

> Ejemplo: composición de funciones usando la notación matemática

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

> Ejemplo: usando `pipe()`

El paradigma de programación funcional utiliza [funciones puras](https://github.com/undefinedschool/notes-fp-js#funciones-puras) como la _unidad primaria de composición_: son los bloques con los que vamos a construir nuestra aplicación.

Para facilitar la composición, es recomendable que las funciones que utilicemos...

- tengan un propósito bien definido, es decir, hagan 1 sola cosa
- sean lo suficientemente genéricas

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

#### `compose`

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

Utilizando [`reduceRight`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/ReduceRight) (para procesar los valores _de adentro hacia afuera_), podemos escribir una _función de composición_ para obtener el mismo resultado.

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

> Ejemplo: función de composición

👉 **`compose` aplica la composición leyendo los argumentos** (que en este caso son funciones) **de DERECHA a IZQUIERDA**, ya que se basa en el orden que usamos cuando componemos funciones en matemáticas, es decir, de adentro hacia afuera. **Conviene utilizarlo cuando resulta más natural pensar en términos de la composición matemática**, ya que el orden de evaluación es _de adentro hacia afuera_. **También es muy útil en desarrollo de UIs, por ejemplo cuando queremos [componer componentes](https://reactjs.org/docs/higher-order-components.html#convention-maximizing-composability).**

![compose](https://i.imgur.com/Fv87jpw.png)

> Este patrón es muy común en la programación funcional y podemos implementarlo utilizando el método [`compose`](https://ramdajs.com/docs/#compose) de la librería utilitaria [Ramda](https://ramdajs.com/)

Un tip muy útil para _debuggear_ es utilizar funciones para _tracear_ el input/output de cada función

```js
const trace = msg => x => (console.log(msg, x), x);
```

```js
const bookTitles = {
  'The Culture Code',
  'Designing Your Life',
  'Algorithms to Live By'
}

const slugify = compose(
  map(join('-')),
  trace('after split'),
  map(split(' ')),
  trace('after lowercase'),
  map(lowerCase),
  trace('before lowercase')
)(bookTitles);
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

#### `pipe`

Además del `compose`, otro patrón muy común en la programación funcional para componer funciones es el `pipe`. Utilizando `reduce`, podemos escribir una _función de composición_ para obtener el mismo resultado.

```js
const pipe = (...fns) => 
  x => fns.reduce((acc, fn) => fn(acc), x);
```

👉 **`pipe` aplica la composición leyendo los argumentos** (que en este caso son funciones) **de IZQUIERDA a DERECHA**, por lo que el orden en el que le pasemos las funciones será el orden en el que las evalúe. **Conviene utilizarlo cuando resulta más natural pensar la composición como una serie de tareas a ejecutar a partir de un valor inicial.** Resulta muy útil, por ejemplo, para eliminar el uso de variables intermedias que sólo existen con el fin de almacenar valores temporales entre una operación y la siguiente.

![pipe](https://i.imgur.com/mE72Zzy.png)

> Este patrón es muy común en la programación funcional y también podemos implementarlo utilizando el método [`pipe`](https://ramdajs.com/0.19.0/docs/#pipe) de la librería utilitaria [Ramda](https://ramdajs.com/)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

##### _Pipeline operator_

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

[Ver ejemplo usando el _Pipeline operator_ en Codepen](https://codepen.io/nhquiroz/pen/xxwVWym)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

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

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

### `reduce`

Es una de las HOF más versátiles que existen

```js
const reducer = (accumulator, currentValue) => accumulator + currentValue;
```

> `reduce` recibe un callback al que llamamos `reducer`, que define cómo vamos a combinar 2 valores (acumulador y valor actual) para obtener otro, que será el input de la próxima iteración

Gracias a `reduce` podemos, por ejemplo

- implementar cualquier método de `Array` (incluyendo `map` y `filter`)
- **componer funciones**: es la base de `compose` y `pipe`

Por lo tanto se trata de una función muy importante dentro del paradigma funcional.

### _Point-Free Style_

En la programación imperativa, cuando realizamos algún tipo de operación sobre alguna variable, siempre vamos a encontrar referencias a la misma en cada paso.

En el paradigma funcional en cambio (y en JavaScript), muchas veces es frecuente operar con argumentos implícitos, es decir, que no están identificados. Por ejemplo, en el siguiente código

```js
const toSlug = pipe(
  split(' '),
  map(toLowerCase),
  join('-'),
  encodeURIComponent
);

console.log(toSlug('JS rlz'));
```

`pipe()` tiene un parámetro implícito (el string). Esta forma de escribir las funciones se conoce como _Point-Free_.

👉 **Otro caso común es utilizar _Point-Free_ para reemplazar funciones anónimas y escribir código más legible y declarativo**. Además, al definir funciones con un nombre, nos va a permitir testear estas funciones. 

Por ejemplo

```js
// utilizando un callback anónimo
const arr = [1, 2, 3];

arr.map(x => x * 2);
```

```js
// utilizando point-free
const arr = [1, 2, 3];
const double = x => x * 2;

arr.map(double);
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

### Recursión

Cuando una función se invoca a si misma, se la conoce como _función recursiva_.

**La recursión es una técnica de programación en la que la solución de un problema depende de las soluciones de sus _subproblemas_**. Los subproblemas consisten básicamente en variantes más pequeñas y sencillas del problema original, hasta llegar eventualemente a algún caso trivial, que llamaremos _caso base_.

Aparte del caso base, para asegurarnos de que enventualmente llegamos a él (y la función retorna un valor), cada llamada recursiva debe ser invocada con una instancia más simple (y diferente) del problema.

En algunas ocasiones, los algoritmos recursivos resultan legibles y simples de entender que sus versiones iterativas.

Un algoritmo recursivo está compuesto de

- **caso(s) base**: definen las condiciones para terminar y retornar la solución a un subproblema.
- **caso recursivo**: hacemos la llamada recursiva con una variante más simple del problema original. 

> Notar que cada vez que llamamos a la función recursiva, los argumentos deberían cambiar y _converger_ al caso base

En el siguiente ejemplo, la función `sumRange` devuelva la suma de los valores de 1 a `n`

```js
function sumRange(n) {
  // caso base
  if (n === 1) return 1;
  
  // llamada recursiva
  return n + sumRange(n - 1);
}
```

> Todo algoritmo recursivo debe tener al menos un caso base y retornar un valor, sino nunca va a terminar y generamos un _stack overflow_!

#### Recursión y ciclos

En el paradigma funcional buscamos evitar los [side effects](https://github.com/undefinedschool/notes-fp-js#side-effects). Al iterar utilizando un ciclo `for` o `while`, estamos reutilizando los resultados de la iteración previa en la siguiente y reasignando valores, como los índices. Es por eso que para iterar utilizamos algoritmos recursivos, para usar siempre funciones puras y valores inmutables.

👉 Ver más detalles en [Introduction to Recursion](https://www.rithmschool.com/courses/javascript-computer-science-fundamentals/introduction-to-recursion)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

### Closures

En programación funcional, los closures nos permiten utilizar [_currying_](https://www.yazeedb.com/posts/deeply-understand-currying-in-7-minutes) y _aplicaciones parciales_ de funciones.

👉 Ver [Notas sobre Closures](https://github.com/undefinedschool/notes-closures/)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

### Function Decorators

Nos permiten _editar_ o modificar el comportamiento de una función, sin reescribirla.

Para esto, se crea una nueva función, que recibe como argumento a la función que queremos _editar_ y utilizamos [_closures_](https://github.com/undefinedschool/notes-closures/) para mantener el estado interno.

Por ejemplo, si quisiéramos 'modificar' el comportamiento de una función para que este se ejecute una sola vez, podemos utilizar la función `once` definida a continuación. 

> `once` es lo que se conoce como _function decorator_ o simplemente _decorator_.

```js
function once(decoratedFn) {
  let counter = 0;

  function innerFn(input) {
    if (counter === 1) return 'Nope.';

    const output = decoratedFn(input);
    counter++;

    return output;
  }

  return innerFn;
}

const multiplyBy2 = x => x * 2;
const multiplyBy2Once = once(multiplyBy2);

multiplyBy2Once(2); // 4;
multiplyBy2Once(5); // 'Nope.'
```

### Currying

La _currificación_ es una técnica que nos permite manipular y transformar los inputs, para generalizar y favorecer la composición de funciones. Utilizando closures, podemos transformar los inputs de la función `add`

```js
const add = (x, y) => x + y;

add(2, 4); // 6
```

en

```js
const add = x =>
  y => x + y;
  
add(2)(4); // 6
```

La función retornada tiene acceso a `x` y a `y` (a través del closure), por lo que podemos hacer

```js
const add10 = add(10);

add10(10); // 20
add10(20); // 30
add10(30); // 40
```

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
8. Implementar la función `isPalindrome`, para chequear si una palabra es _palíndromo_<sup id="cite_ref-3"><a href="#cite_note-3">[3]</a></sup>
9. Implementar la función `map()` de `Array` usando `reduce()`.
10. Implementar la función `filter()` de `Array` usando `reduce()`.
11. Implementar la función `isAnagram: (string, string) -> boolean`, que recibe 2 palabras (o frases, puede haber espacios) y retorna `true` si estas son anagramas (es decir, están formadas por las mismas letras, en la misma cantidad).

Ejemplos de anagramas:

- saco / cosa
- certificable / rectificable
- enfriamiento / refinamiento
- anagramas / A ganar más

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

### Higher-Order Functions

1. Dado el siguiente código, qué problemas encontramos en el mismo? Cómo podemos mejorarlo/refactorizarlo? (usar siempre _funciones puras_)

```js
const copyArrayAndMultiplyBy2 = array => {
  const output = [];
  
  for (const elem of array) {
    output.push(elem * 2);
  }
  
  return output;
}

const copyArrayAndDivideBy2 = array => {
  const output = [];
  
  for (const elem of array) {
    output.push(elem / 2);
  }
  
  return output;
}

const copyArrayAndAdd2 = array => {
  const output = [];
  
  for (const elem of array) {
    output.push(elem + 2);
  }
  
  return output;
}

const arr = [1, 2, 3];

copyArrayAndMultiplyBy2(arr);
copyArrayAndDivideBy2(arr);
copyArrayAndAdd2(arr);
```

2. Implementar la función (pura) `generateUnorderedList`, que dado un array de números de tamaño `n`, genera una lista desordenada (`ul`) con `n` items (`li`), donde cada item de esta lista será un valor del array, realizando las operaciones necesarias en el DOM. Por ejemplo, a partir del array `[1, 2, 3, 4, 5]`, debería obtener la lista

```html
<ul>
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
  <li>5</li>
</ul>
```

Crear un `index.html` para ver el resultado. Implementar las funciones auxiliares (puras) necesarias y luego componer utilizando [`pipe()`](https://ramdajs.com/docs/#pipe) de [Ramda](https://ramdajs.com/).

3. Implementar la función `capitalize: string -> string`, que recibe un texto y devuelve el mismo con todas sus palabras teniendo la primer letra en mayúscula.

Ejemplo:

`'The quick brown fox jumps over the lazy dog' -> 'The Quick Brown Fox Jumps Over The Lazy Dog'`

### Composición de Funciones

1. Descomponer la función `capitalize` del ejercicio anterior (ítem 3) en pequeñas funciones (puras) que hagan 1 cosa y componerlas utilizando [`pipe()`](https://ramdajs.com/docs/#pipe) de [Ramda](https://ramdajs.com/).

2. El siguiente código calcula el costo de comprar algo online. Reescribirlo, utilizando composición de funciones puras. Para componer, vamos a utilizar [`compose`](https://ramdajs.com/docs/#compose) y [`pipe()`](https://ramdajs.com/docs/#pipe) de [Ramda](https://ramdajs.com/) (implementar las 2 versiones)

```js
const ITEM_PRICE = 10;

// tax (6%) + shipping (10)
const calculateTotal = (baseCost) => (1.06 * baseCost) + 10;
  
calculateTotal(ITEM_PRICE);
```

3. Agregar al ítem anterior la función `applySaleDiscount: (number, number) -> number`, que recibe un costo inicial y un porcentaje de descuento y retorna el valor final con el descuento aplicado. Componer esta función utilizando `pipe`, para calcular el costo de una compra online con un 10% de descuento.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

### Recursión

1. Implementar la función recursiva `length: Array -> number`, para calcular la longitud de un array. 

**Bonus:** resolver el ejercicio sin utilizar `Array.length`.

2. Implementar la función recursiva `productOfArray: Array -> number`, que recibe un array de enteros y retorna el producto de los mismos. Si el array es vacío, retornar 0.

3. Implementar la función recursiva `contains: (Object, value) -> boolean`, que devuelve `true` si un objeto contiene cierto valor. Notar que el objeto puede tener a su vez objetos anidados como propiedades, por ejemplo

```js
const nestedObject = {
  data: {
    info: {
      stuff: {
        thing: {
          moreStuff: {
            magicNumber: 44
          }
        }
      }
    }
  }
}

contains(nestedObject, 44);    // true
contains(nestedObject, "foo"); // false
```

4. Implementar la función recursiva `search: Array -> number`, que devuelve el índice de un elemento en un array. Si el valor no se encuentra, retornar -1.

```js
search([1,2,3,4,5],5;)  // 4
search([1,2,3,4,5],15); // -1
```

### Closures

1. Implementar la función `createFunctionPrinter`, que acepta un input (string) y retorna una función. Cuando la función creada es llamada, debe loguear el input utilizado cuando la función fue creada.

```js
const printSample = createFunctionPrinter('sample');
const printHello = createFunctionPrinter('hello');

printSample(); //should console.log('sample');
printHello(); //should console.log('hello');
```

2. Implementar la función `addX`, que retorna una función que incrementa el input en `X`.

```js
const addTwo = addX(2);

addTwo(1); // debe retornar 3
addTwo(2); // debe retornar 4
addTwo(3); // debe retornar 5

const addByThree = addX(3);
addThree(1); // debe retornar 4
addThree(2); // debe retornar 5
```

3. Dado el siguiente código, identificar los side effects y luego refactorizarlo para eliminar los mismos y que las funciones `travelToTheFuture` y `travelToThePast` sólo sean accesibles como métodos del objeto `timeMachine`.

```js
const currentYear = 2020;

function travelToTheFuture(years) {
  const newCurrentYear = currentYear + years;
  
  return newCurrentYear;
}

function travelToThePast(years) {
  const newCurrentYear = currentYear - years;
  
  return newCurrentYear;
}
```

4. Implementar la función `russianRoulette: number -> Function`, que acepta un número `n` y retorna una función. La función retornada no tiene argumentos y va a retornar el string `'Click.'` las primeras `n - 1` veces que es invocada. En la siguiente invocación (`n`, la enésima), la función retornada va a retornar el string `'BANG!'`. Luego, en cada invocación posterior, la función retornada va a retornar el string `'Reload to play again'`.

5. Implementar la función `average`, que no recibe argumentos y retorna una función (que puede recibir un número como su único argumento o ningún argumento directamente). Cuando la función retornada es invocada con un número, el output debe ser el promedio de todos los números que se le pasaron a la función (incluyendo valores duplicados). Cuando la función retornada es invocada sin argumentos, debe retornar el promedio actual. Si la función retornada es invocada sin argumentos antes de que se le pase cualquier número, debe retornar 0.

### Reduce

1. Implementar la función `allTestPassed`, que recibe un array de funciones evaluadoras que definen alguna condición sobre un input (c/u retorna un booleano) y un valor. Usando `reduce`, retornar un booleano indicando si el valor pasa o no todos los tests (funciones evaluadoras).

2. Implementar la función `movieSelector`, que recibe un array de objetos conteniendo información acerca de películas (id, título y puntaje). Encadenar invocaciones de `map`, `filter` y `reduce` para retornar un array que contenga sólo aquellar películas con un puntaje mayor a 5. 

## Lecturas recomendadas: 

- [⭐ Functional-Light JS - Kyle Simpson](https://github.com/getify/Functional-Light-JS) (**empezar por acá!**)
- [Professor Frisby's Mostly Adequate Guide to Functional Programming](https://mostly-adequate.gitbooks.io/mostly-adequate-guide/)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-fp-js#contenido)

---

<sup id="cite_note-1"><a href="#cite_ref-1">1</a></sup> Esto se que se conoce como [idempotencia](https://es.wikipedia.org/wiki/Idempotencia).

<sup id="cite_note-2"><a href="#cite_ref-2">2</a></sup> Se conoce como _mutator_ a los métodos/funciones que modifican los objetos recibidos como argumentos, y _accesor_ a las funciones que retornan un nuevo valor, basado en el input.

<sup id="cite_note-3"><a href="#cite_ref-3">3</a></sup> Un palíndromo es una palabra o frase que se lee igual para adelante y para atrás.

<sup id="cite_note-4"><a href="#cite_ref-4">4</a></sup> Tener en cuenta que `Object.freeze()` funciona a nivel [_shallow_](https://dev.to/krsgrnt/safely-copying-nested-objects-in-javascript-5fpi), es decir, sólo congela el primer nivel y no los objetos anidados, que siguen siendo referencias. Una posible solución para esto es utilizar el método [`cloneDeep()`](https://lodash.com/docs#cloneDeep) de [lodash](https://lodash.com/).
