# issue #
+ Your are given a 2-D array of characters. There is a hidden message in it.    
`I B C A L K A`   
`D R F C A E A`    
`G H O E L A D`     
+ The way to collect the message is as follows
  + start at top left
  + move diagonally down right
  + when cannot move any more, try to switch to diagonally up right
  + when cannot move any more, try switch to diagonally down right, repeat 3
  + stop when cannot neither move down right or up right. the character on the path is the message
  + for the input above, IROCLED should be returned.
+ notes
  + if no characters could be collected, return empty string

# answer #
```
function decode(message) {
  
  let row = 0,
      col = 0,
      cols = message[0]?.length
  let result = '',
      dir = 1

  while(col < cols){
    result += message[row][col]
    if(!message[row+dir]){
      dir *= -1
    }
    row += dir
    col += 1
  }

  return result
}


```

# analysis #
+ The rule for moving is clearly, we can know:
+ first position is row 0 ,column 0.
+ So we define variable `row` and `col` which represent the row and column of current element.
+ we also have a variable to store the length of the array's columns, called it `cols`
+ we create `result` to store the final return value
+ Define the variable `dir` to represent the direction of moving , 1 is down right , -1 is up right.
+ Use while loop to check whether the `col` of current element is less than number of columns in the array ,if so, the decode process is not over
+ Put the current element into the result
+ check the row of current element is equal to the first row or the last row, chenge the direction of moving
+ move to next element, append the `dir` to `row `, `col` add `1`
