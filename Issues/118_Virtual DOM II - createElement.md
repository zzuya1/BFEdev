[118. Virtual DOM II - createElement](https://bigfrontend.dev/problem/virtual-dom-II-createElement)
# issue #
This is > a follow-up on [113. Virtual DOM I](https://bigfrontend.dev/problem/Virtual-DOM-I).

Suppose + you have solved above problem, now let's take a look at [React.createElement()](https://reactjs.org/docs/react-api.html#createelement):
```
React.createElement(
  type,
  [props],
  [...children]
)
```
+ First argument is type, it could be set to Custom Component, but here in this problem, it would only be HTML tag name
+ Second argument is props, here in this problem, it would only be the (common) camelCased HTML attributes
+ the rest arguments are the children, which in React supports many data types, but in this problem, it only has the element type of MyElement, or string for TextNode.
+ You are asked to create your own createElement() and render(), so that following code could create the exact HTMLElement in [113. Virtual DOM I](https://bigfrontend.dev/problem/Virtual-DOM-I).
```
const h = createElement
render(h(
  'div',
  {},
  h('h1', {}, ' this is '),
  h(
    'p',
    { className: 'paragraph' },
    ' a ',
    h('button', {}, ' button '),
    ' from ',
    h('a', 
      { href: 'https://bfe.dev' }, 
      h('b', {}, 'BFE'),
      '.dev')
  )
))
```
+ Notes
  + The goal of this problem is not to create the replica of React implementation, you can have your own object representation format other than the one in [113. Virtual DOM I](https://bigfrontend.dev/problem/Virtual-DOM-I).
  + Details about ref, key are ignored here, they will be put in other problems. Re-render is not covered here, it will be in another problem as well.

# anwser #
```
/**
 * @param { string } type - valid HTML tag name
 * @param { object } [props] - properties.
 * @param { ...MyNode} [children] - elements as rest arguments
 * @return { MyElement }
 */
function createElement(type, props, ...children) {
  // your code here
  return {
    type,
    props:{
      ...props,
      children
    }
  }
}

/**
 * @param { MyElement }
 * @returns { HTMLElement } 
 */
function render(myElement) {
  // your code here
  if(typeof myElement ==='string'){
    return document.createTextNode(myElement)
  }

  const {type,props:{children,...attrs}} = myElement
  const element = document.createElement(type)

  for(let [key,value] of Object.entries(attrs)){
    element[key] =value
  }

  const childrenAttr = Array.isArray(children)?children:[children]
  for(child of childrenAttr){
    element.append(render(child))
  }

  return element
}
```
# analysis #
+ we should change the structure of object according to the structure of `React.createElement() `
+ The first element is the `type`. The second is the `props` object, and it has data attributes and children elements 
+ Then we have obtained the data structure required by the render function. And we can get the render function from question 113
+ In the render function , we check whether the parameter passed in is a string , if so ,we create a text node and return it
+ If it is not, get the `type`, `props:{children,...attrs}` object from the `json`
+ Based on the type ,create the top level node element
+ Using `Object.entries`, we iterate over the other attributes, assign the value to the dom that we created
+ Check if the type of children elements is array , if not , convert to an array
+ Iterate over the children elements array,recursively invoking the `render()` function to append the children into the real DOM
+ Finally ,return the top node
