---
title: "Tab How To sections"
component: "Tab"
description: "This example demonstrates how to render other Essential JS 2 components into Essential JS 2 Toolbar component items using ng-template."
---

# Render other components in Toolbar using ng-template

You can render other components inside Toolbar using Angular **ng-template**. Through this, we can add items as other components directly with
all their functionalities to our Toolbar. We need to use `ng-template` inside the each `e-item` tag with `#template` attribute, which is
mandatory to render that template.

{% tab template="toolbar/direct-components", sourceFiles="app/**/*.ts,index.css"%}

```typescript

import { Component, ViewChild } from '@angular/core';
import { enableRipple, createElement } from '@syncfusion/ej2-base';

enableRipple(true);

@Component({
    selector: 'app-container',
    template: ` <ejs-toolbar>
          <e-items>
           <e-item >
            <ng-template #template>
               <ejs-numerictextbox value="10"></ejs-numerictextbox>
            </ng-template>
            </e-item>
             <e-item >
            <ng-template #template>
                <ejs-datepicker></ejs-datepicker>
            </ng-template>
            </e-item>
             <e-item text='Cut'></e-item>
             <e-item text='Copy'></e-item>
             <e-item text='Paste'></e-item>
             <e-item type='Separator'></e-item>
             <e-item text='Bold'></e-item>
             <e-item text='Italic'></e-item>
             <e-item text='Underline'></e-item>
          </e-items>
        </ejs-toolbar>`
})

export class AppComponent {
}

```

{% endtab %}