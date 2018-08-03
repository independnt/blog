---
layout: post
title:      "CSS box model and making it easier to work with"
date:       2018-08-03 16:01:42 +0000
permalink:  css_box_model_and_making_it_easier_to_work_with
---


This week has been largley focused on improving my CSS3 ability and learning everything CSS3 has to offer. New and powerful tools like transform, transitions, border images, but most importantly **box sizing**.

Long i've been told that the biggest headache for CSS is the box model, and boy were they right. Working with the box model is like making a balloon animal on a unicycle while trying not to burn your omelette. What i mean by that is that you're so focused on getting one element to be exactly how you want it, and then realizing that it has affected something else around it (omelette burned). But luckily, i've been taking a CSS course on Udemy thats really alleviated those strains. Thanks Udemy!

![](https://media.giphy.com/media/111ebonMs90YLu/200.gif)

Let's start with what we already know, the box model. This beautiful and majestic monster that haunts our nightmares when designing our work. 

![](https://www.washington.edu/accesscomputing/webd2/student/unit3/images/boxmodel.gif)

All HTML elements can be looked at as boxes, all consisting of the content, the padding(space inside in the box between the content and the border). The border goes around the padding and the content. Finally the margin, is the space between boxes. Now the annoying thing about the box model is that when we set our content, we generally change the height and width of the content bringing it to our desired size, but the real headache is realizing that height and width are setting the size for the content itself, **not** the entire box model, meaning that on top of your desired height and width, you're getting additional margin on the outside that you do not want, which is usually what causes issues down the line. 

BOX SIZING TO THE RESCUE

![](https://media3.giphy.com/media/vgSJqTTWV7tC0/giphy.gif)

Anytime i begin a CSS project going forward, i will always pre-face my CSS with the following

```
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
```

Using the * to indicate all elements, setting margin and padding to 0 by default, and finally, setting the box-sizing element, to border-box. The box sizing property indicates that the user will decide how to calculate the total height and width of an element. Setting this property to border-box will make sure that width and height properties will be calculated to the content, padding and border, making elements easier to size and having less undesired side effects. Setting the margin and padding to 0 will also ensure no unwanted spaces are added to any element. 

Going forward after this, you can then set your desired heights, widths, paddings, and margins manually to get your exact desired placements, and outcomes. This has been immensley helpful in the design of my portfolio and i hope it helps you too! Happy Designing!

