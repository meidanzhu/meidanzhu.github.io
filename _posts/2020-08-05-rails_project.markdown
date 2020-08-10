---
layout: post
title:      "Rails Project - More about Associations"
date:       2020-08-05 16:51:14 -0400
permalink:  rails_project
---


This project was inspired by my interest in photography. I thought of creating my own image storing website for users who are photographers. They can upload their own images or view the images owned by others. I used Adode XD to create a [wireframe](https://ibb.co/ph10tdS) of how I would like the application to look like. 

Throughout this project, it is very important to set up the correct assocations for the database table and columns. In Rails, an association is a connection between Active Record models. The assocation I used is belongs_to, has_many, and has_many :through. 

A **belongs_to** association sets up a one-to-one connection with another model, such that each instance of the declaring model "belongs to" one instance of the other model. 

* Naming convention - must be singular
* Photos associated to user via "user_id" foreign key on photos table. 

* ```
class Photo < ApplicationRecord
    belongs_to :user
    belongs_to :category
end
```

A **has_many** association indicates a one-to-many connection with another model. This association indicates that each instance of the model has zero or more instances of another model.
* Naming convention - plural
* An user can have many photos in this example. From an instance of the User model, you can retrieve a collection of photos: @user.photos
```
class User < ApplicationRecord
     has_many :photo
end
```

A **has_many :through** association is often used to set up a many-to-many connection with another model. This association indicates that the declaring model can be matched with zero or more instances of another model by proceeding through a third model.
* The *Photo* table will have a row with the user_id and category_id columns corresponding to our given user and category. When submitting a form on the browser, the Photo table will have a new row with the correct user_id and group_id values.
* ```
class User < ApplicationRecord
    has_many :photos
    has_many :categories, through: :photos
end
```
```
class Category < ApplicationRecord
    has_many :photos
    has_many :users, through: :photos
end
```
*In a Rails app, the basic belongsto and hasmany relationship is required for the models to access each other.*
* ActiveRecord association also gives us methods based of the assocations. 
- The build method provides the same functionality as .new would, but instantiates with the defined association. For example, @photo.categories.build instantiates a category object that is already associated with @photo. Just like .new, the object has not been saved to the database. 
- Reader and Writer Methods. 
```
association
association=(associate)
```

- The association method returns the associated object, if any. If no associated object is found, it returns nil. 
- The association= method assigns an associated object to this object. Behind the scenes, this means extracting the primary key from the associated object and setting this object's foreign key to the same value.

Creating a **Join Table** - A model that joins two or more objects by storing their foreign keys on its table in the database.
```
create_table "photos", force: :cascade do |t|
    t.string "title"
    t.text "caption"
    t.integer "user_id"
    t.integer "category_id"
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
    t.index ["category_id"], name: "index_photos_on_category_id"
    t.index ["user_id"], name: "index_photos_on_user_id"
  end
```
Once a join is created, it associates the two models by storing each foreign key on the table, allowing both access to multiple instances of each other.

```
 @photo = Photo.find_by_id(4)
 => #<Photo id: 4, title: "Bunny", caption: "Image of cute rabbit", user_id: 2, category_id: 1>
 @photo.title
 => "Bunny" 
 @photo.user
 => #<User id: 2, username: "Mei", password_digest: [FILTERED]>
 @photo.user.username
 => "Mei" 
 @photo.category
 => #<Category id: 1, name: "Animal">
 @photo.category.name
 => "Animal" 
 
@user = @photo.user
 => #<User id: 2, username: "Mei", password_digest: [FILTERED]
 @user.photos
 =>[#<Photo id: 4, title: "Bunny", caption: "Image of cute rabbit", user_id: 2, category_id: 1>,
 #<Photo id: 5, title: "Rose", caption: "Girona’s old town overflows with colourful display...", user_id: 2, category_id: 3>, 
 #<Photo id: 6, title: "Mountain", caption: "Taken before sun rise", user_id: 2, category_id: 2>
```

Next is to create the sessions controller for logging in and signing up the user. Omniauth was the newest topic and something that I see in many websites who uses different providers to sign in. OmniAuth is a Ruby authentication framework aimed to abstract away the difficulties of working with various types of authentication providers. It is meant to be hooked up to just about any system, from social networks to enterprise systems to simple username and password authentication.

In this project, I was able to use Active Store. Here, I am just storing it to my local disk. Active Storage facilitates uploading files to a cloud storage service like Amazon S3, Google Cloud Storage, or Microsoft Azure Storage and attaching those files to Active Record objects. It comes with a local disk-based service for development and testing and supports mirroring files to subordinate services for backups and migrations. Using Active Storage, an application can transform image uploads with ImageMagick, generate image representations of non-image uploads like PDFs and videos, and extract metadata from arbitrary files.
