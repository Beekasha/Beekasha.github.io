---
layout: post
title:      "Connect within Redux"
date:       2020-07-29 20:05:01 +0000
permalink:  connect_within_redux
---


For beginners, one of the most intimidating factors of redux is using a store. But once the connection is set up between a React component and a Redux store, we can use the Chrome Redux DevTools to see what is happening behind the scenes.

The *connect()* function connects a component with the data it needs from the store. It also connects the functions it can use to dispatch actions to the store. 

*mapStateToProps* deals with the Redux Store state, while *mapDispatchToProps* deals with the dispatch. First we declare mapStateToProps, taking in one parameter. It will be called whenever there is a change to the store. This is expected to return an object. In reference to my React Redux project, we can head into my Search Form and see what's happening. 

```
const mapStateToProps = state => ({
    text: state.movies.text
})

Here, we are getting a text object, aka the serch query. And we are passing the mapStateToProps object into the connect function, along with the actions we need in the form. This is so we can access it from our props within this Form. 

So we imported what we need from the top of the file:

```
import React, { Component } from 'react';
import {connect} from 'react-redux';
import {searchMovie, fetchMovies, setLoading} from '../../actions/searchActions';

```
connect at the bottom, and then we can reference the functions from within our file:

```
    onChange = event => {
        this.props.searchMovie(event.target.value)
    };

    onSubmit = event => {
        event.preventDefault();
        this.props.fetchMovies(this.props.text);
        this.props.setLoading();
    }
```
Using this to your advantage can keep everything within one space that you can easily manipulate. 




