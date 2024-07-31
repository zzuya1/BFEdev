[104. Traverse DOM level by level](https://bigfrontend.dev/problem/Traverse-DOM-level-by-level)
# issue #
+ Given a DOM tree, flatten it into an one dimensional array, in the order of layer by layer, like below.
![image](https://github.com/user-attachments/assets/3b29b11e-46a6-4f61-9391-0476a89afccc)
# answer #
```
function flatten(root) {
  if(root == null){
    return []
  }
  const queue = [root]
  const result = []
  while(queue.length > 0){
    const head = queue.shift()
    result.push(head)
    queue.push(...head.children)
  }
  return result
}
```
# analysis #
+ If `root` is null ,we return an empty array
+ Create a `queue` , put the `root` node into the `queue`
+ Create an array to store our each elements which we call `result`
+ Use a while loop to check whether the length of the queue is greater than 0
+ Get the first element of the queue by using `shift()` method and this element is called `head`
+ Push  `head` to our `result` array
+ If  `head` has child nodes , push them into `queue`
+ Finally , return the `result` array
