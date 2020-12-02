---
title: "Enable ripple"
component: "ButtonGroup"
description: "ButtonGroup how to section, create ButtonGroup using util function, icons, form submit, show selected state on initial render."
---

# Enable ripple

Ripple can be enabled by importing `enableRipple` method from `ej2-base` and set enableRipple as `true`.

The following example illustrates how to enable ripple for ButtonGroup.

<!-- markdownlint-disable MD033 -->

{% tab template="button-group/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render ButtonGroup. -->
               <div class="e-btn-group">
                    <button ejs-button>HTML</button>
                    <button ejs-button>CSS</button>
                    <button ejs-button>Javascript</button>
                </div>`
})

export class AppComponent { }
```

{% endtab %}