# issue #
This is an easy problem.
For all the basic data types in JavaScript, how could you write a function to detect the type of arbitrary data?
Besides basic types, you need to also handle also commonly used complex data type including Array, ArrayBuffer, Map, Set, Date and Function
The goal is not to list up all the data types but to show us how to solve the problem when we need to.
The type should be lowercase
```
detectType(1) // 'number'
detectType(new Map()) // 'map'
detectType([]) // 'array'
detectType(null) // 'null'
// more in judging step
```
# answer #
```
function detectType(data) {
  // your code here
  return Object.prototype.toString.call(data).slice(8,-1).toLowerCase()
}
```
# analysis #
+ First, we can invoke `Object.prototype.toString.call(data)` to get the type of data as a string.
+ Then, use `console.log` to print the output of that line of code, and call the function using the code in the example.We can see the following output:
```
detectType(1) // '[object Number]'
detectType(new Map()) // '[object Map]'
detectType([]) // '[object Array]'
detectType(null) // '[object Null]'
```
+ This is not the format we expected, so we use the slice(8, -1) method to trim the string, which removes '\[object ' at the beginning and '\]' at the end.
+ Next, convert the string to lowercase form by using `.toLowerCase()`
+ Finally,we have obtained the correct format, just return the code above
