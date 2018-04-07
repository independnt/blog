---
layout: post
title:      "Ruby on Rails sets sails"
date:       2018-04-07 20:43:14 +0000
permalink:  ruby_on_rails_sets_sails
---

What began as a small idea about users with projects and categories, very quickly took off into a mind boggling journey into multiple join tables, nested forms and collection_check_boxes. All concepts i was not particulary strong in, but that's why we do these right? To challenge ourselves? To learn?

I can still hear myself screaming about simply trying to get my databases to work the way i wanted in console. While it started small, i ended with this. 

```
create_table "backed_projects", force: :cascade do |t|
    t.integer "user_id"
    t.integer "project_id"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end

  create_table "categories", force: :cascade do |t|
    t.string "name"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end

  create_table "project_categories", force: :cascade do |t|
    t.integer "category_id"
    t.integer "project_id"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end

  create_table "projects", force: :cascade do |t|
    t.string "name"
    t.text "description"
    t.string "category"
    t.string "city"
    t.string "state"
    t.integer "user_id"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
    t.boolean "active", default: false
  end

  create_table "users", force: :cascade do |t|
    t.string "username"
    t.string "password_digest"
    t.string "email"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
    t.string "phone_number"
  end
```

Not exactly what i had in mind when i started. But as the project evolved and grew, i kept thinking of new additions, new features i wanted to implement. 

I loved this project not just because it made me work with aspects of ruby and rails that i wasnt great with, but because its something i will continue to build long after this is over. I'll always be able to look back at how uncertain i was at the beginning, and hopefully how great it will be in the end. 

You may have defeated me before nested forms and resources, but NOT TODAY.
The content of your blog post goes here.
