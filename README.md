# Basic-Algorithm-Scripting

- I will be logging entries only for challenges that I do not really understand

## Reverse a String

- Objective is to create a function that takes a string argument and return a reversed version of the string
- The last module was heavily focused on objects and arrays and I couldn't remember what to do with disassembling strings

```js
function reverseString(str) {       // function 'reverseString' takes a string as its argument
    let revStr = "";                // declare a new variable and assign an empty string. The reversed string will be assigned to the new variable
    for (let i = str.length - 1; i >= 0; i--) { // let the value of i equal to the last character of the string. While i is greater than equal to 0, decrement i by 1
        revStr += str[i];           // concatenate the iterated value of the string to the remaining portion of the original string
    }
    return revStr;                  // return the reversed string
}

console.log(reverseString("hello world")); // "dlrow olleh"
```

- revStr += str[i] portion looks like this

```js
hello world     // Original string
hello worl + d
hello wor + dl
hello wo + dlr
hello w + dlro
hello + dlrow_  // Notice that it also accounts for whitespace
hell + dlrow o
hel + dlrow ol
he + dlrow oll
h + dlrow olle
dlrow olleh     // reversed string
```

- There is a simpler approach to this.
- The use of split(), reverse(), and join() methods.

```js
function reverseString(str) {
    return str.split("").reverse().join("");
}

console.log(reverseString("hello")); // olleh
```

- .split("") will split the string by each character.
- .reverse() will reverse the order of the characters
- .join("") will join the separated characters into a new string.

## Factorialize a Number

- Return a factorial of a positive integer passed to the function

```js
function factorialize(num) { // Use recursive function 
    if (num === 0) {    // base case. If num strictly equals 0, return the result
        return 1;       // When base case is reached, the result will be multiplied by 1 and the function will stop execution
    }                   // It is viable to put an 'else' here but it doesn't seem necessary
    return num * factorialize(num - 1); // Multiply num by the function with decrementing num value until base case is reached
}

console.log(factorialize(5)); // 5 * 4 * 3 * 2 * 1 = 120
```

- Although the recursive function is efficient and easy to read, I am trying other methods to achieve the same result.

```js
function factorialize(num) {
    let newArr = [];
    while (num > 0) {
        newArr.push(num);
        num--;
    }
    return newArr.reduce((accu, val) => accu * val, 1);
}
```

- Use a while loop to generate an array 'newArr' containing the range of numbers to factorialize.
- reduce method is called on the 'newArr' with the accumulator argument and each element of 'newArr', 'val'.
- multiply the accumulator by val with an initial value of 1 for the accumulator.

## Find the Longest Word in a String

- create a function that takes a sentence as a string argument
- The function should return the number of the characters in the longest word in the sentence.

```js
function findLongestWordLength(str) {
    let longestLength = 0;  // Keep a count of the longest word length as it iterates through the string
    let currentLength = 0;  // Keep a count of the length of the current word

    for (let i = 0; i < str.length; i++) {  // Iterate through string
        if (str[i] === " ") {       // If the character at the current position of 'i' is whitespace (i.e. if it's the end of a word)
            if (currentLength > longestLength) {    // and if the current length of the word is greater than the longest length logged
                longestLength = currentLength;      // then the longestLength equals the value of the currentLength
            }
            currentLength = 0;  // reset the count value of the current length and loop through the function.
        } else {
            currentLength++;    // If above condition are not met (i.e. if it's still iterating through a word), move to the next character count
            /* If the code stops here, it is fine as long as the longest word is not at the end of the string.
            This is because the code is setup to update the longestLength variable only when it encounters a whitespace.
            Because of this setup, when it reaches the end of a string, it will not update the variable accordingly 
            even if the last word of the string is the longest in the sentence.
            Add the following 'if' statement AFTER the loop to check to see if the length of the current word (the last word of the string)
            is indeed the longest word of the string.*/
            if (currentLength > longestLength) {
                longestLength = currentLength;
            }
        }
    }
    return longestLength;
}
```

