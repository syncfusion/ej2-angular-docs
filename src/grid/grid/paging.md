---
title: "Paging"
component: "Grid"
description: "Learn how to add and customize the pager in the Essential JS 2 DataGrid control."
---

# Paging

Paging provides an option to display Grid data in page segments. To enable paging, set the
[`allowPaging`](../api/grid/#allowpaging) to true. When paging is enabled, pager component renders at the bottom of the grid.
Paging options can be configured through the [`pageSettings`](../api/grid/pageSettings).

In the below sample, [`pageSize`](../api/grid/pageSettings/#pagesize) is calculated based on the grid height by using the [`load`](../api/grid/#load) event.

To use Paging, you need to inject **PageService** in the provider section of **AppModule**.

{% tab template="grid/paging1", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='PagingGrid' [dataSource]='data' (load)='load()' [allowPaging]='true' height=325>
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
    @ViewChild('grid') public Grid: GridComponent;
    ngOnInit(): void {
        this.data = data;
    }
    load() {
        const rowHeight: number = this.Grid.getRowHeight();  // height of the each row
        const gridHeight: any = this.Grid.height;  // grid height
        const pageSize: number = this.Grid.pageSettings.pageSize;   // initial page size
        const pageResize: any = (gridHeight - (pageSize * rowHeight)) / rowHeight; // new page size is obtained here
        this.Grid.pageSettings.pageSize = pageSize + Math.round(pageResize);
    }
}

```

{% endtab %}

> You can achieve better performance by using grid paging to fetch only a pre-defined number of records from the data source.

## Template

You can use custom elements inside the pager instead of default elements.
The custom elements can be defined by using [`pagerTemplate`](../api/grid/pageSettings/#template).
Inside this template, you can access the [`CurrentPage`](../api/grid/pageSettings/#currentpage),
[`pageSize`](../api/grid/pageSettings/#pagesize),
[`pageCount`](../api/grid/pageSettings/#pagecount),**totalPage** and **totalRecordCount** values.

{% tab template="grid/pager-template", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { ChangeEventArgs } from '@syncfusion/ej2-inputs';
import { PageSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    templateUrl: 'app/app.template.html'
})
export class AppComponent implements OnInit {
    public data: object[];
    public initialPage: PageSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.initialPage = { pageSize: 5 };
    }

    change(args: ChangeEventArgs) {
        this.initialPage = { currentPage: args.value };
    }
}

```

{% endtab %}

## Pager with Page Size Dropdown

The pager Dropdown allows you to change the number of records in the Grid dynamically. It can be enabled by defining the [`pageSettings.pageSizes`](../api/grid/pageSettings/#pagesizes) property as true.

{% tab template="grid/paging1", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowPaging]='true' height='268px' [pageSettings]='pageSettings'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public pageSettings: Object;

    ngOnInit(): void {
        this.data = data;
        this.pageSettings = { pageSizes: true, pageSize: 12 };
    }
}
```

{% endtab %}

## Render Pager at the Top of the Grid

By default, Pager will be rendered at the bottom of the Grid. You can also render the Pager at the top of the Grid by using the [`dataBound`](../api/grid/#databound) event.

{% tab template="grid/paging1", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='pagerAtTop' [dataSource]='data' [allowPaging]='true' (dataBound)='dataBound()'
               height='268px' [pageSettings]='pageSettings'>
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
    public pageSettings: object;
    @ViewChild('grid') public grid: GridComponent;
    public toolbar: ToolbarItems[];
    public initialGridLoad = true;

    ngOnInit(): void {
        this.data = data;
        this.pageSettings = { pageSizes: true, pageSize: 12 };
    }
    dataBound() {
        if (this.initialGridLoad) {
            this.initialGridLoad = false;
            const pager = document.getElementsByClassName('e-gridpager');
            let topElement;
            if (this.grid.allowGrouping || this.grid.toolbar) {
                topElement = this.grid.allowGrouping ? document.getElementsByClassName('e-groupdroparea') :
                    document.getElementsByClassName('e-toolbar');
            } else {
                topElement = document.getElementsByClassName('e-gridheader');
            }
            this.grid.element.insertBefore(pager[0], topElement[0]);
        }
    }
}

```

{% endtab %}

> During the paging action, the pager component triggers the below three events.
> * The [`created`](../api/pager/pagerModel/#created) event triggers when Pager is created.
> * The [`click`](../api/pager/pagerModel/#click) event triggers when the numeric items in the pager is clicked.
> * The [`dropDownChanged`](../api/pager/pagerModel/#dropdownchanged) event triggers when pageSize DropDownList value is selected.

## See Also

* [Group with Paging](./grouping#group-with-paging)
