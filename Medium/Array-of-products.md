
# Array of products
## The problem

## Approach 1: Brute Force
The brute force solution is to run loop within a loop and generate running product for all other elements except self.

```js
	function arrayOfProducts(array) {                             
		let solution = []
		for(let i = 0; i< array.length; i++){
		    let product = 1;
		    for(let j = 0; j<array.length; j++){
		      if(i!==j){
		        product = product * array[j];
		      }
		    }
		    solution[i] = product;
		}
		return solution
	}
```
### Complexity Analysis
Time Complexity : There is a nested for loop inside a for loop. Both loops go through `n` times where `n` is the length of the array. So time complexity is `O(n^2)`

Space Complexity: The solution is of length `n`. So the space complexity is `O(n)`.

## Approach 2 : Left and right products array (Optimal solution)
I had to look up for this solution because it is not apparent and intuitive. 

This solution involves creating two extra arrays, left array and right array. `i`th element of left array contains the product of `0` to `i-1`th elements that is `array[0]*array[1]*array[2]*....array[i-1]`. And right array contains product of `i+1` to `n-1` indexed elements where `n` is the length of array.

Then the `solution` is  such that `solution[i] = left[i] * right[i]`. Creating left and right array can be done in one loop and creating the solution can be done in one loop as well.

```
function arrayOfProducts(array) {
  let leftProducts = [];
  let rightProducts = [];

  for(let i = 0; i < array.length; i++){
    if(i==0){
      leftProducts[i] = 1;
    }else{
      leftProducts[i] = leftProducts[i-1] * array[i-1];
    }

   let revI = array.length - i - 1 ;
   if(revI == array.length-1){
     rightProducts[revI] = 1;  
   }else{
     rightProducts[revI] = rightProducts[revI + 1] * array[revI+1];
   }
  }

  let solution = [];
  for(let i = 0; i<array.length; i++){
    solution[i] = leftProducts[i] * rightProducts[i];
  }

  return solution;
}
```
## Complexity Analysis
Time complexity: There are two for loops running `n` times. So the time complexity is `O(2n)` ie, `O(n)`

Space Complexity: There are three extra arrays of size `n`. So the space complexity is `O(3n)` ie `O(n)`