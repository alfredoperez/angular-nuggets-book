# 08 - Q&A

## When to use it a store?

This question was several times and basically you can use the **SHARI** principle to find out if ngrx or redux is needed for your application or even a specific component inside your app.

> ![Mike Ryan profile image](https://res.cloudinary.com/practicaldev/image/fetch/s--1cDEEpQ2--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://pbs.twimg.com/profile_images/1086460954261389312/V2QEk1Uk_normal.jpg) Mike Ryan @mikeryandev ![twitter logo](https://res.cloudinary.com/practicaldev/image/fetch/s--O8zQMJiw--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://practicaldev-herokuapp-com.freetls.fastly.net/assets/twitter-b32530dfdcd41c7dfe6db7c499483db80a5cd1698cb25021231cd7da7620824b.svg) In it, we introduce the SHARI principle: any state that needs to be Shared, Hydrated, made Available across routes, Retrieved with a side effect, or is Impacted by other components/effects belongs in the Store. 15:18 PM - 22 Apr 2018 [![Twitter reply action](https://dev.to/assets/twitter-reply-action.svg)](https://twitter.com/intent/tweet?in_reply_to=988074549983023104) [![Twitter retweet action](https://dev.to/assets/twitter-retweet-action.svg)](https://twitter.com/intent/retweet?tweet_id=988074549983023104) 3 [![Twitter like action](https://dev.to/assets/twitter-like-action.svg)](https://twitter.com/intent/like?tweet_id=988074549983023104) 10

From the [docs](https://ngrx.io/docs#when-should-i-use-ngrx-for-state-management) we get the following:

> `@ngrx/store` \(or Redux in general\) provides us with a lot of great features and can be used in a lot of use cases. But sometimes this pattern can be an overkill. Implementing it means we get the downside of using Redux \(a lot of extra code and complexity\) without benefiting of the upsides \(predictable state container and unidirectional data flow\).
>
> The NgRx core team has come up with a principle called **SHARI**, that can be used as a rule of thumb on data that needs to be added to the store.
>
> *  **Shared**: State that is shared between many components and services
> *  **Hydrated**: State that needs to be persisted and hydrated across page reloads
> *  **Available**: State that needs to be available when re-entering routes
> *  **Retrieved**: State that needs to be retrieved with a side effect, e.g. an HTTP request
> *  **Impacted**: State that is impacted by other components
>
> Try not to over-engineer your state management layer. Data is often fetched via XHR requests or is being sent over a WebSocket, and therefore is handled on the server side. Always ask yourself **when** and **why** to put some data in a client side store and keep alternatives in mind. For example, use routes to reflect applied filters on a list or use a `BehaviorSubject` in a service if you need to store some simple data, such as settings. Mike Ryan gave a very good talk on this topic: [You might not need NgRx](https://youtu.be/omnwu_etHTY)



## Is it a bad practice to use a service with `BehaviorSubject` to communicate between components?

The following question was asked:

> Once you add ngrx to an application, is it a bad practice to use a service with BehaviorSubject to communicate between components? Example. Having a modal with a form that uses a stepper. Should the modal use NGRX because the whole app is using ngrx.

The response from Mike was:

> **No, you do not have to use ngrx for all your states.**
>
> We have this term called SHARI principle and essentially the only state that goes into the ngrx store is a truly global state, state that is shared between your components, state that needs to be rehydrated when the application boots up or is impacted by actions of other features.
>
> If the state doesn't match that rubric, then **it is totally fine to use a simple state storage mechanism** for it as a service with a Behavior Subject.

Another related comment by Alex:

> One of the things I remember myself when I started using ngrx, I tried to **push anything** ngrx mostly because I wanted the dev tools to the time travel and I think some of the features that are exciting and helpful can misguide you. The moment of realization for me is not to push everything possible into it, at that time we were learning, as the pattern was evolving, now is kind of known what are the best practices.
>
> Some of the things I _**don't put in the store**_ are **Form Controls** \(since it is already a reactive state\), **the local state within components** \(even if it interacts with the network\), some of the lifecycle state for a component. Basically, **the first thing I asked myself is how shareable is the state, how much does the application needs to know about this.**

## How and where to handle loading and error states of ajax calls

{% embed url="https://medium.com/angular-in-depth/ngrx-how-and-where-to-handle-loading-and-error-states-of-ajax-calls-6613a14f902d" %}



