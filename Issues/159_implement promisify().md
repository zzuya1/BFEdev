# issue #
Let's take a look at following error-first callback.
```
const callback = (error, data) => {
  if (error) {
    // handle the error
  } else {
    // handle the data
  }
}
```
Now think about async functions that takes above error-first callback as last argument.
```
const func = (arg1, arg2, callback) => {
  // some async logic
  if (hasError) {
    callback(someError)
  } else {
    callback(null, someData)
  }
}
```
You see what needs to be done now. Please implement promisify() to make the code better.
```
const promisedFunc = promisify(func)
promisedFunc().then((data) => {
  // handles data
}).catch((error) => {
  // handles error
})
```
# answer #
```
function promisify(func) {
   return function(...args){
      return new Promise((resolve,reject)=>{
        return func.call(this,...args,(error,data)=>{
          if(error){
            reject(error)
          }else(
            resolve(data)
          )
        })
      })
   }
}
```
# analysis #
+ Return an anonymous function that accepts all arguments. 
+ This function returns a promise object.
+ Use the call method to invoke the func function, with the last argument being the callback of func. 
+ Depending on the value of error, either reject or resolve is called.
