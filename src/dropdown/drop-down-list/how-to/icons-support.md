---
title: "Drop-down list How to show the list item with icon"
component: "DropDownList"
description: "This section explains on how to show the list items with icon in the Syncfusion Angular drop-down list component."
---

# Show the list items with icons

You can render **icons** to the list items by mapping the
[iconCss](../../api/drop-down-list/#fields)
 &nbsp;fields. This `iconCss` fields create a span in the list item with mapped class name
to allow styling as per your need.

In the following sample, icon classes are mapped with `iconCss` field.

{% tab template="dropdownlist/iconClass", sourceFiles="app/**/*.ts,index.html,styles.css"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component
    template: `<ejs-dropdownlist id='ddlelement' #samples [dataSource]='data' [fields]='fields' [placeholder]='text'></ejs-dropdownlist>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: { [key: string]: Object }[] = [
        { Class: 'asc-sort', Type: 'Sort A to Z', Id: '1' },
        { Class: 'dsc-sort', Type: 'Sort Z to A ', Id: '2' },
        { Class: 'filter', Type: 'Filter', Id: '3' },
        { Class: 'clear', Type: 'Clear', Id: '4' }];
    // map the icon column to iconCSS field.
    public fields: Object = { text: 'Type', iconCss: 'Class', value: 'Id' };
    //set the placeholder to DropDownList input
    public text: string = 'Select a format';
}
```

{% endtab %}
