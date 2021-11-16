---
title: "Excel Export"
component: "Grid"
description: "Documentation on exporting DataGrid content to Excel and customizing the exported document with multi-export, headers and footers, and file name changes."
---

# Excel Export

The excel export allows exporting Grid data to Excel document. You need to use the
 [`excelExport`](../api/grid/#excelexport) method for exporting. To enable Excel export in the grid, set the
 [`allowExcelExport`](../api/grid/#allowexcelexport) as true.

To use excel export, inject **ExcelExportService** in the provider section of **AppModule**.

{% tab template="grid/excel-exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions' height='272px'
               [allowExcelExport]='true' (toolbarClick)='toolbarClick($event)'>
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
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['ExcelExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_excelexport') { // 'Grid_excelexport' -> Grid component id + _ + toolbar item name
            this.grid.excelExport();
        }
    }
}

```

{% endtab %}

## Multiple Grid exporting

The excel export provides an option to export multiple grid data in the same excel file.

### Same sheet

The excel export provides support to export multiple grids in same sheet.
To export in same sheet, define [`multipleExport.type`](../api/grid/excelExportProperties/#multipleexport) as **AppendToSheet** in [`excelExportProperties`](../api/grid/excelExportProperties/).
It have an option to provide blank rows between grids. These blank rows count can be defined by using the **multipleExport.blankRows**.

{% tab template="grid/excel-exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data, employeeData } from './datasource';
import { GridComponent, ToolbarItems, ExcelExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<p><b>First Grid:</b></p>
    <ejs-grid #grid1 id='FirstGrid' [dataSource]='fData' [toolbar]='toolbarOptions' [allowExcelExport]='true'
    (toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>
                <p><b>Second Grid:</b></p>
                <ejs-grid #grid2 id='SecondGrid' [dataSource]='sData' [allowExcelExport]='true'>
                <e-columns>
                    <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                    <e-column field='FirstName' headerText='FirstName' width=150></e-column>
                    <e-column field='LastName' headerText='Last Name' width=150></e-column>
                    <e-column field='City' headerText='City' width=150></e-column>
                </e-columns>
                </ejs-grid>
                `
})
export class AppComponent implements OnInit {

    public fData: object[];
    public sData: object[];
    public toolbarOptions: ToolbarItems[];
    @ViewChild('grid1') public fGrid: GridComponent;
    @ViewChild('grid2') public sGrid: GridComponent;

    ngOnInit(): void {
        this.fData = data.slice(0, 5);
        this.sData = employeeData.slice(0, 5);
        this.toolbarOptions = ['ExcelExport'];
    }

    toolbarClick = (args: ClickEventArgs) => {
        if (args.item.id === 'FirstGrid_excelexport') { // 'Grid_excelexport' -> Grid component id + _ + toolbar item name
            const appendExcelExportProperties: ExcelExportProperties = {
                multipleExport: { type: 'AppendToSheet', blankRows: 2 }
            };

            const firstGridExport: Promise<any> = this.fGrid.excelExport(appendExcelExportProperties, true);
            firstGridExport.then((fData: any) => {
                this.sGrid.excelExport(appendExcelExportProperties, false, fData);
            });
        }
    }
}

```

{% endtab %}

>By default, **multipleExport.blankRows** value is 5.

### New Sheet

Excel exporting provides support to export multiple grids in new sheet.
To export in new sheet, define  **multipleExport.type** as **NewSheet** in [`excelExportProperties`](../api/grid/excelExportProperties/).

{% tab template="grid/excel-exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data, employeeData } from './datasource';
import { GridComponent, ToolbarItems, ExcelExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<p><b>First Grid:</b></p>
    <ejs-grid #grid1 id='FirstGrid' [dataSource]='fData' [toolbar]='toolbarOptions' [allowExcelExport]='true'
    (toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>
                <p><b>Second Grid:</b></p>
                <ejs-grid #grid2 id='SecondGrid' [dataSource]='sData' [allowExcelExport]='true'>
                <e-columns>
                    <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                    <e-column field='FirstName' headerText='FirstName' width=150></e-column>
                    <e-column field='LastName' headerText='Last Name' width=150></e-column>
                    <e-column field='City' headerText='City' width=150></e-column>
                </e-columns>
                </ejs-grid>
                `
})
export class AppComponent implements OnInit {

    public fData: object[];
    public sData: object[];
    public toolbarOptions: ToolbarItems[];
    @ViewChild('grid1') public fGrid: GridComponent;
    @ViewChild('grid2') public sGrid: GridComponent;

