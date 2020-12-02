---
title: "Create a rounded button"
component: "Button"
description: "Angular Button how to section, block button, repeat button, tooltip for Button, customization of button appearance, input and anchor elements."
---

# Create a rounded button

Button with rounded corner can be achieved by adding `border-radius` CSS property to button element.

In the following example, `e-round-corner` class is defined with `5px` `border-radius` property
and added that class to button element using [`cssClass`](../../api/button#cssclass)
property.

{% tab template="button/round-button", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render Button. -->
               <button ejs-button cssClass='e-round-corner'>Button</button>`
})

export class AppComponent { }
```

{% endtab %}