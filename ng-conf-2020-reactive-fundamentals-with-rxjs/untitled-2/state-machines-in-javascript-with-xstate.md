# State Machines in Javascript with XState

## Details

* **URL:** [**https://frontendmasters.com/courses/xstate/introduction/**](https://frontendmasters.com/courses/xstate/introduction/)\*\*\*\*
* **Source Code:** [**https://github.com/davidkpiano/frontend-masters-xstate-workshop**](https://github.com/davidkpiano/frontend-masters-xstate-workshop)\*\*\*\*
* **Presentation**: [https://static.frontendmasters.com/resources/2020-05-14-state-machines-xstate/state-machine-xstate.pdf](https://static.frontendmasters.com/resources/2020-05-14-state-machines-xstate/state-machine-xstate.pdf)

## Learnings

* States
  * 



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

![](../../.gitbook/assets/image%20%28272%29.png)

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





\*\*\*\*

