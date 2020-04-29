# 02 - Reducers

![](../.gitbook/assets/image%20%2825%29.png)

![](../.gitbook/assets/image%20%2813%29.png)

The following is an example of a piece of State

![](../.gitbook/assets/image%20%2826%29.png)

Then we can define the initial state using the State interface

![](../.gitbook/assets/image%20%2817%29.png)

To create a reducer 

![](../.gitbook/assets/image%20%282%29.png)

Reducers are in a shared folder because the state is global

![](../.gitbook/assets/image%20%2857%29.png)

![](../.gitbook/assets/image.png)

To make AOT the reducer needs to be wrapped into a function

![](../.gitbook/assets/image%20%2811%29.png)

The index file declares the state

![](../.gitbook/assets/image%20%2814%29.png)

Modify data in a immutable way. 

![](../.gitbook/assets/image%20%2838%29.png)

Create helper functions to handle the data manipulation of collections.

```typescript
// Helper Functions..

const updateBook = (books: BookModel[], changes: BookModel) =>
    books.map(book => {
        return book.id === changes.id ? Object.assign({}, book, changes) : book;
    });
const deleteBook = (books: BookModel[], bookId: string) =>
    books.filter(book => bookId !== book.id);
    
//... Using them in the reducers
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

### Feature reducer file

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

### Recommendations from NgRx Creators

* States and reducers need to go in the shared directory  that can be globally accessed. 

{% hint style="info" %}
The `example-app` on the [ngrx repo](https://github.com/ngrx/platform/tree/master/projects/example-app/src/app/books) shows a reducer file under the feature and one global in the app
{% endhint %}

![](../.gitbook/assets/image%20%2855%29.png)

* States and reducers need to be in the same reducer file, as the reducer is working directly with the defined state.
  * This was their recommendation, but it wasn't a strong opinion. We should evaluate whether it's preferable to have a separate `.state` file, in the same directory.

