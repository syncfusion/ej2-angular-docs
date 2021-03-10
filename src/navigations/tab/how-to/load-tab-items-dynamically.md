---
title: "Load Tab items dynamically"
component: "Tab"
description: "This example demonstrates how to dynamically load or add a tab item in the Essential JS 2 Tab control."
---

# Load Tab items dynamically

Tabs can be added dynamically by passing array of items and index value to the [`addTab`](../../api/tab#addtab) method.

```typescript
    // New tab title and content inputs are fetched and stored in local variable
    let title: string = document.getElementById('tab-title').value;
    let content: string = document.getElementById('tab-content').value;

    // Required tab item object formed by using textbox inputs
    let item: Object =  { header: { text: title }, content: createElement('pre', { innerHTML: content.replace(/\n/g, '<br>\n') }).outerHTML };

    // Item object and the index argument passed into the addTab method to add a new tab
    this.tabInstance.addTab([item], this.totalItems-1);
```

In the following demo, you can add the tab content by clicking the **+**.  This **+** icon is added on the tab header using
[`iconCss`](../../api/tab/header#iconcss) property.  Enter the new Tab heading and content details in the available text boxes,
click 'Add Tab' button to pass the details as an array and here last index is calculated to append the new tab at the end.

{% tab template="tab/dynamic-tab", sourceFiles="app/**/*.ts,index.css"%}

```typescript

import { Tooltip } from '@syncfusion/ej2-popups';
import { Component, ViewChild } from '@angular/core';
import { enableRipple, createElement } from '@syncfusion/ej2-base';
import { TabComponent, selectEventArgs } from '@syncfusion/ej2-angular-navigations';

enableRipple(true);

/**
 * Add new tabs dynamically
 */

@Component({
    selector: 'app-container',
    template: `<ejs-tab #element id="element" (created)="tabCreated()" (selected)="tabSelected($event)">
            <e-tabitems>
                <e-tabitem [header]='headerText[0]' content="#tab1_content"></e-tabitem>
                <e-tabitem [header]='headerText[1]' content="#form-container"></e-tabitem>
            </e-tabitems>
        </ejs-tab>`
})

export class AppComponent {
      @ViewChild('element') tabInstance: TabComponent;

    public totalItems: number;
    public headerText: Object = [{ 'text': 'Tab1' }, { 'iconCss': 'e-add-icon' }];

    public tabCreated(): void {
        let tooltip: Tooltip = new Tooltip({
            content: 'Add Tab'
        });
        tooltip.appendTo('.e-ileft.e-icon');

        document.getElementById('btn-add').onclick = (e : Event) => {
            let title: string = (document.getElementById('tab-title') as any).value;
            let content: string = (document.getElementById('tab-content') as any).value;
            let item: Object =  { header: { text: title }, content: createElement('pre', { innerHTML: content.replace(/\n/g, '<br>\n') }).outerHTML };

            this.totalItems = document.querySelectorAll('#element .e-toolbar-item').length;
            this.tabInstance.addTab([item], this.totalItems-1);
        };
    }

    public tabSelected(args: SelectEventArgs): void {
        if (args.selectedIndex === document.querySelectorAll('#element .e-toolbar-item').length -1) {
            (document.getElementById('tab-title') as any).value = '';
            (document.getElementById('tab-content') as any).value = '';
        }
    }
}

```

{% endtab %}
