---
title: "ListBox toolbar support"
component: "ListBox"
description: "Angular ListBox supports dual list (i.e) reordering of items within the list box and between two list boxes."
---

# Dual list box

The dual list box allows the user to move items between two list boxes by clicking the toolbar buttons. Dual list box can be created by listing items in the
[`toolbarSettings`](../api/list-box/#toolbarsettings) along with the `scope` property.

The following operations can be performed in dual list box,

| Options | Description |
|------|-------------|
| moveUp | Move the selected item in the upward direction within the list box. |
| moveDown | Move the selected item in the downward direction within the list box. |
| moveTo |  Move the selected item to the another list box. |
| moveFrom | Move the selected item from one list box to the another list box. |
| moveAllTo | Move all the items to the another list box. |
| moveAllFrom |  Move all the items from one list box to the another list box. |

The following example illustrates how to move items from `Group A` to `Group B` list box.

{% tab template="listbox/dual-list-box", isDefaultActive = "true", sourceFiles="app/**/*.ts,duallistbox.css" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<div class="dual-list-wrapper">
               <div class="dual-list-groupa">
               <h4>Group A</h4>
               <ejs-listbox [dataSource]="groupA" [fields]="setfield" height="330px" [toolbarSettings]="toolbar" scope="#listbox"></ejs-listbox>
               </div>
               <div class="dual-list-groupb">
               <h4>Group B</h4>
               <ejs-listbox [dataSource]="groupB" [fields]="setfield" height="330px" id="listbox"></ejs-listbox>
               </div></div>`,
    styleUrls: ['duallistbox.css']
})

export class AppComponent {
    public groupA: { [key: string]: Object }[] = [
    { "Name": "Australia", "Code": "AU" },
    { "Name": "Bermuda", "Code": "BM" },
    { "Name": "Canada", "Code": "CA" },
    { "Name": "Cameroon", "Code": "CM" },
    { "Name": "Denmark", "Code": "DK" },
    { "Name": "France", "Code": "FR" },
    { "Name": "Finland", "Code": "FI" },
    { "Name": "Germany", "Code": "DE" },
    { "Name": "Hong Kong", "Code": "HK" }
];

public groupB: { [key: string]: Object }[] = [
    { "Name": "India", "Code": "IN" },
    { "Name": "Italy", "Code": "IT" },
    { "Name": "Japan", "Code": "JP" },
    { "Name": "Mexico", "Code": "MX" },
    { "Name": "Norway", "Code": "NO" },
    { "Name": "Poland", "Code": "PL" },
    { "Name": "Switzerland", "Code": "CH" },
    { "Name": "United Kingdom", "Code": "GB" },
    { "Name": "United States", "Code": "US" }
];
public setfield = { text: "Name" }
public toolbar = { items: ['moveUp', 'moveDown', 'moveTo', 'moveFrom', 'moveAllTo', 'moveAllFrom'] }
}

```

{% endtab %}