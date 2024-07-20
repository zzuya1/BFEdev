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
# answer #
+ Let's see the first code ` console.log(obj.a) `. It's directly accessing the property 'a' of object 'obj'，so the output will be '1'
+ next code `obj.b()`. The property 'b' is an ordinary function, we have code ` console.log(this.a) ` in it. And 'this' in the ordinary function will refers to object who called it, so 'this' refers to 'obj', finally output '1'.
+ next code `(obj.b)()`. The parentheses have no effect in this code，so the output is the same as the previous line of code.