- Tried another solution. Seems similar but a bit simpler

```js
function findLongestWordLength(str) {
    let strArr = str.split(" "); // split the string into an array
    let longestLength = 0;       // initialize longestLength with 0 assigned to it to keep track of the longest length of word globally
    for (let i = 0; i < strArr.length; i++) {   // use for loop to iterate through split array
        let currentLength = strArr[i].length;   // assign 'currentLength' to the length of the current string being processed
        if (currentLength > longestLength) {    // if 'currentLength' is greater than 'longestLength'
            longestLength = strArr[i].length;   // 'longestLength' is equal to that word at that index
        }
    }
    return longestLength;
}
```

## Return Largest Number in Arrays

- An array containing sub-arrays is passed to a function.
- The function created should return the largest number in each array in a new array.

- declare a new array with an empty array
- iterate through the array and its sub-arrays (one subarray at a time)
- keep track of the largest number and compare to current number
- if largest number in a sub-array is found, push that number to the new array variable

```js
function largestOfFour(arr) {
    let newArr = [];    // declare a new variable 'newArr' with an empty array to which the largest number of each subarray will be added.

    for (let i = 0; i < arr.length; i++) {  // for loop to iterate through each subarray
        let largestNum = arr[i][0];
        /* largestNum variable is declared with value of arr at index [i][0].
        It is indicating where the iteration should begin.
        It is not 'arr[i][j]' since 'j' has not been declared yet.*/
        for (let j = 0; j < arr[i].length; j++) {   // for loop to iterate through each element of subarray
            if (arr[i][j] > largestNum) {   // if number value at 'arr[i][j]' is greater than the current largest number
                largestNum = arr[i][j];     // then reassign largestNum to the number value at the current 'arr[i][j] position
            }
        }
        newArr.push(largestNum);    // AFTER iterating through the first subarray, push largestNum of that subarray to 'newArr'. Then carry on.
        /* The placement of the push was a bit confusing at first. 
        Partly because the editor screen in FCC has the same color for all curly braces.
        It's a bit more clear in vscode.
        Placing the push anywhere above this line in the code will return unexpected results. 
        It will be constantly pushing numbers into 'newArr'
        At first I had 'newArr.push(arr[i][j]);' but the console would read 'j is not defined' since it's outside the 2nd for loop
        Then realized the 'arr[i][j]' is assigned to 'largestNum'.
        I have to get used to thinking through the logic of the problem. 
        Honestly, this one was a bit of a fluke.*/
    }
    return newArr;
}
```

- Tried another solution. A bit more concise

```js
function largestOfFour(arr) {
    let newArr = [];                // declare a new array 'newArr' with an empty array
    for (let i = 0; i < arr.length; i++) { // 'for' loop to iterate through the original array
        let biggestNum = Math.max(...arr[i]); // iterate through each sub-array and retrieve the largest numbers from each using Math.max. 
                                              // remember to use spread operator
        newArr.push(biggestNum);              // push the retrieved numbers in the 'newArr'
    }
    return newArr;
}
```

## Confirm the Ending

- Create a function 'confirmEnding', which takes two strings (str, target) as its arguments.
- The objective of the function is to check if the first string argument (str) passed to the function ends with the second string argument (target)

- I need to iterate through the first string argument
- Iteration should be conducted backwards.

```js
function confirmEnding(str, target) {
  for (let i = str.length - 1; i >= 0; i--) {
    for (let j = target.length -1; j >= 0; j--) {
      if (str[i] === target[j]) {
        return true;
      } else {
        return false;
      }
    }

  }
  return str;
}
```

- Initially tried the above, and it failed.
- The problem is that if the last letter matches, it immediately returns true, even if the next character in sequence does not match.
- It needs to iterate through the entire target string before returning a result.
  
- But come to think of it, I think this is getting way too complex.
- There has to be a simpler method.

