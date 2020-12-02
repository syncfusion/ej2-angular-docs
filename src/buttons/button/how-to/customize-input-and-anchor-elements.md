---
title: "Customize input and anchor elements"
component: "Button"
description: "Angular Button how to section, block button, repeat button, tooltip for Button, customization of button appearance, input and anchor elements."
---

# Customize input and anchor elements

You can customize the appearance of the input and anchor elements using predefined styles through
the class property. In the following code snippet, the input element is customized as a link
button by setting the `e-btn e-link` class, and the anchor element is customized as a primary
button by setting the `e-btn e-primary` class.

{% tab template="button/custom", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template:  `<div>
                    <input type="button" id="inputbtn" value="Input Button" class="e-btn e-link">
                </div><br>
                <div>
                    <a id="anchorbtn" class="e-btn e-primary" href="#">Google</a>
                </div>`
})

export class AppComponent { }
```

{% endtab %}