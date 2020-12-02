---
title: "Show ButtonGroup selected state on initial render"
component: "ButtonGroup"
description: "ButtonGroup how to section, create ButtonGroup using util function, icons, form submit, show selected state on initial render."
---

# Show ButtonGroup selected state on initial render

To show selected state on initial render, `checked` property should to added to the corresponding input element.

The following example illustrates how to show selected state on initial render.

{% tab template="button-group/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render ButtonGroup. -->
               <div class='e-btn-group'>
                    <input type="checkbox" id="checkbold" name="font" value="bold" checked/>
                    <label class="e-btn" for="checkbold">Bold</label>
                    <input type="checkbox" id="checkitalic" name="font" value="italic" />
                    <label class="e-btn" for="checkitalic">Italic</label>
                    <input type="checkbox" id="checkline" name="font" value="underline"/>
                    <label class="e-btn" for="checkline">Underline</label>
                </div>`
})

export class AppComponent { }
```

{% endtab %}