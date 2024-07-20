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
+ Let's see the first code ` console.log(obj.a) `. It's directly accessing the property 'a' of object 'obj'，so the output will be '1'
+ next code `obj.b()`. The property 'b' is an ordinary function, we have code ` console.log(this.a) ` in it. And 'this' in the ordinary function will refers to object who called it, so 'this' refers to 'obj', finally output '1'.
+ next code `(obj.b)()`. The parentheses have no effect in this code，so the output is the same as the previous line of code.
+ next code `const b = obj.b b()`. In this code we assign the 'obj.b()' to variable 'b',because the value of 'this' depends on how the function is called, and 'b()' is invoked in the global scope. We can know 'this' refers to window. So the output is 'undefined'
+ next code `obj.b.apply({a: 2})`. It sets the 'this' context of the b function to the object {a: 2} during its execution. So we will get '2' from the output


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
