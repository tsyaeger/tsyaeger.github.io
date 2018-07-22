---
layout: post
title:      "the followers and the followed: self-joins"
date:       2018-07-21 22:37:10 -0400
permalink:  the_followers_and_the_followed_self-joins
---


For my Sinatra project I chose to build an app that allows users to create and send messages to one another using gifs that they collect from keyword searches. By choosing this type of sender-recipient format, I stumbled upon a type of database relationship that I’d been unaware of-- a "self-join", or a "self-referential" relationship. 

Initially I’d envisioned the app built with four models: User, Recipient, Message, and Gif, but as I mapped out the schema it occurred to me that the Recipient was actually just another User— albeit both a recipient and a User. Fortunately, I was lucky enough to have Dakota steer me in the right direction before things went haywire.

It turns out that there are many scenarios that necessitate this type of arrangement. Any time you use an application like Twitter or Instagram where you can both follow and be followed by other users, the User table will need to look to itself for both ends of the relationship. This is also the case for parent-child relationships, i.e., when two things are of the same essential type and nested hierarchically. 

 I ended up with objects: User, Relationship, Message, and Gif. This is what the User and Relationship models look like right now:

```
class User < ActiveRecord::Base
  has_many :relationships
  has_many :recipients, through: :relationships

  has_many :inverse_relationships, :class_name => "Relationship", :foreign_key => "recipient_id"
  has_many :inverse_recipients, :through => :inverse_relationships, :source => :user

  has_many :messages, through: :relationships
  has_many :gifs, through: :messages
  has_secure_password
end

class Relationship < ActiveRecord::Base
  belongs_to :user
  belongs_to :recipient, class_name: 'User'
  has_many :messages
end
```
Apparently, the self-reference can be implemented without an additional table, but I opted to create an object named Relationship to handle the many-to-many sender-recipient relationships. With the typical has_many relationship the :class_name, :source, and :foreign_key items are implicitly passed, but with the self-referential relationships, you need to explicitly tell the program the instance's object type (:class_name) because there is no object named "inverse_relationship", and where it resides in the table (:foreign_key). In the case of inverse_recipients, which has_many through :inverse_relationships, you have to tell it the instance's associated object type (:souce). 

With the above code you can find a user’s relationships as sender by running: @user.relationships, and as recipient by running @user.inverse_relationships. 

And you can find associated users by running: @user.recipients and @user.inverse_recipients. 

This has served it’s purpose but there is one thing I still need to work out—I’ve as of yet been unable to get @user.inverse_messages to work. Still working on it! Hit me up if you have suggestions.

P.S. this has been very helpful resource: [http://blog.zfeldman.com/2014-07-23-Followings-in-Sinatra/](http://blog.zfeldman.com/2014-07-23-Followings-in-Sinatra/)


