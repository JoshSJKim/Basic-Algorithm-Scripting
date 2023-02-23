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
    return str.slice(-target.length) === target;
}
```
