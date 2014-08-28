---
layout: post
title: Using gravatar avatars in Rails applications
category: ruby on rails
---

Most of the rails apps I've done lately come with the requirement to include the picture (avatar) of the
user that is signed in.  Here is an small example of an app I delivered last week:

![Alt text](/images/gravatar-example.png)

This problem can be solved the hard way implemnting the functionality for uploading, managing and rendering the images
and associating them to the app users (and if you are using heroku, good luck with their restrictive file system), 
or you can delegate this problem to [Gravatar](http://gravatar.com).  Gravatar was conceived to be the place where 
you put once the avatar you want to be recognized for, and any web app can use to render the user picture.

If you don't have your gravatar, its very easy to sign up with a valid email, and manage the avatar you want to use to
be recognized.  Several popular services like [Github](http://github.com) uses gravatar. Once the account is created,
gravatar will identify the user with the email.

To render a gravatar picture in a rails app is very easy.  Just follow these steps.

- Include the gravastic gem in your Gemfile 

    gem 'gravtastic'

and run
  
    bundle install
    
- Now, you need a model to represent a user in your system.  Lets suppose that in our example, the user is represented
by the model class User, and lets asume that this class has an attribute 'email' (remember that Gravatar identifies an user
by his email).

    class User < ActiveRecord::Base
        ...
        # Include these 2 lines
        include Gravtastic
        gravtastic
        ...
    end
    
- To render a gravatar avatar in a page, just go to your view and use the traditional image_tag helper passing as an argument
the gravatar url for the user:

    <!-- Assuming @user was instantiated in the controller properly -->
    <%= image_tag @user.gravatar_url %>    

And that's it. As always, you can go directly to the [source](https://github.com/chrislloyd/gravtastic) for more options offered by this gem.


