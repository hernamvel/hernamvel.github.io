---
layout: post
title: Learning rmagick drawing the Colombian flag
category: ruby
---


This is a very short post to show how to use ruby to generate png dynamic images programatically. For this purpose, I will use one of the most popular gems in ruby called rmagick.

[Rmagick](https://github.com/rmagick/rmagick) is a ruby gem that serves as an interface withe the [imagemagick](http://www.imagemagick.org/) drawing utility.  You can dig in the links provided to learn more about this program.

The example is very simple: To draw the flag of my home country, Colombia:

![Alt text](/images/colombia.png)

Before starting, be sure you have rmagick installed in your gemset:

    gem install rmagick
    
For this example, note that the Colombian flag has 3 rectangles: A yellow one (that means the country's wealth),
the blue one (that means the oceans that sorrounds the country) and the red one (that honors the bloods of the
soldiers that liberated our county on the 19th century).

So this is the program:

    require 'RMagick'
    include Magick
    
    width = 1000
    height = 500     
    image = Image.new(width,height)
    gc = Magick::Draw.new
    gc.fill('yellow')
    gc.rectangle(0, 0, width, height * 0.5)
    gc.fill('blue')
    gc.rectangle(0, height * 0.5, width, height * 0.75)
    gc.fill('red')
    gc.rectangle(0, height * 0.75, width, height)
    gc.draw(image)
    image.write('colombia.png')
    
In short words, image is an object representing a 1000x500 (for this example) image, and gc is the canvas when you can write
the drawing instructions. The canvas has a lot of methods to draw lines, polyongs, circles, etc. but for the flag we only
need to draw 3 rectangles:

    # The yellow rectangle
    gc.fill('yellow')
    gc.rectangle(0, 0, width, height * 0.5)
    # The blue rectangle
    gc.fill('blue')
    gc.rectangle(0, height * 0.5, width, height * 0.75)
    # The red rectangle
    gc.fill('red')
  
At the end, you have to associate the canvas to the image:

    gc.draw(image)

And if you want to generate a png file for the drawing, just use:

    image.write('colombia.png')

In the context of a web app, for example in rails, you can send the image to the browser using something like:

    format.png do
        send_data image.to_blob, :filename => 'colombia.png',
            :disposition => 'inline',
            :type => 'image/png'
    end
    
IF you want to see more flags in action, I'm maintaining this open source project (just for fun):

[magick_flags](https://github.com/hernamvel/magick_flags)

You are very welcome to contribute.  Just fork the project in github, and choose your flag.

Have fun


