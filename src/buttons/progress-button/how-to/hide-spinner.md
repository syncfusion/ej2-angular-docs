---
title: "Hide spinner"
component: "ProgressButton"
description: "Angular ProgressButton how to section, change text content and styles, hide spinner, customize progress."
---

# Hide spinner

You can hide spinner in the ProgressButton by setting the `e-hide-spinner` property to [`cssClass`](../../api/progress-button#cssClass).

{% tab template="progress-button/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<button ejs-progressbutton content='Progress' cssClass='e-hide-spinner' [enableProgress]='true'></button>`
})

export class AppComponent {
}
```

{% endtab %}