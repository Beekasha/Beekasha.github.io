---
layout: post
title:      "Sinatra Project (Mod 2)"
date:       2020-03-23 20:07:35 +0000
permalink:  sinatra_project_mod_2
---


One of the hardest parts of setting up this project, by far, was making sure the associations of my models were correct. 

```
class Teacher < ActiveRecord::Base
    has_many :klasses
    has_many :reviews
    has_many :students, through: :klasses
    
    has_secure_password
end
```

```
class Student < ActiveRecord::Base
    has_many :reviews
    has_and_belongs_to_many :klasses
    has_many :teachers, through: :klasses
end
```

```
class Klass < ActiveRecord::Base
    has_and_belongs_to_many :student
    belongs_to :teacher 
end
```

```
class Review < ActiveRecord::Base
    belongs_to :student
    belongs_to :teacher
    
end
```

```
class KlassesStudents < ActiveRecord::Base
  belongs_to :students
  belongs_to :klasses
end
```

I thought it was not only important to be able to access all of a teacher's reviews, but also all the reviews of their students. Essentially, this makes the app similar to a live feed of all that is necessary to know about your students throughout the school day. 

Another thing I found releatively difficult was having the forsight to name the RESTful routes ahead of time in order to prevent some 'not-so RESTful' routes. I originally dug myself into a hole beacuse I needed to come up with ways to access the :id attribute of my objects, without realizing it would be smart to list them in the url. 

In all, I learned much more from buidling this than the labs can provide, because this build enables you to create by failing. You can read as much documentation as you want, but you never really know how the technology works until you implement it within your own web apps. 
