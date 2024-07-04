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

Typescript is a superset of JavaScript. It builds on JavaScript by adding static typing with optional typying annotations. TypeScript is a strongly typed programming language that build 

#Prerequisites
   Before we go into the basics of Typescipt, you should have gone through or read through: 

- Typescript for New programmers.
- Typescript: A static type checker.
- A typped superset of JavaScript.
- Typescript for Javascript programmers.
- Types by inference, defining types, composing types(unions, generics),and structural type system.
- Typesscript tooling.
- Type annotations(using interfaces and classes).

<br>
<br>

Read more about [Typescript](https://typescriptlang.org/)

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
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
    We will be looking at the following:

- Static type-checking
- Non-exception Failures
- Types for Tooling
- tsc, the TypeScript compiler
- Emitting with Errors
- Explicit Types
- Erased Types
- Downleveling
- Strictness
- noImplicitAny
- strictNullChecks

---

# Introduction: The Basics of Typescript.

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
In TypeScript, a type is a fundamental concept that allows you to describe the shape and behavior of values. A type:

- defines the structure and characteristics of a value.
- specifies the properties, methods, and behavior associated with that value.
-  helps TypeScript catch errors early and provide better tooling support.

Examples of types.
TypeScript includes various built-in types:

**Primitive Types**
- string: Represents text data.
- number: Represents numeric values.
- boolean: Has true and false values.
- null: Has only one value: null.
- undefined: Has only one value: undefined.
- symbol: Represents a unique constant value.

---
hideInToc: true
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

#### **STATIC TYPE CHECKING**
let us this back to the error(bug) we got trying to call our message variable as a function! Typescript is a tool that helps us find the bugs before we run our code, hence, it is a static type checker.
  Eg:
```typescript
  const message ="hello!"; 
  //string
  message();
  // This expression is not callable. Type 'string' has no call signatures
```

---
hideInToc: true
---

# NON-EXCEPTION FAILURES

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

---
hideInToc: true
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
---
hideInToc:true
---

