---
description: 'Entity, Meta-Reducers, ngrx/data, and ngrx/component'
---

# 05 - Other tools

### Entities

{% file src="../.gitbook/assets/image-entity1.png" %}

* Common CRUD operations are basically working with collections.
  * Trying to update many items in the collections at the same time can be problematic.
* Use Entity to assist performing operations on collections.
  * Using ngrx/entity is performant

{% file src="../.gitbook/assets/image-entity1.png" %}

{% file src="../.gitbook/assets/image-entity2.png" %}

{% file src="../.gitbook/assets/image-entity3.png" %}

{% file src="../.gitbook/assets/image-entity4.png" %}

{% file src="../.gitbook/assets/image-entity5.png" %}

{% file src="../.gitbook/assets/image-entity6.png" %}

{% file src="../.gitbook/assets/image-entity7.png" %}

{% file src="../.gitbook/assets/image-entity8.png" %}

### Meta-Reducers

{% file src="../.gitbook/assets/image-metareducer1.png" %}

{% file src="../.gitbook/assets/meta-reducer.gif" %}

### @ngrx/data

* Goal is to separate what data the client needs from how to retrieve it
* Large apps may not scale so well with app with large set of entities
* NgRx Data is built with NgRx State for full reactivity, and simplifies the code bulkiness
* You don’t need to use NgRx State to make use of NgRx data.

### @ngrx/component

* New in NgRx version 9 with Ivy support!
* @ngrx/components uses observables to detect changes and schedules the change detecction
* Instead of "foo$ \| async", use "foo$ \| ngRxPush"
* Instead of "_ngIf=foo$ \| async as foo" use "_ngrxLet=foo$"

