---
layout: post
title: How to build a react application(with redux)
tags:
- javascript
---


## firstly, design the view

## secondly, based on the view, decide what components do you need.

## Thirdly, based on the components decide what states do you need.

## At last, use redux to handle the manipulation of States by the components

Redux is the state manager for react component

## Concepts of redux

Actions are objects can be dispatched by store

Reducers are functions who manipulated the state according to the action dispatched

Store is the object that link actions and the reducer together. It is able to dispatch actions and also subscribe actions and deal with actions with reduces. Store can be connected to the component.
When you decided certain component need a state you can connect this component to a store. By doing this you component can get some part of the store as its State and also get a dispatch function from the store that you can dispatch actions inside the component.

## Some advices
When you want to dispatch some actions in a component, the component must be connected to the store. its okay to connect any component with a store but it will be a good idea to have more dumb component and less smart component. Because dumb component is easier to be reused.
