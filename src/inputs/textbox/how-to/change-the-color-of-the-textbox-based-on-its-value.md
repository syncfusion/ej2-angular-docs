---
title: "Change the color of the TextBox based on its value"
component: "Textbox"
description: "Covers customization of the text box component such as a rounded corner, disabled, read-only state, background color, and font color."
---

# Change the color of the TextBox based on its value

You can change the color of the TextBox by validating its value using regular expression in the `keyup` event
for predicting the numeric values as demonstrated in the following code sample.

{% tab template="textbox/getting-started", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">
                <label> Normal Input </label>
                <div class="e-input-group">
                    <input class="e-input" type="text" (focus)="focusIn($event.target)"
                    placeholder = "Enter numeric values" (blur)="focusOut($event.target)" (keyup)="onKeyup($event)"/>
                </div>
                 <label> Floating Input </label>
                <div class="e-float-input">
                    <input type="text"(focus)="focusIn($event.target)" (blur)="focusOut($event.target)" (keyup)="onKeyup($event)" required/>
                    <span class="e-float-line"></span>
                    <label class="e-float-text">Enter numeric values</label>
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
    public onKeyup(event): void {
    let str = event.target.value.match(/^[0-9]+$/);
    if (!((str && str.length > 0)) && event.target.value.length) {
       event.target.parentElement.classList.add('e-error');
    } else {
      event.target.parentElement.classList.remove('e-error');
    }
  }
}

```

{% endtab %}
