---
layout: post
title:      "Ruby on Rails ecommerce database associations"
date:       2018-09-21 22:32:51 +0000
permalink:  ruby_on_rails_ecommerce_database_associations
---


The last few weeks i've largely been focused on learning more about javascript and improving my understanding of algorithms and data base structures, which is all good and fine, but never forget where you came from! During the carriculum of FlatIron, a large portion of it was teaching us ruby code, and i'd be lying if i said i wasn't a little rusty. So instead of forging forward, lets go back a few steps and sharpen the original sword we used to enter the forest of the programming world, Rails!

![](https://media.giphy.com/media/b40bIk4Isg7Wo/giphy.gif)

I started with an ecommerce site so i could work on the model associations, because right off the bat, even when i was writing ruby code everyday, this was the hardest part for me, especially once you start exceeding 4 models. Of course depending on what you're making, difficulty will vary, but nevertheless, these are the models i'm working with. 

* Products
* Categories
* Orders 
* Product Categories
* Product Variants
* Order Items

Right off the bat, i had to shake off the rust, use the *rails new* command to create my new rails application and save it to my repository. We're making moves! Next step, was creating my models, which i did using the good ole fashioned rails generator command *rails generate model*, or rails g model. I created all my models with their associated attributes, like so.

```
rails g model Product title description: text price: decimal
```

You'll of course notice that for description and text i named the data type, but by default rails will set the data type to string, which is what i wanted for the title attribute.

Once, all was said and done, i had an entire schema that looked like this:

```
create_table "categories", force: :cascade do |t|
    t.string "title", null: false
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end

  create_table "order_items", force: :cascade do |t|
    t.integer "quantity", default: 0, null: false
    t.decimal "price", precision: 15, scale: 2, null: false
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
    t.bigint "order_id", null: false
    t.index ["order_id"], name: "index_order_items_on_order_id"
  end

  create_table "orders", force: :cascade do |t|
    t.string "first_name"
    t.string "last_name", null: false
    t.decimal "sub_total", precision: 15, scale: 2, null: false
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end

  create_table "product_categories", force: :cascade do |t|
    t.bigint "product_id", null: false
    t.bigint "category_id", null: false
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
    t.index ["category_id"], name: "index_product_categories_on_category_id"
    t.index ["product_id"], name: "index_product_categories_on_product_id"
  end

  create_table "product_variants", force: :cascade do |t|
    t.string "title", null: false
    t.decimal "price", precision: 15, scale: 2, null: false
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
    t.bigint "product_id", null: false
    t.index ["product_id"], name: "index_product_variants_on_product_id"
  end

  create_table "products", force: :cascade do |t|
    t.string "title", null: false
    t.text "description"
    t.decimal "price", precision: 15, scale: 2, null: false
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end
```

You'll also notice after certain attributes i entered *null: false*. This is so that the attribute MUST be included to be input to the database, even from the command line. You also have options like 

```
validates :title, presence: true
```

So what's the difference between that and entering *null: false* in the database directly? If you attempt to create something that has the code above, it won't even attempt to hit the database, so you can catch that exception earlier on. 

From here, i got to create the actual associations. We have a few has_many relationships such as

* Product has_many product_categories (product_categories is our join table!)
* Product has_many categories through product_categories
* Product has_many product_variants
* Order has_many order_items
* Category has_many product_categories 
* Category has_many products through product_categories 

and we also have of course, the belong to's

* Product Category model belongs_to Product and Category
* Order Item belongs_to the Order and Product
* Product Variant model belongs_to the Product 

::Phew:: okay, now that the complex part is out of the way, now we can get to actually building our controllers, and our views. But first we of course want to test that all our associations are working as we expect. This is where i missed rails and i completely forgot how amazing it can be. Being able to jump right into the console with *rails c* and being able to test those associations was a breath of fresh air. 

Now we can actually start to build out our controllers, and our views, but before we do that, especially with something like a store front, it's always a good idea to seed data, and what better way than using the faker gem. Check it out [here](https://github.com/stympy/faker). You can seed almost any kind of data you can imagine, which is way more convenient than having to hand code it yourself. 

I'm going to update on how this project finishes along next week, until then, adios!


