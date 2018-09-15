---
layout: post
title:      "Same Problems, different solutions"
date:       2018-09-15 00:48:22 +0000
permalink:  same_problems_different_solutions
---


So far i've been on my fair share of interviews and while many of them require knowledge of JSON, Ajax, Jquery, it always comes back to the simple things. Do you know your higher order functions? Can you implement them to non-destructively alter input data? But most importantly, can you solve little javascript problems. Because this blog is more so a way for me to reiterate information i've picked up, i'm going to go over Javascript problems you may run into in an interview, or that i HAVE run into. 

Typically, it's good to have a few solutions to a single problem, here i'll go over three in particular, the first, easy, the second, a bit more challenging and the third a bit more challenging still. 

**Reversing a string**

Reversing a string is a typically very standard, simply function to write out, most people will do this typically by using higher order functions because, well, it's definitely the easiest. First solution is below

```
function reverse(str){
 return str.split('').reverse().join('')
}
```

very simply. First we split the string into an array of individual characters. The next step is to reverse the array, and finally, join it back together, returning the final result. Simple and straight forward. But what if you're asked to reverse a string using an iteration loop? Well, in that case, we can try something like this.

```
function reverse(str){
let reversed = ''
 for(let char of str){
  reversed = char + reversed
 }
 return reversed
}
```

In this solution, we have an empty variable "reversed", we iterate using a for of loop and set reversed equal to the chracter, plus the current value of reversed, thus giving us a reversed string. But of course, we want to get our ES6 on, so let's try this again using a higher order function and some ES6. 

```
function reverse(str) {
  return str.split('').reduce((rev, char) => char + rev, '')
}
```

Here, we have a very similair solution using a higher order function of reduce. We set the rev argument to an empty string, and the same way as we had previously, we add the characters to the beginning of the rev argument. Finally, we return the outcome and as you can see, we threw in an arrow function, no return statement inside reduce and no curly braces. Clean, and ES6-ified.

**Find the most reccuring item in an array**

Here, lets say we have an array of numbers

```
let arr = [1,2,3,3,3,4,5,2,3,2,2,7,8,5,4,3,3,4]
```

the most logical thing to do is to put these in a javascript object, or hash map, and once the keys are the letter and the value is the number of occurences, we choose the key with the highest value.

```
function most(array){
   let obj = {}

   for(let x in array){
     if(obj.hasOwnProperty(array[x])){
       obj[array[x]]++
     }else{
       obj[array[x]] = 1
     }
   }

     let mostKey = 0
     let mostVal = 0
   Object.keys(obj).forEach(function(key){
     var value = obj[key]
     if(value > mostVal){
       mostVal = value 
       mostKey = key
     }
   })
   return mostKey
 }
```

Here, we set 'ob' set to an empty object, we iterate through the array, and we say that if the obj has the key already, we increased its value by one, if not, we add the key and set its value to one. Afterwards, we have two variables, a mostKey and mostValue both set to 0. We then iterate through our newly populated object variable, check its keys, and if the value is higher than the current mostValue variable, we set the mostValue variable equal to said value, and immediately set the mostKey variable to the values key. Once finished, we return the mostKey variable. However, there is a cleaner way to write this!

```
function most(arr){
  const arrMap = {}
  let mostVal = 0
  let mostKey = 0
  for(let char of str){
    charMap[char] = charMap[char] + 1 || 1
  }
  
  for(let char in arrMap){
    if(charMap[char] > max){
      mostVal = arrMap[char]
      mostKey = char
    }
  }

  return mostKey
}
```

Here we have the same logic, but a little cleaner, specifically on line 6. Here instead of writing an if else statement, we simply say the key is equal to the key plus one, if the key does not exist, it returns undefined and goes to our next option, which is to simply set the key to the value of 1. Great!

**Valid brackets test**

This was a question i had found in an interview and had quite a bit of trouble with it. Essentially the point is to be able to take a string of brackets or parentheses and return true if the syntax is valid, and false if not. Examples:

"(){}" - true 
"((()))" - true
"([{]])" - false 

The key here is the the paramters we're looking for. The code i had come up with is below.

```
function isValid(str) {

  if (str.length <= 1)
    return false

  let matchingOpening, char
  let stack = []

  let openingBrackets = ['[', '{', '(']
  let closingBrackets = [']', '}', ')']

  for (let i = 0; i < str.length; i++) {
    char = str[i]

    if (closingBrackets.indexOf(char) > -1) {
      matchingOpening = openingBrackets[closingBrackets.indexOf(char)]
      if (stack.length == 0 || (stack.pop() != matchingOpening)) {
        return false
      }
    } else {
      stack.push(char)
    }
  }

  return (stack.length == 0)
};
```

The trick here is, if the bracket is an opening bracket, the statement *so far* is valid. In that case, add it to the stack or array. If the next bracket is a closing bracket, check if it matches the previous opening bracket, if so, remove them entirely and continue. If not, the string is false. This function only returns true if the stack is equal to 0 in the end. 

Here you create the stack variable, create two arrays containing the opening and closing brackets, both having the matching opening and closing brackets at the same indexes. Iterate through the string and set the char variable to the current character, if it is a closing bracket, set the matchingOpening variable to the opening bracket that aligns with the index of the closing bracket (this is why the indexes aligning is key). If the stacks length is currently 0, or the bracket in the stack does not match the opening bracket that it should be, return false, otherwise push the bracket to the stack(it's an opening bracket). Finally, return the boolean value of the statement stack.length === 0. 

Yea, i know, pretty complicated. However, i found this solution to be much cleaner, and more efficient. 

```
function isValid(str) {
  var stack = [];
  var open = { '{': '}', '[': ']', '(': ')' };
  var closed = { '}': true, ']': true, ')': true };
  
  for (var i = 0; i < str.length; i ++) {
    var chr = str[i];
    if (open[chr]) {
      stack.push(chr);
    } else if (closed[chr]) {
      if (open[stack.pop()] !== chr) return false;
    }
  }
  
  return stack.length === 0;
};
```

MUCH shorter. Here we have two objects, an open and closed object. The open object has values equal to the closing matching bracket, the closing bracket object has values equaling the boolean true. We iterate through the string, set the chracter to the chr variable, and if the open object contains the character, push it to the stack, if it's a closing bracket, check if its equal to the *value* of the previous open bracket, if not, return false. Finally, same as before, return the boolean value of the stack.length === 0.

I hope these can be helpful to others, it certainly helps me to just rewrite them again. Until next week!
