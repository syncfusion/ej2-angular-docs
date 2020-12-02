---
title: "Create ButtonGroup with icons"
component: "ButtonGroup"
description: "ButtonGroup how to section, create ButtonGroup using util function, icons, form submit, show selected state on initial render."
---

# Create ButtonGroup with icons

To create ButtonGroup with icons, `iconCss` property of the button component can be used.

The following example illustrates how to create ButtonGroup with icons.

{% tab template="button-group/icon", sourceFiles="app/**/*.ts, styles.css", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render ButtonGroup. -->
               <div class='e-btn-group'>
                  <button ejs-button iconCss='e-icons e-left-icon'>Left</button>
                  <button ejs-button iconCss='e-icons e-middle-icon'>Right</button>
                  <button ejs-button iconCss='e-icons e-right-icon'>Middle</button>
                </div>`
})

export class AppComponent { }
```

{% endtab %}