- if I subtract the length of target from the length of str, I could use that value to extract the number of characters from 'str' equal to that of 'target'.
- Then, if the value of the extraction from 'str' is equal to the value of 'target', return true.
- if not return false.
- use slice() method

```js
function confirmEnding(str, target) {
    let diff = str.length - target.length; //declare a variable and assign it the value of the diff. between the lengths of 'str' and 'target'
    let extract = str.slice(diff); //declare a variable and assign it the value of applying slice() to the string.
    // If a single parameter is passed to slice(), it will begin extraction from the character following the index position specified to the end of the string.
    // I found this to be pleasantly convenient.

    if (extract === target) { // if the value extracted through slice() is equivalent to the value of 'target'
        return true;         
    } else {
        return false;
    }
}
```

- This passes, now looking at it in retrospect, I think it can be simplified without declaring variables.

```js
function confirmEnding(str, target) {
    return str.slice(str.length - target.length) === target;
}
```

- I still find declaring variables to be more readable.
- I guess it's because I still have trouble 'thinking' in JS. I need to see it visually.

- NOTE: looking at the solutions provided in FCC, if a negative number is provided as the first parameter to slice(), the offset is then backwards from the end of the string.

```js
function confirmEnding(str, target) {
    return str.slice(-target.length) === target;    // REMEMBER THIS!!!! 
}
```

- There is a method introduced here but I'm not supposed to use it
- ```.endsWith()```

```js
function confirmEnding(str, target) {
    return str.endsWith(target); // That's it!?
}
```

## Repeat a String Repeat a String

- create a function that repeats a string (str) for 'num' times specified.
- It should return an empty string if num is not a positive number.

- I should use a loop to repeat the process 'num' times
- I should declare a new variable to 'store' the result

```js
function repeatStringNumTimes(str, num) {
    let newStr = "";        // declare a new variable to store the result
    while (num > 0) {       // while 'num' is greater than 0,
        newStr += str;      // append 'str' to 'newStr'
        num--;              // decrement 'num' by 1 after every loop until num = 0
    }
    return newStr;
}
```

- Tried this using recursive function

```js
function repeatStringNumTimes(str, num) {
    if (num <= 0) {     // set the base case. If num is less than or equal to 0, 
        return "";      // return an empty string.
    } else {            // if not
        return str + repeatStringNumTimes(str, num - 1); // keep concatenating string until base case is reached.
    }
}
```

- Another method is introduced in this challenge but forbids me to use it
- ```.repeat()```

```js
function repeatStringNumTimes(str, num) {
    return str.repeat(num);
}
```

## Truncate a String

- create a function that truncates a string (first argument) if it is longer than the specified max string length (second argument).
- The returned truncated string should end with ```...```
- If the 'num' value is greater than or equal to the string length, return the string.

- Declare a variable to return the result
- Use an if statement to determine whether the string length exceeds the max value
  - if it exceeds the max value, use slice() method to truncate the string and append '...'
  - if it does not exceed the max value, return the string.

```js
function truncateString(str, num) {
    let newStr = ""; // initialize a new variable. Strings are immutable.

    if (str.length > num) {
        newStr = str.slice(0, num).concat('...'); // wasn't sure if .concat() was going to work. Now I know it does!
    } else if(str.length <= num) { // 'if' is not really necessary. I just put it there for personal clarification
        newStr = str;
    }
    return newStr;
}
```

- I tried the following

```js
function truncateString(str, num) {
    return str.slice(0, 8).concat("...");
}
```

- The above passes as long as the second argument is an actual numerical value.
- But FCC had to throw in challenges like 'str.length' and 'str.length + 2'.
- I guess that's the point of the challenge, but I learned something new today.

- Thought of this in the shower
- convert the 'str.length' value to a numerical value.

```js
function truncateString(str, num){
    num = Number(num);
    if (str.length > num) {
        return str.slice(0, num).concat("...");
    } else {
        return str;
    }
}
```

