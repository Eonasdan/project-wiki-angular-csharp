[[_TOC_]]

Note: The following guide has been adapted from the [here](https://github.com/basarat/typescript-book/blob/master/docs/styleguide/styleguide.md). Angular guidelines take precedence over guidelines listed here.

# Variable and Function

**Do** `camelCase` for variable and function names

**Why?** Conventional JavaScript.

```ts
/* avoid */
var FooVar;
function BarFunc() { }
```

```ts
var fooVar;
function barFunc() { }
```

**Do** use whole words in variable, function and property names.

**Avoid** short hand.

**Why?** Using descriptive terms makes it less confusing for the next person reading your code and improves readability.

```ts
/* avoid */
var ret;
function DSmTg() { }
```

```ts
var result;
//or even better
var userDto;
function doSomething() { }
```

## Declarations
**Do** explicitly declare the object type when required.
**Avoid** explicit type declaration when type is inferred (implicit).


```ts
/* avoid */
firstName: string = 'Bob';
function BarFunc() {
    var lastName: string = 'Builder';
}
```

```ts
firstName = 'Bob';
things: string[] = [];
mishap: AtbMishapObject;
function doSomething() {
    const lastName = 'Builder';
}
```


# Class
**Do** `PascalCase` for class names.

**Why?** Conventional JavaScript.

```ts
/* avoid */
class foo { }
```

```ts
class Foo { }
```

**Do** `camelCase` of class members and methods

**Why?** Naturally follows from variable and function naming convention.

```ts
/* avoid */
class Foo {
    Bar: number;
    Baz() { }
}
```

```ts
class Foo {
    bar: number;
    baz() { }
}
```

# Interface

**Do** `PascalCase` for name.

**Do** `camelCase` for members.

**Avoid** prefix with `I`

```ts
/* avoid */
interface IFoo {
}
```


```ts
interface Foo {
}
```

# Type

**Do** `PascalCase` for name.

**Do** `camelCase` for members.

# Namespace

**Do** `PascalCase` for names

**Why?** Convention followed by the TypeScript team. Namespaces are effectively just a class with static members. Class names are `PascalCase` => Namespace names are `PascalCase`

```ts
/* avoid */
namespace foo {
}
```

```ts
namespace Foo {
}
```

# Enum

**Do** `PascalCase` for enum names

```ts
/* avoid */
enum color {
}
```

```ts
enum Color {
}
```

**Do** `PascalCase` for enum member

**Why?** Convention followed by TypeScript team i.e. the language creators e.g `SyntaxKind.StringLiteral`. Also helps with translation (code generation) of other languages into TypeScript.

```ts
/* avoid */
enum Color {
    red
}
```

```ts
enum Color {
    Red
}
```

# Equality

**Do** use strict equality comparisons.
**Why** JavaScript differs from C# in that an abstract comparison `==` does not allows guarantee results compared to a strict comparison `===`
**Note** Strict comparison does not do type conversion e.g. `'0' === 0` will return `false`

```js
//javascript
var num = 0;
var obj = new String('0');
var str = '0';

console.log(num === num); // true
console.log(obj === obj); // true
console.log(str === str); // true

console.log(num === obj); // false
console.log(num === str); // false
console.log(obj === str); // false
console.log(null === undefined); // false
console.log(obj === null); // false
console.log(obj === undefined); // false
```

[See more on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)


# Null vs. Undefined

**Prefer** not to use either for explicit unavailability

**Why?** these values are commonly used to keep a consistent structure between values. In TypeScript you use *types* to denote the structure

```ts
/* avoid */
let foo = {x:123,y:undefined};
```

```ts
let foo:{x:number,y?:number} = {x:123};
```

**Do** use `undefined` in general (do consider returning an object like `{valid:boolean,value?:Foo}` instead)

**Avoid**
```ts
return null;
```

```ts
return undefined;
```

**Do** use `null` where its a part of the API or conventional

**Why?** It is conventional in Node.js e.g. `error` is `null` for NodeBack style callbacks.

```ts
/* avoid */
cb(undefined)
```

```ts
cb(null)
```

**Do** use *truthy* check for **objects** being `null` or `undefined`

```ts
/* avoid */
if (error === null)
```


```ts
if (error)
```

**Do** `== undefined` / `!= undefined` (not `===` / `!==`) to check for `null` / `undefined` on primitives as it works for both `null`/`undefined` but not other falsy values (like `''`,`0`,`false`) e.g.

```ts
/* avoid */
if (error !== null)
```

```ts
if (error != undefined)
```

# Formatting
The TypeScript compiler ships with a very nice formatting language service. Whatever output it gives by default is good enough to reduce the cognitive overload on the team.

Use [`tsfmt`](https://github.com/vvakame/typescript-formatter) to automatically format your code on the command line. Also your IDE (atom/vscode/vs/sublime) already has formatting support built-in.

Examples:
```ts
// Space before type i.e. foo:<space>string
const foo: string[] = [];
```

# Quotes

**Do** Prefer single quotes (`'`) unless escaping.

**Why?** More JavaScript teams do this (e.g. [airbnb](https://github.com/airbnb/javascript), [standard](https://github.com/feross/standard), [npm](https://github.com/npm/npm), [node](https://github.com/nodejs/node), [google/angular](https://github.com/angular/angular/), [facebook/react](https://github.com/facebook/react)). Its easier to type (no shift needed on most keyboards). [Prettier team recommends single quotes as well](https://github.com/prettier/prettier/issues/1105)

Double quotes are not without merit: Allows easier copy paste of objects into JSON. Allows people to use other languages to work without changing their quote character. Allows you to use apostrophes e.g. `He's not going.`. But I'd rather not deviate from where the JS Community is fairly decided.

**Do** When you can't use double quotes, try using back ticks (\`).

**Why?** These generally represent the intent of complex enough strings.

# Semicolons

**Do** semicolons.

**Why?** Explicit semicolons helps language formatting tools give consistent results. Missing ASI (automatic semicolon insertion) can trip new devs e.g. `foo() \n (function(){})` will be a single statement (not two). Recommended by TC39 as well.

# Array

**Do** Annotate arrays as `foos: Foo[]` instead of `foos: Array<Foo>`.

**Why?** Its easier to read. Its used by the TypeScript team. Makes easier to know something is an array as the mind is trained to detect `[]`.

# Filename
**Do** Name files with `camelCase`. E.g. `accordian.tsx`, `myControl.tsx`, `utils.ts`, `map.ts` etc.

**Why?** Conventional across many JS teams.

# type vs. interface

**Do** `type` when you *might* need a union or intersection:

```
type Foo = number | { someProperty: number }
```
**Do** `interface` when you want `extends` or `implements` e.g

```
interface Foo {
  foo: string;
}
interface FooBar extends Foo {
  bar: string;
}
class X implements FooBar {
  foo: string;
  bar: string;
}
```