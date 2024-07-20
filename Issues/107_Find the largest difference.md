# issue #
Given an array of numbers, pick any two numbers a and b, we could get the difference by Math.abs(a - b).
Can you write a function to get the largest difference?
```
largestDiff([-1, 2,3,10, 9])
// 11,  obviously Math.abs(-1 - 10) is the largest
largestDiff([])
// 0
largestDiff([1])
// 0
```
# answer #
```
/**
 * @param {number[]} arr
 * @return {number}
 */
function largestDiff(arr) {
  // your code here
  if(arr.length < 2){
    return 0
  }

  let max = -Infinity,
      min = Infinity;
  
  arr.forEach((e)=>{
    max = Math.max(e,max)
    min = Math.min(e,min)
  })
  return Math.abs(max - min)
}
```
# analysis #
+ First,we need to pick any two number, so if the length of arr is less than 2, just return 0.
+ We define variable max that reprsent the maximum value of arr. At the beginning, we set it equel to -Infinity.
+ We create variable min that reprsent the minimum value of arr. At the beginning, we set it equel to Infinity.
+ The next step, iterator over the arr by using forEach method 

