---
description: >-
  quicklink implementation for Angular. It provides router preloading strategy
  which automatically downloads the lazy-loaded modules associated with all the
  visible links on the screen.
---

# Angular quicklink Preloading Strategy

{% embed url="https://github.com/mgechev/ngx-quicklink" %}

{% code title="shared.module.ts" %}
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
{% endcode %}

{% code title="app.module.ts" %}
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
{% endcode %}

