# 01 - Actions

## 

> ### Actions are like the global @output for your whole app

![](../.gitbook/assets/screen-shot-2020-05-31-at-3.32.37-pm.png)

![](../.gitbook/assets/image-action1.png)

![](../.gitbook/assets/screen-shot-2020-05-31-at-3.34.12-pm.png)

### Good Action Hygiene

* Unique events get unique actions
* Actions are grouped by their source
  * meaning they should be grouped by each page
  * located close to the components dispatching them for traceability of @outputs
* Actions are never reused - Present tense for action names

![](../.gitbook/assets/image-action7.png)

### Benefits

This makes easier to **debug**, and the specific names makes it **easy to back track.**  
It is easier to refactor, because of the Single-Responsibility-Principle if multiple components use the same action, it is harder to abstract.  


### Example

```typescript
export const enter = createAction("[Movies Page] Enter")
```

Metadata can be added to the actions

![](../.gitbook/assets/image%20%2837%29.png)

An action file is made of a collection of actions

![](../.gitbook/assets/image%20%2873%29.png)

Then it can be used in the components

![](../.gitbook/assets/image%20%283%29.png)

The index file can be used to define the names for the actions exported.

```typescript
import * as BooksPageActions from "./books-page.actions";
import * as BooksApiActions from "./books-api.actions";

export { BooksPageActions, BooksApiActions };
```

## Event Storming

![](../.gitbook/assets/image%20%2861%29.png)

### Example

This is the event storming a a page that creates books

![](../.gitbook/assets/image%20%2811%29.png)

### 

