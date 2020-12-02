---
title: "Add dynamic template for Angular Toast"
component: "Toast"
description: "This example demonstrates how to dynamically change a template for display in multiple Syncfusion Angular Toast component."
---

# Add dynamic template

Toast can support to change templates in dynamically, with displaying in multiple toasts. We can change Toast properties while calling in [`show`](../../api/toast#show) method.

{% tab template="toast/toast", sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id="toast_target"></div>
        <div id='templateToast' style="display: none;color:red"> System affected by virus !!! </div>
        <button ejs-button [isPrimary]="true" (click)="btnClick($event)">Show Toast</button>
        <ejs-toast #element (created)="onCreate($event)"  [position] = 'position' > </ejs-toast>
        `
})

export class AppComponent {
    @ViewChild('element') element;
    public position = { X: 'Right', Y: 'Bottom' };
    public toasts = [ { template: '2 Mail has received'},{ template: 'User Guest Logged in'},{ template: 'Logging in as Guest'},{ template: 'Ticket has reserved '},{ template: '#templateToast' }]
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