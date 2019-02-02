---
layout: post
title:      "From state to props and back again"
date:       2019-02-02 02:16:42 +0000
permalink:  from_state_to_props_and_back_again
---


At first glance, state seems full of contradictions. It is merely a Plain JS Object, but your entire app is built around it. It stores dynamic data, but it is treated as immutable. It is private, but its attributes can appear in and seem to be altered by actions in various components throughout your app. State is easily misunderstood, and that misunderstanding can be compounded by adding Redux to the mix. So let’s start with the basics.

If you wanted to update state, you’d probably just think to write state.thing = “new thing”.  
But that’s not going to do the job. Instead, changes to state must be made to a copy of the current version of state.  That new object becomes the state and the old state is stored away. Once you make this change, the reconciliation process begins and will cause all of the affected   components to re-render.

Though state lives in one place, its data can be passed around within props (properties). Props are vehicles for data and functions that can be used by both functional and class components.
These components can access the props data and functions, but they can never make changes to them. Functions sent through props allow child components to trigger changes to the state. 

In Redux, state is stored outside of components in a centralized store. By mapping props to a class component, that component can access both the properties of the state and actions that trigger changes to the state. The changes to state are made by dispatching an action made available by the mapped props, that communicates with the reducer, which changes the state based on its interpretation of the action object.

In React without Redux, a class component can initialize and manage its own state. Only the owner component can make changes to its state and it must do so using the asynchronous method setState(). It’s not that parent components are greedy with their state—they share it willingly—they are just protective of it. 

Just as in Redux, parent components use props as a sharing mechanism. A component can send properties of its state down to child components so that they can access and use it how they may. The parent component can also send callback functions to a child that, when triggered by an event in the props-receiving child component, will send the callback to the parent so that it can update its state. 

Essentially, state and props work together to manage the data flow in your app’s component structure. State maintains the core data while props conveys that data and the functions that can change it.

A few quality resources:                                                                                                                                                                                          
[props](https://reactjs.org/docs/components-and-props.html)                                                                                                                 
[state](https://reactjs.org/docs/state-and-lifecycle.html)