## Finders Keepers

- create a function that iterates through an array (arr) and returns the first element that returns 'true' for the function (func) passed to the function.
- If no element passes, return 'undefined'

- use a 'for' loop to iterate through the array passed to the function
- if 'num' returns 'true' when it is passed to the function that is passed through the function as it iterates through the array, return that 'num' in the array.
- If none of the 'num' values return true, return 'undefined'

```js
function findElement(arr, func) {
    for (let num = 0; num < arr.length; num++) { // for loop to iterate through given array
        if (func(arr[num]) === true) {  // if current 'num' of the array returns true for the function passed to the function
            return (arr[num]);  // return that 'num'
        }
    }
    return undefined;   // If none of the elements return true, return 'undefined'. Notice this return is placed outside of the loop. 
}
```

- Tried the following and surprised it worked

```js
function findElement(arr, func) {
  const result = arr.filter(func);
  return result[0];
}

findElement([1, 2, 3, 4], num => num % 2 === 0)
```

- use filter on arr and pass the callback function
- The callback function will iterate through the array and return a new array with even numbers, which in the case above would be [2, 4]
- Then just return the first element at index 0 to get the first element that passes the truth test.

## Boo Who

- create a function that checks if the argument passed to the function is a 'boolean'
- Return true or false

- sounds simple enough but I had a bit of trouble with this one.
- For one thing, I didn't know that I had to use 'boolean' as a string to compare.
- I had the right idea initially, but it took me a while to figure out how to compare the (typeof bool) to 'boolean'.

- use an 'if' statement to check if the 'typeof' argument value is a "boolean".
- Return true if it is, false if not.

```js
function booWho(bool) {
    if ((typeof bool) === "boolean") { // I initially had 'if ((typeof bool) === true || false)', which was silly.
        return true;
    }
    return false;
}
```

- To this point, I still didn't understand why 'typeof(bool)' had to be compared with the string 'boolean', not ```Boolean```
- ```Boolean``` with a capital 'B' is a constructor function used to create 'boolean' objects.

```js
const myBoolean = new Boolean(true);
```

- The above example will create a boolean object 'myBoolean' with a value 'true' assigned to it.
- But if you check the 'typeof(myBoolean)' it will still return 'object' since it is a created object with a boolean value assigned to it.
- However, 'true' and 'false' are known as ```primitive boolean values```.
- in other words, if you check 'typeof(true)' or 'typeof(false)' it will return the string 'boolean'
- since we're looking for the ```primitive boolean values```, it makes sense to compare it to the string 'boolean'

## Various Methods

- There are more and more methods that are mentioned in the challenges, but I have not yet been introduced to them.
- I guess it's time to start digging around and find out for myself.

### split()

- split() method is used to split a string into an array of substrings.
- It takes two parameters

```js
string.split(separator, limit);
```

- The separator specifies the character(s) or regular expression used to determine where to split the string.
- If 'separator' is not specified, the entire string will be returned.
- The 'limit' parameter specifies the max number of splits to be performed.
- if not specified, all possible splits will be returned.

```js
const str = "apple, banana, orange, grape, kiwi";
const arr = str.split(",", 3);
console.log(arr); // ["apple", "banana", "orange"]
```

- In the above example, the string will be split at every ',', three times.

### toUpperCase() / toLowerCase()

- Append .toUpperCase() or .toLowerCase() to a variable assigned to a string to change the letter-casing

```js
someString.toUpperCase();
someString.toLowercase();
```

- It does not take any parameters

### .charAt()

- This method is used to extract a character specified by the passed parameter
- It uses zero-based indexing

```js
let string = "Hello world!";
console.log(string.charAt(4));   // 'l'
```

- if the specified parameter value is outside the range of valid indices, it will return an empty string.

### .join()

- .join() method works opposite to .split()
- It takes a separator parameter, which is used to join the elements of an array into a string.
- If the separator is not specified, it will use its default separator (',').

