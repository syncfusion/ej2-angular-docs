---
title: "Disable"
component: "ButtonGroup"
description: "ButtonGroup how to section, create ButtonGroup using util function, icons, form submit, show selected state on initial render."
---

# Disable

## Particular button

To disable a particular button in a ButtonGroup, `disabled` attribute should be added to corresponding button element.

## Whole ButtonGroup

To disable whole ButtonGroup, `disabled` attribute should be added to all the button elements.

The following example illustrates how to disable the particular and the whole ButtonGroup.

{% tab template="button-group/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render ButtonGroup. -->
               <div class='e-btn-group'>
                    <button ejs-button>HTML</button>
                    <button ejs-button [disabled]="true">CSS</button>
                    <button ejs-button>Javascript</button>
                </div>
                <div class='e-btn-group'>
                    <button ejs-button [disabled]="true">HTML</button>
                    <button ejs-button [disabled]="true">CSS</button>
                    <button ejs-button [disabled]="true">Javascript</button>
                </div>`
})

export class AppComponent { }
```

{% endtab %}

> To disable radio/checkbox type ButtonGroup, the `disabled` attribute should be added to the particular input element.