---
title: "Multiselect CheckBox"
component: "MultiSelect"
description: "This sample for Syncfusion angular multiselect component demonstrates the built-in support to select the multiple values through checkbox."
---

# CheckBox

The MultiSelect has built-in support to select multiple values through checkbox,
when [`mode`](../api/multi-select/#mode) property set as `CheckBox`.

To use checkbox, inject the `CheckBoxSelection` module in the MultiSelect.

{% tab template="multiselect/checkbox", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component, OnInit } from '@angular/core';
import { CheckBoxSelectionService, FilteringEventArgs } from '@syncfusion/ej2-angular-dropdowns';
@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='sportsData' [fields]='fields'(filtering)='onFiltering($event)' [mode]='mode' [placeholder]='placeholder'></ejs-multiselect>`,
    providers: [CheckBoxSelectionService]
})
export class AppComponent {
    public mode: string;
    constructor() {
    }
    //set the data to dataSource property
    public sportsData: Object[] =  [
        { id: 'Game1', sports: 'Badminton' },
        { id: 'Game2', sports: 'Basketball' },
        { id: 'Game3', sports: 'Cricket' },
        { id: 'Game4', sports: 'Football' },
        { id: 'Game5', sports: 'Golf' }
    ];
    // maps the appropriate column to fields property
    public fields: Object = { text: 'sports', value: 'id' };
    // set placeholder to MultiSelect input element
    public placeholder: string = 'Select games';
    //Bind the filter event
    public onFiltering: EmitType =  (e: FilteringEventArgs) => {
        let query = new Query();
        //frame the query based on search string with filter type.
        query = (e.text != "") ? query.where("country", "startswith", e.text, true) : query;
        //pass the filter data source, filter query to updateData method.
        e.updateData(this.searchData, query);
    };
    ngOnInit(): void {
        // set the type of mode for checkbox to visualized the checkbox added in li element.
        this.mode = 'CheckBox';
    }
}

```

{% endtab %}

## Select All

The MultiSelect component has in-built support to select the all list items using `Select All` options in the header.

When the [`showSelectAll`](../api/multi-select/#showselectall)
property is set to true, by default Select All text will show.
You can customize the name attribute of the Select All option by using
[`selectAllText`](../api/multi-select/#selectalltext).

For the unSelect All option, by default unSelect All text will show.
You can customize the name attribute of the unSelect All option by using
[`unSelectAllText`](../api/multi-select/#unselectalltext).

{% tab template="multiselect/checkbox", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component, OnInit } from '@angular/core';
import { CheckBoxSelectionService } from '@syncfusion/ej2-angular-dropdowns';
@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='sportsData' [fields]='fields' [mode]='mode' [selectAllText]='selectAllText' showSelectAll=true [placeholder]='placeholder'></ejs-multiselect>`,
    providers: [CheckBoxSelectionService]
})
export class AppComponent {
    public mode: string;
    public selectAllText: string
    constructor() {
    }
    //set the data to dataSource property
    public sportsData: Object[] =  [
        { id: 'Game1', sports: 'Badminton' },
        { id: 'Game2', sports: 'Basketball' },
        { id: 'Game3', sports: 'Cricket' },
        { id: 'Game4', sports: 'Football' },
        { id: 'Game5', sports: 'Golf' }
    ];
    // maps the appropriate column to fields property
    public fields: Object = { text: 'sports', value: 'id' };
    // set placeholder to MultiSelect input element
    public placeholder: string = 'Select games';
    ngOnInit(): void {
        // set the type of mode for checkbox to visualized the checkbox added in li element.
        this.mode = 'CheckBox';
        // set the select all text to MultiSelect checkbox label.
        this.selectAllText= 'Select All';
    }
}

```

{% endtab %}

## Selection Limit

Defines the limit of the selected items using [`maximumSelectionLength`](../api/multi-select/#maximumselectionlength).

{% tab template="multiselect/checkbox", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component, OnInit } from '@angular/core';
import { CheckBoxSelectionService } from '@syncfusion/ej2-angular-dropdowns';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='sportsData' [fields]='fields' [mode]='mode' [maximumSelectionLength]='maximumSelectionLength' [placeholder]='placeholder'></ejs-multiselect>`,
    providers: [CheckBoxSelectionService]
})
export class AppComponent {
    public mode: string;
    public maximumSelectionLength: number;
    constructor() {
    }
    //set the data to dataSource property
    public sportsData: Object[] =  [
        { id: 'Game1', sports: 'Badminton' },
        { id: 'Game2', sports: 'Basketball' },
        { id: 'Game3', sports: 'Cricket' },
        { id: 'Game4', sports: 'Football' },
        { id: 'Game5', sports: 'Golf' }
    ];
    // maps the appropriate column to fields property
    public fields: Object = { text: 'sports', value: 'id' };
    // set placeholder to MultiSelect input element
    public placeholder: string = 'Select games';
    ngOnInit(): void {
        // set the type of mode for checkbox to visualized the checkbox added in li element.
        this.mode = 'CheckBox';
        // Sets limitation to the value selection
        this.maximumSelectionLength = 3;
    }
}

```

{% endtab %}

## Selection Reordering

Using [`enableSelectionOrder`](../api/multi-select/#enableselectionorder) to Reorder the selected items in popup visibility state.

{% tab template="multiselect/checkbox", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component, OnInit } from '@angular/core';
import { CheckBoxSelectionService } from '@syncfusion/ej2-angular-dropdowns';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='sportsData' [fields]='fields' [mode]='mode' [enableSelectionOrder]='false' [placeholder]='placeholder'></ejs-multiselect>`,
    providers: [CheckBoxSelectionService]
})
export class AppComponent {
    public mode: string;
    constructor() {
    }
    //set the data to dataSource property
    public sportsData: Object[] =  [
        { id: 'Game1', sports: 'Badminton' },
        { id: 'Game2', sports: 'Basketball' },
        { id: 'Game3', sports: 'Cricket' },
        { id: 'Game4', sports: 'Football' },
        { id: 'Game5', sports: 'Golf' }
    ];
    // maps the appropriate column to fields property
    public fields: Object = { text: 'sports', value: 'id' };
    // set placeholder to MultiSelect input element
    public placeholder: string = 'Select games';

    ngOnInit(): void {
        // set the type of mode for checkbox to visualized the checkbox added in li element.
        this.mode = 'CheckBox';
    }
}

```

{% endtab %}

## See Also

* [How to bind the data](./data-binding/)
* [How to filter the bound data](./filtering/)
* [How to add custom value to the MultiSelect](./custom-value/)
* [How to render grouping with checkbox](./grouping/#grouping-with-checkbox).