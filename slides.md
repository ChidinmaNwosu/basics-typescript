---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Typescript-The basics.
info: |
  ## Typescript: The Basics.
  Creating clean code, one step at a time.

  Learn more at [Sli.dev](https://sli.dev)
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# https://sli.dev/guide/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/guide/syntax#mdc-syntax
mdc: true
---

# Typescript: The basics.

Creating clean code, one step at a time.

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: fade-out
---

# What is TypeScript?
<div></div>
Typescript is a superset of JavaScript. It builds on JavaScript by adding static typing with optional typying annotations. TypeScript is a strongly typed programming language that builds on JavaScript.<br>
<br>


# Prerequisites
<div></div>
Before we go into the basics of Typescipt, you should have gone through or read through:
 <v-clicks> 
 <ul> 
<li>Typescript for New programmers.</li>
<li>Typescript: A static type checker.</li>
<li>A typped superset of JavaScript.</li>
<li>Typescript for Javascript programmers.</li>
<li>Types by inference, defining types, composing types(unions, generics),and structural type system.</li>
<li>Typesscript tooling.</li>
<li>Type annotations(using interfaces and classes).</li>
</ul>
</v-clicks>

Read more about [Typescript](https://typescriptlang.org/)

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #FFD700 10%, #FFD700 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

<!--
Here is another comment.
-->

---

# Let's get started: The Basics of Typescript

- <Link to="8">Static type-checking</Link>
- <Link to="9">Non-exception failures</Link>
- <Link to="11">Types for tooling</Link>
- <Link to="12">Tsc,the Typescript compiler</Link>
- <Link to="14">Emitting with Errors</Link>
- <Link to="15">Explicit Types</Link>
- <Link to="16">Erased Types</Link>
- <Link to="17">Downlevling</Link>
- <Link to="18">Strictness</Link>
- <Link to="18">noImplicitAny</Link>
- <Link to="18">strictNullChecks</Link>

<style scoped>
  h1 {
    color: #FFD700;
  }
</style>
---

# Introduction: The Basics of Typescript.
<div></div>
<v-click>
The behaviour of each operation is determined by the value given to it. Each and every value in javascript  has a set of behaviours that you can observe from running different operations. If we don't know the value of an operation we can't reliably say what the result will be!
</v-click>

```javascript
function add(a, b) {
  return a+ b;
}
add();//  We called our function without arguments

```
Or:

```javascript
message.toLowerCase()//accessing the property toLowerCase() in message

message();//calling the message function
```
Let us assume that we don't know the value of message, we can't reliably say what the result will be. Things to note:

- Is message callable?
- Does message have a property called toLowerCase() ?
- If it does, is toLowerCase() callable?

<style scoped>
  h1 {
    color: #FFD700;
  }

</style>

---

- If both of these values are callable, what do they return?

Let's say that 'message' is defined as follows:

```javascript
const message = "Hello, world!";
```

- If we try to do (message.toLowerCase();) we will get "hello, world!"
- If we try to call(message();) we will get a type error:
```typescript
message is not a function
```

The way javascript runtime figures out what to do:

- figuring out the type.
- The behaviour and capabilities of the value type.

NOTE: Some primitive values such as "string" and "number", their type can be determined at runtime using the **typeof operator**. But for functions, there is no corresponding runtime mechanism to identify their types.

---
hideInToc: true
---

# What is a type?
<div></div>
In TypeScript, a type is a fundamental concept that allows you to describe the shape and behavior of values. A type:
- defines the structure and characteristics of a value.
- specifies the properties, methods, and behavior associated with that value.
-  helps TypeScript catch errors early and provide better tooling support.<br>

# Examples of types.
<div></div>
TypeScript includes various built-in types:

**Primitive Types**
- string: Represents text data.
- number: Represents numeric values.
- boolean: Has true and false values.
- null: Has only one value: null.
- undefined: Has only one value: undefined.
- symbol: Represents a unique constant value.

<style scoped>
  h1 {
    color: #FFD700;
  }
</style>

---

**Object Types**
- Functions, arrays, classes, and custom object types fall into this category.
- You can create your own object types using interfaces or type aliases.
<br/>
<br/>

<v-click>
Javascript => dynamically typed => running code to see what happens<br/>
</v-click>
<v-click>
Typescript => statically typed => what the code is expected to do before it runs
</v-click>
<br/>
<br/>

---

# STATIC TYPE CHECKING
<div></div>
let us this back to the error(bug) we got trying to call our message variable as a function! Typescript is a tool that helps us find the bugs before we run our code, hence, it is a static type checker.Eg:

```typescript
  const message ="hello!"; 
  //string
  message();
  // This expression is not callable. Type 'string' has no call signatures
```
<style scoped>
  h1 {
    color: #FFD700;
  }
</style>

---

# NON-EXCEPTION FAILURES
<div></div>
Javascript ECMAScript specifiactions has explicit instructions on  how the language should behave when it runs into something unexpected. For example, trying to call something that is not callable should throw an error, but why is Javascript returning undefined for the code below?

```javascript
    const user = {
      name: "Chidinma",
      age: 26,
    };

    user.id;
    //it is not declared 
    //return undefined
```
NOTE: Typescript makes a call of what code should be flagged as an error in the system, even if it is "vaild" Javascript, that won't immediately throw an errorr. Eg:

```typescript
  const user = {
    name: "Chidinma",
    age: 26,
  }
user.id;
//Property of 'id' doesn't exist on type '{name:string, age:number}'.
```
<style scoped>
  h1 {
    color: #FFD700;
  }
</style>

---

# The bugs Typescript handles

- Typos:
```typescript
greet.toLocaleLowercase(); 
greet.toLocalLowerCase(); 
greet.toLocaleLowerCase(); 
//Spot the correctly written code
```

- Uncalled function
```typescript
function randomNum(){
  return Math.random < 0.5;
}
//Error thrown: Operator '<' cannot be applied to types '()=>number' and 'number'
```

- Basic errors
```typescript
const randonValue = Math.random() < 0.5 ? "a" : "b" ;
if (value !== "a"){
  //...
 } else if(value ==="b"){
    //Oops, ureacheable
}
//Error message: This comparism appears to be unintentional beacuse 'a' and 'b' have no overlap
```

<style scoped>
  h1 {
    color: #FFD700;
  }
</style>

---

# TYPES FOR TOOLING
<div></div>
<v-click>
Typescript can catch bugs when we make mistakes with our code. 
</v-click>
<v-click>
Typescript can also prevent us from making those mistakes in the first place. 
</v-click>
<v-click>
The type-checker makes sure we are accessing the right properties on variables, and  it can also suggest properties we might use or want to use.
</v-click>
<br />
<v-click>
Typescript takes tooling seriously, it goes beyond "completions" and "error" as you type. Examples of tools in Typescript are:
</v-click> 

- tsc: helps you compile a javascript file that is a replica of the Typescript file.
- typescript language service: it provides auto-completion, type checking, error highlighting in editors
- tsconfig.json: allows you configure your own tsc option for your project.
- Type definitions(.d.ts files): provides you with info about existing Javascript libraries and API's.

<style scoped>
  h1 {
    color: #FFD700;
  }
</style>

---

# TSC-TYPESCRIPT COMPILER
<div></div>

Step 1: Create a folder 
```typescript
mkdir typescript-practice
```
Step 2: Change into that directory

```javascript
cd typescript-practice
```
Step 3: This installs tsc globally, we can use "npx" or similar tools if you'd prefer to run "tsc" from a "local node_modules package" instead.
```typescript
npm install -g typescript
```
Step 4: Create a file called **hello.ts**, our first typecsript program
```javascript
console.log("Hello, World!"); 
//Greets the world
```
Step 5: Let us type check it using **command tsc**
```typescript
tsc hello.ts
```

<style scoped>
  h1 {
    color: #FFD700;
  }
</style>

---

Step 6: let us introduce a type checking error to our hello.ts file

```typescript
function greet(person, date){
  console.log(`Hello ${person}, today is ${date}!`);
}
greet("chidinma");
```
Step 7: If we run our command tsc, we will get an error
```typescript
tsc hello.ts

Expected 2 arguemnts, but got 1
```

---

# EMITTING WITH ERRORS
<div></div>
The "--noEmitOnError flag" affects the behaviour of the tsc. It disables emitting files if any type checking errors are reported. It instructs typecript not to emit any output files (eg Javascript source code) if there are any errors during the compilation process. How do we enable it?

```typescript
noEmitOnError: true,
```
or:
```typescript
tsc --noEmitOnError hello.ts
```

<style scoped>
  h1 {
    color: #FFD700;
  }
</style>

---

# EXPLICIT TYPES
<div></div>
Till this very moment we haven't told TypeScript what "person" and "date" is. "Person" is a string and "date" is should be a Date object. We can use some methods(toString()method) on our date parameter. For example:

```typescript
function greet(person:string, date: Date){
   console.log(`Hello ${person}, today is ${date.toDateString()}!`);
}
```
We added type annotations(:) to 'person' and 'date' to describe what type of value greet can be called with.
<br/>
If we call our greet function like this, an error will be thrown:

```typescript
greet("Chidinma", Date());
// Argument type 'string' is not assignable to paramater of type 'Date'
```
Calling Date() in javascript returns a 'string' while constructing a Date with new Date() actually gives what we are expecting(an object). To fix the error, we do this:

```typescript
function greet(person:string, date: Date){
  console.log(`Hello ${person}, today is ${date.toDateString()}!`);
}
//call our greet function
greet("Chidinma", new Date());
```

<style scoped>
  h1 {
    color: #FFD700;
  }
</style>

---

Note: We don't always have to write explicit type annotations, in many cases typescript can just infer(figure out) the types for us, even if we omit them, Eg:

```typescript
let msg = "hello, there!";
// let msg:string
```

# ERASED TYPES 
<div></div>
What happens when you compile the above function to JavaScript using tsc ?

```javascript
'use strict';
function greet(person, date){
  //it stripped our type annotations
  console.log('Hello'.concat(person, 'today is').concat(date.toDateString(), '!'));
  //our template strings was converted to plain strings with concatenations.
}

greet('chidinma', new Date());

```
NB:Type annotations aren't a part of JavaScript/ECMAScript.

<style scoped>
  h1 {
    color: #FFD700;
  }
</style>

---

# DOWNLEVELING
<div></div>
Another thing to note is the own template string was rewritten from:

```typescript
`Hello ${person}, today is ${date.toDateString()}!`;
```
to:
```typescript
"Hello".concat(person, "today is").concat(date.toDateString(), "!");
```

<span><v-mark>WHY?</v-mark></span>
<br>

- Template strings are a feature from a version of ECMAScript called ECMAScript 2015/ ECMASCript 6/ ES2015/ ES6.

- Typescript has the ability to rewrite code from a newer version of ECMAScript to an older one like: ECMAScript 3 or ECMAScript 5(ES3 and ES5 rwspectively).

- This ability is called downleveling. By default, typescript targets ES3, to stop this default behaviour, we can do this:

```typescript
tsc ---target es2015 hello.ts
//change target option
```

<style scoped>
  h1 {
    color: #FFD700;
  }
</style>

---

# STRICTNESS
<div></div>
In typescript, types are optional, you can opt for a loose-type check or a strict-type check. Typescript has several typechecking strictness flags that you can turn on and off using a boolean value. For example:

- The strict flag in the CLI
- "strict": true; in the tsconfig
- noImplicitAny: assigns the (:any) type to 'null' and 'undefined'.
- strictNullChecks: treats 'null' and 'undefined' as distinct types, so it raises an alarm or throws an error when we try to use null or undefined where a concrete value is expected.

NOTE: In our tsconfig.json file,we can assign a boolean value of 'true' to our noImplicitAny and strictNullChecks to activate them.

<style scoped>
  h1 {
    color: #FFD700;
  }
</style>

---
layout: center
---

<p>Thank You: Any Questions????</p>

<style scoped>
  p {
    color: #FFD700;
    font-size: 50px;
  }
</style>
