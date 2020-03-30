# Guidelines

## Folder Structure

```typescript
|- books\
|        actions\
|            books-api.actions.ts
|            books-page.actions.ts
|
|
|- shared\
|       state\
|          {feature}.reducer.ts
|          index.ts
| 
```





## Actions

* Should be close to the feature that are using it. That is why the feature include an actions folder
* Use either present or past tense to describe the action. 

  * Page -&gt; Use present. Eg.  Create Book
  * API -&gt; Use past tense. Eg. Books Loaded Successfully

* The index file defines the names used to export the actions

```typescript
import * as BooksPageActions from "./books-page.actions";
import * as BooksApiActions from "./books-api.actions";

export { BooksPageActions, BooksApiActions };
```







## Reducers

* Separate reducer per feature
* Should live outside the feature, because the state it is shared in the whole application
* Combine actions that can use the same reducer

```typescript
  on(BooksPageActions.enter, BooksPageActions.clearSelectedBook, (state, action) => ({
          ...state,
          activeBookId: null
   })),
```

* Only reducers can modify state
* The index file in the reducers declares the state 

![](../.gitbook/assets/image%20%2814%29.png)

* Feature state file
  * Declare a `State` interface with the state for the feature
  * Declares an `initialState` that included the initial state
  * Declare a feature reducer that contains the result of using `createReducer`
  * Exports a `reducer` function that wraps the reducer created. This is needed for AOT and it is not needed when using Ivy.

```typescript
export interface State {
    collection: BookModel[];
    activeBookId: string | null;
}

export const initialState: State = {
    collection: [],
    activeBookId: null
};

export const booksReducer = createReducer(
    initialState,
    on(BooksPageActions.enter,
        BooksPageActions.clearSelectedBook, (state, action) => ({
        ...state,
        activeBookId: null
    })),
    on(BooksPageActions.selectBook, (state, action) => ({
        ...state,
        activeBookId: action.bookId
    })),
);

export function reducer(state: State | undefined, action: Action) {
    return booksReducer(state, action);
}

```

* The index file defines the state and assigns each reducer to a property on the state

```typescript
export interface State {
    books: fromBooks.State;
}

export const reducers: ActionReducerMap<State> = {
    books:fromBooks.reducer
};

export const metaReducers: MetaReducer<State>[] = [];
```

