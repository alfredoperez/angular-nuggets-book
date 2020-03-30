# Guidelines

## Folder Structure

```typescript
├─ books\
│     actions\
│         books-api.actions.ts
│         books-page.actions.ts
│         index.ts
│      books.selectors.ts
│     
├─ shared\
│       state\
│          {feature}.reducer.ts     // Includes state interface, initial interface, reducers and local selectors
│          index.ts
│ 
```





## Actions

* Should be close to the feature that are using it. That is why the feature include an actions folder
* Use either present or past tense to describe the action. 

  * Page -&gt; Use present tense because they are related to events. It is like in HTML the events do not use past tense. Eg. `OnClick` or `click` is not `OnClicked` or `clicked`

  ```text
  export const createBook = createAction(
      '[Books Page] Create a book',
      props<{book: BookRequiredProps}>()
  );

  export const selectBook = createAction(
      '[Books Page] Select a book',
      props<{bookId: string}>()
  );
  ```

  * API -&gt; Use past tense because they are used to describe an action that happened

  ```text
  export const bookUpdated = createAction(
      '[Books API] Book Updated Success',
      props<{book: BookModel}>()
  );

  export const bookDeleted = createAction(
      '[Books API] Book Deleted Success',
      props<{bookId: string}>()
  );
  ```

* The index file defines the names used to export the actions

```typescript
import * as BooksPageActions from "./books-page.actions";
import * as BooksApiActions from "./books-api.actions";

export { BooksPageActions, BooksApiActions };
```



## Reducers

* Separate reducer per feature
* Should live outside the feature, because the state it is shared in the whole application
* State should save the model as it comes from the API. This can be later transformed on the selectors.
* Combine actions that can use the same reducer

```typescript
  on(BooksPageActions.enter, BooksPageActions.clearSelectedBook, (state, action) => ({
          ...state,
          activeBookId: null
   })),
```

* Only reducers can modify state and it should do it in an immutable way
* The index file in the reducers declares the state for the whole application

```typescript
import * as fromBooks from "./books.reducer";

export interface State {
    books: fromBooks.State;
}

export const reducers: ActionReducerMap<State> = {
    books:fromBooks.reducer
};

export const metaReducers: MetaReducer<State>[] = [];

```

* Feature reducer file
  * Declares a `State` interface with the state for the feature
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

* Create helper functions to handle the data manipulation of collections

```typescript
const createBook = (books: BookModel[], book: BookModel) => [...books, book];
const updateBook = (books: BookModel[], changes: BookModel) =>
    books.map(book => {
        return book.id === changes.id ? Object.assign({}, book, changes) : book;
    });
const deleteBook = (books: BookModel[], bookId: string) =>
    books.filter(book => bookId !== book.id);
    
...

    on(BooksApiActions.bookCreated, (state, action) => {
        return {
            collection: createBook(state.collection, action.book),
            activeBookId: null
        };
    }),
    on(BooksApiActions.bookUpdated, (state, action) => {
        return {
            collection: updateBook(state.collection, action.book),
            activeBookId: null
        };
    }),
    on(BooksApiActions.bookDeleted, (state, action) => {
        return {
            ...state,
            collection: deleteBook(state.collection, action.bookId)
        };
    })
```

## Selectors

* They should be near the state they usually in the reducer file
* They are in charge of transforming the data to how the UI uses it. State in store should be clean and easy to serialize and since selector are easy to test this is the best place to transform. Is also makes it easier to hydrate 
* "Getter" selectors are simple selector that get data from a property on the state

```typescript
export const selectAll = (state: State) => state.collection;
export const selectActiveBookId = (state: State) => state.activeBookId;
```

* Complex selectors combine selectors and this should be created using `createSelector` . The function only gets called if any of the inputs selectors are modified

```typescript
export const selectActiveBook = createSelector(
    selectAll,
    selectActiveBookId,
    (books, activeBookId) =>
        books.find(book => book.id === activeBookId)
);
```

* Selectors can go next to the component where they are used or in the reducer file located in the `state` folder. Local selectors makes it easier to test
* Global selectors are added in the `state/index`

```typescript
export const selectBooksState = (state:State)=> state.books;
export const selectActiveBook = createSelector(
    selectBooksState,
    fromBooks.selectActiveBook
)
```

* When using the selector in the component is recommended to initialize in the constructor. If using the strict mode in TypeScript, the compiler will not be able to know that the selectors where initialized on `ngOnInit`

## Effects











## Other

{% embed url="https://medium.com/angular-in-depth/ngrx-how-and-where-to-handle-loading-and-error-states-of-ajax-calls-6613a14f902d" %}



