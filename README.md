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
