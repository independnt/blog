---
layout: post
title:      "Rails and Javascript, sitting in a tree"
date:       2018-05-22 19:22:21 +0000
permalink:  rails_and_javascript_sitting_in_a_tree
---


I'd been here before. A situation that was foreign yet familiar all at the same time. Profusely overthinking every detail of the coming project, all the while feeling somewhat inadequete and shorthanded. Armed with only my knowledge, my keyboard, and way too many coke zero's, i jumped into my rails project, only this time, i was building upon the foundation of my own rails project. 

I would be lying if i said i felt completely ready for this project, but then again, we seldom are, or at least, we seldom feel like it. As i stumbled through old lessons, lectures and stackoverflow pages, i learned many things, very quickly. 

Try to get a return from an asynchronous call inside a synchronous method? Nope. Changing a POST request link by simply changing its action? Wrong. I really could go on and on here. I stumbled and fell more times then i care to remember. Everytime getting frustrated, but never making the same mistake twice, and if ever, usually correcting myself very quickly. 

The most difficulty i had here was the "next" button i wanted to create to siphon through a users projects. Sounds easy right? That's what i thought, until i realized how many links changed, how many controller paths and POST requests were different page to page. And once i added a comments feature, getting the correct comments to appear on each page. Little by little, i chipped away at the changes, first the html of the title, then the attr actions, serializing the post requests so that i would carry over authenticity tokens, ect. and the worst part? That my projects werent in order. I couldn't simply tell my ajax GET requests the URL and ID +1. I had to find a way to get all project ID's, and cycle through them correctly. The code which ive included below. 
```
function nextProjectListener(){
  let allProjects = []
  let currentId = parseInt($(".js-next").attr("data-uid"))

  //get all project Id's for the current user
  $.get("/users/" + currentId + ".json").done(resp => {
    resp["projects"].forEach(function(project){
      allProjects.push(project.id)
    })
  })

  $(".js-next").on('click', () => {
    let projectId = parseInt($(".js-next").attr("data-id"))
    let currentIndex = allProjects.indexOf(projectId)
    let nextIndex = currentIndex + 1
    let next = projectId

    if(allProjects.length === 1){
      alert("This user only has one project")
    }else if(nextIndex === allProjects.length){
      next = allProjects[0]
    }else{
      next = allProjects[nextIndex]
    }

    let nextURL = `/users/${currentId}/projects/${next}.json`
```


Now there's more to it, but this took me much longer than i'd like to admit. 

Here i am, roughly 87 coke zero's later, completing everything i set out to, but consistently thinking about additional changes to make. 

On the verge of the final sections, i can see the light at the end of the tunnel, but really, its still only the beginning. 

Onward to REACT!
