---
layout: post
title:      "Ruby on Rails ecommerce finale"
date:       2018-10-06 00:29:03 +0000
permalink:  ruby_on_rails_ecommerce_finale
---


So the purpose of me going through all of this was essentially to brush up on basics, use a few more advanced techniques with the aggregate sql functions, and learn a little bit about other ruby functions i haven't used before. The last thing that really needs to be done for any ecommerce site to be as basic as can be, is being able to add items to a shopping cart, and displaying those in a shopping cart page to see the list of items we've added. When we last left off, we had added to the product view, showing the items we have, their prices and variants. 

Next thing to do is to add a form to add items to the cart. Although my first thought was "why not just add a button that adds to the cart?", well, we want to not only add an item, but give the ability to add more than 1 item at a time. We also want to use the products id to track what item we're storing in the cart, so we use a form_tag, and a hidden field, along with a number field to get the results we want:

```
<ol>
  <% @products.each do |product| %>
    <li>
      <%= product.title %> (<%= number_to_currency product.price %>)

      <%= form_tag order_items_path do %>
        <%= hidden_field_tag :product_id, product.id %>
        <%= number_field_tag :quantity, 1 %>
        <%= submit_tag "Add to Cart" %>
      <% end %>

      <ul>
        <% product.product_variants.each do |variant| %>
          <li><%= variant.title %> (<%= number_to_currency variant.price %>)</li>
        <% end %>
      </ul>
    </li>
    <% end %>
</ol>
```

I know, the order_items_path doesn't even exist yet, so next is to create that route, which simply put looks like this:

```
get '/cart', to: 'order_items#index'
  resources :order_items, path: '/cart/items'
```

now, our /cart route will respond to the order_items index, and at /cart/items we have the resources for order_items. We're creating routes that are dependent on an order_items controller, so that's the next thing that needs to be created next, ALSO, our form above (order_items_path) is going to post to a create method, as rails does, so that needs to be added first. 

After creating an order_items controller, and create method, the method needs to add to the current cart(usually i would do current_user, but same concept, just instead of users, we have a cart, which will get created momentarily), and we want to include the products ID and the quantity, both of which we get through the params. Finally, we'll just redirect back to the cart to view what we added:

```
def create
    current_cart.add_item(
      product_id: params[:product_id],
      quantity: params[:quantity]
    )

    redirect_to cart_path
  end
```

Next, of course, what is current_cart? This is usually something created in the application controller, you know, the one that all other controllers inherit from. This way, we can access the current cart anywhere we need to! 

In order to create a current cart, two things need to happen, we need to write the method under application controller, and we need to create a ShoppingCart model! Easy enough. Once a Shopping Cart model is created, we'll want to initialize it with something, but what? A token. So we have our Shopping Cart model, that initializes with a token, like so:

```
def initialize(token:)
    @token = token
  end
```

Now we're ready for current cart. We create a current cart method with the or equals operator, so either it returns our current cart, or it creates our current cart.

```
def current_cart
    @current_cart ||= ShoppingCart.new(token: cart_token)
 end
```

Beautiful stuff, but what's cart_token? This is also a method we need to create, also under application controller. As a private method, we write the cart_token, which returns a cart token, if there is no current cart_token, we create it using something new i had never encountered before. *SecureRandom*, this is a random number generator that can be used to generating session keys. You can pair it with things like base64, random number, or a few others. You can read about it [here](https://ruby-doc.org/stdlib-1.9.3/libdoc/securerandom/rdoc/SecureRandom.html). In this case, we use hex, which generates a random hex string, you can give it a length, and if no length is given, 16 is assumed. So this is our cart_token method:

```
def cart_token
    return @cart_token unless @cart_token.nil?

    session[:cart_token] ||= SecureRandom.hex(8)
    @cart_token = session[:cart_token]
  end
```

Also we want to add helper_method :current_cart, so that we can have access to this where we need it in the controllers. Now to make sure that our orders are tied specifically to the cart or token, we created. We'll create an order method, which either returns our order, or creates one with the @token the shopping cart is initialized with, like so:

```
def order
    @order ||= Order.find_or_create_by(token: @token) do |order|
      order.sub_total = 0
    end
  end
```

either we get our order back, or we create a new one with the 0 subtotal. Lastly, we need a method to add items. How about add_item, sounds good, since that's what we used in the order items controller. This will take the param information from the form_tag and put it to work. 

```
def add_item(product_id:, quantity: 1)
    product = Product.find(product_id)

    order_item = order.order_items.find_or_initialize_by(product_id: product_id)

    order_item.price = product.price
    order_item.quantity = quantity

    order_item.save
  end
```

So we find the product based on it's ID, we find the product in the order if it exists, and if not, we create it within our order_item table. We set the price and quantity equal to the data found from our params or arguments, and we save our order_item. This should do it, now just to create the index in the order_items controller and then the view. 

```
def index
    @items = current_cart.order.order_items
  end
```

Here we used the order method from our Shopping Cart model (remember current cart is an instance of the model) and our order table has many order_items, so we grab the order_items associated with that order to our @items instance. Now we're ready to display everything in our cart however we like. That's all for rails for a bit, next week it's time to dive back into some react.js!



