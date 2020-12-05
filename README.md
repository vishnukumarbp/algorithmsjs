# algorithmsjs
Learning algorithms and examples in js


## Problem solving patterns

### Frequency counter & Multiple pointers:

#### Problem - sameFrequency
Frequency Counter - Samefrequencywrite A Function Called Samefrequency. Given Two Positive Integers, Find Out If The Two Numbers Have The Same Frequency Of Digits.

Your Solution Must Have The Following Complexities:
Time: O(N)

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

Restrictions: Time - O(n) Space - O(n)
Bonus: Time - O(n log n)Space - O(1)

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
Time: O(N)
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
Write A Function Called Issubsequence Which Takes In Two Strings And Checks Whether The Characters In The First String Form A Subsequence Of The Characters In The Second String. 
In Other Words, The Function Should Check Whether The Characters In The First String Appear Somewhere In The Second String, Without Their Order Changing.

Your Solution Must Have At Least The Following Complexities: 
Time Complexity - O(N + M)
Space Complexity - O(1)

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

