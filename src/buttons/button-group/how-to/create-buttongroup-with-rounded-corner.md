---
title: "Create ButtonGroup with rounded corner"
component: "ButtonGroup"
description: "ButtonGroup how to section, create ButtonGroup using util function, icons, form submit, show selected state on initial render."
---

# Create ButtonGroup with rounded corner

The ButtonGroup with rounded corner has round edges on both side. In the ButtonGroup with rounded corner, `e-round-corner` class is to be
added to the target element.

The following example illustrates how to create ButtonGroup with rounded corner.

{% tab template="button-group/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render ButtonGroup. -->
               <div class='e-btn-group e-round-corner'>
                 <button ejs-button>HTML</button>
                 <button ejs-button>CSS</button>
                 <button ejs-button>Javascript</button>
               </div>`
})

export class AppComponent { }
```

{% endtab %}