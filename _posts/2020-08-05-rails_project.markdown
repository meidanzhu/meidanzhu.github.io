---
layout: post
title:      "Rails Project"
date:       2020-08-05 20:51:13 +0000
permalink:  rails_project
---


This project was inspired by my interest in photography. I thought of creating my own image storing website for users who are photographers. They can upload their own images or view the images owned by others. I used Adode XD to create a [wireframe](https://ibb.co/ph10tdS) of how I would like the application to look like. 

Throughout this project, it is very important to set up the correct assocations. In Rails, an association is a connection between two Active Record models. The assocation I used is belongs_to, has_many, and has_many :through. 
* A belongs_to association sets up a one-to-one connection with another model, such that each instance of the declaring model "belongs to" one instance of the other model. 
* A has_many association indicates a one-to-many connection with another model. 
* A has_many :through association is often used to set up a many-to-many connection with another model. This association indicates that the declaring model can be matched with zero or more instances of another model by proceeding through a third model.

Next is to create the sessions controller for logging in and signing up the user. Omniauth was the newest topic and something that I see in many websites who uses different providers to sign in. OmniAuth is a Ruby authentication framework aimed to abstract away the difficulties of working with various types of authentication providers. It is meant to be hooked up to just about any system, from social networks to enterprise systems to simple username and password authentication.

In this project, I was able to use Active Store. Here, I am just storing it to my local disk. Active Storage facilitates uploading files to a cloud storage service like Amazon S3, Google Cloud Storage, or Microsoft Azure Storage and attaching those files to Active Record objects. It comes with a local disk-based service for development and testing and supports mirroring files to subordinate services for backups and migrations. Using Active Storage, an application can transform image uploads with ImageMagick, generate image representations of non-image uploads like PDFs and videos, and extract metadata from arbitrary files.
