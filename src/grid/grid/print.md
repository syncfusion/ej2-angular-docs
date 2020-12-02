---
title: "Print"
component: "Grid"
description: "Learn how to print DataGrid content, set up pages for printing, perform external print, and print visible pages in the Essential JS 2 DataGrid control."
---

# Print

To print the Grid, use the [`print`](../api/grid/#print) method from grid instance. The print option can be displayed on the
[`toolbar`](../api/grid/#toolbar) by adding the **Print** toolbar item.

{% tab template="grid/print", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

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
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['Print'];
    }
}

```

{% endtab %}

## Page Setup

Some of the print options cannot be configured through JavaScript code. So, you have to customize the layout, paper size,
and margin options using the browser page setup dialog. Please refer to the following links to know more about the browser page setup:

* [`Chrome`](https://support.google.com/chrome/answer/1069693?hl=en&visit_id=1-636335333734668335-3165046395&rd=1)
* [`Firefox`](https://support.mozilla.org/en-US/kb/how-print-web-pages-firefox)
* [`Safari`](http://www.mintprintables.com/print-tips/adjust-margins-osx/)
* [`IE`](http://www.helpteaching.com/help/print/index.htm)

## Print by external button

To print the grid from an external button, invoke the [`Print`](../api/grid/#print) method.

{% tab template="grid/paging-api", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template:
    `<button ej-button id='print' (click)='print()'>Print</button>
        <ejs-grid #grid='' [dataSource]='data' height='280px'>
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

    print() {
        this.gridObj.print();
    }
}

```

{% endtab %}

## Print visible Page

By default, the grid prints all the pages. To print the current page alone, set the [`printMode`](../api/grid/#printmode) to **CurrentPage**.

{% tab template="grid/print-api", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { ToolbarItems, PageSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' printMode='CurrentPage' [allowPaging]='true'
               [pageSettings]='pageOptions' [toolbar]='toolbarOptions'>
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
    public pageOptions: PageSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['Print'];
        this.pageOptions = { pageSize: 6 };
    }
}

```

{% endtab %}

## Print the hierarchy grid

By default, the grid will be print the master and expanded child grids alone. you can change the print option by using the [`hierarchyPrintMode`](../api/grid/#hierarchyprintmode) property. The available options are,

| Mode     | Behavior    |
|----------|-------------|
| Expanded | Prints the master grid with expanded child grids. |
| All      | Prints the master grid with all the child grids. |
| None     | Prints the master grid alone. |

{% tab template="grid/default", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data, employeeData } from './datasource';
import { DetailRowService, GridModel, ToolbarService, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='pData' height='265px' [childGrid]='childGrid' [toolbar]='["Print"]' hierarchyPrintMode='All'>
                    <e-columns>
                        <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                        <e-column field='FirstName' headerText='FirstName' width=150></e-column>
                        <e-column field='LastName' headerText='Last Name' width=150></e-column>
                        <e-column field='City' headerText='City' width=150></e-column>
                    </e-columns>
                </ejs-grid>
                `,
    providers: [DetailRowService, ToolbarService]
})
export class AppComponent implements OnInit {

    public pData: object[];
    public childGrid: GridModel = {
        dataSource: data,
        queryString: 'EmployeeID',
        columns: [
            { field: 'OrderID', headerText: 'Order ID', textAlign: 'Right', width: 120 },
            { field: 'CustomerID', headerText: 'Customer ID', width: 150 },
            { field: 'ShipCity', headerText: 'Ship City', width: 150 },
            { field: 'ShipName', headerText: 'Ship Name', width: 150 }
        ],
    };
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.pData = employeeData;
    }

}

```

{% endtab %}

## Print large number of columns

By default, the browser uses A4 as page size option to print pages and to adapt the size of the page the browser print preview will auto-hide the overflowed contents. Hence grid with large number of columns will cut off to adapt the print page.

To show large number of columns when printing, adjust the scale option from print option panel based on your content size.

![Scale Option Setting](./images/print-preview.png)

## Show or Hide columns while Printing

You can show a hidden column or hide a visible column while printing the grid using [`toolbarClick`](./api/grid#toolbarclick) and [`printComplete`](./api/grid#printcomplete) events.

In the [`toolbarClick`](./api/grid#toolbarclick) event, based on **args.item.id** as **grid_print**. We can show or hide columns by setting [`column.visible`](../api/grid/column/#visible) property to **true** or **false** respectively.

In the printComplete event, We have reversed the state back to the previous state.

In the below example, we have **CustomerID** as a hidden column in the grid. While printing, we have changed **CustomerID** to visible column and **ShipCity** as hidden column.

{% tab template="grid/print-api", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { ToolbarItems, PageSettingsModel, GridComponent, Column } from '@syncfusion/ej2-angular-grids';


@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' (toolbarClick)='toolbarClick()' (printComplete)='printComplete()'
                [allowPaging]='true' [pageSettings]='pageOptions' [toolbar]='toolbarOptions'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' [visible]= 'false' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    public pageOptions: PageSettingsModel;
    @ViewChild('grid') public grid: GridComponent;
    toolbarClick() {
        for (const columns of this.grid.columns) {
            if ((columns as Column).field === 'CustomerID') {
                (columns as Column).visible = true;
            } else if ((columns as Column).field === 'ShipCity') {
                (columns as Column).visible = false;
            }
        }
    }

    printComplete() {
        for (const columns of this.grid.columns) {
            if ((columns as Column).field === 'CustomerID') {
                (columns as Column).visible = false;
            } else if ((columns as Column).field === 'ShipCity') {
                (columns as Column).visible = true;
            }
        }
    }

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['Print'];
        this.pageOptions = { pageSize: 6 };
    }
}


```

{% endtab %}

## Limitations of Printing Large Data

When grid contains large number of data, printing all the data at once is not a best option for the browser performance. Because to render all the DOM elements in one page will produce performance issues in the browser. It leads to browser slow down or browser hang. Grid have option to handle large number of data by Virtualization. However while printing, it is not possible to use virtualization for rows and columns.

If printing of all the data is still needed, we suggest to Export the grid to [`Excel`](https://ej2.syncfusion.com/angular/documentation/grid/excel-exporting/) or [`CSV`](https://ej2.syncfusion.com/angular/documentation/grid/excel-exporting/) or [`Pdf`](https://ej2.syncfusion.com/angular/documentation/grid/pdf-export/) and then print it from another non-web based application.