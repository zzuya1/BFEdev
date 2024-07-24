# issue #
+ Memoization is a common technique to boost performance. If you use React, you definitely have used React.memo before.
+ Memoization is also commonly used in algorithm problem, when you have a recursion solution, in most cases, you can improve it by memoization, and then you might be able to get a Dynamic Programming approach.
+ So could you implement a general memo() function, which caches the result once called, so when same arguments are passed in, the result will be returned right away.
```
const func = (arg1, arg2) => {
  return arg1 + arg2
}
const memoed = memo(func)
memoed(1, 2) 
// 3, func is called
memoed(1, 2) 
// 3 is returned right away without calling func
memoed(1, 3)
// 4, new arguments, so func is called
```
+ The arguments are arbitrary, so memo should accept an extra resolver parameter, which is used to generate the cache key, like what _.memoize() does.
```
const memoed = memo(func, () => 'samekey')
memoed(1, 2) 
// 3, func is called, 3 is cached with key 'samekey'
memoed(1, 2) 
// 3, since key is the same, 3 is returned without calling func
memoed(1, 3) 
// 3, since key is the same, 3 is returned without calling func
```
+ Default cache key could be just Array.from(arguments).join('_')
+ note
+ It is a trade-off of space for time, so if you use this in an interview, please do analyze how much space it might cost.
# answer #
```
/**
 * @param {Function} func
 * @param {(args:[]) => string }  [resolver] - cache key generator
 */
function memo(func, resolver) {
  // your code here
  const cache = new Map()

  return function(...args){
    const cacheKey = resolver?resolver(...args):args.join('-')
    if(cache.has(cacheKey)){
      return cache.get(cacheKey)
    }

    const cacheValue = func.call(this,...args)
    cache.set(cacheKey,cacheValue)
    return cacheValue
  }
}
```
# analysis #
+ First create a map named 'cache' which represents the storage of the value returned by the func called  before.
+ Return a closure function ,and pass argument in this function
+ Beacuse the memo function accept an extra resolver parameter, which is used to generate the cache key, default it could be just `Array.from(arguments).join('_')`. If the resolver is exist, invoking the given resolver handle the args，otherwise we use the default resolver to handle args. Assign the result of handle to the cacheKey
+ Next ,we check whether the cacheKey is already in the cache，if it exists,  just return the value that we have already stored in the cache by using the `cache.get(cacheKey)`
+ If it does not exist， we should calculate the cacheValue by invoking `func.call(this,...args)`. Then, we put the `cacheKey` and `cacheValue` into the cache by using `set()` method
+ Finally, just return the value we calculated, and this question is over
