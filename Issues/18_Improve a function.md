[18. Improve a function](https://bigfrontend.dev/problem/improve-a-function)
# issue #
```
// Given an input of array, 
// which is made of items with >= 3 properties
let items = [
  {color: 'red', type: 'tv', age: 18}, 
  {color: 'silver', type: 'phone', age: 20},
  {color: 'blue', type: 'book', age: 17}
] 
// an exclude array made of key value pair
const excludes = [ 
  {k: 'color', v: 'silver'}, 
  {k: 'type', v: 'tv'}, 
  ...
] 
function excludeItems(items, excludes) { 
  excludes.forEach( pair => { 
    items = items.filter(item => item[pair.k] === item[pair.v])
  })
 
  return items
}
```
+ What does this function excludeItems do?
+ Is this function working as expected ?
+ What is the time complexity of this function?
+ How would you optimize it ?
+ note
  + we only judge by the result, not the time cost. please submit the best approach you can.
# answer #
+ 1.What does this function 'excludeItems' do?
  + The function 'excludeItems' filters an array of items based on an array of exclusion criteria.
    Each exclusion criterion is an object with a key ('k') and a value ('v').
    The function removes items from the 'items' array that match any of the exclusion criteria.
+ 2.Is this function working as expected?
  + No, the function does not work as expected.
    The current implementation removes items incrementally for each exclusion pair,
    which means if multiple exclusion criteria are met by the same item, it may not be excluded properly.
    Additionally, it modifies the 'items' array in place, which can lead to unexpected results during iteration.
+ 3.What is the time complexity of this function?
  + The time complexity of the function is O(n×m),
    where n is the number of items in the items array and m is the number of exclusion criteria in the excludes array.
    This is because for each exclusion criterion, the function iterates through the entire items array to filter out matching items.
+ 4.How would you optimize it?
  + To optimize the function, we can combine the exclusion criteria into a set of conditions and filter the items array in a single pass.
    This avoids multiple iterations over the items array and ensures that items are only removed once if they meet any of the exclusion criteria.
```
function excludeItems(items, excludes) {
  const excludeMap = new Map()
  for (let { k, v } of excludes) {
      if (!excludeMap.has(k)) {
          excludeMap.set(k, new Set())
      }
      excludeMap.get(k).add(v)
  }

  return items.filter(item => {
      return Object.keys(item).every(
          key => !excludeMap.has(key) || !excludeMap.get(key).has(item[key])
      )
  })
}
```
