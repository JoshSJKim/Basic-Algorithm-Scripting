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
