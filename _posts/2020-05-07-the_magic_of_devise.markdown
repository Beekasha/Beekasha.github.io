---
layout: post
title:      "The Magic of Devise"
date:       2020-05-07 17:45:29 +0000
permalink:  the_magic_of_devise
---


One of the aspects that gave me the most pause during the Mod 3 Rails Project was the vast amount of information about the authentication process and the amount of generated files during a rails g command. It makes sense then, that I would get very lost during the integration of the devise gem.   

However, if you take a step back and realize what devise is doing at a higher level, everything begins to make sense. Essentially, in my case, we're just looking for a way to make a quick and secure user system. Most importantly, the database authenticatable module, registerable module, and the omniauthable module (and a few more). The other modules can then be removed, because we do not need all ten of their modules. They mostly deal with ways to reset user passwords, tracking location, and general security measures in regards to users. 

One thing to keep in mind while working with Devise is ruby strong params. It's not always clear to remember to add these to your Registrations Controller. If you forget, devise just won't persist your data because of the value not being added to the strong params. 



Adding Omniauth was also a whole other beast. If anything, the concept that got solidified for me while working to integrate it is to always go back to the documentation. Tutorials, videos, and stack overflow can only get one so far. But the documentation is almost always the best resource to refer back to. 

Devise also adds the error messages to the flash hash, which is available in our views. The reasoning for this is that it allows us to present the errors without overriding the templates that devise provided. 

All in all this was a good project, but I believe the most learning experience was due to the integration of devise in our apps. 