```js
const arr = ['apple', 'banana', 'orange'];
const str = arr.join(" ");  // separate elements with a whitespace
console.log(str); // "apple banana orange"
```

## Title Case a Sentence

- Create a function that takes a sentence string and converts the first letter of every word to uppercase and remaining words to lowercase

```js
function titleCase(str) {
    let newArr = [];        // initialize a new variable 'newArr' with an empty array
    let splitArr = str.split(" ");  // initialize a new variable and assign it the result of splitting the string passed to the function. Separate with whitespace
  for (let i = 0; i < splitArr.length; i++) {   // setup the for loop to iterate through the split string
      if (/^[A-Z][a-z]*$/.test(splitArr[i])) {  // use regex to check if the first character of the current element is uppercase and the remaining are lowercase
          newArr.push(splitArr[i]);             // if the regex test returns true, push that element to 'newArr'
      } else {                                  // if the regex test does not return true
        splitArr[i] = splitArr[i].toLowerCase();    // Convert all characters of the current element to lowercase
        splitArr[i] = splitArr[i].charAt(0).toUpperCase() + splitArr[i].slice(1);
        // After converting to lowercase, extract the character at (charAt) index 0 and convert that character to uppercase.
        // Concatenate the character converted to uppercase with the result of slicing the current element at index 1.
        // .slice(1) will extract all characters from index 1 to the end of the string.
        newArr.push(splitArr[i]);   // push the newly updated string and push to 'newArr'
      }
  }
  return newArr.join(" ");  // Join the elements from 'newArr' with a whitespace between each element
}

console.log(titleCase("I'm a little tea pot")); // I'm A Little Tea Pot
```

- I'm sure there are much simpler methods.
- But this is what I have at the moment

- tried a different approach

```js
function titleCase(str) {
    str = str.toLowerCase().split(/\s+/);
    for (let i = 0; i <str.length; i++) {
        str[i] = str[i].charAt(0).toUpperCase() + str[i].slice(1);
    }
    return str.join(" ");
}
```

- reassign th string by converting all characters to lower case and split string at any whitespace character using regex
- use a 'for' loop to iterate through the string array created by splitting the string
- for each of the string element int the array, convert the characters at index 0 of the string (charAt(0)) to uppercase
  - note that this portion of the code will only return the capitalized portion of the string ['I', 'A', 'L', 'T', 'P'].
  - the rest of the string needs to be concatenated.
- To concatenate, slice the current string from index 1 to the end of the string.
- the result would be [ 'I\'m', 'A', 'Little', 'Tea', 'Pot' ]
- Then use .join() method to convert the array back into a single string.

## Slice and Splice

- create a function that takes two arrays and an index value as its arguments
- The function should take the elements of the first array and insert it into the second array in order.
- The insertion should begin at the index specified.
- The original arrays should not be modified.

```js
function frankenSplice(arr1, arr2, n) {
    let arr2Slice = arr2.slice(0);  // slice arr2 and assign it to a new variable to prevent modification of the original array
    for (let i = arr1.length - 1; i >= 0; i--) { // Iterate through arr1 in reverse order
        arr2Slice.splice(n, 0, arr1[i]);    // Insert the iterated elements one by one into arr2Slice starting at index 'n'
    }
    return arr2Slice;
}

console.log(frankenSplice([1, 2, 3][4, 5, 6], 1));  // [4, 1, 2, 3, 5, 6]
```

Shown below is what I originally had

```js
function frankenSplice(arr1, arr2, n) {
  let arr2Slice = arr2.slice(0);
  for (let i = 0; i < arr1.length; i++) {
    arr2Slice.splice(n, 0, arr1[i]);
  }
  return arr2Slice;
}

console.log(frankenSplice([1, 2, 3], [4, 5, 6], 1)); // [4, 3, 2, 1, 5, 6]
```