    ngOnInit(): void {
        this.fData = data.slice(0, 5);
        this.sData = employeeData.slice(0, 5);
        this.toolbarOptions = ['ExcelExport'];
    }

    toolbarClick = (args: ClickEventArgs) => {
        if (args.item.id === 'FirstGrid_excelexport') { // 'Grid_excelexport' -> Grid component id + _ + toolbar item name
            const appendExcelExportProperties: ExcelExportProperties = {
                multipleExport: { type: 'NewSheet' }
            };

            const firstGridExport: Promise<any> = this.fGrid.excelExport(appendExcelExportProperties, true);
            firstGridExport.then((fData: any) => {
                this.sGrid.excelExport(appendExcelExportProperties, false, fData);
            });
        }
    }
}

```

{% endtab %}

## To customize excel export

The excel export provides an option to customize mapping of the grid to excel document.

### Export current page

The excel export provides an option to export the current page into excel. To export current page, define [`exportType`](../api/grid/excelExportProperties/#exporttype) to **CurrentPage**.

{% tab template="grid/excel-exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, PageService, ExcelExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions' height='220px'
              [allowPaging]='true' [allowExcelExport]='true' (toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`,
    providers: [PageService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['ExcelExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_excelexport') { // 'Grid_excelexport' -> Grid component id + _ + toolbar item name
            const excelExportProperties: ExcelExportProperties = {
                exportType: 'CurrentPage'
            };
            this.grid.excelExport(excelExportProperties);
        }
    }
}

```

{% endtab %}

### Export hidden columns

The excel export provides an option to export hidden columns of grid by defining [`includeHiddenColumn`](../api/grid/excelExportProperties/#includehiddencolumn) as **true**.

{% tab template="grid/excel-exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, ExcelExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions' height='272px'
               [allowExcelExport]='true' (toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' width=150 [visible]='false'></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['ExcelExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_excelexport') { // 'Grid_excelexport' -> Grid component id + _ + toolbar item name
            const excelExportProperties: ExcelExportProperties = {
                includeHiddenColumn: true
            };
            this.grid.excelExport(excelExportProperties);
        }
    }
}

```

{% endtab %}

### Show or Hide columns on Exported Excel

