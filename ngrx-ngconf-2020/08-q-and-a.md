# 09 - Q&A

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

{% hint style="info" %}
SHARI principle  can be used to find out if you need to put the state into store
{% endhint %}

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

The following are from the "Advanced NgRx" Workshop from ng-conf 2019  


![](../.gitbook/assets/image%20%2895%29.png)

{% hint style="info" %}
It is ok to user service with subjects to handle component state even when the project already has NgRx and a store.
{% endhint %}

## How to keep the old model and new model when editing an entity?

This question originated when discussing about how to do `JSONPatch` since it is required to have the original data and the modified to generate the set of commands.

#### Keep Original Data from API in the Store

We always should have the original data provided by the API  in the store and the data transformation or mapping is done in the selectors.

It is wrong to keep flatten view models directly in the store because it hard to shared the same view model in different component that might not have the same view model. 

If the data in the store is only shared by a single view, it should not be in the store.

#### Use the form value to have the new value

The form should have the new value of the entity. Even if it is a collection of form groups, we should rely that we are getting the new value from the form.

**Selector to get Original Data + Transformed Form Value**  


{% hint style="success" %}
Keep original API data in the store
{% endhint %}

## **Are resolvers needed when using NgRx?**

> A data provider class can be used with the router to **resolve data during navigation**. ****The router will then **wait for the data t**o be resolved before the route is finally activated.

{% embed url="https://angular.io/api/router/Resolve\#resolve" %}

There is not a pattern of how to use resolvers when using ngrx. I found the following examples:

* Resolvers just dispatching effects

![](../.gitbook/assets/image%20%28103%29.png)

* Resolvers waiting for the data to be returned

![](../.gitbook/assets/image%20%2899%29.png)

* Resolvers with explicit wait for data to be loading and redirection

![](../.gitbook/assets/image%20%28102%29.png)

{% hint style="success" %}
Use a guard to handle re-directs and checks for data
{% endhint %}

> From Mike Ryan
>
> Resolvers and guards are totally fine to use with NgRx. Keep in mind that the goal of @ngrx/effects is to **isolate side effects** from your components to keep rendering pure. Resolvers and guards are another means of isolating those side effects.
>
> With that being said, I'll tell you how I approach those problems.   
> - First, I don't use resolvers or guards.  
> - I have my components dispatch actions like `[Books Page] Enter` to signal that the user has entered a certain page.  
>   
> These actions typically flip some kind of `loading` flag in state to `true`. These pages use selectors to reading the loading flag and hide their content until `loading` becomes `false`.  
>   
>  In the meantime they show some kind of **spinner or progress bar.** If multiple pages need the same data it becomes really easy to model that with an effect, where the effect starts off like this:
>
> ```typescript
> this.actions$.pipe(
>   ofType(enterBooksPage, enterAuthorsPage, enterOverviewPage),
>   exhaustMap(...)
> );
> ```



{% hint style="success" %}
Use a guards to handle re-directs and checks for data
{% endhint %}

{% hint style="success" %}
Prefer to avoid resolvers, since it is cleaner to have the `dispatch` actions in the  in the same component to visualize what actions are dispatched and handle loading states.
{% endhint %}

{% hint style="info" %}
Re-use effects when they get same data that is needed for multipleow and where to handle loading and error states of AJAX calls?
{% endhint %}



## How to handle loading and error states?

{% embed url="https://medium.com/angular-in-depth/ngrx-how-and-where-to-handle-loading-and-error-states-of-ajax-calls-6613a14f902d" %}

### Handling errors

When the only component that needs to handle the error is a **snackbar** or any other type of **pop-up,** then Effects can handle that error.

```typescript
// Dispatch is set to false, so this effect will not try to dispatch
// the result of this effect.
@Effect({ dispatch: false })
handleFetchError: Observable<unknown> = this.actions$.pipe(
  ofType(actions.FETCH_PRODUCTS_ERROR),
  map(() => {
    // Setting the timeout, so that angular would re-run change detection.
    setTimeout(
      () =>
        this.snackBar.open('Error fetching products', 'Error', {
          duration: 2500,
        }),
      0);
  })
);
```

When is needed in the component, subscribe to it using `Actions`

```typescript
@Component({
  selector: 'app-movies-page',
  template: `
    <h1>Movies Page</h1>
    <div *ngIf="error$ | async as error">
      {{ error }}
    </div>
    <button (click)="reload()">Refresh List</button>
  `
})
export class MoviesPageComponent {
  error$: BehaviorSubject<string>;

  constructor(
    private store: Store<fromRoot.State>,
    actions$: Actions,
  ) {
    this.error$ = new BehaviorSubject<string>('');
    actions$.pipe(
      ofType('[Movies/API] Load Movies Failure'),
    ).subscribe(this.error$);
      
   this.store.dispatch({ type: '[Movies Page] Load Movies' });
  }

  reload() {
    this.error.next('');
    this.store.dispatch({ type: '[Movies Page] Load Movies' });
  }
}
```

