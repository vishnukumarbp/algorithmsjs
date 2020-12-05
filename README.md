# algorithmsjs-
Learning algorithms in js


## Problem solving patterns

### Frequency counter:

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
