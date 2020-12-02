---
title: "Angular Toast Accessibility"
component: "Toast"
description: "The Syncfusion Angular Toast component has accessibility support to access the features via keyboard, screen readers or other assistive technology devices."
---

# Accessibility

The Toast component has been designed keeping in mind the [WAI-ARIA](http://www.w3.org/WAI/PF/aria-practices/) specifications, by applying
 the prompt WAI-ARIA roles, states, and properties along with the keyboard support. Thus, making it usable for people who use assistive WAI-ARIA Accessibility supports that is achieved through the attributes.
It helps to provides information about the elements in a document for assistive technology.
The component implements the keyboard navigation support by following the
  [WAI-ARIA practices](https://www.w3.org/TR/wai-aria-practices/) and tested in major screen readers.

## ARIA attributes

<!-- markdownlint-disable MD033 -->

| Class | Description |
| -------- | -------- |
| role | <b>alert:</b> <br/>   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Identifies the element as the container where alert content will be added or updated. |

{% tab template="toast/toast", sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id="toast_target"></div>
        <button ejs-button [isPrimary]="true" (click)="btnClick($event)">Show Toast</button>
        <ejs-toast #element (created)="onCreate($event)" [position] = 'position' >
              <ng-template #title>
                  <div>Matt sent you a friend request</div>
              </ng-template>
              <ng-template #content>
                  <div>Hey, wanna dress up as wizards and ride our hoverboards?</div>
              </ng-template>
    </ejs-toast>
        `
})

export class AppComponent {
    @ViewChild('element') element;
    public position = { X:'Right' };

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