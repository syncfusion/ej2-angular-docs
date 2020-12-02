---
title: "Multiselect Grouping"
component: "MultiSelect"
description: "This section for Syncfusion angular multiselect component demonstrates the grouping of suggestions based on different categories with individual header."
---

# Grouping

The MultiSelect supports wrapping nested elements into a group based on different categories. The category
of each list item can be mapped through the [groupBy](../api/multi-select/#fields) field in
the data table. The group header is displayed both as inline and fixed headers. The fixed group header content
is updated dynamically on scrolling the popup list with its category value.

In the following sample, vegetables are grouped according on its category using `groupBy` field.

{% tab template="multiselect/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='vegetableData' [fields]='fields'[placeholder]='placeholder' [popupHeight]='height'></ejs-multiselect>`
})
export class AppComponent {
    constructor() {
    }
    //define the data with category
    public vegetableData: { [key: string]: Object }[] = [
        { vegetable: 'Cabbage', category: 'Leafy and Salad', id: 'item1' },
        { vegetable: 'Spinach', category: 'Leafy and Salad', id: 'item2' },
        { vegetable: 'Wheat grass', category: 'Leafy and Salad', id: 'item3' },
        { vegetable: 'Yarrow', category: 'Leafy and Salad', id: 'item4' },
        { vegetable: 'Pumpkins', category: 'Leafy and Salad', id: 'item5' },
        { vegetable: 'Chickpea', category: 'Beans', id: 'item6' },
        { vegetable: 'Green bean', category: 'Beans', id: 'item7' },
        { vegetable: 'Horse gram', category: 'Beans', id: 'item8' },
        { vegetable: 'Garlic', category: 'Bulb and Stem', id: 'item9' },
        { vegetable: 'Nopal', category: 'Bulb and Stem', id: 'item10' },
        { vegetable: 'Onion', category: 'Bulb and Stem', id: 'item11' }
    ];
    // map the groupBy field with category column
    public fields: Object = { groupBy: 'category', text: 'vegetable', value: 'id' };
    // Set the popup list height
    public height: string = '200px';
    // set the placeholder to the MultiSelect input
    public placeholder: string = 'Select vegetables';
}

```

{% endtab %}

## Customization

The grouping header is also provided with customization option. This allows custom
designing using the [`groupTemplate`](../api/multi-select/#grouptemplate) property for both inline and fixed headers.

## Grouping with CheckBox

Previously, there is no checkbox for group headers. Now, this feature allow to render checkbox in group header to select the group items in single selection. You can enable this feature by setting [`enableGroupCheckBox`](../api/multi-select/#enablegroupcheckbox) property value as **true** and **mode** property as **CheckBox**.

Inject the `CheckBoxSelection` module in the MultiSelect to use the checkbox.

{% tab template="multiselect/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component, OnInit } from '@angular/core';
import { CheckBoxSelectionService } from '@syncfusion/ej2-angular-dropdowns';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='vegetableData' [fields]='fields'[placeholder]='placeholder' [popupHeight]='height' [mode]='mode' [enableGroupCheckBox]='enableGroupCheckBox' [allowFiltering]='allowFiltering' [filterBarPlaceholder]='filterBarPlaceholder' [showSelectAll]='showSelectAll'></ejs-multiselect>`
    providers: [CheckBoxSelectionService]
})
export class AppComponent {
    public mode: string;
    constructor() {
    }
    //define the data with category
    public vegetableData: { [key: string]: Object }[] = [
        { vegetable: 'Cabbage', category: 'Leafy and Salad', id: 'item1' },
        { vegetable: 'Spinach', category: 'Leafy and Salad', id: 'item2' },
        { vegetable: 'Wheat grass', category: 'Leafy and Salad', id: 'item3' },
        { vegetable: 'Yarrow', category: 'Leafy and Salad', id: 'item4' },
        { vegetable: 'Pumpkins', category: 'Leafy and Salad', id: 'item5' },
        { vegetable: 'Chickpea', category: 'Beans', id: 'item6' },
        { vegetable: 'Green bean', category: 'Beans', id: 'item7' },
        { vegetable: 'Horse gram', category: 'Beans', id: 'item8' },
        { vegetable: 'Garlic', category: 'Bulb and Stem', id: 'item9' },
        { vegetable: 'Nopal', category: 'Bulb and Stem', id: 'item10' },
        { vegetable: 'Onion', category: 'Bulb and Stem', id: 'item11' }
    ];
    // map the groupBy field with category column
    public fields: Object = { groupBy: 'category', text: 'vegetable', value: 'id' };
    // Set the popup list height
    public height: string = '200px';
    // set the placeholder to the MultiSelect input
    public placeholder: string = 'Select vegetables';
    // set value of enableGroupCheckBox to true
    enableGroupCheckBox: boolean = true;
    // set value of allowFiltering to true
    allowFiltering: boolean = true;
    // set the placeholder to the filterbar
    filterBarPlaceholder: string = "Search Vegetables";
    // set the value of showSelectAll as true
    showSelectAll: boolean = true;
    ngOnInit(): void {
        // set the type of mode for checkbox to visualized the checkbox added in li element.
        this.mode = 'CheckBox';
    }
}

```

{% endtab %}

## See Also

* [Group Template support to MultiSelect](./templates#group-template).