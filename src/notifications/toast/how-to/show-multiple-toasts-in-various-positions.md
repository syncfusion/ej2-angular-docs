---
title: "Show multiple Angular Toasts in various positions"
component: "Toast"
description: "This example demonstrates how to create multiple Essential JS 2 Toast component in various position on the screen."
---

# Show multiple Toast in various position

In default Toast position only updates once visible toasts get destroyed. If You needs to display multiple toasts with different position means needs to initiate another toast for achieving this.

Here below sample demonstrates to add multiple toasts adding in the different position.

{% tab template="toast/toast", sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id="toast_target"></div>
        <div style="display:inline-block">
          <div style="margin-right:10px;display:inline-block">
           <button ejs-button (click)="btnRightClick($event)">Show Left Position Toast</button>
          </div>
          <div style="display:inline-block">
           <button ejs-button (click)="btnClick($event)" >Show Right Position Toast</button>
          </div>
        </div>
        <ejs-toast #element (created)="onCreate($event)" [position] = 'position' >
              <ng-template #title>
                  <div>Warning !</div>
              </ng-template>
              <ng-template #content>
                  <div>There was a problem with your network connection.</div>
              </ng-template>
       </ejs-toast>
        <ejs-toast #rightToast (created)="onCreate1($event)" [position] = 'position1' >
              <ng-template #title>
                  <div>Success !</div>
              </ng-template>
              <ng-template #content>
                  <div>Your message has been sent successfully.</div>
              </ng-template>
         </ejs-toast>
        `
})

export class AppComponent {
    @ViewChild('element') element;
    @ViewChild('rightToast') rightToast;
    public position = { X: 'Left', Y: 'Bottom' };
    public position1 = { X: 'Right', Y: 'Bottom' };


   onCreate1() {
     this.rightToast.show();
   }

    onCreate() {
      this.element.show();
    }
    btnRightClick() {
      this.element.show();
    }
    btnClick() {
      this.rightToast.show();
    }
}
```

{% endtab %}