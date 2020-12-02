---
title: "Scrolling"
component: "Grid"
description: "Learn how to set width and height for DataGrid content, display a scrollbar, freeze rows and columns, and make the DataGrid responsive with a parent container."
---

# Scrolling

 The scrollbar will be displayed in the grid when content exceeds the element [`width`](../api/grid/#width) or
 [`height`](../api/grid/#height).
 The vertical and horizontal scrollbars will be displayed based on the following criteria:

* The vertical scrollbar appears when the total height of rows present in the grid exceeds its element height.
* The horizontal scrollbar appears when the sum of columns width exceeds the grid element width.
* The [`height`](../api/grid/#height) and [`width`](../api/grid/#width)
are used to set the grid height and width, respectively.

> The default value for [`height`](../api/grid/#height) and [`width`](../api/grid/#width) is `auto`.

## Set width and height

To specify the [`width`](../api/grid/#width) and [`height`](../api/grid/#height)
of scroller in pixel, set the pixel value as number.

{% tab template="grid/scrolling", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height=315 width=400>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
               </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
}

```

{% endtab %}

## Responsive with parent container

Specify the [`width`](../api/grid/#width) and [`height`](../api/grid/#height)
as **100%** to make the grid element fill its parent container.
Setting the [`height`](../api/grid/#height) to **100%** requires the grid parent element to have explicit height.

{% tab template="grid/scrolling", sourceFiles="app/app.component.ts,index.html,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height='100%' width='100%'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
               </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
}

```

{% endtab %}

## Scroll To Selected Row

You can scroll the grid content to the selected row position by using the
[`rowSelected`](../api/grid/#rowselected) event.

{% tab template="grid/scrolling-select", sourceFiles="app/app.component.ts,index.html,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { RowSelectEventArgs, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-numerictextbox #numeric format='N' min='0' placeholder='Enter index to select a row'
                width=200 [showSpinButton]='false' (change)='onchange($event)'></ejs-numerictextbox>
    <ejs-grid #grid [dataSource]='data' height='315' width='100%' (rowSelected)='rowSelected($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                </e-columns>
               </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('grid') public grid: GridComponent;
    @ViewChild('numeric') public numeric;

    ngOnInit(): void {
        this.data = data;
    }
    onchange() {
        this.grid.selectionModule.selectRow(parseInt(this.numeric.getText(), 10));
    }
    rowSelected(args: RowSelectEventArgs) {
        const rowHeight: number = this.grid.getRows()[this.grid.getSelectedRowIndexes()[0]].scrollHeight;
        this.grid.getContent().children[0].scrollTop = rowHeight * this.grid.getSelectedRowIndexes()[0];
    }
}

```

{% endtab %}

## Frozen rows and columns

Frozen rows and columns provides an option to make rows and columns always visible in the top and left side of the grid while scrolling.

To use frozen rows and columns support, inject the **FreezeService** in the provider section of **AppModule**.

In this demo, the [`frozenColumns`](../api/grid/#frozencolumns) is set as **2** and the [`frozenRows`](../api/grid/#frozenrows)
is set as **3**. Hence, the left two columns and top three rows are frozen.

{% tab template="grid/frozenrows", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height=315 [frozenColumns]='2' [frozenRows]='3' [allowSelection]='false' [enableHover]='false'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='OrderDate' headerText='Order Date' width=130 format='yMd' textAlign='Right'></e-column>
                    <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                    <e-column field='ShipAddress' headerText='Ship Address' width=170></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' width=150></e-column>
                    <e-column field='ShipRegion' headerText='Ship Region' width=150></e-column>
                    <e-column field='ShipPostalCode' headerText='Ship Postal Code' width=150></e-column>
                    <e-column field='Freight' headerText='Freight' width=120></e-column>
                </e-columns>
               </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
}

```

{% endtab %}

> * The `allowScrolling` must be true while giving frozen rows and columns.
> * Frozen rows and columns should not be set outside the grid view port.
> * Frozen Grid will support row and column virtualization feature, which helps to improve the Grid performance while loading a large dataset.

### Limitations

The following features are not supported in frozen rows and columns:

* Grouping
* Row Template
* Detail Template
* Hierarchy Grid