You can show a hidden column or hide a visible column while printing the grid using [`toolbarClick`](../api/grid/#toolbarclick) and [`excelExportComplete`](../api/grid/#excelexportcomplete) events.

In the [`toolbarClick`](../api/grid/#toolbarclick) event, based on **args.item.id** as **Grid_excelexport**. We can show or hide columns by setting [`column.visible`](../api/grid/column/#visible) property to **true** or **false** respectively.

In the excelExportComplete event, We have reversed the state back to the previous state.

In the below example, we have **CustomerID** as a hidden column in the grid. While exporting, we have changed **CustomerID** to visible column and **ShipCity** as hidden column.

{% tab template="grid/excel-exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, ToolbarService, ExcelExportService, Column } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions' height='272px' [allowExcelExport]='true'
    (excelExportComplete)='excelExportComplete()' (toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' [visible]='false' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['ExcelExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_excelexport') { // 'Grid_excelexport' -> Grid component id + _ + toolbar item name
            (this.grid.columns[1] as Column).visible = true;
            (this.grid.columns[3] as Column).visible = false;
            this.grid.excelExport();
        }
    }

    excelExportComplete(): void {
        (this.grid.columns[1] as Column).visible = false;
        (this.grid.columns[3] as Column).visible = true;
    }
}

```

{% endtab %}

### Export with filter options

The excel export provides an option to export with filter option in excel by defining `enableFilter` as **true** .
It requires the [`allowFiltering`](../api/grid/#allowfiltering) to be true.
{% tab template="grid/excel-exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, ExcelExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [allowFiltering]='true' [toolbar]='toolbarOptions' height='272px'
               [allowExcelExport]='true' (toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' width=150 [visible]='false'></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['ExcelExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_excelexport') { // 'Grid_excelexport' -> Grid component id + _ + toolbar item name
            const excelExportProperties: ExcelExportProperties = {
                enableFilter: true
            };
            this.grid.excelExport(excelExportProperties);
        }
    }
}

```

{% endtab %}

### Conditional Cell Formatting

Grid cells in the exported Excel can be customized or formatted using [`excelQueryCellInfo`](../api/grid/excelQueryCellInfoEventArgs) event. In this event, we can format the grid cells of exported PDF document based on the column cell value.

In the below sample, we have set the background color for **Freight** column in the exported excel by **args.cell** and **backColor** property.

{% tab template="grid/excel-exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, ExcelQueryCellInfoEventArgs } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions' height='272px' [allowExcelExport]='true'
     (queryCellInfo)='queryCellInfo($event)' (excelQueryCellInfo)='excelQueryCellInfo($event)' (toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='Freight' headerText='Freight' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['ExcelExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_excelexport') { // 'Grid_excelexport' -> Grid component id + _ + toolbar item name
            this.grid.excelExport();
        }
    }

    excelQueryCellInfo(args: ExcelQueryCellInfoEventArgs): void {
        if (args.column.field === 'Freight') {
            if (args.value < 30) {
                args.style = { backColor: '#99ffcc' };
            } else if (args.value < 60) {
                args.style = { backColor: '#ffffb3' };
            } else {
                args.style = { backColor: '#ff704d' };
            }
    }
}

    queryCellInfo(args: any): void {
        if (args.column.field === 'Freight') {
            if (args.data[args.column.field] < 30) {
                args.cell.bgColor = '#99ffcc';
            } else if (args.data[args.column.field] < 60) {
                args.cell.bgColor = '#ffffb3';
            } else {
                args.cell.bgColor = '#ff704d';
            }
        }
    }
}

```

{% endtab %}

### Theme

The excel export provides an option to include theme for exported excel document.

To apply theme in exported Excel, define the [`theme`](../api/grid/excelExportProperties/#theme) in [`excelExportProperties`](../api/grid/excelExportProperties/) .

{% tab template="grid/excel-exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, ExcelExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions' height='272px' [allowExcelExport]='true'
     (toolbarClick)='toolbarClick($event)'>
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
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['ExcelExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_excelexport') { // 'Grid_excelexport' -> Grid component id + _ + toolbar item name
            const excelExportProperties: ExcelExportProperties = {
                theme:
                    {
                        header: { fontName: 'Segoe UI', fontColor: '#666666' },
                        record: { fontName: 'Segoe UI', fontColor: '#666666' },
                        caption: { fontName: 'Segoe UI', fontColor: '#666666' }
                    }
            };
            this.grid.excelExport(excelExportProperties);
        }
    }
}

```

{% endtab %}

>By default, material theme is applied to exported excel document.

### To add header and footer

The excel export provides an option to include header and footer content for exported excel document.

{% tab template="grid/excel-exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, ExcelExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions' height='272px' [allowExcelExport]='true'
              (toolbarClick)='toolbarClick($event)'>
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
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['ExcelExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_excelexport') { // 'Grid_excelexport' -> Grid component id + _ + toolbar item name
            const excelExportProperties: ExcelExportProperties = {
                header: {
                    headerRows: 7,
                    rows: [
                        {
                            cells: [{
                                colSpan: 4, value: 'Northwind Traders',
                                style: { fontColor: '#C67878', fontSize: 20, hAlign: 'Center', bold: true, }
                            }]
                        },
                        {
                            cells: [{
                                colSpan: 4, value: '2501 Aerial Center Parkway',
                                style: { fontColor: '#C67878', fontSize: 15, hAlign: 'Center', bold: true, }
                            }]
                        },
                        {
                            cells: [{
                                colSpan: 4, value: 'Suite 200 Morrisville, NC 27560 USA',
                                style: { fontColor: '#C67878', fontSize: 15, hAlign: 'Center', bold: true, }
                            }]
                        },
                        {
                            cells: [{
                                colSpan: 4, value: 'Tel +1 888.936.8638 Fax +1 919.573.0306',
                                style: { fontColor: '#C67878', fontSize: 15, hAlign: 'Center', bold: true, }
                            }]
                        },
                        {
                            cells: [{
                                colSpan: 4, hyperlink: { target: 'https://www.northwind.com/', displayText: 'www.northwind.com' },
                                style: { hAlign: 'Center' }
                            }]
                        },
                        { cells: [{ colSpan: 4, hyperlink: { target: 'mailto:support@northwind.com' }, style: { hAlign: 'Center' } }] },
                    ]
                },
                footer: {
                    footerRows: 4,
                    rows: [
                        { cells: [{ colSpan: 4, value: 'Thank you for your business!', style: { hAlign: 'Center', bold: true } }] },
                        { cells: [{ colSpan: 4, value: '!Visit Again!', style: { hAlign: 'Center', bold: true } }] }
                    ]
                },
            };
            this.grid.excelExport(excelExportProperties);
        }
    }
}

