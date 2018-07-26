---
layout: post
title:      "Deploying to Heroku using buildpacks with 3rd Party API's"
date:       2018-07-26 21:31:08 +0000
permalink:  deploying_to_heroku_using_buildpacks_with_3rd_party_apis
---


I want to preface this with one note. **Make all your 3rd party API calls in the backend, for the love of god.**

Anyways, 

Before starting Flatiron school, i very much literally would not have understood a word in this title. So self five for learning 

![](https://media.giphy.com/media/cJgkhpLgsuTkY/giphy.gif)

My project is called Brew-View and for anyone who's curious, check it out here: http://brew-view.herokuapp.com/ 
It's a beer/brewery finder using an API called the Beer Mapping Project, which between you and i is actually quite unreliable. Please bear with me for any bugs that you find while i search for another API to use, its 100% issues with the API i promise. 

Anyways, when i decided to deploy my project to Heroku, I knew it would come with its headaches, but boy i wasn't ready for what i encountered. Instead of deploying two applications to heroku, much like some had advised me to do, i decided to use heroku buildpacks and end up with a Rails server that handles both front and back end. I also had heard this helps with performance.

First things, first, while in my rails project, i needed to run npm init. Heroku will recognize an application as node.js if it sees a package.json file, which npm init created for me. All in all, it created a package.json with more information than i needed, so ultimately, i ended with this 

```
{
  "name": "brewview",
  "engines": {
    "node": "6.3.1",
    "npm": "5.6.0"
  },
  "scripts": {
    "build": "cd client && npm install && npm run build && cd ..",
    "deploy": "cp -a client/build/. public/",
    "postinstall": "npm run build && npm run deploy && echo 'Client built!'"
  }
}
```

Long story short (and to the best of my knowledge), this instructs Heroku how to start the application. By first cd-ing into my client folder, running npm install, and ultimately building my client frontend. It seems to have copied all of my client code into a public/static folder. This also held true for any commits i made going forward. Any changes made to my react app was also updated in public/static as well. 

Once i created my Heroku app using 
```
heroku create brew-view
```
I was then able to use the build packs, which per the heroku documentation, transform deployed code into a slug (compressed and pre-packaged copies of the app code), to then be executed on a heroku dyno (containers that hold the code and dependencies). These dynos execute on user specified commands(our package.json file!). After executing this:

```
heroku buildpacks:add heroku/nodejs --index 1
heroku buildpacks:add heroku/ruby --index 2
```

This told heroku to build the node.js app per my package.json file and then the rails server. After updating my Procfile with `web: bundle exec rails s` , I was in business!.....or so i thought.

The problem i ran into? Well, once i deployed my application to heroku with `git push heroku master`, everything seemed to work just fine, except for one HUGE problem. My application is largely reliant on a third party API (remember that?) and in order to make proper API calls, i needed my API key, which originally i had stored in a .env file using 'dotenv' library. However, this only works for development, not production (heroku and dotenv with react dont play well together). 

So heroku has something called config vars! Essentially environmental variables that you can access, should you need them. I quickly added my API key through the heroku dashboard, followed the documentation and used process.env.Apikey(the proper way to call an environmental variable in react) and still got the same error from before, which was something along the lines of "cross origin access denied" (this was not the actual error, i forget what it was). Essentially telling me that the web page i was trying to call was forbidding information to be sent to heroku servers, which devastated me. Would i have to re-build my entire project? No, there had to be another way. 

I came to notice that in local environment, my calls worked just fine, but when the API key wasn't present, i got the same exact error i got in production. The error was occuring not because of CORS, as i originally thought, but with the lack of API key. It turns out, that if you built an application like mine, and it relies on a 3rd party API, make sure that your API calls happen IN THE BACKEND. Save yourself the grief. Sure, there are ways around it, but it will be less trouble for you if you just do this in the beginning. 

As it turns out, my application could not access the environmental variables declared in the heroku dash, only my rails backend could. So i had to completely remove the way i was making API calls, via fetch in react, and instead, ended up making fetch calls for my backend, and had my backend make the API call in order to pass the data to redux to be rendered in react, like so.

```
class Api::SearchController < ApplicationController
  require 'rest-client'
  require 'uri'

  def get_state_info
    apiKey = ENV['BEERDB_KEY']
    state = params[:state]
    url = 'https://beermapping.com/webservice/locstate/' + apiKey + '/' + state + '&s=json'
    if response = RestClient.get(url)
      render json: response
    else
      render json: {message: "Sorry, something went wrong with the API, refresh and try again!"}
    end
  end
```

This was a huge learning experience and believe me, i will never forget. In the moments that you're bashing your head into the desk, you're actually hammering home the mistakes you'll never make again.

But now, my application works just fine, albiet some issues with the API. Now to just get my next project to heroku....

