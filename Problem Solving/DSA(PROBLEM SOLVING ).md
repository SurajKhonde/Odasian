
### STRING 
#### 1. Reverse a String
   *Brute Force Code*
```javascript
function reverseString(str) {
  let reversed = "";
  for (let i = str.length - 1; i >= 0; i--) {
    reversed += str[i];
  }
  return reversed;
}
console.log(reverseString("hello")); // "olleh"
```
*Two Pointer Approach*
```javascript
function reverseStringOptimal(str) {
  let arr = str.split("");
  let left = 0;
  let right = arr.length - 1;
  while (left < right) {
    // Swap characters
    [arr[left], arr[right]] = [arr[right], arr[left]];
    left++;
    right--;
  }
  return arr.join("");
}
console.log(reverseStringOptimal("hello")); // "olleh"
```

#### 2. Check if a string is a palindrome
``` javascript
function isPalindrome(str) {
  let left = 0, right = str.length - 1;

  while (left < right) {
    if (str[left] !== str[right]) return false;
    left++;
    right--;
  }

  return true;
}

```
#### 3. Anagram Check
Check if two strings are **anagrams** of each other.
Two strings are anagrams if they have the **same characters** with the **same frequencies**, just in a different order.
Time Complexity: `O(n)`
Space Complexity: `O(1)` (if limited to lowercase English letters)
```javascript
function isAnagram(str1, str2) {
  if (str1.length !== str2.length) return false;
  const count = Array(26).fill(0); // for lowercase 'a' to 'z'
  for (let i = 0; i < str1.length; i++) {
    count[str1.charCodeAt(i) - 97]++;
    count[str2.charCodeAt(i) - 97]--;
  }
  return count.every(c => c === 0);
}
console.log(isAnagram("listen", "silent")); // true
console.log(isAnagram("hello", "world"));   // false

```
- It avoids sorting (which is `O(n log n)`).
- It does a single scan over both strings (`O(n)` time).
- It uses fixed-size space (array of 26 for a-z), not a dynamic object.

 *With a Frequency Hash Map (supports any character set)*
 ```javascript
 function isAnagramHash(str1, str2) {
  if (str1.length !== str2.length) return false;
  const map = {};
  for (let char of str1) {
    map[char] = (map[char] || 0) + 1;
  }
  for (let char of str2) {
    if (!map[char]) return false;
    map[char]--;
  }
  return true;
}
```
How it works step by step:
Suppose `str1 = "abbc"`
Initial: `map = {}`
Loop through each character:
1. First `a`:
    - `map['a']` is `undefined`, so `(undefined || 0)` → `0`
    - So `map['a'] = 0 + 1 = 1`
    - Result: `{ a: 1 }`

#### 4. Longest Substring Without Repeating Characters
    Given a string `s`, return the **length** of the **longest substring** without repeating characters.
*Best Approach: Sliding Window + Set*
```javascript
function longestUniqueSubstring(str) {
  let left = 0; // Window का बायाँ हिस्सा
  let maxLength = 0; // सबसे लंबी अनूठी सबस्ट्रिंग की लंबाई
  let charSet = new Set(); // Set का उपयोग कर के हम यूनिक characters ट्रैक करेंगे

  for (let right = 0; right < str.length; right++) {
    // अगर चरित्र पहले से मौजूद है तो left pointer को बढ़ाओ
    while (charSet.has(str[right])) {
      // duplicate character को हटाने के लिए बायें pointer को इधर-उधर करेंगे
      charSet.delete(str[left]);
      left++;
    }
    
    // नए character को सेट में डालना
    charSet.add(str[right]);

    // Max length को अपडेट करना
    maxLength = Math.max(maxLength, right - left + 1);
  }

  return maxLength;
}

// Example
const inputString = "abcdefaxy";
console.log(longestUniqueSubstring(inputString)); // Output: 7

 // example
longestUniqueSubstring("abcabcbb");
// Output: 3
// Longest: "abc"
longestUniqueSubstring("bbbbb");
// Output: 1
// Longest: "b"

```
#### 5. Remove Duplicates
```javascript
function removeDuplicate(str) {
  return [...new Set(str)].join('');
}

```
Method 2: Using `Map` (if you want both uniqueness + frequency)
```javascript
function removeDuplicate(str) {
  const map = new Map();
  let result = '';

  for (const char of str) {
    if (!map.has(char)) {
      map.set(char, 1);
      result += char;
    }
  }

  return result;
}

```

