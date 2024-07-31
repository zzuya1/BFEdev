# issue #
+ what is Composition? It is actually not that difficult to understand, see @dan_abramov 's explanation.
+ Here you are asked to create a pipe() function, which chains multiple functions together to create a new function.
+ Suppose we have some simple functions like this
```
const times = (y) =>  (x) => x * y
const plus = (y) => (x) => x + y
const subtract = (y) =>  (x) => x - y
const divide = (y) => (x) => x / y
```
+ Your pipe() would be used to generate new functions
```
pipe([
  times(2),
  times(3)
])  
// x * 2 * 3
pipe([
  times(2),
  plus(3),
  times(4)
]) 
// (x * 2 + 3) * 4
pipe([
  times(2),
  subtract(3),
  divide(4)
]) 
// (x * 2 - 3) / 4
```
+ notes
  + 1.to make things simple, functions passed to pipe() will all accept 1 argument

# answer #
```
function pipe(funcs) {
	 return function(arg){
		return funcs.reduce((result,func)=>{
			return func.call(this,result)
		},arg)
	 }
}
```
# analysis # 
+ look at the example, we should return a function, and pass in the argument which is the unknow number `x`
+ By using `reduce()` to iterate over the parameters of passed-in `pipe()` which is called `funcs`
+ The `reduce()` method will accept a callback function as an accumulator, it will accumulate the elements of `funcs` from right to left
+ `result` is the return value of last callback function,func is the handler element currently being processed
+ the second parameter of `reduce()` is the initial value of the accumulator
+ finally , return the accumulated value 
