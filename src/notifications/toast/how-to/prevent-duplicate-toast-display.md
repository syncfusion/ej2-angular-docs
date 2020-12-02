---
title: "Prevent duplicate Angular Toast display"
component: "Toast"
description: "This example demonstrates how to prevent the identical same Syncfusion angular Toast Component is displayed on a screen."
---

# Prevent duplicate Toast display

You can prevent identical same toast displaying in a screen by event function. You can terminate the toast displaying process by setting cancel event property in [`beforeOpen`](../../api/toast#beforeopen) Event.

Here below sample demonstrates preventing duplicate title Toast element displaying, with custom code blocks.

{% tab template="toast/toast", sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
      <div id="toast_target"></div>
      <button ejs-button [isPrimary]="true" (click)="btnClick($event)">Show Toast</button>
      <ejs-toast #element (created)="onCreate($event)" (beforeOpen)="onBeforeOpen($event)" (close)='onClose($event)' [position]='position' > </ejs-toast>
      `
})

export class AppComponent {
    @ViewChild('element', null) element;
  public position = { X: 'Center' };
  public prevDuplicates: boolean = false;
  public toastFlag: number = 0;

  public toasts = [
    { title: 'Warning !', content: 'There was a problem with your network connection.', isOpen: false },
    { title: 'Success !', content: 'Your message has been sent successfully.', isOpen: false },
    { title: 'Error !', content: 'A problem has been occurred while submitting your data.', isOpen: false }
  ];

  onBeforeOpen(e) {
    if(this.preventDuplicate(e)){
      e.cancel =true;
    };
  }

  preventDuplicate(e) {
    for (let i: number = 0; i < this.toasts.length; i++) {
      if (this.toasts[i].title === e.options.title && !this.toasts[i].isOpen) {
        this.toasts[i].isOpen = true;
        return false;
      }
    }
    return true;
  }

  onClose(e) {
    for (let i: number = 0; i < this.toasts.length; i++) {
      if (this.toasts[i].title === e.options.title) {
        this.toasts[i].isOpen = false;
      }
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
}
```

{% endtab %}