- I didn't take into account that each iterated element is inserted in to the same index 'n' position.
- Which in turn would 'push' the inserted elements.
- Reverse the loop iteration to reverse this effect.

- tried something else without the for loop

```js
function frankenSplice(arr1, arr2, n) {
    arr2 = arr2.slice(0).splice(n, 0, ...arr1);
    return arr2;
}
```

- Tried the above initially but it returned an empty array.
- arr2.slice(0) effectively created a copy of arr2, but the splice method returns an array with the deleted elements.
- Since nothing is deleted using the splice method, it returns an empty array.

```js
function frankenSplice(arr1, arr2, n) {
    arr2.splice(n, 0, ...arr1);
    return arr2;
}
```

- This achieves the intended result, but it modifies the original array, so it doesn't pass

```js
function frankenSplice(arr1, arr2, n) {
    arr2 = arr2.slice(0);
    arr2.splice(n, 0, ...arr1);
    return arr2;
}
```

- The above code works, but I think it would be better to declare a new variable for arr2 for clarity and readability.


```js
function frankenSplice(arr1, arr2, n) {
    let newArr2 = arr2.slice(0);
    newArr2.splice(n, 0, ...arr1);
    return newArr2;
}
```

- create a copy of arr2 using slice at index 0.
- use splice on the copied array to insert arr1 (using spread operator, otherwise it will insert the array itself) at index 'n', and delete 0 elements
- return the modified array

## More new methods

### Boolean()

- Use ```Boolean()``` (notice the uppercase B) to convert any value to a boolean value (i.e. true or false)

```js
let value = "string";
let booleanValue = Boolean(value);
console.log(booleanValue); // true
```

- You can also use double negation operator (!!)

```js
let value = null;
let booleanValue = !!value;
console.log(booleanValue); // false
```

## Falsy Bouncer

- Create a function that removes all falsy values from an array
- The original array should not be modified

```js
function bouncer(arr) {
    let bounced = [];
    for (let i = 0; i < arr.length; i++) {
        let booleanValue = !!(arr[i]);  // or you can remove this line and go directly to the if statement
        if (booleanValue === true) {    // if (Boolean(arr[i]) === true)
            bounced.push(arr[i]);
        }
    }
    return bounced;
}

console.log(bouncer([7, "ate", "", false, 9])); // [7, "ate", 9]
```

- I originally tried going the other way, looking for falsy values to kick out

```js
function bouncer(arr) {
    let bounced = arr.slice(0);
    for (let i = 0; i < arr.length; i++) {
        let booleanValue = Boolean(arr[i]);
        if (booleanValue === false) {
            bounced.splice(arr[i], 1);
        }
    }
    return bounced;
}
```

- This returned some unexpected results. I believe it was ["", false, 9]
- I later realized that 'arr[i]' is directing to the string rather than the index value.
- So I changed the splice line to

```js
bounced.splice(i, 1);
```

- But this also returned an unexpected result.
- [7, "ate", false]
- I thought that looking for falsy values may be causing some confusion in the code. I really can't explain what it is though.
- So I changed the code to look for truthy values instead.
- I was sticking to falsy values because I wanted to get more practice using splice and slice methods.

## New Method

### sort()

- use ```sort()``` to sort elements of an array in logical sequence.
- default sort order is ascending
- The default comparison criteria is based on UTF-16 code unit values (I really don't know what this means but it's not the common logical order)
- If no function is passed to .sort(), by default, it will convert the elements into strings for comparison.

- by passing a function to the sort method, you can specify the sorting order.

```js
let numbers = [4, 56, 23, 8]
numbers.sort(function(a, b) {
    return  a - b;
});
console.log(numbers); // [4, 8, 23, 56]
```

