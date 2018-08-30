---
layout: post
title:      "Learning more about Sass"
date:       2018-08-30 18:42:40 -0400
permalink:  learning_more_about_sass
---


Recently i completed a course specifically on HTML5 and CSS3 teaching me very cool new features from both most recent versions of HTML and CSS. On the HTML side, i learned a lot of new selectors like article, details and section. On the CSS side, things like border-radius, box-shadow, and transform. While i hone my CSS and frontend skills, i've also noticed a lot of job postings requesting proficiency or knowledge of something called Sass. I've heard of it before and worked with it slightly but never really looked into what its advantages were and what it really does. 

Sass stands for Syntactically Awesome Style Sheets. Its a pre-processing stylesheet language that once written, compiles *into* CSS. This allows for us to write code that is both less repetitive using both nesting, and variables. As we know, the less we have to repeat ourselves the better. 

Lets look at nesting for instance. We can write code that looks like this 

```
.description {
 font-family: Arial;
 .title{
  position: absolute;
	text-align: center;
 }
}
```

Which will compile into CSS and look like this 

```
.description{
 font-family: Arial;
}

.description .title {
 position: absolute;
 text-align: center;
}
```

Already we're able to be a little less repetitive. Another thing i've learned is that nesting can be done on multiple levels, we dont need to limit it to simply two elements, we can nest, 3, or 4 deep, which will save us even more space, and still let us clearly see the DOM relationships between selectors. 

We aren't limited to nesting withing only selectors as well, we can also nest properties within CSS. Many of the properties of a box, such as margin, border, or padding all have top, bottom, left and right, so what if we could just nest these into one of those properties? With Sass, instead of writing this

```
.description {
 border-top: 20px;
 border-bottom: 30px;
 border- right: 15px;
}
```

we can instead write this 

```
.description{
 border {
  top: 20px;
	bottom: 20px;
	right: 15px;
 }
}
```

and what about variables? We can also use variables in Sass, which is greatly handy, especially if you've ever worked with several color schemes. Having to write out the color code everytime can be somewhat of a pain, so instead, we can do this 

```
$main-orange: #f26818;
```

Using the $ symbol to preface a variable name is how to assign and call a vairable in Sass. To use this variable, i would simply call upon it like so. 

```
background-color: $main-orange
```

and just like that, i no longer need to look up the code everytime i need to use my main orange color, pretty nifty, and already, we're saving time and space on our code. Keep in mind that assigning variables can be used with multiple data types such a booleans, integers and even strings. there are also two additional data types, lists i.e 8px solid $main-orange (using our variable in a list!) or maps, which look like javascript objects {key: value, key: value}.

Now this all sounds great, and certainly seems like it will save us time on productions, but are there any downsides to using a preprocessor like Sass? While it's crazy convenient, the answer is still yes. 

Preprocessors like Sass are harder to debug. Keep in mind, what your writing needs to be compiled, so what your writing, isnt the final product. When something goes wrong, and usually, something will, the CSS line numbers wont be of assistance to you, because it's not going to match your Sass code. 

We're also losing a little bit of control. Writing straight CSS, you know exactly what your writing, and how it will be used, its the final product after all. But with something like Sass, your files may seem small, but your compiled files could end up being huge, and in terms of performance, that's what matters most. 

Also, i've read that using a preprocessor can be easy to implement, but much harder to remove, shoudl you decide much later on you wish to go on without it. 

I'll continue to practice Sass and play around with both CSS and Sass to see which one is my preference, but best practice would be to just try and master both. I'm off to continue my learnings, adios for now!




