---
title: "Set the Read-only TextBox"
component: "Textbox"
description: "Covers customization of the text box component such as a rounded corner, disabled, read-only state, background color, and font color."
---

# Set the Read-only TextBox

You can make the TextBox as `read-only` by setting the `readonly` attribute to the input element.

{% tab template="textbox/getting-started", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">
                <input class="e-input" type="text" value="John"  placeholder="Enter Name" readonly />
                <div class="e-float-input">
                    <input type='text' value="John" required readonly/>
                    <span class="e-float-line"></span>
                    <label class="e-float-text e-label-top">Enter Name</label>
                </div>
              </div>`
})

export class AppComponent {}
```

{% endtab %}
