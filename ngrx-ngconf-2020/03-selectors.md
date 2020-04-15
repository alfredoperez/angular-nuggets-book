# 03 - Selectors

![](../.gitbook/assets/image%20%2829%29.png)

This is where the performance of NGRX comes, it allows to create reactive applications

Example of selector

![](../.gitbook/assets/image%20%287%29.png)

Selectors are composable:

![](../.gitbook/assets/image%20%2817%29.png)

This can be made explicit

![](../.gitbook/assets/image%20%2816%29.png)

### Tips

* The `createSelector` allows memoized and cached value returns, so try to take advantage of this. 
  * Create selectors that can be used by components that can be used without additional modification.
* When using the selector in the component is recommended to **initialize in the constructor**. If using the strict mode in TypeScript, the compiler will not be able to know that the selectors where initialized on `ngOnInit`
* Instead of having API services transform the data, **transform the data in the selectors**.
  * Easier to test selectors
  * Easier to hydrate the stores with original API data
  * Easier to **re-use and share the original API data** in the store that can be transformed for other view-models.

