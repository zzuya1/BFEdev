# issue #
+ According to lit-html homepage,
  + lit-html lets you write HTML templates in JavaScript, then efficiently render and re-render those templates together with data to create and update DOM
+ This video explains it pretty well about how it works. Let's take a look at the example.
```
import {html, render} from 'lit-html'
const helloTemplate = (name) => html`<div>Hello ${name}!</div>`
// This renders <div>Hello Steve!</div> to the document body
render(helloTemplate('Steve'), document.body)
// This updates to <div>Hello Kevin!</div>, but only updates the ${name} part
render(helloTemplate('Kevin'), document.body);
```
+ The magic happens in the second call of render() which only updates the necessary parts.
+ But there will be a series of problems on BFE.dev leading to that, here you are asked to :
+ implement html() and render() to make above example work, without considering the rerender, so html() could just return the raw HTML string.
+ The input data are all valid.
# answer #
```
function html(strs,...args) {
  let result = ""
  strs.forEach((e,i)=>{
    result += e
    result += args[i]??""
  })
  return result
}

// render the result from html() into the container
function render(result, container) {
  container.innerHTML = result
}
```
# analysis #
+ we can know that the html function is a tag function , which will handle an HTML template.
+ The tag function will accept two parameters,:the first is an array of static strings , and the second is an array of interpolation expressions
+ for the size of the second array ,if it is `n` ,the size of the first must be `n+1`
+ So let's create an empty string to store out final return
+ next iterator over the array `strs` by using `forEach()` method , passing the current element `e` and index `i` into the arrow function
+ append the current element of `strs` to the `result`, 
+ after that, get the corresponding value from args using the current index, append it to the result, if it is null , append empty string
+ finally ,return the `result`
+ In the render function , assign the result to `container.innerHTML`
