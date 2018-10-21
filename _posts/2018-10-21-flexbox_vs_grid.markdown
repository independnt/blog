---
layout: post
title:      "Flexbox vs Grid"
date:       2018-10-21 19:02:23 +0000
permalink:  flexbox_vs_grid
---

The unmitigated rage i'm feeling at this very moment is almost incomprehensible, mainly because all of the work that had gone into this blog had dissapeared. I had written an in depth analysis of the reasons for using flexbox, vs grid, the reasons to use either or, and an example of each, using a simple div to create a row in html. However, for some reasons, which i do not understand, after the tab was closed, the work wasn't saved. The draft was gone, and here i am, hopeless, upset, angry, and not wanting to reiterate everything i had written, but the only positive i can think of, is that this blog's main purpose is for me to learn. So in the process of writing, and researching and coding, i have learned a bit more about each of these technologies. Suffice to say, the purpose of the blog writing, as been fullfilled. So without further adue ado, here i go again, in spark notes fashion. 

 ### when to use either or
 
 In times when you're wanting to create a one dimensional design, flexbox is the way to go, however if trying to implement a two dimensional design, grid is the optimal option. But what exactly does that mean? It means that when you're trying to create something with a single row, flexbox is great, but if you're attempting to use multiple rows and columns, then grid is the best way to go. Examples below!
 
 ## Flexbox
 
 Creating a div with the class of Nav, (even though navbar should be used, but for the purposes of this blog, we're creating something custom) we can create a row, very easily:
 
```
<div class="nav">
 <div>logo</div>
 <div>home</div>
 <div>signup</div>
 <div>login</div>
</div>

#CSS

.nav {
 display: flexbox;
 }
```

automatically, this will give us a row, and if we want the logo on left, and the others on right, we can implement:

```
.nav > div:nth-child(4){
 margin-left: auto
}
```

this will bring all our items to the right, which is great, also, we can utelize any of the flexbox commands to get this same result. Using any of these:

flex-start: Items aligned at the left end of div.
flex-end: Items aligned to the right end of a div.
center: Items aligned at center.
space-between: Items displayed with equal space between.
space-around: Items displayed with equal space around them.

perfect, let's look at how to achieve this with grid

```
.nav {
 display: grid;
 grid-template-columns: repeat(8, 1fr)
```

Here, we're creating 8 columns, each a fraction of space on the row, and to achieve the same result as above, we'll do:

```
.nav > div:nth-child(4){
 grid-column: 8
}
```

This places the 4th item to the very last column we have available. Great, we can also achieve this in a less sexy way, like so:

```
.nav{
 display: grid;
 grid-template-columns: 180px 100px 100px auto auto auto auto 100px;
}
```

Much less appealing, also for each auto in there, we'd have to enter a div to take the place of the space. and we'd have to put the items in the order we want them to appear in the row, meaning login would actually have to come after all those empty div's, gross. I would dive deeper, but my soul is still crushed from all my lost previous writing. Until next week. 