#### 6. Find two distinct elements in the array such that their sum is equal to the target.
  Sorted array hai? → Use Two Pointers
  ```javascript
  function findPairWithSum(arr, target) {
  let i = 0, j = arr.length - 1;
  while (i < j) {
    let sum = arr[i] + arr[j];
    if (sum === target) {
      return [arr[i], arr[j]]; 
    } else if (sum < target) {
      i++;  
    } else {
      j--; 
    }
  }
  return null; 
}

```
Brute Force
```javascript
function findPairBruteForce(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] + arr[j] === target) {
        return [arr[i], arr[j]]; //  Return first pair found
      }
    }
  }

  return null; // ❌ No pair found
}

```
Using Set(O(n))
```js
function findPairUsingSet(arr, target) {
  const seen = new Set();

  for (let num of arr) {
    const complement = target - num;
    if (seen.has(complement)) {
      return [complement, num]; //  Pair found
    }
    seen.add(num);
  }
  return null; // ❌ No pair found
}
```
findPairUsingMap (O(n))
```js
function findPairUsingMap(arr, target) {
  const map = new Map(); // value → index (optional if just checking for values)
  for (let i = 0; i < arr.length; i++) {
    const complement = target - arr[i];
    if (map.has(complement)) {
      return [complement, arr[i]];
    }
    map.set(arr[i], i);
  }

  return null;

```
#### 7.  Most Frequent Character
```js
function mostFrequentCharBrute(str) {
  let maxChar = '';
  let maxCount = 0;
  for (let i = 0; i < str.length; i++) {
    let count = 0;
    for (let j = 0; j < str.length; j++) {
      if (str[i] === str[j]) {
        count++;
      }
    }
    if (count > maxCount) {
      maxCount = count;
      maxChar = str[i];
    }
  }

  return { char: maxChar, count: maxCount };
}

```

Return the Most Frequent Character
```javascript
function mostFrequentChar(str) {
  const freqMap = new Map();
  let maxChar = '';
  let maxCount = 0;
  for (let char of str) {
    const count = freqMap.has(char) ? freqMap.get(char) + 1 : 1;
    freqMap.set(char, count);
    // 🔍 Keep track of the max while building the map
    if (count > maxCount) {
      maxCount = count;
      maxChar = char;
    }
  }
  return { char: maxChar, count: maxCount };
}

```
#### 8.Valid Parentheses
Given a string containing just the characters (, ), {, }, [ and ], determine if the input string is valid.

Brute-Force Idea Version
```js
function isValidParenthesesBrute(s) {
  let prev = '';
  
  while (s !== prev) {
    prev = s;
    s = s.replace('()', '');
    s = s.replace('{}', '');
    s = s.replace('[]', '');
  }

  return s.length === 0;
}
```
Solution Using Stack (Best Way)
```js
function isValidParentheses(s) {
  const stack = [];
  const map = {
    ')': '(',
    '}': '{',
    ']': '[',
  };
  for (let char of s) {
    if (char === '(' || char === '{' || char === '[') {
      stack.push(char);
    } else {
      if (stack.pop() !== map[char]) {
        return false;
      }
    }
  }
  return stack.length === 0;
}
```
#### 9. Longest Common Prefix
**Given an array of strings**, find the **longest common prefix string** among them.
If there is no common prefix, return an **empty string `""`**.
```js
Input: ["flower", "flow", "flight"]
Output: "fl"

```