---
layout: post
title:      "Search Functionality + ActiveRecord Associations"
date:       2020-06-03 19:40:46 +0000
permalink:  search_functionality_activerecord_associations
---


For my Rails assessment, I was tasked to build a search bar function to search for students by name. It would also have to have partial search functionality in order to find students based on a partial match of their name string. 

First, I had to create a search form on the student index view. I had the search button go to the students_path, and collect a :student_search param (This refers to the inputted string, if a user decides to use the search function). 

```
 <%= form_tag students_path, :method => 'get'  do %>
   <%= text_field_tag :student_search, params[:student_search]%>
   <%= submit_tag "Search", :name => nil  %>
 <% end %>
```

Originally I was confused by this next step because I thought the task was to render a new page with the new list of students. But, the much simpler method was in changing how @students was declared in the student index within the students controller. 

```
    def index
        
        if params[:student_search]
            @students = Student.search(params[:student_search])
        else
            @students = current_teacher.students.sort_by_name
        end
		end

```

This way, if a user decides to use the search function, the :student_search parameter will be available. If so, @student is set to a list of students whose names match the inputted string. If the search function is not used, @students will be set using my scope method, as a list of all their students.

However, I still needed to define my .search method. In my Student model, I defined it as the following.

```
    def self.search(string)
        if string == ""
            Student.all.sort_by_name
        else
            Student.where("name like ?", "%#{string}%")
        end
    end
```

This way, if the searched string is empty, it returns a list of all students. Otherwise, we'll make a SQL query to check for partial matches within the student's name string. If there are no matches, no students will be put into @students. 

And that's it! We have a fully working search function implemented within our students index.

I was also asked to touch on available ActiveRecord associations once the models are associated. Let's say we have a class: 

```
class Project < ActiveRecord::Base
  belongs_to              :portfolio
  has_one                 :project_manager
  has_many                :milestones
  has_and_belongs_to_many :categories
end
```
The belongs_to and has_one relationship means we can call Project#portfolio, and Project#project_manager.

The has_many relationship adds similar methods, but with the addition of more (similar to array methods). We can call Project#milestones, but now with the added functionality of Project#milestones.empty?, .size, .create, .build, etc. 

has_and_belongs_to_many also adds similar functions on Project#categories, such as .empty?, .size, and others. 

One of the main redundancies I had in my code was seperately setting a comment's teacher id, instead of creating it in one line, like so:

```
    @comment = current_teacher.comments.new(comment_params)

```

This is a much cleaner syntax, instead of doing the much uglier:

```
@comment = Comment.new(comment_params)
@comment.teacher_id = current_teacher.id
```

