---
title: "Drop-down list Grouping"
component: "DropDownList"
description: "This section for Syncfusion angular drop-down list component demonstrates the grouping based on different categories with individual header."
---

# Grouping

The DropDownList supports wrapping nested elements into a group based on different categories. The category
of each list item can be mapped through the [groupBy](../api/drop-down-list/#fields) field in
the data table. The group header is displayed both as inline and fixed headers. The fixed group header content
is updated dynamically on scrolling the popup list with its category value.

In the following sample, vegetables are grouped according on its category using `groupBy` field.

{% tab template="dropdownlist/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component
    template: `<ejs-dropdownlist id='ddlelement' #samples [dataSource]='data' [fields]='fields' [placeholder]='text' [popupHeight]='height'></ejs-dropdownlist>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: { [key: string]: Object }[] = [
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
    public fields: Object = { groupBy: 'Category', text: 'Vegetable', value: 'Id' };
    // set the placeholder to the DropDownList input
    public text: string = "Select a vegetable";
    // Set the popup list height
    public height: string = '200px';
}
```

{% endtab %}

## Customization

The grouping header is also provided with customization option. This allows custom designing using
the [groupTemplate](../api/drop-down-list/#grouptemplate) property for both
inline and fixed headers.

## See Also

* [How to limit the search result while filtering](./how-to/search-on-filtering/)
* [How to highlight the matched characters in filtering](./how-to/highlight-filtering/)
* [How to modify the result data using remote data source](./how-to/modify-data/)