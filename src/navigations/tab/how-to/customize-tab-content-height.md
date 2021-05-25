---
title: "Tab Content Height"
component: "Tab"
description: "This section explains how to customize the Syncfusion Essentail JS 2 Tab content height based on different needs."
---

# Customize Tab content height

You can change the Tab content height by using the [`heightAdjustMode`](../../api/tab#heightadjustmode) property. By default, the Tab content [`heightAdjustMode`](../../api/tab#heightadjustmode) property is set to `Content` value.

* **None**: Each tab content height is set based on the Tab height. This value is used only the tab component having the [`height`](../../api/tab#height) property.
* **Auto**: Each tab content height will take the maximum height of all other tabs content.
* **Content**: Each tab content height is set based on their own content.
* **Fill**: Each tab content height is set based on the full height of Tabs parent element.

{% tab template="tab/height", sourceFiles="app/**/*.ts,index.css,header.html"%}

```typescript

import { Component, ViewChild } from '@angular/core';
import { DropDownListComponent, ChangeEventArgs } from '@syncfusion/ej2-dropdowns';
import { TabComponent } from '@syncfusion/ej2-angular-navigations';
import { enableRipple } from '@syncfusion/ej2-base';
/**
 * Adaptive Tab Component
 */

@Component({
    selector: 'app-container',
    // specifies the template url path
    templateUrl: './header.html'
    })
export class AppComponent {
    @ViewChild('element') tabObj: TabComponent;
    @ViewChild('contentHeight') listObj: DropDownListComponent;
    public heightData: Object[] = [
        { mode: 'None', text: 'None' },
        { mode: 'Content', text: 'Content'},
        { mode: 'Fill',text: 'Fill' },
        { mode: 'Auto', text: 'Auto' }
    ];
    public fields: Object = { text: 'text', value: 'mode' };
    public height: string = '220px';
    public value: string = 'Content';
    public onChange(ChangeEventArgs: any): void {
          this.tabObj.heightAdjustMode = this.listObj.value;
    }
    public headerText: Object = [{ 'text': 'Twitter' }, { 'text': 'Facebook' },{ 'text': 'WhatsApp' }];

}

```

{% endtab %}