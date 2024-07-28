# issue #
+ Can you create a range(from, to) which makes following work?
```
for (let num of range(1, 4)) {
  console.log(num)  
}
// 1
// 2
// 3
// 4
```
+ This is a simple one, could you think more fancy approaches other than for-loop?
+ Notice that you are not required to return an array, but something iterable would be fine.

# answer #
```
function *range(from, to) {
  // your code here
  while(from<=to){
    yield from++
  }
}
```

# analysis #
+ Look for our code ,we will get a iterable object from the return of function `rang()`
+ So ,we can change the function `range()` as a generator function by add a asterisk after the keyword function
+ We will pass in two parameters， the start of number `from`, the end of number `end`
+ In the generator function , use while loop ,check whether the `from` is not more than `to`
+ yield from increment