```

{% endtab %}

### File Name for Exported document

You can assign the file name for the exported document by defining [`fileName`](../api/grid/excelExportProperties/#filename) property in [`excelExportProperties`](../api/grid/excelExportProperties).

{% tab template="grid/excel-exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, ExcelExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions' height='272px'
               [allowExcelExport]='true' (toolbarClick)='toolbarClick($event)'>
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
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['ExcelExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_excelexport') { // 'Grid_excelexport' -> Grid component id + _ + toolbar item name
            const excelExportProperties: ExcelExportProperties = {
                fileName: 'new.xlsx'
            };
            this.grid.excelExport(excelExportProperties);
        }
    }
}

```

{% endtab %}

## Custom data source

The excel export provides an option to define datasource dynamically before exporting.
To export data dynamically, define the [`dataSource`](../api/grid/excelExportProperties/#datasource) in [`excelExportProperties`](../api/grid/excelExportProperties/).

{% tab template="grid/excel-exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, ExcelExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions' height='272px'
               [allowExcelExport]='true' (toolbarClick)='toolbarClick($event)'>
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
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['ExcelExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_excelexport') { // 'Grid_excelexport' -> Grid component id + _ + toolbar item name
            const excelExportProperties: ExcelExportProperties = {
                dataSource: data
            };
            this.grid.excelExport(excelExportProperties);
        }
    }
}

```

{% endtab %}

## Exporting grouped records

The excel export provides outline option for grouped records which hides the detailed data for better viewing.
In grid, we have provided the outline option for the exported document when the data's are grouped.

{% tab template="grid/excel-exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, GroupService, PageService, GroupSettingsModel } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions' height='220px' [allowGrouping]='true'
     [groupSettings]='groupOptions' [allowPaging]='true' [allowExcelExport]='true' (toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`,
    providers: [PageService, GroupService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    @ViewChild('grid') public grid: GridComponent;
    public groupOptions: GroupSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['ExcelExport'];
        this.groupOptions = { columns: ['CustomerID', 'ShipCity'] };
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_excelexport') { // 'Grid_excelexport' -> Grid component id + _ + toolbar item name
            this.grid.excelExport();
        }
    }
}

```

{% endtab %}

## Export the hierarchy grid

The grid have an option to export the hierarchy grid to excel document. By default, grid will exports the visible child grids in expanded state. you can change the exporting option by using the **ExcelExportProperties.hierarchyExportMode** property. The available options are,

| Mode     | Behavior    |
|----------|-------------|
| Expanded | Exports the visible child grids in expanded state. |
| All      | Exports the all the child grids in expanded state. |
| None     | Exports the child grids in collapse state. |

{% tab template="grid/excel-exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data, employeeData } from './datasource';
import { DetailRowService, GridModel, GridComponent, ExcelExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='pData' height='265px' [allowExcelExport]='true' [childGrid]='childGrid'
               [toolbar]='["ExcelExport"]' (toolbarClick)="toolbarClick($event)">
                    <e-columns>
                        <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                        <e-column field='FirstName' headerText='FirstName' width=150></e-column>
                        <e-column field='LastName' headerText='Last Name' width=150></e-column>
                        <e-column field='City' headerText='City' width=150></e-column>
                    </e-columns>
                </ejs-grid>
                `,
    providers: [DetailRowService]
})
export class AppComponent implements OnInit {

    public pData: object[];
    @ViewChild('grid') public grid: GridComponent;
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
    ngOnInit(): void {
        this.pData = employeeData;
    }

    toolbarClick(args: ClickEventArgs) {
        if (args.item.id === 'Grid_excelexport') {
            const exportProperties: ExcelExportProperties = {
                hierarchyExportMode: 'Expanded'
            };
            this.grid.excelExport(exportProperties);
        }
    }

}

```

{% endtab %}

### Limitations

* Microsoft Excel permits up to seven nested levels in outlines. So that in the grid we can able to provide only up to seven nested levels
  and if it exceeds more than seven levels then the document will be exported without outline option.
  Please refer the [Microsoft Limitation](https://docs.microsoft.com/en-us/sql/reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs?view=sql-server-2017#ExcelLimitations)

## Exporting Grid in server

The Grid have an option to export the data to Excel in server side using Grid server export library.

### Server Dependencies

The Server side export functionality is shipped in the Syncfusion.EJ2.GridExport package, which is available in Essential Studio and [nuget.org](https://www.nuget.org/).The following list of dependencies is required for Grid server side Excel exporting action.

* Syncfusion.EJ2
* Syncfusion.EJ2.GridExport

### Server Configuration

The following code snippet shows server configuration using ASP.NET Core Controller Action.

To Export the Grid in server side, You need to call the
 [`serverExcelExport`](../api/grid/#serverexcelexport) method for passing the Grid properties to server exporting action.

```typescript

        public ActionResult ExcelExport([FromForm] string gridModel)
        {
            GridExcelExport exp = new GridExcelExport();
            Grid gridProperty = ConvertGridObject(gridModel);
            return exp.ExcelExport<OrdersDetails>(gridProperty, orddata);
        }

        private Grid ConvertGridObject(string gridProperty)
        {
           Grid GridModel = (Grid)Newtonsoft.Json.JsonConvert.DeserializeObject(gridProperty, typeof(Grid));
           GridColumnModel cols = (GridColumnModel)Newtonsoft.Json.JsonConvert.DeserializeObject(gridProperty, typeof(GridColumnModel));
           GridModel.Columns = cols.columns;
           return GridModel;
        }

        public class GridColumnModel
        {
            public List<GridColumn> columns { get; set; }
        }
        public IActionResult UrlDatasource([FromBody]DataManagerRequest dm)
        {
            IEnumerable DataSource = OrdersDetails.GetAllRecords();
            DataOperations operation = new DataOperations();
            int count = DataSource.Cast<OrdersDetails>().Count();
            return dm.RequiresCounts ? Json(new { result = DataSource, count = count }) : Json(DataSource);
        }