The **advantages** of such an approach are that the error becomes part of the **local state of the Component**, and as a result, this error is **cleaned up** when Component is destroyed.

It also helps if we hydrate/rehydrate Store State to and from `localStorage` via meta-reducer, we wouldn’t be saving/restoring the State with _**Error**._

This does not work to well if you have multiple components that rely in the same error

### Handling  `loading`  state

A `isLoading` state is necessary when loading data from a cached list or loading data in chunks

### Handling `Success/Loaded` State

This should be used that much. Since we are working with a collection `Result[]` the initial/loading state should be `null` and loaded/success state should `[]` or with tdata.

### All-in-one State

We could combine them all under a **single state property**, and still get the error message if needed. It also helps eliminate the invalid states, such as `{ isLoading: true, error: 'Failed', isLoaded: true }`

```typescript
export const enum LoadingState {
    INIT = 'INIT',
    LOADING = 'LOADING',
    LOADED = 'LOADED',
}
export interface ErrorState {
    errorMsg: string;
}

export type CallState = LoadingState | ErrorState;

// Helper function to extract error, if there is one.
export function getError(callState: CallState): string | null { 
    if ((callState as ErrorState).errorMsg !== undefined) { 
        return (callState as ErrorState).errorMsg;
    } 
    return null;
}
```

The reducer becomes cleaner and prone to errors

![](../.gitbook/assets/image%20%28105%29.png)

Helper `getError` function can be used in the selectors.

![](../.gitbook/assets/image%20%28109%29.png)

## Atomic State and State Machines in NgRx?

{% embed url="https://youtu.be/JP4dEM4bjE8" %}

{% embed url="https://twitter.com/robocell/status/1257339635048603650" %}

The idea is that sometimes **multiple state variables are related**, but no one of them is derivable from any other one. People expend a lot of effort trying to keep these variables in sync with each other, and often have bugs when they don't succeed.

A classic example is when working with forms, people might track whether the form is: `dirty`, `valid` `submitting`, `submitted`,`canceled`, `rejected`, etc.

These states are not necessarily derivable from each other, but often change in concert with each other = they are not atomic.

In such circumstances, this might point to the presence of another variable that IS atomic, from which our data can be derived, and reduces the complexity of our store.

In this case, we can look to a state machine. More information on state machines here:

