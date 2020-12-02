---
title: "Restrict the maximum Angular toast to show"
component: "Toast"
description: "This example demonstrates how to restrict the maximum Essential JS 2 Toast count is displayed on a screen."
---

# Restrict the maximum toast to show

You can restrict the maximum toast count by event callback function. You can terminate the toast displaying process by setting cancel event property in [`beforeOpen`](../../api/toast#beforeopen) Event.

Here below sample demonstrates restrict toast displaying up to 3. You can restrict by your own count with custom code blocks.

{% tab template="toast/toast", sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id="toast_target"></div>
        <button ejs-button [isPrimary]="true" (click)="btnClick($event)">Show Toast</button>
        <ejs-toast #element (created)="onCreate($event)" (beforeOpen)="onBeforeOpen($event)"  [position] = 'position' > </ejs-toast>
        `
})

export class AppComponent {
    @ViewChild('element') element;
    public position = { X: 'Right', Y: 'Bottom' };
    public toasts = [
    { title: 'Warning !', content: 'There was a problem with your network connection.' },
    { title: 'Success !', content: 'Your message has been sent successfully.' },
    { title: 'Error !', content: 'A problem has been occurred while submitting your data.' },
    { title: 'Information !', content: 'Please read the comments carefully.' }];
    public maxCount: number = 3;
    public toastFlag:number = 0;

    onBeforeOpen(e) {
      if (this.maxCount === this.element.element.childElementCount) {
   e.cancel =true;
  } else {
    e.cancel = false;
  }
    }

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
    ngAfterViewInit() {
    }
}
```

{% endtab %}