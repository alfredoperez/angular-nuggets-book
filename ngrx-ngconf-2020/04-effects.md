# 04 - Effects

![](../.gitbook/assets/image%20%2842%29.png)

We can move the interaction to the service from the components to the effects

![](../.gitbook/assets/image%20%283%29.png)

![](../.gitbook/assets/image%20%289%29.png)

Then register the effects. Note: effects are subscribed immediately

![](../.gitbook/assets/image%20%2815%29.png)

### Tips

* By modularizing the effects \(creating separate effects files for each page\), only the necessary effects are loaded and subscribed when the page is loaded.

### What map operator should I use?

{% file src="../.gitbook/assets/image-effects5.png" %}

{% file src="../.gitbook/assets/image-effects6.png" %}

_Using the switchMap as the default map operator in effects is dangerous._

{% file src="../.gitbook/assets/image-effects7.png" %}

_Use concatMap when the ordering of the operation matters_

### Good Effects Hygiene

* Let one effect handle one side effect.
  * _"If you are having to dispatch multiple actions from a single effect, that's a code smell. It usually means you probably need to create another set of actions or effects. Try to make diagrams of your control flow and define what your actions and side effects are."_
* _"So in general, an effect dispatching more than 1 action is not advisable. There could be edge cases, but it means perhaps your action is not unique enough."_
* _"If different actions are calling the same API call, they can share the same effect."_
* _"Rather than trying to dispatch multiple actions from 1 effect, it is encouraged to create multiple reducers that listens to 1 action dispatched from the effect instead."_

