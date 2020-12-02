---
title: "Combo box How to show the list items with icons"
component: "ComboBox"
description: "This section explains how to add icons with combo box options."
---

# Show the list items with icons

You can render **icons** to the list items by mapping the [iconCss](../../api/combo-box/#fields) &nbsp;fields.
 This `iconCss` field create a span in the list item with mapped class name
to allow styling as per your need.

In the following sample, icon classes are mapped with `iconCss` field.

{% tab template="combobox/iconClass", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the ComboBox component.
    template: `<ejs-combobox id='comboelement' #samples [dataSource]='data' [fields]='fields' [placeholder]='text'></ejs-combobox>`
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
    //set the placeholder to ComboBox input
    public text: string = 'Select a format';
}
```

{% endtab %}