```

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { ToolbarItems, GridComponent } from '@syncfusion/ej2-angular-grids';
import { DataManager, UrlAdaptor } from '@syncfusion/ej2-data';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbar' height='273px'(toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;
    public toolbar: ToolbarItems[];

    public dataManager: DataManager = new DataManager({
        url: 'Home/UrlDatasource',
        adaptor: new UrlAdaptor()
    });

    @ViewChild('grid')
    public grid: GridComponent;

    ngOnInit(): void {
        this.data = this.dataManager;
        this.toolbar = ['ExcelExport'];
    }
    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_excelexport') { // 'Grid_excelexport' -> Grid component id + _ + toolbar item name
            this.grid.serverExcelExport('Home/ExcelExport');
        }
    }
}

```

> **Note:** Refer to the GitHub sample for quick implementation and testing from [here](https://github.com/SyncfusionExamples/Angular-EJ2-Grid-server-side-exporting).

### CSV Export in server side

You can export the Grid to CSV format by using the [`serverCsvExport`](../api/grid/#servercsvexport) method which will pass the Grid properties to server.

In the below demo, we have invoked the above method inside the [`toolbarClick`](../api/grid/#toolbarclick) event. In server side, we have deserialized the Grid properties and passed to the `CsvExport` method which will export the properties to CSV format.

```typescript

        public ActionResult CsvGridExport([FromForm] string gridModel)
        {
            GridExcelExport exp = new GridExcelExport();
            Grid gridProperty = ConvertGridObject(gridModel);
            return exp.CsvExport<OrdersDetails>(gridProperty, orddata);
        }

        private Grid ConvertGridObject(string gridProperty)
        {
           Grid GridModel = (Grid)Newtonsoft.Json.JsonConvert.DeserializeObject(gridProperty, typeof(Grid));
           GridColumnModel cols = (GridColumnModel)Newtonsoft.Json.JsonConvert.DeserializeObject(gridProperty, typeof(GridColumnModel));
           GridModel.Columns = cols.columns;
           return GridModel;
        }

        public IActionResult UrlDatasource([FromBody]DataManagerRequest dm)
        {
            IEnumerable DataSource = OrdersDetails.GetAllRecords();
            DataOperations operation = new DataOperations();
            int count = DataSource.Cast<OrdersDetails>().Count();
            return dm.RequiresCounts ? Json(new { result = DataSource, count = count }) : Json(DataSource);
        }


```

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { ToolbarItems, GridComponent } from '@syncfusion/ej2-angular-grids';
import { DataManager, UrlAdaptor } from '@syncfusion/ej2-data';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbar' height='273px'(toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;
    public toolbar: ToolbarItems[];

    public dataManager: DataManager = new DataManager({
        url: 'Home/UrlDatasource',
        adaptor: new UrlAdaptor()
    });

    @ViewChild('grid')
    public grid: GridComponent;

    ngOnInit(): void {
        this.data = this.dataManager;
        this.toolbar = ['CsvExport'];
    }
    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_csvexport') { // 'Grid_csvexport' -> Grid component id + _ + toolbar item name
            this.grid.serverCsvExport('Home/CsvGridExport');
        }
    }
}

```

## See Also

* [Exporting Grid in Cordova application](./how-to/exporting-grid-in-cordova-application)
* [How to get grid display numbers without grouping and same format to be exported to excel in Angular Grid](https://www.syncfusion.com/forums/151524/how-to-get-grid-display-numbers-without-grouping-and-same-format-to-be-exported-to-excel-in)
