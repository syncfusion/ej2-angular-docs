---
title: "Customize the textbox background-color and text-color"
component: "Textbox"
description: "Covers customization of the text box component such as a rounded corner, disabled, read-only state, background color, and font color."
---

# Customize the textbox background-color and text-color

You can customize the textbox styles such as background-color, text-color and border-color by overriding its default styles.

> To change the styles of the `floating label`, you must override the style to the input element.

{% tab template="textbox/textbox-customize", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">
                <label> Normal Input </label>
                <div class="e-input-group">
                    <input (focus)="focusIn($event.target)" (blur)="focusOut($event.target)" class="e-input" type="text" placeholder="First Name">
                </div>
                 <label> Floating Input </label>
                <div class="e-float-input">
                    <input (focus)="focusIn($event.target)" (blur)="focusOut($event.target)" type="text" required>
                    <span class="e-float-line"></span>
                    <label class="e-float-text">Last Name</label>
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
