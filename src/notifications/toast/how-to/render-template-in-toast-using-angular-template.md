---
title: "Render template in Angular Toast using ng-template"
component: "Toast"
description: "This example demonstrates how to render other Essential JS 2 components into Essential JS 2 Toast component using ng-template."
---

# Render template in Toast using ng-template

You can also render the template support in Toast using the Angular **ng-template**. We need to use this ng-template within the e-toast tag with #template attribute, which is mandatory to render template property. Also you don't need to use the template property if you used this ng-template.

{% tab template="toast/toast", sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <button ejs-button [isPrimary]="true" (click)="btnClick($event)">Show Toast</button>
        <ejs-toast #element (created)="onCreate($event)"  [position] = 'position' >
          <ng-template #template>
             <div id="template_toast_ele">
               <ejs-datepicker></ejs-datepicker>
             </div>
            </ng-template>
           </ejs-toast>`
})

export class AppComponent {
   @ViewChild('element') element;
     public position = { X: 'Right', Y: 'Bottom' };

    onCreate(){
         setTimeout(
        () => {
        this.element.show();
        }, 200);
    }

    btnClick() {
      this.toastShow();
    }

    toastShow() {
      this.element.show();
    }

}
```

{% endtab %}