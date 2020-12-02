---
title: "Set the Rounded Corner"
component: "Textbox"
description: "Covers customization of the text box component such as a rounded corner, disabled, read-only state, background color, and font color."
---

# Set the Rounded Corner

Render the TextBox with `rounded corner` by adding the `e-corner` class to the input parent element.

>This rounded corner visible only in box model input component

{% tab template="textbox/rounded-corner", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">
                <div class="e-input-group e-corner">
                    <input class="e-input" type="text" (focus)="focusIn($event.target)"
                    placeholder = "Enter Date" (blur)="focusOut($event.target)"/>
                    <span class="e-input-group-icon e-input-popup-date" ></span>
                </div>
                <div class="e-float-input e-input-group e-corner">
                    <input type='text' required />
                    <span class="e-float-line"></span>
                    <label class="e-float-text">Enter Date</label>
                    <span class="e-input-group-icon e-input-popup-date" ></span>
                </div>
               </div>`
})

export class AppComponent {
    public focusIn(target: HTMLElement): void {
        target.parentElement.classList.add('e-input-focus');
    }

    public focusOut(target: HTMLElement): void {
        target.parentElement.classList.remove('e-input-focus');
    }
}
```

{% endtab %}
