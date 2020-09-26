## Javascript is going crazy

Javascript is crazy. That is a fact. But I still love it. 

It allows you to express yourself with voodoo code, like this (wtf #1):

```js
(![]+[])[+!+[]]+([][[]]+[])[+!+[]]+([][[]]+[])[!+[]+!+[]]+(!+[]+[])[+!+[]]+(![]+[])[+!+[]]+(![]+[])[!+[]+!+[]+!+[]]+(+(+!+[]+(!+[]+[])[!+[]+!+[]+!+[]]+(+!+[])+(+[])+(+[])+(+[]))+[])[+[]]+(![]+[])[!+[]+!+[]+!+[]]+([!![]+!![]+!![]]+[+[]+!![]])+(+(+!+[]+[+!+[]]+(!![]+[])[!+[]+!+[]+!+[]]+[!+[]+!+[]]+[+[]])+[])[+!+[]] + ' 🎉')
```
This is a valid javascript expression. Don't you believe me? Then see it with your own eyes.

%[https://codesandbox.io/embed/javascript-is-going-crazy-fyoib]

# What the... How?
For the explanation, you need to understand some basics of Javascript.

- **JS is weakly typed / untyped / loosely typed**: JS figures out the type of the data dynamically by the value. It does not specify types of variables.

```js
let a = 30 // Number
a = '30'   // String
a = [30]   // Object
```

- **Unary plus operator (+ sign)**: It converts the operand on the right side of it to Number type. [mdn](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#Unary_plus_())

```js
+30             // 30 (Number)
+'30'           // 30 (Number)
+[]             // 0 (Number)
+true           // 1 (Number)
+true+true      // 2 (Number)
+true+true+true // 3 (Number) (wtf #2)
```

- **Truthy or falsy (!! double exclamation mark)**: Every value has an inherent boolean value in JS. 

The basic rule to follow:
   - _false_, _0_, _""_ (empty string), _null_, _undefined_ and _NaN_ are **falsy**
   - Everyhing else is **truthy**.

```js 
!!'Iam30' // true (boolean)
!!false   // false (boolean)
!!true    // true (boolean)
!!''      // false (boolean)
!![]      // true (boolean)

// With unary operator
+!!true   // 1 (number)
!![]+!![] // 2 (number)  (wtf #3)
!!+[]     // false (boolean)
+!![]     // true (boolean)
```

# Let's jump on a roller-coaster with me!

With these three in our pockets, we can write creative spaghetti code: 

```js
![] // false (boolean)
!![] // true (boolean)

// Weakly type makes the boolean + number = 'string'
![]+[]  // 'false' (string) - (wtf #4).
!![]+[] // 'true (string) - (wtf #5).

// We can access each element of the 'false' string with the help of array
(![]+[])[1] // 'a' (string)

// But remember - 1 could be written as:
(![]+[])[+!!true]

// Or if you would like to get rid of the letter characters altogether (wtf #6)
(![]+[])[+!![]]
```

# What about other characters?

Following the same logic, we can magically create *NaN* and *undefined* and *Infinity* strings:

```js
// NaN - Converting an invalid number to number
![]           // false (boolean)
[![]]         // [false] (object with false boolean in it)
+[![]]        // NaN (number)
+[![]]+[]     // 'NaN' (string)

// undefined - Access an undefined index of an array
[]            // [] (object, empty array)
[![]]         // [![]] (object, array with false (boolean) in it)
[][![]]       // undefined (undefined, array's false (boolean) element) (wtf #6)
[][![]]+[]    // 'undefined' (string)

// Infinity - Get a huge number which cause Infinity
1e1000        // Infinity (number)

// 1 => +!![]
+!![]+'e1000' // +!![]+'e1000' (wtf #7)

// e => accessing the 4th element of 'false' string
(![]+[])                       // 'false' string
[+!![]+!![]+!![]+!![]]         // [4]
(![]+[])[+!![]+!![]+!![]+!![]] // 'e' string (wtf #8)

// 1000 => adding together a number + array of number 
// (this logic prevents the mathematical plus operation)
+!![]                   // 1 (number)
+[+[]]                  // [0]
+!![]+[+[]]+[+[]]+[+[]] // '1000' - This is different what I used in the codesandbox example, to show you that my solution is not unique. There are plenty of possibilities which generates the same output. (wtf #9)

// Merging
+!![]+(![]+[])[+!![]+!![]+!![]+!![]]+(+!![]+[+[]]+[+[]]+[+[]]) 
// '1e1000' (string)

// Converting to number
+(+!![]+(![]+[])[+!![]+!![]+!![]+!![]]+(+!![]+[+[]]+[+[]]+[+[]])) // Infinity (number)

// Converting to string
+(+!![]+(![]+[])[+!![]+!![]+!![]+!![]]+(+!![]+[+[]]+[+[]]+[+[]]))+[] // 'Infinity' (string) (wtf #10)
```

![CRAZY](https://media.giphy.com/media/5QFbWsGn5rLOg/giphy.gif)

Ok, enough. Ten wtf's. That is way too much.
With this logic, you can access any characters - you need a lot of patient.

---

> I hope you had fun reading this absurd article. Feel free to contact me on  [twitter](https://twitter.com/andrasbacsai), and if you have any questions, I'm happy to answer - except if you would like me to transform some ridiculously long text to this spaghetti code.

---