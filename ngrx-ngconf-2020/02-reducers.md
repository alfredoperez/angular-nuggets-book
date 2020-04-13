# 02 - Reducers

![](../.gitbook/assets/image%20%2820%29.png)

![](../.gitbook/assets/image%20%2811%29.png)

The following is an example of a piece of State

![](../.gitbook/assets/image%20%2821%29.png)

Then we can define the initial state using the State interface

![](../.gitbook/assets/image%20%2813%29.png)

To create a reducer 

![](../.gitbook/assets/image%20%281%29.png)

Reducers are in a shared folder because the state is global

![](../.gitbook/assets/image%20%2840%29.png)

![](../.gitbook/assets/image.png)

To make AOT the reducer needs to be wrappped into a function

![](../.gitbook/assets/image%20%2810%29.png)

The index file declares the state

![](../.gitbook/assets/image%20%2812%29.png)

Modify data in a immutable way

![](../.gitbook/assets/image%20%2828%29.png)

### Recommendations from NgRx Creators

* States and reducers need to go in the shared directory  that can be globally accessed.
* States and reducers need to be in the same reducer file, as the reducer is working directly with the defined state.
  * This was their recommendation, but it wasn't a strong opinion. We should evaluate whether it's preferable to have a separate `.state` file, in the same directory.

