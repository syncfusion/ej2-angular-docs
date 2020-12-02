---
title: "Show different types of Angular Toast"
component: "Toast"
description: "This example demonstrates how to create different types of Essential JS 2 Toast component is displayed on a screen."
---

# Show different types of Toast

The Essential JS 2 Toast has the following predefined styles that can be defined using the [`cssClass`](../../api/toast#cssclass) property for achieving different types of toast.

| Class | Description |
| -------- | -------- |
| e-success | Used to represent a positive Toast. |
| e-info |  Used to represent an informative Toast. |
| e-warning | Used to represent a Toast with caution. |
| e-danger | Used to represent a negative Toast. |

{% tab template="toast/toast", sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id="toast_target"></div>
        <button ejs-button [isPrimary]="true" (click)="btnClick($event)">Show Toast</button>
        <ejs-toast #element (created)="onCreate($event)"  [position] = 'position' > </ejs-toast>
        `
})

export class AppComponent {
    @ViewChild('element') element;
    public position = { X: 'Right', Y: 'Bottom' };
    public toasts = [
    { title: 'Warning !', content: 'There was a problem with your network connection.', cssClass: 'e-toast-warning' },
    { title: 'Success !', content: 'Your message has been sent successfully.', cssClass: 'e-toast-success'},
    { title: 'Error !', content: 'A problem has been occurred while submitting your data.', cssClass: 'e-toast-danger' },
    { title: 'Information !', content: 'Please read the comments carefully.', cssClass: 'e-toast-info' } ];
    public toastFlag: number = 0;


    onCreate() {
      this.element.show(this.toasts[this.toastFlag]);
      ++this.toastFlag;
    }
    btnClick() {
      this.toastShow();
    }
    toastShow() {
          setTimeout(
        () => {
            this.element.show(this.toasts[this.toastFlag]);
            ++this.toastFlag;
              if (this.toastFlag === (this.toasts.length)) {
                this.toastFlag = 0;
               }
        }, 0);
    }
}
```

{% endtab %}