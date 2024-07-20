# issue #
What does the code snippet to the right output by console.log?
```
// This is a JavaScript Quiz from BFE.dev
const obj = {
  a: 1,
  b: function() {
    console.log(this.a)
  },
  c() {
    console.log(this.a)
  },
  d: () => {
    console.log(this.a)
  },
  e: (function() {
    return () => {
      console.log(this.a);
    }
  })(),
  f: function() {
    return () => {
      console.log(this.a);
    }
  }
}

console.log(obj.a)
obj.b()
;(obj.b)()
const b = obj.b
b()
obj.b.apply({a: 2})
obj.c()
obj.d()
;(obj.d)()
obj.d.apply({a:2})
obj.e()
;(obj.e)()
obj.e.call({a:2})
obj.f()()
;(obj.f())()
obj.f().call({a:2})
```
# analysis #
+ Let's see the first code ` console.log(obj.a) `.
  It's directly accessing the property 'a' of object 'obj'，so the output will be '1'
+ next code `obj.b()`.
  The property 'b' is an ordinary function, we have code ` console.log(this.a) ` in it. And 'this' in the ordinary function will refers to object who called it, so 'this' refers to 'obj', finally output '1'.
+ next code `(obj.b)()`.
  The parentheses have no effect in this code，so the output is the same as the previous line of code.
+ next code `const b = obj.b b()`.
  In this code we assign the 'obj.b()' to variable 'b',because the value of 'this' depends on how the function is called, and 'b()' is invoked in the global scope. We can know 'this' refers to window. So the output is 'undefined'
+ next code `obj.b.apply({a: 2})`.
  It sets the 'this' context of the b function to the object {a: 2} during its execution. So we will get '2' from the output
+ next code `obj.c()`.
  The function c is a different way of writing the code with the same effect as the function above. So the output will be '1'
+ next code `obj.d()`.
  The function d is an arrow function.Arrow functions capture the value of 'this' from their enclosing context and use that value as their own 'this' value. So in this code 'this' will refers to window, and output will be 'undefined' 
+ next code `(obj.d)()`.
  The parentheses have no effect in this code, so it's also 'undefined' 
+ next code `obj.d.apply({a:2})`.
  In an arrow function, 'this' binding does not change no matter how or where the arrow function is called or executed. So the apply method have no effect, it's also 'undefined' 
+ next code `obj.e(); (obj.e)(); obj.e.call({a:2})`.
  The function e is defined as the result of an IIFE (Immediately Invoked Function Expression) that is immediately invoked upon definition, so e is the arrow function inside this IIFE. It have the same effect as the function d, the output of above three lines code are 'undefined','undefined','undefined'
+ next code `obj.f()()`.
  In the function f, it will return an arrow function. When we call `obj.f()`, the 'this' in function will refers to 'obj'. 'this' in the arrow function inside function f is inherits the 'this' value from its enclosing lexical scope, so it also refers to 'obj'. The output of consol.log will be '1'
+ next code `(obj.f())()`.
  The parentheses have no effect,'1'
+ next code `obj.f().call({a:2})`.
  The 'this' value in arrow function not be change in the execution, So it's also '1'
# answer #
```
1
1
1
undefined
2
1
undefined
undefined
undefined
undefined
undefined
undefined
1
1
1
```
