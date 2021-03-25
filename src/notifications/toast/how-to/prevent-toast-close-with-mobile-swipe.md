---
title: "Prevent toast close with mobile swipe"
component: "Toast"
description: "This example demonstrates how to prevent the identical same Syncfusion angular Toast Component is displayed on a screen."
---

# Prevent toast close with mobile swipe

You can prevent the toast close with mobile swipe action by setting [beforeClose](../../api/toast/#beforeClose) argument cancel value to true while argument type as a swipe. The following code shows how to prevent toast close with mobile swipe.

The following sample demonstrates preventing toast close with mobile swipe element displaying with custom code blocks.

{% tab template="toast/toast", sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id="toast_target"></div>
        <button ejs-button [isPrimary]="true" (click)="btnClick($event)">Show Toast</button>
        <ejs-toast #toastObj (created)="onCreate($event)" (beforeClose)="onBeforeClose($event)" [position] = 'position' >
            <ng-template #title>
                <div>Matt sent you a friend request</div>
            </ng-template>
            <ng-template #content>
                <div>Hey, wanna dress up as wizards and ride our hoverboards?</div>
            </ng-template>
        </ejs-toast>`
})

export class AppComponent {
    @ViewChild('toastObj') element;
    public position = { X: 'Right' };

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
    onBeforeClose(e){
        if (e.type === "swipe") {
            e.cancel = true;
        }
    }
}
```

{% endtab %}