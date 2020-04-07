---
layout: post
title:      "Rendering vs. Redirecting"
date:       2020-04-07 15:23:27 -0400
permalink:  rendering_vs_redirecting
---


Initially I was confused as to when to use a redirect vs a render :erb.

Rendering a view is done by calling an erb file within a controller. If you call a render, all of the logic from your methods will not be accessible within the normal instance variables. A render does not load any context associated with the controller action. Render wants to render a view without passing any data to the next controller action. 

Redirect on the other hand, will make a brand new request to the controller action, and you will be able to use the logic from your controllers in the view. 

This is why you RENDER a new form, fill it out, and REDIRECT (to lets say - an index page). 
