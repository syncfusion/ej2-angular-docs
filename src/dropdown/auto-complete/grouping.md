---
title: "Autocomplete Grouping"
component: "AutoComplete"
description: "This section for Syncfusion angular autocomplete component demonstrates the grouping of suggestions based on different categories with individual header."
---

# Grouping

The AutoComplete supports wrapping nested elements into a group based on different categories. The
category of each list item can be mapped through the
[groupBy](../api/auto-complete/#fields) field in the data table. The group
header is displayed as both inline and fixed headers. The fixed group header content
is updated dynamically on scrolling the suggestion list with its category value.

In the following sample, vegetables are grouped according on its category using `groupBy` field.

{% tab template="autocomplete/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component
    template: `<ejs-autocomplete id='atcelement' [dataSource]='vegetableData' [fields]='fields' [placeholder]='text'></ejs-autocomplete>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public vegetableData: { [key: string]: Object }[] = [
        { Vegetable: 'Cabbage', Category: 'Leafy and Salad', Id: 'item1' },
        { Vegetable: 'Spinach', Category: 'Leafy and Salad', Id: 'item2' },
        { Vegetable: 'Wheat grass', Category: 'Leafy and Salad', Id: 'item3' },
        { Vegetable: 'Yarrow', Category: 'Leafy and Salad', Id: 'item4' },
        { Vegetable: 'Pumpkins', Category: 'Leafy and Salad', Id: 'item5' },
        { Vegetable: 'Chickpea', Category: 'Beans', Id: 'item6' },
        { Vegetable: 'Green bean', Category: 'Beans', Id: 'item7' },
        { Vegetable: 'Horse gram', Category: 'Beans', Id: 'item8' },
        { Vegetable: 'Garlic', Category: 'Bulb and Stem', Id: 'item9' },
        { Vegetable: 'Nopal', Category: 'Bulb and Stem', Id: 'item10' },
        { Vegetable: 'Onion', Category: 'Bulb and Stem', Id: 'item11' }];
    // maps the appropriate column to fields property
    public fields: Object = { groupBy: 'Category', value: 'Vegetable' };
    // set the placeholder to the AutoComplete input
    public text: string = "Find a vegetable";
}

```

{% endtab %}

## Customization

The grouping header is also provided with customization option. This allows custom designing
using the [groupTemplate](../api/auto-complete/#grouptemplate) property for both inline and
fixed headers.

## See Also

[Group Template support to AutoComplete](./templates#group-template).
