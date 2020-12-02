---
title: "Angular Toast Template"
component: "Toast"
description: "The Essential JS 2 Toast control template section explains how to customize the toast control as needed."
---

# Template

Template property can be given as the `HTML element` that is either a `string`  or a `query selector`.

The HTML element tag can be given as a string for the template property.

```typescript
template: "<div>Toast Content</div>"

```

The template property also allows getting template content through query `selector`. Here, element 'ID' attribute is specified in the template.

```typescript
template: "#Template"

```

{% tab template="toast/toast", sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id="toast_target"></div>
        <button ejs-button [isPrimary]="true" (click)="btnClick($event)">Show Toast</button>
        <ejs-toast #element id='element' (created)="onCreate($event)" [template]='templateEle' extendedTimeOut= '0' timeOut= '120000' [position] = 'position' > </ejs-toast>`
})

export class AppComponent {
    @ViewChild('element') element;
    public position = { X: 'Right', Y: 'Bottom' };
    public templateEle = document.getElementById('template_toast_ele').innerHTML;

    onCreate() {
      this.toastShow();
    }
    btnClick() {
      this.toastShow();
    }
    toastShow() {
          setTimeout(
        () => {
            this.element.show();
        }, 700);
    }
}

```

{% endtab %}

## See Also

* [Add template dynamically](./how-to/add-dynamic-template/)
