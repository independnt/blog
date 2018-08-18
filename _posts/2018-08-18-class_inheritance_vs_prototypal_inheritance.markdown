---
layout: post
title:      "Class Inheritance vs Prototypal Inheritance"
date:       2018-08-18 23:06:30 +0000
permalink:  class_inheritance_vs_prototypal_inheritance
---


This question has been asked in interview after interview in every conveivable universe or parallel dimension for any position that has to do with Javascript dev. I know i was asked in my mock technical interview and while i definitely knew what class inheritance was, i wasn't so sure on how to describe what prototypal inheritance was. I have a feeling this is a topic that a lot of people, including myself, will struggle to understand, let alone explain. Let's learn together, follow MEEEEE

![](https://uproxx.files.wordpress.com/2015/08/rick-morty-tinkles.gif?w=650)

**Class Inheritance**

Full disclaimer, this discussion will be looking at classes as they operate specifically in Javascript. Technically speaking, Javascript has no classes. Sure it has a *class* keyword, but that doesnt mean that they are classes in the traditional sense of other programming languages. Normally, in OOP, a class is a blueprint, as i've heard so many people put it, or as i like to call it, a factory. This factory can create instances of itself. So a **Person** class can create instances of people i.e ("jane", "margaret", "james" ect..). These people will all inherit the traits of the factory that created them. So an instance of a person, will have all the methods and attributes of the Person class. 

You can also have something called, subclasses. These are classes that inherit from their parent class (class inheritance!). So for instance, a student. A student is still a person, albiet a very stressed out person, but a person none the less! So if a Person class has methods to retrieve a name, a gender, or age, then a Student class should be able to do so as well! This creates a parent child heirarchy relationship. Things work a little differently in Javascript.

**Prototypal Inheritance**

Javascript, while being an Object Oriented Language has something called prototypal inheritance. All Objects in Javascript have a prototype property, everything from Arrays, to functions, to classes like the Person class we created above (for obvious reasons, don't mess around with prototypes on things like Arrays, things could get crazy). 

Now if we create a class in Javascript, like lets say, a Person. Any methods or properties we want our instances of a Person to inherit, we need to attach to the prototype of the parent, in this case **Person**. 

```
var Person = function(name, age, gender){
     this.name = name
		 this.age = age
		 this.gender = gender
}
```

Now we have a person constructor! Now we can create instances of person like so 

```
var denzel = new Person("Denzel", 26, "male")
```

Now the object denzel, inherits all the functionality of the Person class. But let's say we want to add functionality to the Person class, maybe a greet function? We can simply call 

```
Person.prototype.greet = function(){
     console.log(`${this.name} says hi there!`)
}
```

Now all instances of person will have access to the greet function, even though it's not in the constructor! the greet function is attached to the prototype of the constructor, which is inherited by all of its children, in this case, all the instances of people. Super cool.

**Conclusion**

Keep in mind, i'm still not 100% on all of the aspects that make these two different, but i do know how prototypal inheritance works, and how powerful it can be! I'll be sure to revisit this topic in a few weeks to try and flesh it out even more, as i hear its a pretty hefty topic. Ttyl.

