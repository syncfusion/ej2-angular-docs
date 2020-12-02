---
title: "Create a Block Button"
component: "Button"
description: "Angular Button how to section, block button, repeat button, tooltip for Button, customization of button appearance, input and anchor elements."
---

# Create a Block Button

You can customize a button into a block button that will span the entire width of its parent element.
To create a block button, set the [`cssClass`](../../api/button#cssclass) property as `e-block`.

{% tab template="button/block", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls:['styles.css'],
    template:  `<!-- Block button. -->
                <button ejs-button cssClass="e-block">Block Button</button>

                <!-- Primary block button. -->
                <button ejs-button cssClass="e-block e-primary">Block Button</button>

                <!-- Success block button. -->
                <button ejs-button cssClass="e-block e-success">Block Button</button>`
})

export class AppComponent { }
```

{% endtab %}