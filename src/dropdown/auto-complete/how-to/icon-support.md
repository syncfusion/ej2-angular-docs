---
title: "Autocomplete How to show the list items with icons"
component: "AutoComplete"
description: "This section explains how to add icons with autocomplete options."
---

# Show the list items with icons

You can render **icons** to the list items by mapping the
[`iconCss`](../../api/auto-complete/#fields) field. This `iconCss` field
create a span in the list item with mapped class name to allow styling as per your need.

In the following sample, the icon classes are mapped with `iconCss` field.

{% tab template="autocomplete/icon-class", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component
    template: `<ejs-autocomplete id='atcelement' [dataSource]='sortFormatData' [fields]='fields' [placeholder]='text'></ejs-autocomplete>`
})

export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public sortFormatData: { [key: string]: Object }[] = [
    { Class: 'asc-sort', Type: 'Sort A to Z', Id: '1' },
    { Class: 'dsc-sort', Type: 'Sort Z to A ', Id: '2' },
    { Class: 'filter', Type: 'Filter', Id: '3' },
    { Class: 'clear', Type: 'Clear', Id: '4' }
    ];
    // maps the appropriate column to fields property
    public fields: Object = { value: 'Type', iconCss: 'Class' };
    // set the placeholder to the AutoComplete input
    public text: string = "Find a format";
}

```

{% endtab %}