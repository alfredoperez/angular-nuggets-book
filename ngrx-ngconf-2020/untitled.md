# 01 - Actions

## Good Action Hygiene

* Unique events get unique actions
* Actions are grouped by their source
* Actions are never reused - Present tense for action names

### Benefits

This makes easier to debug, and the specific names makes it easy to back track.  
It is easier to refactoring, because of the SRP if multiple components use the same service is harder to abstract.  


### Example

```typescript
export const enter = createAction("[Movies Page] Enter")
```

Metadata can be added to the actions

![](../.gitbook/assets/image%20%288%29.png)

An action file is made of a collection of actions

![](../.gitbook/assets/image%20%2815%29.png)

Then it can be used in the components

![](../.gitbook/assets/image%20%282%29.png)

## Event Storming

![](../.gitbook/assets/image%20%2813%29.png)

### Example

This is the event storming a a page that creates books

![](../.gitbook/assets/image%20%283%29.png)

### 

