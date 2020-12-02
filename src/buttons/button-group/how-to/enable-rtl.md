---
title: "Enable RTL"
component: "ButtonGroup"
description: "ButtonGroup how to section, create ButtonGroup using util function, icons, form submit, show selected state on initial render."
---

# Enable RTL

ButtonGroup supports RTL functionality. This can be achieved by adding `e-rtl` class to the target element.

The following example illustrates how to create ButtonGroup with RTL support.

{% tab template="button-group/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render ButtonGroup with RTL. -->
               <div class='e-btn-group e-rtl'>
                   <button ejs-button>HTML</button>
                   <button ejs-button>CSS</button>
                   <button ejs-button>Javascript</button>
               </div>`
})

export class AppComponent { }
```

{% endtab %}