---
layout: post
title:      "Ruby on Rails ecommerce part duex!"
date:       2018-09-30 17:30:19 +0000
permalink:  ruby_on_rails_ecommerce_part_duex
---


We last left off creating a mock ecommerce site, it had all of the necessary models, mapped out the database schema, and finalized all the asssociations necessary. We event created some false data using the *faker* gem. Today i'd like to continue, as we build out the controllers, the views, and instead of just getting things to work, we make our queries a bit more efficient for performance sake. 

The next step for creating my mock ecommerce site was of course, the create our root route, which i would direct to categories. I would also want to create nested routes for each category which pointed to the products that corresponded with the Product Categories join table. Like so.

```
root 'categories#index

resources :categories, only: [:index] do 
 resources :products, only: [:index]
```

At this time, i'll only go so deep as to create indexes for each, perhaps the show route will come in part 3!

Next, i created my Categories Controller, which of course, inherits from ApplicationController. I would define one method, the *index* method. During my time at Flatiron, i was taught that here we could take our data, and insert it into an instance variable of our choosing, which at this time, we can call @categories, and previously, i would have simply done something like this:

```
def index 
 @categories = Category.all
end 

#But in this case, we order them alphabetically so instead, i do 

def index
 @categories = Category.order(:title)
end
```

Great, but notice that i said *previously* would have done this. Why change it? Well, in my views/categories/index.html.erb file, we had this:

```
<h2>Categories (<%= @categories.count%>)</h2>

<ul>
<% @categories.each do |category| %>
  <li>
    
      <%=category.title%>
			(<%=category.products.count%>)

  </li>
<% end %>
</ul>
```

I used our @categories instance to a.) display how many categories are in our category array, and a simple each loop to display the title of each category, while utelizing our join table of product categories to grab the count of products under each category. The wonder of Rails. BUT, while this does work, for each category that gets looped through, we're running a query through the entirety of the product categories join table, which is a huge waste of time. We can do better, and before this, i had no idea, but let's utilize some inner joins and aggregate functions to make this a bit more efficient. 

```
def index
    @categories = Category.joins(:products).select('categories.*, count(products.id) as products_count').group('categories.id').order(:title)
  end
```

Wow. What does all that mean. This is still a little advanced for my level, but what we're doing, is an inner join with the products table, and then creating a custom select (categories.* because we want all the information on our categories) and setting our product.id count as the variable *products_count*. Then grouping them by categories.id, which apparently must be done because this is an aggregate sql function which you can read more about [here](https://en.wikipedia.org/wiki/Aggregate_function). Now, i input this code in my view:

```
<h2>Categories (<%= @categories.length %>)</h2>

<ul>
<% @categories.each do |category| %>
  <li>

    <%= link_to category_products_path(category) do %>
      <%=category.title%>
      (<%=category.products_count%> products)
    <% end %>

  </li>
<% end %>
</ul>
```

Now why did i change .count to .length? To be entirely honest, i'm not sure, but apparently, .count doesn't play well with aggregate functions, i'll have to do some more reading on this, but .length provides the same result as before. Now we have the same information, all display correctly, and now we're only running ONE query, as opposed to many, many more because we are selecting only the information we want. Great! Now we are linking to each individual product, listing how many products per category, but we have no product controller! So that's next on the list.

Once we create the Product Controller, we will add its index method, and because this is going to be a nested route, we need to grab two pieces of information, the category first, and we follow with the list of products. 

```
def index
    @category = Category.find(params[:category_id])
    @products = @category.products.includes(:product_variants).order(:title)
  end
```

Here we grab the @category by the params category_id. We then grab all products associated with that category and we *include* all product_variants, again, we want less queries, not more, so this is again helping us grab only the information we want. Now i create the product view!

```
<h2><%= link_to "Categories", root_path %> / <%= @category.title %> / Products </h2>

<ol>
  <% @products.each do |product| %>
    <li>
      <%= product.title %> (<%= number_to_currency product.price %>)

      <ul>
        <% product.product_variants.each do |variant| %>
          <li><%= variant.title %> (<%= number_to_currency variant.price %>)</li>
        <% end %>
      </ul>
    </li>
    <% end %>
</ol>
```

Here, i'm linking the categories root path, followed by showing the category title. Looping through our products, we show the title, the price, which we use the *number_to_currency* method (god i love rails), and then show all variants for each individual product. We're on our way to having a fully functioning ecommerce site! But of course, every site requires a shopping cart! This is something i'll be expanding on in another blog post. Rails, my long lost love, i remember now why i fell for you to begin with. Thanks for checking in, until next week!




