---
description: >-
  quicklink implementation for Angular. It provides router preloading strategy
  which automatically downloads the lazy-loaded modules associated with all the
  visible links on the screen.
---

# Angular quicklink Preloading Strategy

{% embed url="https://github.com/mgechev/ngx-quicklink" %}

{% code-tabs %}
{% code-tabs-item title="shared.module.ts" %}
```typescript
import { QuicklinkModule } from 'ngx-quicklink';
...

@NgModule({
  imports: [QuicklinkModule],
  declarations: [...],
  exports: [QuicklinkModule]
})
export class SharedModule {}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="app.module.ts" %}
```typescript
import { QuicklinkModule } from 'ngx-quicklink';
...

@NgModule({
  imports: [QuicklinkModule],
  declarations: [...],
  exports: [QuicklinkModule]
})
export class SharedModule {}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

