---
layout: post
title:      "Portfolio page on Github Pages"
date:       2018-08-10 20:47:02 +0000
permalink:  portfolio_page_on_github_pages
---


One of the most important things in setting yourself apart in any type of situation is your personality, what makes you who you are as a person, and this is where a portfolio page is crucial. 

Perhaps i'm wrong, but your portfolio page in my eyes shouldn't just be what technologies you know and where you went to school, that's what a resume is for. A portfolio page is your oppertunity to show first hand what you can design, how you can make it and more importantly, who you are. This is the oppertunity to give a glimpse into the personality you bring with you, perhaps some of your character, because let's face it, every developer is going to have a resume and portfolio, and any developer can know CSS, or HTML or javascript, but setting yourself apart starts with you. 

With that thought in mind, i wanted to launch a portfolio page with a personal domain from goDaddy.com, and one of the best solutions to this that i've found is github pages because it's free, it's easy and it's free. Emphasis on free. 

Trust me, the naming of your domain will be the most difficult part, especially if you're like me and you have a famous jazz musician hogging up all the pages available (i'm looking at you dennis the trumpet player). I ended up with[](dennis-emmanuel.com), check it out! So lets launch our page, with or without a custom domain.

**NON-CUSTOM**

Okay! So we don't care about custom domains or any of that nonsense, we just want to get our page out there in the open web for people to see so they can talk about how great we are and how much they'd love to hire us on their team! Visit the repository page of the project that you wish to launch and click on the settings button on the top right hand side of your repo page.

Scroll down to the section that will read "GitHub Pages". Under the first option "source", select "master branch" or whichever branch of your project you wish to launch, most likely the master. You can add a theme if you haven't styled it too much, which you can learn more about [here](https://help.github.com/articles/adding-a-jekyll-theme-to-your-github-pages-site-with-the-jekyll-theme-chooser/). Make sure to have the Enforce HTTPS option checked off for added security, and once you're done, hit "save" next to source and BAM! instant website. Github will compile and launch your site at a certain domain which it will provide to you. Super easy, super fast, super convenient. 

**CUSTOM**

Now if you've purchased a custom domain like i did from GoDaddy, you need a bit more work. First thing's first, log into your GoDaddy account and click on the "DNS" button next to your domain. Here you should see a few lines of information under a section that reads "RECORDS". You should also see one line that has a column of "type" and it will be marked "A". Click the edit icon on this where it reads "Points to", you'll want to include this IP address below:
*185.199.108.153*

This IP address will point your "A" record to the GitHub Servers. You'll now need to add additional "A" records. So under your "Records" click "Add" and create three more "A" records, pointing to the following IP Adresses:
*185.199.109.153
185.199.110.153
185.199.111.153*

Once that's done, create a CNAME file in the root of your program and include in there the domain name exactly as it was purchased. For example, mine simply has `dennis-emmanuel.com`. Not prefixed with www, or http or anything like that.

Finally, use the steps listed for the non-custom domain. Click your settings, scroll to github pages, select your branch, and under "custom domain" enter the domain you wish to use (the one in your CNAME file), and hit save. Then presto! Your page should be compiled and available shortly, granted there are no syntax issues or code problems. 

If you do happen to have any problems, check [here](https://help.github.com/articles/troubleshooting-custom-domains/).

Best of luck!
