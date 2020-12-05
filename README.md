# algorithms in js
Learning algorithms and examples in js

### Topics under Algorithms

#### Big O notation:
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

##### Big O Shorthands:

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
