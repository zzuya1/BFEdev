# issue #
_.once(func) is used to force a function to be called only once, later calls only returns the result of first call.
Can you implement your own once()?
```
function func(num) {
  return num
}
const onced = once(func)
onced(1) 
// 1, func called with 1
onced(2)
// 1, even 2 is passed, previous result is returned 
```
# answer #
```
/**
 * @param {Function} func
 * @return {Function}
 */
function once(func) {
  // your code here
  let isCalled = false,
      result = null;

  return function(...args){
    if(!isCalled){
      result = func.call(this,...args)
      isCalled = true
    }
    return result
  }
}
```
# analysis #
+ We define a variable `isCalled`, which value repersents whether the function has been called before. At the beginning, we assign `false` to `isCall`
+ Create variable `result` to store the first call value of `func`.
+ Let's return new function, and pass in the `args`
+ In the closure function，we check whether the func has been called by judging the value of `isCalled`, if the value is false，calculate the value of func
and assign the value to result.Then ，change the value of `isCalled` to true.
+ Finally, just return the variable `result` directly




