# 09 - Best Practices and Pitfalls

## Store

### What to put in the store?

Use SHARI principle. Start from a reasonable standpoint that nothing should be in the store unless it proves itself to be in the store. Rather than to put everything in the store and pull it out once it becomes it problematic

### Do not put model objects/ view models into the store

#### Why? 

it can be reused by multiple components and view models should be constructed using selectors

## Actions

### Create actions based on events not commands

todo submitted vs \(Save todo, show loading, etc\)

### Use Event Storming as a tool to figure it out the events and actions

This helps to think in terms of events and not in terms of things that you want to happens as a response when an event happens. This also helps the team to get better at using ngrx, because this is done as a group exercise. This can help to have one developer buld UI and selectors while  other builds the effect and reducers.



## Reducers





## Selectors

### Use selector to map/transform data

#### Why?

To keep the store state in a usable format for multiple selectors and components.

### Use selectors to create View Model

![](../.gitbook/assets/image%20%2829%29.png)

#### Why?

To keep store lean, create specific model for a container and get the benefits of selectors memoization

### **Use higher level selectors**

This helps with refactoring when the state changes it is easier to modify the higher selector

## Effects

### Beware Effects Dominoes

Effect dominoes are actions that are dispatch which trigger effects that dispatch action and so on.  A  heusristic that can be used is, "allow action to be dispatched which triggers effect which are allowed to dispatch one more action that can be only reduced". There are valid reasons to break this  


![](../.gitbook/assets/image%20%2854%29.png)

#### Beware of selector based effects

#### Try to not use selectors in the effects

## Components

#### Make component simpler and purer by passing the data directly

If components need to use store to select data it create a dependency to the store and hurts the ability to reuse the component



## Links

[https://www.youtube.com/watch?v=JP4dEM4bjE8](https://www.youtube.com/watch?v=JP4dEM4bjE8)

