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
Prefer to use spies over mocks to avoid having to mock all the dependencies and instead mcok the method returned value when it is needed
{% endhint %}