- It took me a while to understand this.
- The function passed as the parameter for numbers.sort will take two numbers and compare the two.
- in the array above, first two will be 4 (a) and 56 (b)
- If 'a - b' is negative, it means that a is less than b; So it their positions will not change
- The next pair would be 56 (a) and 23 (b)
- If 'a - b' is positive, it means that a is greater than b; so a will move to the right of b.
- if 'a - b' is 0, it means that the two numbers are equal and order does not matter.
- this process will repeat until swapping of positions is no longer required, resulting in an ascending numerical array.

## Where do I Belong

- create a function that accepts two arguments - an array 'arr' and a number 'num'.
- The function should sort the elements of the array in logical sequence and determine the lowest index at which the 'num' value should be inserted.
- The return value should be a number that indicates the index value.
- if the number specified is greater than the last value of the array, it should return the last number's index value + 1 (which is also equal to the array length)
- if the array is empty, it should return 0.

```js
function getIndexToIns(arr, num) {
    if (arr.length === 0) { // Placed here before anything else to check if the array is empty
        return 0;           // If it's empty, there is no need for the loop. return 0
    }
    arr.sort(function (a, b) { 
        return a - b;
    });
    for (let i = 0; i < arr.length; i++) {
        if (num <= arr[i]) {
            return i;
        }
    }
    return arr.length; // Initially made the mistake of placing this one level deeper, which is within the loop.
                       // It needs to finish the loop and determine that there is no match and return the arr.length
}
```

- The function takes an array and a number.
- 'if' statement is placed outside of the loop.
  - It will check the array length to begin with. If the array length is 0 (i.e. it's an empty array),
  - it will immediately return 0. No need to iterate through the array.
- The sort function will sort the elements of the array from lowest to highest numerical value.
- Now for the loop.
  - Use a for loop to iterate through the array
  - During iteration, as soon as it encounters a numerical value in the element that is greater than the number passed to the function,
  - return the value of the current 'i'.
- If none of the numerical values in the array is greater than the number passed to the function (in other words, no match is found until the end of the array)
- return the length of the array.

- Always think about whether to place something before the loop, inside the loop, or after the loop.

## Mutations

- Create a function that accepts an array containing two strings as its argument.
- Return true if the first string contains all of the characters of the second string
- ignore letter-casing

- convert all letter casing to upper or lower for both strings
- It would be easier to work with each string separately.
- using a for loop, iterate through the second string and check if each character is found in the first string using .indexOf()
- Use an 'if' statement to return false if it encounters a character that is not found in the first string.
- If .indexOf() is used to return true if a character match is found, it will always return true if the first character in the second string is a match, regardless if there is a character that does not match later in the string.
- So, look for non-matching character to return false.
- If it does not return false until the end of the string, return 'true' (after the loop is finished iteration)

```js
function mutation(arr) {
    let str1 = arr[0].toLowerCase(); // both of the strings can be converted to uppercase
    let str2 = arr[1].toLowerCase();

    for (let i = 0; i < str2.length; i++) {
        if (str1.indexOf(str2[i]) === -1) {
            return false;
        }
    }
    return true;
}
```

## Chunky Monkey

- Write a function that accepts an array 'arr' and a number 'size'
- The function should split the elements of the original array into groups of 'size'
- It should then push those split elements into separate subarrays of one nested array

```js
function chunkArrayInGroups(arr, size) {    // function accepts an array 'arr' and a number 'size' as its arguments.
    let newArr = [];                        // initialize a new variable 'newArr' with an empty array
    // Use a 'for' loop to iterate through the array passed to the function.
    // Out of habit, I initially had 'i++' for the increment value. But this was adding 4 subarrays to the result.
    // Had to do some thinking and trial & error process to realize that it should increment by the specified 'size'
    for (let i = 0; i < arr.length; i+=size) {
        // initialize 'subArr' with sliced subarrays. 'i' would indicate the current element, and it should slice at 'i + size'.
        // it works well because the index value of 'i + size' is not inclusive when slice is executed.
        let subArr = arr.slice(i, i + size);
        newArr.push(subArr); // push the sliced subArr to newArr and return.
    }
    return newArr;
}
```
