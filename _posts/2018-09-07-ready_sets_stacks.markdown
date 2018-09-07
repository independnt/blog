---
layout: post
title:      "Ready? Sets. Stacks."
date:       2018-09-07 17:34:26 +0000
permalink:  ready_sets_stacks
---


Throughout the FlatIron Schools full stack web development track, they introduced us to several kinds of basic data structures, such as arrays, and objects which can contain many values i.e. 

```
var car = {name: "toyota", make: 1998}
```

However, beyond this are a wide variety of other data strcutures that can be used for various different reasons, some of the main ones i've recently been looking into are sets, stacks, queues, data trees, and linked lists. Let's go over a few of these to see what they do, how to differentiate them, and what they can be used for. 

**Sets**

A data set is quite simply a collection of related data, and in Javascript, it looks like an array except for two key changes. 

1. the values is presented in no particular order, this is important to know because if order is important, than a data set is probably not the best data structure for what you're trying to accomplish

2. There are no duplicates! Sets are comprised of completely unique data, so if you're wanting to keep track of something but want no duplicates, then Sets would be a good place to start. 

ES6 actually comes with a built in Set object, so creating a Set is as easy as 

```
var thisSet = new Set();
```

which when called will output 

```
Set(0) {}
```

Easy as 1,2,3. ES6 has pre-built in functions for Sets that you can use such as add() to add data, or to delete, simply use the .delete() function. You can also entirely clear a Set using the .clear() function. 

Keep in mind, if you ever have an array of objects, you can convert the array into a Set should you want only unique items, like so. 

```
var newArr = [1,2,3,4,5,5,5,6,6,7]

var mySet = new Set(newArr);

mySet
//ouput//
Set(7) {1, 2, 3, 4, 5, 6, 7}
```

Pretty nifty.

**Stacks**

When thinking about stacks, think about the physical implementation of stacking an object on top of one another. The last item places on the stack, is at the forefront of the structure. Thus, if you were to begin taking the stack down, you would start from the top down. That is the idea behind Stacks, it's a last in, first out data structure. Or first in, last out, whatever helps you remember better! 

Because of how it works, these are the Javascript functions that work for a stack: 
.pop(), .length(), .push(), and .peek()(gives you the top value in the stack). Keep in mind, all of these are built into ES6 except for peek() which must be added by extending the JS array prototype, or create your own like this

```
var peek = newArr[newArr.length - 1];
```

Stacks can be implemented as an Array, simple as that!

**Queues**

If you look at a Stack and think of last in, first out, then you can look at a Queue in the opposite way, think of it as a first in, first out. You can think of this as a phone queue, when calling a customer service line. First person in line, is the first person taken care of and discarded!

to give an example, you can create a Queue like so 

```
function Queue(){
 let line = []
 this.print = function() {
  console.log(line)
 };
 this.addQueue = function(data){
  line.push(data);
 }
 this.removeQueue = function(data){
  return line.shift();
 }
}
```

This gives all the qualities of a queue. When adding an item, it gets added to the line, and when you remove an item, it's always the first item that gets removed. 

There are a lot more data structures types to go through and for my next blog post i'll probably go into the binary search tree's, linked lists, and hash tables. 

Adios!




