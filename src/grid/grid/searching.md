---
title: "Search"
component: "Grid"
description: "Learn how to search DataGrid content, change search operators, perform searches using external buttons, and search particular fields."
---

# Search

You can search records in a Grid, by using the [`search`](../api/grid/#search) method with search key as a parameter.
This also provides an option to integrate search text box in grid's toolbar by adding **Search** item to the
[`toolbar`](../api/grid/#toolbar).

To use Searching, you need to inject **SearchService** in the provider section of **AppModule**.

{% tab template="grid/searching", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { ToolbarItems } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [toolbar]='toolbarOptions' height='272px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C' width=120></e-column>
                    <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=140></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['Search'];
    }
}

```

{% endtab %}

## Initial search

To apply search at initial rendering, set the fields, operator, key, and ignoreCase in the [`searchSettings`](../api/grid/#searchsettings).

{% tab template="grid/searching", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { ToolbarItems, SearchSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [searchSettings]='searchOptions' [toolbar]='toolbarOptions' height='272px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C' width=120></e-column>
                    <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=140></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    public searchOptions: SearchSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.searchOptions = { fields: ['CustomerID'], operator: 'contains', key: 'Ha', ignoreCase: true };
        this.toolbarOptions = ['Search'];
    }
}

```

{% endtab %}

> By default, grid searches all the bound column values. To customize this behavior define
the [`searchSettings.fields`](../api/grid/searchSettings/#fields) property.

## Search operators

The search operator can be defined in [`searchSettings.operator`](../api/grid/searchSettings/#operator) property
to configure specified searching.

The following operators are supported in searching:

Operator |Description
-----|-----
startsWith |Checks whether a value begins with the specified value.
endsWith |Checks whether a value ends with specified value.
contains |Checks whether a value contains with specified value.
equal |Checks whether a value equal to specified value.
notEqual |Checks whether a value not equal to specified value.

## Search by external button

To search grid records from an external button, invoke the [`search`](../api/grid/#search) method.

{% tab template="grid/searching", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template:
    `<div class="e-float-input" style="width: 200px; display: inline-block;">
            <input type="text" class="searchtext"/>
            <span class="e-float-line"></span>
            <label class="e-float-text">Search text</label>
        </div>
    <button ej-button id='search' (click)='search()'>Search</button>
        <ejs-grid #grid='' [dataSource]='data' height='260px'>
            <e-columns>
                <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
            </e-columns>
        </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    @ViewChild('grid') public gridObj: GridComponent;

    ngOnInit(): void {
        this.data = data;
    }

    search() {
        const searchText: string = (document.getElementsByClassName('searchtext')[0] as any).value;
        this.gridObj.search(searchText);
    }
}

```

{% endtab %}

## Search Specific Columns

By default, grid searches all visible columns. You can search specific columns by defining the specific column's field names in the
[`searchSettings.fields`](../api/grid/searchSettings/#fields) property.

{% tab template="grid/searching", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { ToolbarItems, SearchSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='260' [searchSettings]='searchSettings' [toolbar]='toolbar' >
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Center' format='C2' width=80></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=100 ></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public searchSettings: SearchSettingsModel;
    public toolbar: ToolbarItems[];

    ngOnInit(): void {
        this.data = data;
        this.toolbar = ['Search'];
        this.searchSettings = {fields: ['CustomerID', 'Freight', 'ShipCity']};
    }
}

```

{% endtab %}

## Clear search by external button

To clear the searched grid records from the external button, set [`searchSettings.key`](../api/grid/searchSettings/#key) property as `empty` string.

{% tab template="grid/searching", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { ToolbarItems, SearchSettingsModel, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template:
        `<button ej-button id='clear' (click)='clearSearch()'>Clear Search</button>
        <ejs-grid #grid [dataSource]='data' [searchSettings]='searchOptions' [toolbar]='toolbarOptions' height='260px'>
            <e-columns>
                <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
            </e-columns>
        </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    public searchOptions: SearchSettingsModel;
    @ViewChild('grid') public gridObj: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.searchOptions = { fields: ['CustomerID'], operator: 'contains', key: 'Ha', ignoreCase: true };
        this.toolbarOptions = ['Search'];
    }

    clearSearch() {
        this.gridObj.searchSettings.key = '';
    }
}

```

{% endtab %}