# State Machines in Javascript with XState

## Details

* **URL:** [**https://frontendmasters.com/courses/xstate/introduction/**](https://frontendmasters.com/courses/xstate/introduction/)\*\*\*\*
* **Source Code:** [**https://github.com/davidkpiano/frontend-masters-xstate-workshop**](https://github.com/davidkpiano/frontend-masters-xstate-workshop)\*\*\*\*
* **Presentation**: [https://static.frontendmasters.com/resources/2020-05-14-state-machines-xstate/state-machine-xstate.pdf](https://static.frontendmasters.com/resources/2020-05-14-state-machines-xstate/state-machine-xstate.pdf)



![](../.gitbook/assets/image%20%28210%29.png)



![](../.gitbook/assets/image%20%28212%29.png)

![](../.gitbook/assets/image%20%28215%29.png)

![](../.gitbook/assets/image%20%28213%29.png)

* Finite States \(Mode/Status\): idle, pending, resolved, rejected
* Transitions: from Idle to pending
* Events: fetch, resolve, reject
* Initial state 

![](../.gitbook/assets/image%20%28216%29.png)

* Final State 

![](../.gitbook/assets/image%20%28209%29.png)

### Creating a state machine

![](../.gitbook/assets/image%20%28206%29.png)

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







\*\*\*\*

