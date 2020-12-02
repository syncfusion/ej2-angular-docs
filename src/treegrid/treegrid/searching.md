---
title: "Search"
component: "TreeGrid"
description: "Learn how to search TreeGrid content, change search operators, perform searches using external buttons, and search particular fields."
---

# Search

You can search records in a TreeGrid, by using the [`search`](../api/treegrid/#search) method with search key as a parameter. This also provides an option to integrate search text box in treegrid's toolbar by adding `search` item to the [`toolbar`](../api/treegrid/#toolbar).

To search records, inject the [`Filter`](../api/treegrid/#fitermodule) module in the treegrid.

{% tab template="treegrid/searching", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' height='270'  [toolbar]='toolbarOption' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public toolbarOption: string[];

    ngOnInit(): void {
        this.data = sampleData;
        this.toolbarOption = ['Search'];
    }
}

```

{% endtab %}

## Initial search

To apply search at initial rendering, set the fields, operator, key, and ignoreCase in the [`searchSettings`](../api/treegrid/#searchsettings).

{% tab template="treegrid/searching", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' height='270' [toolbar]='toolbarOption' childMapping='subtasks' [searchSettings]='searchSettings' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public toolbarOption: string[];
    public searchSettings: Object;
    ngOnInit(): void {
        this.data = sampleData;
        this.toolbarOption = ['Search'];
        this.searchSettings = { fields: ['taskName'], operator: 'contains', key: 'plan', ignoreCase: true };
    }
}

```

{% endtab %}

> By default, treegrid searches all the bound column values. To customize this behavior define the [`searchSettings.fields`](../api/treegrid/searchSettingsModel/#fields) property.

## Search operators

The search operator can be defined in the [`searchSettings.operator`](../api/treegrid/searchSettingsModel/#operator) property to configure specific searching.

The following operators are supported in searching:

Operator |Description
-----|-----
startsWith |Checks whether a value begins with the specified value.
endsWith |Checks whether a value ends with the specified value.
contains |Checks whether a value contains the specified value.
equal |Checks whether a value is equal to the specified value.
notEqual |Checks for values not equal to the specified value.

> By default, the [`searchSettings.operator`](../api/treegrid/searchSettingsModel/#operator) value is `contains`.

## Search by external button

To search treegrid records from an external button, invoke the [`search`](../api/treegrid/#search) method.

{% tab template="treegrid/searching", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { TreeGridComponent } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<div class="e-float-input" style="width: 200px; display: inline-block;">
            <input type="text" class="searchtext"/>
            <span class="e-float-line"></span>
    <label class="e-float-text">Search text</label></div>
    <button ejs-button (click)="btnClick()">Search</button>  
    <ejs-treegrid #treegrid [dataSource]='data' [treeColumnIndex]='1' height='190' childMapping='subtasks'  >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;
    ngOnInit(): void {
        this.data = sampleData;
    }
    btnClick(e: any){
    let searchText: string = (<HTMLInputElement>document.getElementsByClassName('searchtext')[0]).value;
    this.treeGridObj.search(searchText);
});
}

```

{% endtab %}

## Search specific columns

By default, treegrid searches all visible columns. You can search specific columns by defining the specific column's field names in the [`searchSettings.fields`](../api/treegrid/searchSettingsModel/#fields) property.

{% tab template="treegrid/searching", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='270' [treeColumnIndex]='1'  [toolbar]='toolbarOption' childMapping='subtasks' [searchSettings]='searchSettings'>
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public toolbarOption: string[];
    public searchSettings: Object;
    ngOnInit(): void {
        this.data = sampleData;
        this.toolbarOption = ['Search'];
        this.searchSettings = { fields: ['taskName', 'duration']}
    }
}

```

{% endtab %}