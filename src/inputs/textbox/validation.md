---
title: "Validation"
component: "Textbox"
description: "Covers how to apply different validation styles to the text box (input) control such as error, warning, and success with a ripple effect."
---

# Validation

The TextBox supports three types of validation styles namely `error`, `warning`, and `success`. These states are
enabled by adding corresponding classes `.e-error`, `.e-warning`, or `.e-success` to the input parent element.

{% tab template="textbox/getting-started", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">
                <input class="e-input e-warning" type="text" placeholder="Input with warning"/>
                <div class="e-input-group e-error">
                    <input class="e-input" type="text" (focus)="focusIn($event.target)"
                    placeholder = "Input with error" (blur)="focusOut($event.target)"/>
                </div>
                <div class="e-input-group e-success">
                    <input class="e-input" type="text" (focus)="focusIn($event.target)"
                    placeholder = "Input with success" (blur)="focusOut($event.target)"/>
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
