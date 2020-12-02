---
title: "Multiselect How to"
component: "MultiSelect"
description: "This section demonstrates the add an icon in each list item of the Angular multiselect component."
---

# Show the list items with icons

You can render **icons** to the list items by mapping the
[iconCss](../../api/multi-select/#fields)
 &nbsp;fields. This `iconCss` fields create a span in the list item with mapped class name
to allow styling as per your need.

In the following sample, icon classes are mapped with `iconCss` field.

{% tab template="multiselect/iconClass", sourceFiles="app/**/*.ts,index.css" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='data' [fields]='fields' [placeholder]='text'></ejs-multiselect>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: { [key: string]: Object }[] = [
        { class: 'asc-sort', type: 'Sort A to Z', id: '1' },
        { class: 'dsc-sort', type: 'Sort Z to A ', id: '2' },
        { class: 'filter', type: 'Filter', id: '3' },
        { class: 'clear', type: 'Clear', id: '4' }];
    // map the icon column to iconCSS field.
    public fields: Object = { text: 'type', iconCss: 'class', value: 'id' };
    //set the placeholder to MultiSelect input
    public text: string = 'Select a format';
}

```

{% endtab %}
