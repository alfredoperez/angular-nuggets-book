# Unit Testing Angular Like a Boss

**Author:** Joe Eames  
**Link**: [https://thinkster.io/tutorials/unit-testing-angular-like-a-boss-workshop](https://thinkster.io/tutorials/unit-testing-angular-like-a-boss-workshop)

## Writing Good Tests

* Structure in **Arrange, Act,  and Assert**
* **DAMP** and **DRY**. It is ok to have some duplication on tests. Repeat yourself if necessary to make it easy to read
* Tell the story.
  *  A test should be a complete story, all within the `it()` 
  * **Should not need to look around much to understand the test**
  * Techniques:
    * Remove less interesting setup to `beforeEach()`
    * **Keep critical setup within the `it()`**
    * Include all of the "Act" and "Assert" test parts are in the `it()` clause

{% hint style="info" %}
Do not be afraid of repeating code for unit tests and make sure to have all the important parts of the test inside the`it`
{% endhint %}

* Only test the unit and not its dependents or dependencies
* Use Test Doubles to isolate dependencies

{% hint style="info" %}
Prefer to use spies over mocks to avoid having to mock all the dependencies and instead mock the method returned value when it is needed
{% endhint %}

### Best Practices

* Prefer to test the initial state separately
* Every test should test a single state case. It is possible to have multiple assertions to test a single test 

```typescript
it('should add a new message to the list when add is called', () => {
    const service = new MessageService();

    const message = 'new Message';
    service.add('new Message');

    expect(service.messages[0]).toBe(message);
    expect(service.messages.length).toBe(1);
  });
```

* Create a test for every different result or behavior that the method has
* Make sure to include boundary testing when needed. In the following, it means to test the boundaries that give different result \(E.g. 5,10,20, 25\) 

```typescript
transform(value: number): string {
    if (value < 10) {
      return value + ' (weak)';
    } else if (value >= 10 && value < 20) {
      return value + ' (strong)';
    } else {
      return value + ' (unbelievable)';
    }
  }
```

* Tests should not expect a specific order. Tests should be able to run isolated.
* Unit tests help to write better code, documents the requirements of code

## Unit Test Types in Angular

* **Isolated**: only the class, mocking everything
* **Integration**: Compiling components and using the injector 
  * **Shallow**: Builds the component via the TestBed and mock out or ignore related components
  * **Deep**: include all components

#### Component Fixture

Access to the component, its DOM, and change detection

* `componentInstance` - the instance of the component created by TestBed
* `debugElement`- provides insight into the component and its DOM element
* `nativeElement`- the native DOM element at the root of the component
* `detectChanges()` - trigger a change detection cycle for the component

#### Debug Element

Insights into the component's DOM representation

* parent / children - the immediate parent or children of this `DebugElement`
* `query`\(predicate\) - search for one descendant that matches
* `queryAll`\(predicate\) - search for many descendants that match
* injector - this component's injector
* listeners - this callback handlers for this component's events and `@Outputs`
* `triggerEventHandler`\(listener\) - trigger an event or `@Output`

#### Querying the DOM

* NativeElement provides:
  * `querySelector`\(cssSelector\)
  * `querySelectorAll`\(cssSelector\)
* DebugElement provides:
  * `query`\(predicate\)
  * `queryAll`\(predicate\)
* Predicates can be created by helpers:
  * `By.css`\(selector\)
  * `By.directive`\(DirectiveType\)

#### Interacting with the  DOM

* `nativeElement` - can't use outside the browser
  * `dispatchEvent`
  * `textContent`
* `debugElement` - doesn't have access to textContent
  * `triggerEventHandler`
  * properties
  * attributes
  * classes
  * styles

###   



