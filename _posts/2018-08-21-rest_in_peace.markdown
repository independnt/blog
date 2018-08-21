---
layout: post
title:      "REST in peace?"
date:       2018-08-21 15:06:25 +0000
permalink:  rest_in_peace
---


I've been hearing a lot about a certain technology called graphQL in the recent weeks. Little whispers about a way to query data in the front end without needing all of these get, post and delete requests, but surely something so convenient couldn't exist could it? 

![](https://i.imgur.com/MWAV5YJ.gif)

After seeing graphQL on a few job applications, i finally came across it in the form of a coding challenge. Forcing me to (somewhat) understand how it works and why it could potentially be the future of querying data. I'm certainly no expert but i've learned quite a bit about graphQL and Apollo Client(allows you to connect your data to your UI).

**Setup**

Honestly, it seems that vs conventional REST, there's a lot more setup involved in utilizing graphQL, but the payoff is pretty outstanding. With graphQL, you can query only the data you want and nothing more. Graphql is all about asking for only the specific data you want on particular objects. Using graphQL is as easy as using the *query* keyword(Not required, but certainly makes it easier to read/debug) followed by the query name, and then the data that you want to retrieve. Like so below!

```
query getDogs {
     dogs {
		      name
					breed
					age
		 }
}
```

pretty simply right? This would in turn return to you a simple response of all dogs, with the requested data, the names, breeds, and ages of each dog. And again, we're the ones requesting the data WE want, so the query above can always be altered to include less, or additional fields of data (granted our GraphQLObjectType includes said fields, but that's for another day). 

**arguments/variables**

Graphql also allows for queries using arguments, say you want a very specific Dog, you can submit a query such as 

```
query myDog{
     dogs(name: "fido"){
		      breed
					favorite-food
		 }
}
```

This query would then return to us the dog who's name matches the argument provided, again, super cool, super fast, very intuitive and responsive. We can also add variables to the mix, this is advantageous when we want our clients to interact with the data. Let's say that we have a dropdown select and we want our clients to be able to select the breed of dogs that THEY want to see. Upon select of the breed, we can input the response into the query below. 

```
query BreedDogs($breed: Breed){
     dogs(breed: $breed){
		      name
					favorite-food
		 }
}
```

It's a little strange at first, but in the above case, $breed would be essentially the variable and the following Breed is the assignment of that variable. Underneath where we request the dogs, we then place the variable next to the argument of breed, thus giving us the requested breed of dog. Also very cool.(spoilers, it's all pretty cool).

**mutations**

mind you i'm talking about the BARE basics here, but i encountered something in graphql called mutations, probably the portion of it that gave me the most trouble. In Graphql, when trying to mutate data (add, remove, edit), you need to implement what's called a mutation. There's a lot of moving parts here which i wont go into detail about, but long story short, you need to have fields not just for your data, but for your queries, and for your mutations, this is what allows you to call upon them in the front end. On top of that, those mutations need to have their own types, so they know what kind of data they are manipultating, this also includes arguments that those mutations need to take in order to make the mutation happen successfully. In the case of creating a dog, the arguments needed would be the dogs name, breed, age and favrotie food/ in the case of deletion, you would need the dogs ID to locate it, ect. I wont be posting code of the mutations because i myself have only scratched the surface, but now that i've started, you can call me a believer, graphql is an amazing technology that's going to reshape the way we query and manipulate data. 

Adios REST. 



