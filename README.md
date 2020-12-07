# algorithms in js
Learning algorithms and examples in js

### Topics under Algorithms

- [Big O notation](https://github.com/vishnukumarbp/algorithmsjs#big-o-notation)
  * [Most commonly used notations](https://github.com/vishnukumarbp/algorithmsjs#most-commonly-used-notations-are)
  * [Big O shorthands](https://github.com/vishnukumarbp/algorithmsjs#big-o-shorthands)
- [Problem solving](https://github.com/vishnukumarbp/algorithmsjs#problem-solving)
- [Problem solving patterns](https://github.com/vishnukumarbp/algorithmsjs#problem-solving-patterns)
  * [Frequency counter](https://github.com/vishnukumarbp/algorithmsjs#frequency-counter)
  * [Multiple pointer](https://github.com/vishnukumarbp/algorithmsjs#multiple-pointers)
  * [Sliding window](https://github.com/vishnukumarbp/algorithmsjs#sliding-window)
  * [Divide and conquer](https://github.com/vishnukumarbp/algorithmsjs#divide-and-conquer)
- [Recursion](https://github.com/vishnukumarbp/algorithmsjs#recursion)
- [Searching algorithms](https://github.com/vishnukumarbp/algorithmsjs#searching-algorithms)
  * [Linear search](https://github.com/vishnukumarbp/algorithmsjs#linear-search)
  * [Binary search](https://github.com/vishnukumarbp/algorithmsjs#binary-search)
  * [Naive/Basic String Search](https://github.com/vishnukumarbp/algorithmsjs#naivebasic-string-search)
  * [Kunth Moriss Pratt String matching algorithm](https://github.com/vishnukumarbp/algorithmsjs#kunth-morris-pratt-string-matching-algorithm)
- [Sorting algorithms](https://github.com/vishnukumarbp/algorithmsjs#sorting-algorithms)
  * [Bubble sort](https://github.com/vishnukumarbp/algorithmsjs#bubble-sort)
  * [Selection sort](https://github.com/vishnukumarbp/algorithmsjs#selection-sort)
  

## Big O notation:
*Talk formally about how the runtime of an algorithm grows as the input grows*

**Time complexity:** Time taken to run/execute the algorithm/program with input to the function as "n"

**Space complexity:** Amount of memory/space taken by the program while execution with respect to the input length "n". In most cases, when we say space complexity we talk about auxiliary space.
Auxiliary space is the temporary or extra space used by the algorithm while it is being executed. Space complexity of an algorithm is commonly expressed using Big O (O(n))(O(n)) notation.**


**In JS:**

- Most primitive types (boolean, numbers, undefined, null) are constant space
- String type are linear O(n) - where n is the length of a string
- Reference types are linear too O(n) where, for arrays: n is the length of the array, and for objects: n is the number of keys in an object

**Examples:**

Space complexity in the here is: O(2) as there are two assignments, which will be shortend to **O(1)**
```javascript
function addUpTo(n) {
    let total = 0;
    for (let i = 1; i <= n; i++) {
        total += i;
    }
    return total;
}
```

Space complexity in the here is: O(n + 2) as there are two assignments, which will be shortend to **O(n)**
```javascript
function double(arr) {
    let newArray = []; // newArray => 1 
    for (let i = 0; i <= arr.lengtn; i++) { // let i => 2
        newArray.push(2 * arr[i]); // n items in the array
    }
    return total;
}
```

##### Most commonly used notations are*
* Linear O(n)
* Quadratic O(n^2)
* Constant O(1)
* Lograithmic O(log n)


<img src="https://res.cloudinary.com/practicaldev/image/fetch/s--q9gaD0m_--/c_imagga_scale,f_auto,fl_progressive,h_900,q_auto,w_1600/https://thepracticaldev.s3.amazonaws.com/i/3ms2d5rfv25a2swyz1vs.png" alt="Big O timing graph" width="550" height="400">


**Note: Rules of thumb:**
- Constants doesnt matter:
O(2n) => O(n),
O(1000) => O(1),
O(10n^2) => O(n^2)
- Smaller terms doesnt matter:
O(2n + 10) => O(n),
O(n^2 + 1000) => O(n^2),
O(10n^2 + 100n + 2) => O(n^2)

##### Big O shorthands:

- Arithmatic operations are constants
- Assignments are constants
- Accessing elements in an array or keys in an object are constants
- In a loop, the complexity is the length of the loop times the complexity of whatever happens inside the loop (O(n^2))

<img src="https://user-images.githubusercontent.com/10495294/101241427-e1fc8700-371b-11eb-89a4-96a337061ae9.png" alt="Big O of object" width="350" height="200">


<img src="https://user-images.githubusercontent.com/10495294/101241500-a4e4c480-371c-11eb-8bce-518e11b97b73.png" alt="Big O of object" width="350" height="200">



References:
[Stack overflow answer with example for each complexities](https://stackoverflow.com/questions/2307283/what-does-olog-n-mean-exactly/36877205#36877205)



## Problem solving
1. Understand the problem
2. Explore the concrete example
3. Break it down
4. Solve/Simplyfy
5. Look back and refactor


## Problem solving patterns

### Frequency counter & Multiple pointers:

### Frequency counter:
This pattern uses objects or set to store the frequency of a value to avoid nester loop (O(n^2)).

#### Problem - Frequency counter - sameFrequency
Write a function called sameFrequency. Given two positive integers, find out if the two numbers have the same frequency of digits.

Your solution must have the following complexities:
Time: O(n)

#### **Sample Input:**

- sameFrequency(182,281) // True
- sameFrequency(34,14) // False
- sameFrequency(3589578, 5879385) // True
- sameFrequency(22,222) // False

#### **Solution:**

```javascript
function sameFrequency(num1, num2){
  let strNum1 = num1.toString();
  let strNum2 = num2.toString();
  if(strNum1.length !== strNum2.length) return false;
  
  let countNum1 = {};
  let countNum2 = {};
  
  for(let i = 0; i < strNum1.length; i++){
    countNum1[strNum1[i]] = (countNum1[strNum1[i]] || 0) + 1
  }
  
  for(let j = 0; j < strNum1.length; j++){
    countNum2[strNum2[j]] = (countNum2[strNum2[j]] || 0) + 1
  }
  
  for(let key in countNum1){
    if(countNum1[key] !== countNum2[key]) return false;
  }
 
  return true;
}
```


#### Problem - Frequency Counter / Multiple Pointers - areThereDuplicates
Implement a function called, areThereDuplicates which accepts a variable number of arguments, and checks whether there are any duplicates among the arguments passed in.

You can solve this using the frequency counter pattern OR the multiple pointers pattern.

Restrictions: Time - O(n), Space - O(n)
Bonus: Time - O(n log n), Space - O(1)

#### **Sample Input:**

- areThereDuplicates(1, 2, 3) // false
- areThereDuplicates(1, 2, 2) // true 
- areThereDuplicates('a', 'b', 'c', 'a') // true 


#### **Solutions:**

##### areThereDuplicates Solution (Frequency Counter)
```javascript
function areThereDuplicates() {
  let collection = {}
  for(let val in arguments){
    collection[arguments[val]] = (collection[arguments[val]] || 0) + 1
  }
  for(let key in collection){
    if(collection[key] > 1) return true
  }
  return false;
}
```


##### areThereDuplicates Solution (Multiple Pointers)

```javascript
function areThereDuplicates(...args) {
  // Two pointers
  args.sort((a,b) => a > b);
  let start = 0;
  let next = 1;
  while(next < args.length){
    if(args[start] === args[next]){
        return true
    }
    start++
    next++
  }
  return false
}
```

##### areThereDuplicates One Liner Solution

```javascript
function areThereDuplicates() {
  return new Set(arguments).size !== arguments.length;
}
```


### Multiple Pointers:
Creating pointers or values that correspond to an index or position and move towards beginning, end or middle based on a certain conditions


#### Problem - Multiple Pointers - averagePair
Write a function called averagePair. Given a sorted array of integers and a target average, determine if there is a pair of values in the array where the average of the pair equals the target average. 
There may be more than one pair that matches the average target.

Bonus Constraints:
Time: O(n)
Space: O(1)

#### **Sample Input:**

- averagePair([1,2,3],2.5) // true
- averagePair([1,3,3,5,6,7,10,12,19],8) // true
- averagePair([-1,0,3,4,5,6], 4.1) // false
- averagePair([],4) // false


#### **Solutions:**

```javascript
function averagePair(arr, num){
  let start = 0
  let end = arr.length-1;
  while(start < end){
    let avg = (arr[start]+arr[end]) / 2 
    if(avg === num) return true;
    else if(avg < num) start++
    else end--
  }
  return false;
}
```


#### Problem - Multiple Pointers - isSubsequence
Write a function called isSubsequence which takes in two strings and checks whether the characters in the first string form a subsequence of the characters in the second string.
in other words, the function should check whether the characters in the first string appear somewhere in the second string, without their order changing.

Your solution must have at least the following complexities: 
Time complexity - O(n + m)
Space complexity - O(1)

#### **Sample Input:**

- isSubsequence('hello', 'hello world'); // true
- isSubsequence('sing', 'sting'); // true
- isSubsequence('abc', 'abracadabra'); // true
- isSubsequence('abc', 'acb'); // false


#### **Solutions:**
##### isSubsequence Solution - Iterative

```javascript
function isSubsequence(str1, str2) {
  var i = 0;
  var j = 0;
  if (!str1) return true;
  while (j < str2.length) {
    if (str2[j] === str1[i]) i++;
    if (i === str1.length) return true;
    j++;
  }
  return false;
}
```

##### isSubsequence Solution - Recursive but not O(1) Space

```javascript
function isSubsequence(str1, str2) {
  if(str1.length === 0) return true
  if(str2.length === 0) return false
  if(str2[0] === str1[0]) return isSubsequence(str1.slice(1), str2.slice(1))  
  return isSubsequence(str1, str2.slice(1))
}
```


### Sliding Window:
This pattern involves creating a window which can be either an array or number from one position to another. Based on a certain condition, the window either increases or closes (a new window is created). This pattern is very effect when we have to create a subset of an array/string.


#### Problem - Sliding Window - maxSubarraySum
Given an array of integers and a number, write a function called maxSubarraySum, which finds the maximum sum of a subarray with the length of the number passed to the function. 

Note that a subarray must consist of consecutive elements from the original array. In the first example below, [100, 200, 300] is a subarray of the original array, but [100, 300] is not.

Your solution must have at least the following complexities:
Time complexity - O(n)
Space complexity - O(1)

#### **Sample Input:**

- maxSubarraySum([100,200,300,400], 2) // 700
- maxSubarraySum([1,4,2,10,23,3,1,0,20], 4)  // 39 
- maxSubarraySum([-3,4,0,-2,6,-1], 2) // 5
- maxSubarraySum([3,-2,7,-4,1,-1,4,-2,1],2) // 5
- maxSubarraySum([2,3], 3) // null


#### **Solutions:**
```javascript
function maxSubarraySum(arr, num){
    if (arr.length < num) return null;
 
    let total = 0;
    for (let i=0; i<num; i++){
       total += arr[i];
    }
    let currentTotal = total;
    for (let i = num; i < arr.length; i++) {
       currentTotal += arr[i] - arr[i-num];
       total = Math.max(total, currentTotal);
    }
    return total;
}
```


#### Problem - Sliding Window - minSubArrayLen
Write a function called minSubArrayLen which accepts two parameters - an array of positive integers and a positive integer.

This function should return the minimal length of a contiguous subarray of which the sum is greater than or equal to the integer passed to the function. If there isn't one, return 0 instead.

Your solution must have at least the following complexities:
Time complexity - O(n)
Space complexity - O(1)

#### **Sample Input:**

- minSubArrayLen([2,3,1,2,4,3], 7) // 2 -> because [4,3] is the smallest subarray
- minSubArrayLen([2,1,6,5,4], 9) // 2 -> because [5,4] is the smallest subarray
- minSubArrayLen([3,1,7,11,2,9,8,21,62,33,19], 52) // 1 -> because [62] is greater than 52
- minSubArrayLen([1,4,16,22,5,7,8,9,10],39) // 3
- minSubArrayLen([1,4,16,22,5,7,8,9,10],55) // 5
- minSubArrayLen([4, 3, 3, 8, 1, 2, 3], 11) // 2
- minSubArrayLen([1,4,16,22,5,7,8,9,10],95) // 0


#### **Solutions:**
```javascript
function minSubArrayLen(nums, sum) {
  let total = 0;
  let start = 0;
  let end = 0;
  let minLen = Infinity;
 
  while (start < nums.length) {
    // if current window doesn't add up to the given sum then 
		// move the window to right
    if(total < sum && end < nums.length){
      total += nums[end];
			end++;
    }
    // if current window adds up to at least the sum given then
		// we can shrink the window 
    else if(total >= sum){
      minLen = Math.min(minLen, end-start);
			total -= nums[start];
			start++;
    } 
    // current total less than required total but we reach the end, need this or else we'll be in an infinite loop 
    else {
      break;
    }
  }
 
  return minLen === Infinity ? 0 : minLen;
}
```


#### Problem - Sliding Window - findLongestSubstring
Write a function called findLongestSubstring, which accepts a string and returns the length of the longest substring with all distinct characters.

Your solution must have at least the following complexities:
Time complexity - O(n)

#### **Sample Input:**

- findLongestSubstring('') // 0
- findLongestSubstring('rithmschool') // 7
- findLongestSubstring('thisisawesome') // 6
- findLongestSubstring('thecatinthehat') // 7
- findLongestSubstring('bbbbbb') // 1
- findLongestSubstring('longestsubstring') // 8
- findLongestSubstring('thisishowwedoit') // 6


#### **Solutions:**
```javascript
function findLongestSubstring(str) {
  let longest = 0;
  let seen = {};
  let start = 0;
 
  for (let i = 0; i < str.length; i++) {
    let char = str[i];
    if (seen[char]) {
      start = Math.max(start, seen[char]);
    }
    // index - beginning of substring + 1 (to include current in count)
    longest = Math.max(longest, i - start + 1);
    // store the index of the next char so as to not double count
    seen[char] = i + 1;
  }
  return longest;
}
```

### Divide and conquer
This is pattern involves in dividing a data set into smaller chunk and applying the process on the subset of data.

This pattern can tremendously **decreases time complexity**

For eg: 
**Problem:** Find the index of 88 from given the **sorted** input array [1,2,8,19,20,34,56,82,88,93,95,96,102,120,150]
In this case, instead of searching 88 in a loop starting from index 0 to array.length, we can apply divide and conquer pattern to improve the time complexity.

i.e, divide the input by 2, and compare the middle element with the value to search, whether the value is greater than the middle element or less. 
If value is greater than middle element, we reset the start to middle element, else, we reset the end to middle element. (which is like creating a subset),
And continue the same steps, until we find the value we want.

And we use this pattern for binary search, and the time complexity of the search is O(log n)


## Recursion
A process (or a function) that call itself until it reaches the base case.

**Objectives:**

1. Define recursion and how to use
2. Two essential components of recursion
3. Visualize the call stack

**It's Everywhere:**
1. JSON.parse/JSON.stringify
2. document.getElementById and DOM traversal algorithm
3. Object traversal
4. Mostly used in complex data strcuture algotithms
5. Cleaner/Better alternative to iteration

**Two essential components of recurstion:**
1. base case ie, A case/situation when the recursion ends
2. different input on each recursive calls


**Call stack:**

A stack data structure, and everytime a function is called, an entry is pushed, popped when function return a value or ends

**Example**
```javascript

function countDown(num) {
    if(num == 0){
        console.log("Done!");
        return false;
    }
    console.log(num);
    num--;
    countDown(num);
}
```

## Searching Algorithms


## Linear Search
It is a basic search. Starts searching for element from left to right linearly. Most of the inbuild methods of an array uses linear search algorithms, for eg: `indexOf`, `includes`, `find`, `findIndex`

## Binary Search
Binary search works with sorted array, and it uses divide and conquer pattern to create subset at the end of the loop. This algorithm should be more efficient than linearSearch. Time complexity is O(1) - best case and O(log n) average and worst case.
you can read how to implement it here
https://www.khanacademy.org/computing/computer-science/algorithms/binary-search/a/binary-search 
and here 
https://www.topcoder.com/community/data-science/data-science-tutorials/binary-search/

#### **Problem:**
Write a function called binarySearch which accepts a sorted array and a value and returns the index at which the value exists. Otherwise, return -1. 

#### **Sample Input:**
- binarySearch([1,2,3,4,5],2) // 1
- binarySearch([1,2,3,4,5],3) // 2
- binarySearch([1,2,3,4,5],5) // 4
- binarySearch([1,2,3,4,5],6) // -1
- binarySearch([5, 6, 10, 13, 14, 18, 30, 34, 35, 37, 40, 44, 64, 79, 84, 86, 95, 96, 98, 99], 10) // 2
- binarySearch([5, 6, 10, 13, 14, 18, 30, 34, 35, 37, 40, 44, 64, 79, 84, 86, 95, 96, 98, 99], 95) // 16
- binarySearch([5, 6, 10, 13, 14, 18, 30, 34, 35, 37,   40, 44, 64, 79, 84, 86, 95, 96, 98, 99], 100) // -1"


#### **Solution:**
```javascript
function binarySearch(arr, value) {
    let start = 0;
    let end = arr.length - 1;
    let middle = Math.floor((start + end) / 2);
    while (arr[middle] !== value && start <= end) {
        if (arr[middle] < value)
            start = middle + 1;
        else
            end = middle - 1;
        middle = Math.floor((start + end) / 2);
    }
    return arr[middle] === value ? middle : -1;
}
```

## Naive/Basic String Search
This is similar to sub string search using **Multiple pointer pattern**. Time complexity is O(mn) where m is the length of the substring and n is the length of the string

```javascript
function subString(str, subStr) {
    if(subStr.length > str.length)
        return 0;
    let count = 0;
    for (let i = 0; i < str.length - (subStr.length - 1); i++) {
        for (let j = 0; j < subStr.length; j++) {
            if (str[i + j] !== subStr[j])
                break;
            if (j === subStr.length - 1)
                count++;

        }
    }
    return count;
}

console.log(subString("wnomgwnomg", "omg"));
```

## Kunth Morris Pratt String matching algorithm
This algorithm avoid the problem of backtracking the main index when matching wasnt found. Instead it creates pi table (or lps) and uses the to match string.

Time complexity for this algorithm is

To prepare the table - m

To match (parse through entire string n once) - n

**O (m + n)**

[Refer video](https://www.youtube.com/watch?v=V5-7GzOfADQ)


## Sorting algorithms
Sorting is a process of arranging items in a collection (for eg: array) in ascending or decending order


## Bubble sort
A sorting algorithm where the largest value bubble up to the top. Time complexity is O(n^2)

To visualize, refer [visualgo.net](https://visualgo.net/en)

**Basic algorithm:**

```javascript
function bubbleSort(arr) {
    const swap = (idx1,idx2)=>{
        [arr[idx1],arr[idx2]] = [arr[idx2], arr[idx1]];
    }
    for (let i = arr.length; i > 0; i--) {
        for (let j = 0; j < i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(j, j + 1);
            }
        }
    }
    return arr;
}
```


**Optimize with noSwaps** This is the best case when the input array is nearly sorted
```javascript
function bubbleSort(arr) {
    let noSwap;
    const swap = (idx1,idx2)=>{
        [arr[idx1],arr[idx2]] = [arr[idx2], arr[idx1]];
    }
    for (let i = arr.length; i > 0; i--) {
        noSwap = true;
        for (let j = 0; j < i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(j, j + 1);
                noSwap  = false;
            }
        }
        if(noSwap) break;
    }
    return arr
}
```

## Selection sort
Similar to bubble sort, but instead of first placing large values in to sorted position, place the small value first.
i.e, look for a min value each time the loop is execurted, and swap it with the initial position (initial position of unsorted values)


**Basic version:**
```javascript
function selectionSort(arr) {
    const swap = (idx1,idx2)=>{
        [arr[idx1],arr[idx2]] = [arr[idx2], arr[idx1]];
    }
    for (let i = 0; i < arr.length; i++) {
        for (let j = i + 1; j < arr.length; j++) {
            if(arr[i] > arr[j]){
                swap(i, j);
            }
        }
    }
    return arr;
}

selectionSort([23, 12, 43, 22, 55, 1, 2, 5]);
```


**Optimized version:** Here we are going to swap only at the end of the first loop when lowest has changed. When this is the case, (swap when required), Selection sort is considered little better than bubble sort.
```javascript
function selectionSort(arr) {
    let lowest;
    const swap = (idx1,idx2)=>{
        [arr[idx1],arr[idx2]] = [arr[idx2], arr[idx1]];
    }
    for (let i = 0; i < arr.length; i++) {
        lowest = i
        for (let j = i + 1; j < arr.length; j++) {
            if(arr[lowest] > arr[j]){
                lowest = j
            }

            console.log(arr, i, j)
        }
        if (i !== lowest) {
            swap(i, lowest);
        }
    }
    return arr
}

selectionSort([23, 12, 43, 22, 55, 1, 2, 5]);
```
