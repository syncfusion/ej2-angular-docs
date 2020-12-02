---
title: "Set the Disabled State"
component: "Textbox"
description: "Covers customization of the text box component such as a rounded corner, disabled, read-only state, background color, and font color."
---

# Set the Disabled State

Disable the TextBox by adding the `e-disabled` to the input parent element and set `disabled` attribute to the input element.

{% tab template="textbox/getting-started", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">
                <input class="e-input" type="text"  placeholder="Enter Name" disabled />
                <div class="e-float-input e-disabled">
                    <input type='text' required disabled/>
                    <span class="e-float-line"></span>
                    <label class="e-float-text">Enter Name</label>
                </div>
              </div>`
})

export class AppComponent {}
```

{% endtab %}
