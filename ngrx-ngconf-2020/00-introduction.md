---
description: A reactive state of mind with Angular and NgRx
---

# 00 - Introduction

## The Goal

Understand the architectural implications of NgRx and how to build Angular applications with it

### How does NgRx work?

![](../.gitbook/assets/screen-shot-2020-05-31-at-3.22.31-pm.png)

Well, it's really supposed to work a lot like the components. Components have inputs & outputs. What are the inputs & outputs of NgRx?

![&quot;States flow down, changes flow up&quot;](../.gitbook/assets/screen-shot-2020-05-31-at-3.25.47-pm.png)

### Inputs & Outputs offer Indirection

![](../.gitbook/assets/screen-shot-2020-05-31-at-3.29.19-pm.png)

![](../.gitbook/assets/screen-shot-2020-05-31-at-3.29.30-pm.png)

### Responsibilities

* Containers connect data to components
* Effects trigger side effects
* Reducers handle transitions

![](../.gitbook/assets/image%20%2891%29.png)

