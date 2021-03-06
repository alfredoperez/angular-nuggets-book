# State Machines in Javascript with XState

## Details

* **URL:** [**https://frontendmasters.com/courses/xstate/introduction/**](https://frontendmasters.com/courses/xstate/introduction/)\*\*\*\*
* **Source Code:** [**https://github.com/davidkpiano/frontend-masters-xstate-workshop**](https://github.com/davidkpiano/frontend-masters-xstate-workshop)\*\*\*\*
* **Presentation**: [https://static.frontendmasters.com/resources/2020-05-14-state-machines-xstate/state-machine-xstate.pdf](https://static.frontendmasters.com/resources/2020-05-14-state-machines-xstate/state-machine-xstate.pdf)

## Learnings

#### API Request 

* States
  * pending /stopping
  * failed
  * rejected
  * resolved
  * stopped
* Actions
  * Fetch / FetchAll / Query / Update / Set / Delete / Create / invoke
  * Stop
  * Retry

#### Component 

* States
  * init
  * loading
  * loaded / idle 
  * 
* Actions
  * 
* 
#### Ideas for Ngrx Entity

```text
const entitySate = {
  state,
  retries,
  query
}

const componentState = {
  state,
  history, // a state before the last transaction. This can be used for re-hydration
};
```







## Notes



![](../../.gitbook/assets/image%20%28212%29.png)



![](../../.gitbook/assets/image%20%28214%29.png)

![](../../.gitbook/assets/image%20%28219%29.png)

![](../../.gitbook/assets/image%20%28215%29.png)

* Finite States \(Mode/Status\): idle, pending, resolved, rejected
* Transitions: from Idle to pending
* Events: fetch, resolve, reject
* Initial state 

![](../../.gitbook/assets/image%20%28222%29.png)

* Final State 

![](../../.gitbook/assets/image%20%28210%29.png)

### Creating a state machine

![](../../.gitbook/assets/image%20%28206%29.png)

```javascript
const machine = {
    initial: 'idle',
    states: {
        idle: {
            on: {
                FETCH: 'pending'
            },
        },
        pending: {
            on: {
                RESOLVE: 'resolved',
                REJECT: 'rejected'
            },
        },
        resolved: {},
        rejected: {}
    }

};

const transition = (state, event) => {
    return machine.states[state]?.on?.[event] || state;
};
output(transition('idle', 'FETCH'))
```

![](../../.gitbook/assets/image%20%28284%29.png)

The interpreter keeps track of the current state and knows what to do after effect happen a 

```typescript
// Creating the interpreter
let currentState = machine.initial;

const send = (event)=>{
  const nextState = transition(currentState,event);
  console.log({nextState})
  currentState = nextState;
}

```

![](../../.gitbook/assets/image%20%28276%29.png)

![](../../.gitbook/assets/image%20%28281%29.png)

![](../../.gitbook/assets/image%20%28275%29.png)

![](../../.gitbook/assets/image%20%28279%29.png)

![](../../.gitbook/assets/image%20%28285%29.png)

![](../../.gitbook/assets/image%20%28286%29.png)

### Guarded Transitions

![](../../.gitbook/assets/image%20%28274%29.png)

### Transient Transitions

![](../../.gitbook/assets/image%20%28273%29.png)

### Delayed Transtions

![](../../.gitbook/assets/image%20%28287%29.png)

![](../../.gitbook/assets/image%20%28288%29.png)

![](../../.gitbook/assets/image%20%28282%29.png)

### Nested or Hierarchical States

![](../../.gitbook/assets/image%20%28280%29.png)

![](../../.gitbook/assets/image%20%28283%29.png)

### History States

![](../../.gitbook/assets/image%20%28278%29.png)

#### Parallel / Orthogonal states

![](../../.gitbook/assets/image%20%28272%29.png)

### The actor model

![](../../.gitbook/assets/image%20%28277%29.png)



\*\*\*\*

\*\*\*\*

