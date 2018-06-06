---
layout: post
title:      "var, let, const, a new scope....and arrow functions"
date:       2018-06-06 13:19:40 -0400
permalink:  var_let_const_a_new_scope_and_arrow_functions
---


Prior to Flatiron i had attempted to learn some Javascript on my own, but this was the ES5 days, before **var** was a dirty word and before arrow functions were all the rave. So upon introductions to let and const, i was specifically told **DO NOT USE VAR**. Of course, i avoided var like the plague, but never really looked too deeply as to the *why*, and the reasons go much further into how Javascript interprets variable declarations made by these keywords.

If you're on the Javascript track, then you already know how Javascript works. It runs through our code once, combing the code for declarations within the variables scope and allocates memory for that variable. This is important, especially with var, as it doesnt alter or literally move the code, simply sets its default value to *undefined*. It is these declarations that are then hoisted. One thing to take note of is this is true **only** for declarations, not initializations. Now, this is where our three amigos, var, let and const come in. 

![](https://media.giphy.com/media/sY1yvrxROgCM8/giphy.gif)

# Var

Used easily enough to declare variables and just like our other keywords it has global and local scope. Granted you're within the scope to do so, variables declared with var can be re-declared 
```
var greeting = "Hey how's it goin"
var greeting = "What's the dealio"
```
and updated
```
var greeting = "Hey how's it goin"
greeting = "What's the dealio"
```
As discussed earlier, declaring variables with var will cause Javascript to hoist up any declarations to the top of its current scope. Meaning that this code
```
function some(){
  console.log(x)
  var x = 3
}
```
is interpreted like this
```
function some(){
  var x
  console.log(x)
  x = 3
}
```
But beware, because unlike its brothers (or sisters), it doesn't have block scope, meaning it's not bound by curly brackets, whether it be from an if statement, or for statement. So if for some reason have variables with the same names, this could have unintended consequences, especially once your code start getting larger and more complex.

Lucky for us, there's something better, a dynamic duo which DOES have block scope. You guessed it....

![](https://media.giphy.com/media/DKznWTry3u9Q4/giphy.gif)

let and const! 

# let
Let is the preferred method for variable declaration as it **does** have block scope. Blocks are anything within these handy dandy brakcets {}, so variables declared in a block are only available for use within that block. While var will allow these changes to take place, let will keep things in their lane, so to speak.
```
var x = 5
console.log(x)  // logs 5

{
  var x = 3
  console.log(x) // logs 3
}

console.log(x) // logs 3
```
The value of x is changed, because var lacks discipline....or rather, it lacks block scope. Here we see the same example, but with the power of let!
```
let x = 5
console.log(x)  // logs 5

{
  let x = 3
  console.log(x) // logs 3
}

console.log(x) // logs 5
```
Because the re-assignment of x happens within a block, the actual value of x is not changed. Also, let won't allow for the re-assignment of variables in the same scope, while our var example with the greeting variable above worked no problem, doing this with let? Not a chance. Let realizes that a variable has already been declared with the same name, so even if you attempt to change a var variable with let, well, to put it simply...

![](https://78.media.tumblr.com/b5f616a2b3a24d436da9f552b7fd23b1/tumblr_mqv3dkTiU91rdrzfmo1_250.gif)

# const
A good way to remember this one, is, well, constant = const. This keyword has the same synatx as both let and var, with the same lifecycle as let. However, because these are treated as constants, they **cannot** be re-assigned values after being defined. Because of this, every const variable must be initialized at the time of declaration. Event if you were to try and change a const variable, you'd get "Assignment to constant variable" errors.

There is ONE acception to this rule, and that's that the objects *properties* can be changed! 

```
const blog = {
  name: "Dennis"
	posts: 5
}

//This works!
blog.posts = 8
blog.name = "Caesar"
```

This is because we're altering what blog *contains* not what it's bound to!

![](https://media.giphy.com/media/12luQDyqvum5l6/giphy.gif)

# Arrow functions
Clean, sleak, some might even say....sexy. The arrow function wasn't present when i last was trying to learn Javascript, but boy does it make things prettier. 

Arrow functions are a shorthand way to create functions without the function keyword prefix. So why use them? Well for one, shorter syntax and better readability! Let's take a look below.

```
const array = [
{name: "Harry Potter", type: "book"},
{name: "Interstellar", type: "movie"},
{name: "1985", type: "book"},
{name: "Sin City", type: "book"},
{name: "Avengers", type: "movie"}
]

//Get all objects of type movie

const movies = array.filter(function(event){
   return event.type === "movie"
	 })
```
This works, and does exactly what it's supposed to do. Now we have a variable "movies" that has all objects of type movie, but let's refactor this using arrow functions.
```
const movies = array.filter(event => event.type === "movie")
```
Wow, and this code does the exact same thing.

![](https://media.tenor.com/images/71d8713dc41782d5c96edd7d0079e8e0/tenor.gif)

Let's dissect what we've just seen. Right off the bat, we notice there's no function keyword, already shaving off a few pounds there. So we start our function with the argument, followed by an arrow =>. Since our example is a single statement of code, we can also remove our return keyword, as it will be returned implicitly! This allows us to shave off return, and the brackets. Now we're simply left with the logic, we want the objects of type movie, and that's all we need. As long as the code is a single statement, no complex logic or variable declarations ect., we can trim a lot of fat. If your code will have multiple lines, curly brackets should remain. Of course, you'll run into situations where you have more than one argument, or perhaps no argument at all! These can be handled like this.
```
// No argument
() => code 

//More than one argument 
(arg1, arg2) => code
```
When it comes to arrow functions, i personally like to think of it like this:
Use the function keyword in the global scope and for Object.prototype properties
Use class for constructing objects
Use => functions everywhere else!

I hope if anyone reads this it's helpful in one way or another. Blasting off.
![](https://vignette.wikia.nocookie.net/fairytailfanon/images/c/c7/Blasting_off_again%21.gif/revision/latest?cb=20151031005831)
