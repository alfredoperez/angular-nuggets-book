# Advanced NgRx: Complex Angular State Management - JavaScript Marathon

{% embed url="https://www.youtube.com/watch?v=JP4dEM4bjE8&t=367s" %}

![](../.gitbook/assets/image%20%2862%29.png)

## Bloated Stores

### Ideal Store Data

SHARI

Start from a reasonable standpoint that nothing should be in the store unless it proves itself to be in the store. Rather than to put everything in the store and pull it out once it becomes it problematic

DUGSA -&gt; 

* D- dependent - data that is needed for actions and effects
* U- unique - data can not be derived from other part. If data can be derived it should be a selector
* G- Global - data needed everywhere
* S- Serializable - 
* A- Atomic - it goes into state machines

## Too Few Selectors

Prefer specific selectors. Make sure to compose selectors

Use selectors to map data

use selectors to create view models

![](../.gitbook/assets/image%20%2858%29.png)

## Command-Based Actions

Actions are Events Not Commands

Do not dispatch actions as if they were commands like "Save Result" or "Open Modal".  Instead think about it as what buttons the user clicked, what text did they enter, what flow did they began.

DRY - Don't Repeat Yourself

when this is done in NgRx create a situation that acts counter to the intention of the architecture. Repeating and reusing to much code in NgRX can actually lead to  code which has a lot of regression and is more difficult to maintain

AHA Programming - Avoid Hasty Abstraction 

Actions should be unique, a user clicking a certain button vs a similar button in a different view are unique events. They are similar in what they will trigger but they are unique in the context where they occur. It is cheap to make actions

if 1 event  occurs it should be1 action

![](../.gitbook/assets/image%20%289%29.png)

If somebody submits a form to put some to-do sent they might dispatch actions to  
1\)  post the to do  
2\) open a toast   
3\) go to the dashboard   
This will require to thave effects that post the to do, that open the toast and that navigate to the dashboard .  
This is making some of your code and your actions much harder to understand and your flows much harder to understand because if you ever arrive at the open toast action it is harder to find how many different places is this used? where is it dispatched from? what if I want to change what happens when a toast is opened ? Eg. to have another step that has happens before,  is it ok to have it every single place that I'm showing a toast to have that occur.  
When you make your actions super super super specific you lose that functional programming/ declarative  style and the  ability to change and adapt. Tis is changing it to an imperative mode since it is specified exactly what needs to happen and removes all that flexibility.  
Again you go back to having things which are tightly coupled but they're **tightly coupled through the indirection of ngrx** which is the worst of both worlds 

Instead this should dispatch a single action and all the different steps should be handle in the effect

The component does not need to know.

### Struggling? Try Event Storming

Go through the UI and find what are all the thing that can be treat as an action



## Beware Effect Dominoes

Effect dominoes are actions that are dispatch which trigger effects that dispatch action and so on

![](../.gitbook/assets/image%20%2854%29.png)

Instead Leverage Independent Effects and handle them independently

![](../.gitbook/assets/image%20%2894%29.png)

Every effect does a specifc task. We have taken off the parts which are both independent and generic and split them off into thir own effects. 

#### What happens with multiple effects that interact concurrently with the same data?

 It can be refactored into a single effect If they in fact rely on the same data

#### How to deal with dependency order? when one effect need to happen after the other?

By adding more action that signify that the effect has completed, and tied the completion of that effect to an action. If they are more interconnected, they can be  modeled as a single effect, 

## Beware of Effect Based Selector

The following example is subscribing to the store. 

![](../.gitbook/assets/image%20%2825%29.png)

There is not easy way to trace what actions modified the state. This can also trigger that effect start happening not in purpose when some state changes

Make the effect based on events.

## Overly Smart Components - Make Fewer, Dumber Components





## Links

{% embed url="https://github.com/wesleygrimes/managing-file-uploads-with-ngrx" %}

{% embed url="https://github.com/ngrx/platform/tree/master/projects/example-app" %}







