# algorithmsjs-
Learning algorithms in js


## Problem solving patterns

### Frequency counter:

#### Problem - sameFrequency
Frequency Counter - Samefrequencywrite A Function Called Samefrequency. Given Two Positive Integers, Find Out If The Two Numbers Have The Same Frequency Of Digits.

Your Solution Must Have The Following Complexities:
Time: O(N)

#### **Sample Input:**

- Samefrequency(182,281) // True
- Samefrequency(34,14) // False
- Samefrequency(3589578, 5879385) // True
- Samefrequency(22,222) // False

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
