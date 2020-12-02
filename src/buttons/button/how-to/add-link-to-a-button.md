---
title: "Add link to a Button"
component: "Button"
description: "Angular Button how to section, block button, repeat button, tooltip for Button, customization of button appearance, input and anchor elements."
---

# Add link to a Button

Link can be added to the Button by adding `e-link` using `cssClass` property and `<a>` tag with `href` attribute should be added inside the button element.

The following example illustrates how to add link to a Button.

{% tab template="button/round-button", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render Button. -->
               <button ejs-button cssClass='e-link'><a href="https://www.google.com/" target='_blank'>Go to google</a></button>`
})

export class AppComponent { }
```

{% endtab %}