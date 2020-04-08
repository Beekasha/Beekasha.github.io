---
layout: post
title:      "Rendering vs. Redirecting"
date:       2020-04-07 15:23:27 -0400
permalink:  rendering_vs_redirecting
---


Initially I was confused as to when to use a redirect vs a render :erb.

Rendering a view is done by calling an erb file within a controller. This is done without losing access to the instance variables defined in the corresponding controller. 

While you can access instance variables through a render, their values will be wiped out with a redirect.

Redirect on the other hand, will make a brand new request to the controller action, and you will be able to use the logic from your controllers in the view. For example, sending a request to another address. The new view that’s rendered after a redirect will not have access to the instance variables defined in the previous controller action.

This is why you RENDER a new form, fill it out, and REDIRECT (to lets say - an index page). 
