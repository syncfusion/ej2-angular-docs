---
title: "Close the Angular Toast with click/tap"
component: "Toast"
description: "This example demonstrates how to close the Syncfusion angular Toast Component with a click or tap operation."
---

# Close the Toast with click/tap on toast

In default, toast gets expired based on timeOut value. You can customize toast hiding process, You can customize only hide with click/tap action by setting event args in [clicked](../../api/toast/toastClickEventArgs#clicktoclose) callback function with [static Toast](../../toast/timeout#static-toast).

{% tab template="toast/toast", sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id="toast_target"></div>
            <button ejs-button (click)="btnClick($event)" >Show Toast</button>
        <ejs-toast #element (created)="onCreate($event)" (click)= "onClick($event)" timeOut='0'  [position] = 'position' >
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
    public position = { X: 'Left', Y: 'Bottom' };

    onClick(e) {
      e.clickToClose = true;
    }

    onCreate() {
      this.element.show();
    }

    btnClick() {
      this.element.show();
    }
}
```

{% endtab %}