---
title: "ListBox drag and drop"
component: "ListBox"
description: "Angular ListBox supports drag and drop with in single list box and between two list boxes."
---

# Drag and drop

The ListBox has support to drag an item or a group of selected items and drop it within the same list box or into another list box.

The elements can be customized on drag and drop by using the following events,

| Events | Description |
|------|------|
| [`dragStart`](../api/list-box/#dragstart) | Triggers when the selected element is being dragged. |
| [`drag`](../api/list-box/#drag) | Triggers when the selected element is being dragged. |
| [`drop`](../api/list-box/#drop) | Triggers when the selected element is being dropped. |

## Single listbox

To drag and drop an item or group of item within the list box can be achieved by setting [`allowDragAndDrop`](../api/list-box/#allowdraganddrop) property as `true`.

The following sample illustrates how to drag and drop an item within the same list box by enabling `allowDragAndDrop` property.

{% tab template="listbox/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component ({
    selector: 'app-container',
    template: `<ejs-listbox [dataSource]="data" [allowDragAndDrop]="true" [fields]="setfield"><ejs-listbox>`
})

export class AppComponent {
   public data: {[key: string]: Object}[] = [
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
   public setfield = { text : "Name" }
}
```

{% endtab %}

## Multiple listbox

To drag and drop an item or group of item between two list boxes can be achieved by setting `allowDragAndDrop` property as `true` and [`scope`](../api/list-box/#scope) property should be set to both the list boxes.

In the following sample, the `allowDragAndDrop` property is set as `true` and `scope` is set as `combined-list` to enable drop and drop in both list boxes.

{% tab template="listbox/multiple-listbox", isDefaultActive = "true", sourceFiles="app/**/*.ts,draganddrop.css" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<div class="drag-drop-wrapper">
                     <div class="listbox-control1">
                     <h4>Group A</h4>
                     <ejs-listbox [dataSource]="groupA" [allowDragAndDrop]="true" [fields]="setfield" scope="combined-list" height="290px"></ejs-listbox>
                     </div>
                     <div class="listbox-control2">
                     <h4>Group B</h4>
                     <ejs-listbox [dataSource]="groupB" [allowDragAndDrop]="true" [fields]="setfield" scope="combined-list" height="290px"></ejs-listbox>
                     </div></div>`,
    styleUrls: ['draganddrop.css'],
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
}

```

{% endtab %}