[https://css-tricks.com/robust-react-user-interfaces-with-finite-state-machines/](https://css-tricks.com/robust-react-user-interfaces-with-finite-state-machines/)

So in our form example, we could store the state of our form state machine in our `state` and update that in our reducers.

Then, we **use selectors to get back all the variables** we needed before based on the single state machine state variable.

{% hint style="success" %}
Use atomic state to represent state of components and rely on selectors to get back variables like `dirty, submitted, canceled, etc.`
{% endhint %}

## How to dispatch a single action per effect?

{% embed url="https://twitter.com/brandontroberts/status/1266113040623304704" %}

{% embed url="https://twitter.com/MannIsaac/status/1253126370030485506" %}

{% embed url="https://twitter.com/brandontroberts/status/1253144569606295552" %}

### AHA - Avoid Hasty Abstraction

If somebody submits a form to put some to-do sent they might dispatch actions to:

1. Post the to-do
2. Open a toast
3. Go to the dashboard

```typescript
function submitFormCommands({todo}){
  this.store.dispatch(postTodo());
  this.store.dispatch(openToast('Form Submitted));
  this.store.dispatch(navigateTo('Dashboard));
}
```

Instead, this should dispatch a single action and all the different steps should be handle in the effect.

```typescript
function submitFormCommands({todo}){
    this.store.dispatch(todoSubmitted());
}
```

### Avoid Effect Dominoes

![Image with the example code of effect domino](https://res.cloudinary.com/practicaldev/image/fetch/s--IZeDJZU1--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/2vydfm8ht9z6t73heshi.png)

Instead, Leverage Independent Effects and handle them independently

![Image with the example code for independent effetcs](https://res.cloudinary.com/practicaldev/image/fetch/s--LVQlUlVG--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/mdraxbssjel4nj54py28.png)

* Every effect does a specific task \*. We have taken off the parts which are both independent and generic and split them off into their own effects.

####  What happens with multiple effects that interact concurrently with the same data?

It can be refactored into a single effect if they, in fact, rely on the same data

####  How to deal with dependency order for example when one effect need to happen after the other?

By adding more action that signifies that the _effect has completed_, and tied the completion of that effect to an action. If they are more interconnected, they can be modeled as a single effect.

### Mike's Answer

I think you have two ways to go about this. First, only use one action. Then you can either...

Have one effect that gets all of the data:

```typescript
this.actions$.pipe(
   ofType(enterPageAction),
   exhaustMap(() => forkJoin(this.http.get('a'), this.http.get('b'))
);
```

Have multiple effects each listening to the same action:

```typescript
this.actions$.pipe(
   ofType(enterPageAction),
   exhaustMap(() => this.http.get('a'))
);

this.actions$.pipe(
   ofType(enterPageAction),
   exhaustMap(() => this.http.get('b'))
);
```

### Example 1 - Effect with multiple dispatches



![](../.gitbook/assets/image%20%28107%29.png)

![](../.gitbook/assets/image%20%28112%29.png)

![](../.gitbook/assets/image%20%28111%29.png)

### Example 2 - state and selectors

![](../.gitbook/assets/image%20%28108%29.png)

### Example 3 - Resolvers 

![](../.gitbook/assets/image%20%28106%29.png)

![](../.gitbook/assets/image%20%28113%29.png)

### Example 4 - Effect

![](../.gitbook/assets/image%20%28110%29.png)

{% hint style="danger" %}
Avoid hasty abstractions when using dispatching actions. Remember to actions are related to events and not commands
{% endhint %}

## Should we use stateless effects?

{% embed url="https://twitter.com/brandontroberts/status/1253144569606295552" %}

The following example is subscribing to the store.

![Example of an effect that subscribes to a store](https://res.cloudinary.com/practicaldev/image/fetch/s--Z8fAOoDm--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/itq83n30h3nwcpaus715.png)

{% hint style="info" %}
Make stateless effects and based on events.
{% endhint %}

## Should you have stateless in guards and resolvers of overlays or modals?

It makes it harder to re-use the overlay or modal from any other view.

![](../.gitbook/assets/image%20%28114%29.png)

This guard is checking the following things:  
- Any errors in search  
- Number of tagged objects  
- Id of the tag object

{% hint style="info" %}
**Make SRP Guards**. One guard can be checking the current state of search only when the overlay is open from Search. The other guard can check if it is getting the tag Id when  there are not multiple tags  
  
**Pass data through router**. It is harder to use guards whenever they rely on data set via store from a different component. In the example we can see that a consumer of this guard needs to set the correct `searchState` even if it is not related to the page where is used.
{% endhint %}

## Where should we initialize the selectors?

When using the selector in the component, it is recommended not initialize them in the declaration and instead declared in the constructor

```typescript
export class FindBookPageComponent {
  searchQuery$: Observable<string>;
  books$: Observable<Book[]>;
  loading$: Observable<boolean>;
  error$: Observable<string>;

  constructor(private store: Store<fromBooks.State>) {
    this.searchQuery$ = store.pipe(
      select(fromBooks.selectSearchQuery),
      take(1)
    );
    this.books$ = store.pipe(select(fromBooks.selectSearchResults));
    this.loading$ = store.pipe(select(fromBooks.selectSearchLoading));
    this.error$ = store.pipe(select(fromBooks.selectSearchError));
  }

  search(query: string) {
    this.store.dispatch(FindBookPageActions.searchBooks({ query }));
  }
}
```

If using the strict mode in TypeScript, the compiler will not be able to know that the selectors were initialized on `ngOnInit`

{% embed url="https://mariusschulz.com/blog/strict-property-initialization-in-typescript" %}

{% embed url="https://indepth.dev/a-look-at-major-features-in-the-angular-ivy-version-9-release/\#strict-mode" %}

The `strictPropertyInitialization` is added by default in the `--strict` mode in Angular 9.

Also, it adds the following checks:

```bash
{
  "//": "tsconfig.json",
  "compilerOptions": {
    "noImplicitAny": true,
    "noImplicitReturns": true,
    "noImplicitThis": true,
    "noFallthroughCasesInSwitch": true,
    "strictNullChecks": true
  }
}
```

> The strict-mode allows us to write much safe and robust application. Honestly, I think all Angular application should be written in strict-mode, but it is a little hard to understand every error messages caused by the compiler.

{% embed url="https://medium.com/lacolaco-blog/guide-for-type-safe-angular-6e9562499d93" %}

## Linter

{% embed url="https://github.com/timdeschryver/ngrx-tslint-rules" %}



