# Introduction

### Organization

Feature modules with state included

### Rules of thumb. You probably don't need NgRx

Consider:

* Service with Behavior Subject 

> There is a common misconception that once you have NgRx it has to be everywhere. It is fine to have most of the application with a Behavior Subject Service and use NgRx only where is needed

* Container Presenter
  * [https://stackblitz.com/github/jessesanders/tour-of-heroes](https://stackblitz.com/github/jessesanders/tour-of-heroes)
  * [https://stackblitz.com/github/jessesanders/tour-of-heroes/tree/container-presenter](https://stackblitz.com/github/jessesanders/tour-of-heroes/tree/container-presenter)
  * Containers: 
    * Interact with the store
    * Pass observables streams via `async` pipe
    * Receive events from child presenter components
    * Decide what to do with events/data
  * Presenters:
    * Receive plain data from parent
    * display date and make it pretty
    * User/ system events are raised parent via emitters
      * Decisions are deferred
      * Component is reusable and flexible
    * No knowledge of stores, services, selectors, actions, etc.
* Easy upgrade path to NgRx



![](../.gitbook/assets/image%20%2822%29.png)

Do not try to cheat by creating a single action that updates everything. **Actions should be SRP**

![](../.gitbook/assets/image%20%2849%29.png)

![](../.gitbook/assets/image%20%2862%29.png)

![](../.gitbook/assets/image%20%2859%29.png)

![](../.gitbook/assets/image%20%2856%29.png)

![](../.gitbook/assets/image%20%2848%29.png)

![](../.gitbook/assets/image%20%2871%29.png)

![](../.gitbook/assets/image%20%281%29.png)

