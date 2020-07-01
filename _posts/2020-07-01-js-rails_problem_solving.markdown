---
layout: post
title:      "JS-Rails Problem Solving"
date:       2020-07-01 19:34:04 +0000
permalink:  js-rails_problem_solving
---

One of the most challenging hurdles of this project materialized because I decided to have an third-party API supplementing the custom rails API. Originally, my app was designed similar to a blog-post type app, where all data must be manually entered. But for my movie watchlist app, I wanted there to be a movie title search bar responsible for dynamically creating custom movie objects with already-populated data. So I know the flow would be something like: GET request from 3rd-party API --> parse the data for Rails API --> POST request to Rails API.

A good amount of fixes that I found for my project seem to be problems that will most likely be abstracted in React. But here, I had to monkey-patch them. However, most of the problems seemed to stem from the fact that I was unsure about how to have objects on the DOM that could reference their corresponding database objects from which their data was pulled. More on that in a bit. 

Referencing objects based on objects on the page was another problem. I ended up leveraging the html by giving the images id numbers that referenced their corresponding movie id. When being rendered by the page, each movie in the db gets assigned their corresponding poster and id. That way, it would be a sort of messy way of linking my DOM elements back to the objects that populated them. 
```
    renderLi() {
        return `<img src="${this.poster}" id=${this.id} vspace="10" hspace="10" class="rendered-posters">`
    }
```


Another example is having to render an entirely new page of javascript instantly. My solution to this: Each poster from the database that is put onto the DOM will have a click listener set on it. If clicked, it calls a renderSelectedMoviePage() function that renders some new HTML onto the DOM. However, this still seems really messy, as I have to manually drop it all into a singular function. It’s almost definitely considered bad practice. . Notice, it also deletes any posters that were already existing on the page. 
(renderingposters pic)
```
```
let posters = document.querySelectorAll('.rendered-posters')  // select all posters
     

        // listening for click on all posters
        posters.forEach(poster => {
            poster.addEventListener("click", (event) => {

                this.removeAllPosters(),
                fetch(`http://localhost:3000/movies/${event.target.id}`)
                .then(resp => resp.json())
                .then(data =>  this.renderSelectedMoviePage(data))
            })

            poster.addEventListener("contextmenu", (event) => {
                // console.log("")
                this.adapter.deleteMovie(event.target.id)
            })

        })
```
renderSelectedMoviePage = (movie) =>
    {
        let main = document.querySelector("body");
        main.innerHTML = 
        `
        <div>
            <h1> ${movie.title} (${movie.year}) </h1>
            <img src="${movie.poster}" id="${movie.id}"/>
            <p>Rated: ${movie.rated}</p>
            <p>Runtime: ${movie.runtime}</p><br>
            <p>Director: ${movie.director}</p>
            <p>Actors: ${movie.actors}</p>
            <p>Plot: ${movie.plot}</p>
            <p>
                Reviews: 
                <ul id="reviews-list">
                </ul>
            </p>
            <div id="new-review-container">
            <form id="new-review-form">
                <input type="text" name="review-body" id="new-review-body">
                <input type="submit" value="Save review">
            </form><br>
            </div>
            
            <button type="button" onclick="location.reload()">Back to Watchlist</button>
        </div>
        `

        this.fetchReviewsByMovieId(movie.id)

        let new_review_form = document.querySelector('#new-review-form')
        new_review_form.addEventListener('submit', this.saveNewReview.bind(this))

    }

```

I'm looking forward to (hopefully) be giving a solution to this common-seeming problem in react. It would give a world of options for the front end viewpoint. 


