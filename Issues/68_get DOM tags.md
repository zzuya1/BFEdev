# issue #
+ Given a DOM tree, please return all the tag names it has.
+ Your function should return a unique array of tags names in lowercase, order doesn't matter.
# answer #
```
function getTags(tree) {
  // your code here
  const set = new Set()
  const stack = [tree]
  while(stack.length>0){
    const top = stack.pop()
    set.add(top.tagName.toLowerCase())
    stack.push(...top.children)
  }
  return [...set]
}
```
# analysis #
+ Ok, we will return all the tag names and they must be in lowercase
+ First, we create a new set to store our tag names
+ put the tree node into an array and assign it to the stack
+ we use a while loop, and check whether the length of stack is greater than 0  
+ get the last element from the stack by using `pop()` method and assign it to `top`
+ get the `tagName` of `top`,  convert `tagName` to lowercase, and put it into the `set`
+ if the `top` has children node ,push them into the stack
+ finally , return the `set` converted into an array
