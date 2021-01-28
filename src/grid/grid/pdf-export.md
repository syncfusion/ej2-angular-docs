---
title: "PDF Export"
component: "Grid"
description: "Documentation on exporting DataGrid content to PDF format and customizing the exported document with multi-export, headers and footers, and file name changes."
---

# PDF Export

PDF export allows exporting Grid data to PDF document. You need to use the
 [`pdfExport`](../api/grid/#pdfexport) method for exporting.
 To enable PDF export in the grid, set the [`allowPdfExport`](../api/grid/#allowpdfexport) as true.

To use PDF export, inject **PdfExportService** in the provider section of **AppModule**.

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions'
                height='272px' [allowPdfExport]='true' (toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`,
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    @ViewChild('grid')
    public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['PdfExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_pdfexport') { // 'Grid_pdfexport' -> Grid component id + _ + toolbar item name
            this.grid.pdfExport();
        }
    }
}

```

{% endtab %}

## Multiple exporting

PDF export provides an option for exporting multiple grids to same file.
In this exported document, each grid will be exported to new page of document in same file.

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data, employeeData } from './datasource';
import { GridComponent, ToolbarItems } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';

@Component({
    selector: 'app-root',
    template: `<p><b>First Grid:</b></p>
    <ejs-grid #grid1 id='FirstGrid' [dataSource]='fData' [toolbar]='toolbarOptions' [allowPdfExport]='true'
        (toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>
                <p><b>Second Grid:</b></p>
                <ejs-grid #grid2 id='SecondGrid' [dataSource]='sData' [allowPdfExport]='true'>
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
        this.toolbarOptions = ['PdfExport'];
    }

    toolbarClick = (args: ClickEventArgs) => {
        if (args.item.id === 'FirstGrid_pdfexport') { // 'Grid_pdfexport' -> Grid component id + _ + toolbar item name
            const firstGridPdfExport: Promise<object> = this.fGrid.pdfExport({}, true);
            firstGridPdfExport.then((pdfData: object) => {
                this.sGrid.pdfExport({}, false, pdfData);
            });
        }
    }
}


```

{% endtab %}

## To customize PDF export

PDF export provides an option to customize mapping of grid to exported PDF document.

### File Name for Exported document

You can assign the file name for the exported document by defining [`fileName`](../api/grid/pdfExportProperties/#filename) property in [`ExcelExportProperties`](../api/grid/pdfExportProperties/).

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, PageService, PdfExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [allowPaging]='true' [toolbar]='toolbarOptions'
          height='220px' [allowPaging]='true' [allowPdfExport]='true' (toolbarClick)='toolbarClick($event)'>
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
        this.toolbarOptions = ['PdfExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_pdfexport') { // 'Grid_pdfexport' -> Grid component id + _ + toolbar item name
            const pdfExportProperties: PdfExportProperties = {
                fileName: 'new.pdf'
            };
            this.grid.pdfExport(pdfExportProperties);
        }
    }
}

```

{% endtab %}

### Default Fonts for PDF exporting

By default, grid uses **Helvetica** font in the exported document. You can change the default font by using [`pdfExportProperties.theme`](../api/grid/pdfExportProperties/#theme) property. The available default fonts are,

* Helvetica
* TimesRoman
* Courier
* Symbol
* ZapfDingbats

The code example for changing default font,

```typescript

    import { PdfStandardFont, PdfFontFamily, PdfFontStyle } from '@syncfusion/ej2-pdf-export';

    ...

    const pdfExportProperties: PdfExportProperties = {
        theme: {
            header: {font:  new PdfStandardFont(PdfFontFamily.TimesRoman, 11, PdfFontStyle.Bold),
            caption: { font: new PdfStandardFont(PdfFontFamily.TimesRoman, 9) },
            record: { font: new PdfStandardFont(PdfFontFamily.TimesRoman, 10) }
        }
    };

```

### Add Custom Font for PDF exporting

You can change the default font of Grid header, content and caption cells in the exported document by using [`pdfExportProperties.theme`](../api/grid/pdfExportProperties/#theme) property.

In the following example, we have used Algeria font to export the grid.

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts, app/datasource.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data, base64AlgeriaFont } from './datasource';
import { GridComponent, ToolbarItems, PdfExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';
import { PdfTrueTypeFont } from '@syncfusion/ej2-pdf-export';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions' height='272px'
             [allowPaging]='true' [allowPdfExport]='true' (toolbarClick)='toolbarClick($event)'>
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
    @ViewChild('grid')
    public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['PdfExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_pdfexport') {
            const pdfExportProperties: PdfExportProperties = {
                theme: {
                    header: { font: new PdfTrueTypeFont(base64AlgeriaFont, 12) },
                    caption: { font: new PdfTrueTypeFont(base64AlgeriaFont, 10) },
                    record: { font: new PdfTrueTypeFont(base64AlgeriaFont, 9) }
                }
            };
            this.grid.pdfExport(pdfExportProperties);
        }
    }
}

```

{% endtab %}

> **PdfTrueTypeFont** accepts base 64 format of the Custom Font.

### To add header and footer

You can customize text, page number, line, page size and changing orientation in header and footer.

#### How to write a text in header/footer

You can add text either in Header or Footer of exported PDF document using [`pdfExportProperties`](../api/grid/pdfExportProperties).

```typescript

const exportProperties: PdfExportProperties = {
    header: {
        fromTop: 0,
        height: 130,
        contents: [
            {
                type: 'Text',
                value: "Northwind Traders",
                position: { x: 0, y: 50 },
                style: { textBrushColor: '#000000', fontSize: 13 }
            },
        ]
    }

```

#### How to draw a line in header/footer

you can add line either in Header or Footer of the exported PDF document.

Supported line styles:
* Dash
* Dot
* DashDot
* DashDotDot
* Solid

```typescript

const exportProperties: PdfExportProperties = {
    header: {
        fromTop: 0,
        height: 130,
        contents: [
            {
                type: 'Line',
                style: { penColor: '#000080', penSize: 2, dashStyle: 'Solid' },
                points: { x1: 0, y1: 4, x2: 685, y2: 4 }
            }
        ]
    }
}

```

#### Add page number in header/footer

you can add page number either in Header or Footer of exported PDF document.

Supported page number types:
* LowerLatin - a, b, c,
* UpperLatin - A, B, C,
* LowerRoman - i, ii, iii,
* UpperRoman - I, II, III,
* Number - 1,2,3.

```typescript

 const exportProperties: PdfExportProperties = {
    header: {
        fromTop: 0,
        height: 130,
        contents: [
            {
                type: 'PageNumber',
                pageNumberType: 'Arabic',
                format: 'Page {$current} of {$total}', //optional
                position: { x: 0, y: 25 },
                style: { textBrushColor: '#ffff80', fontSize: 15, hAlign: 'Center' }
            }
        ]
    }
}

```

#### Insert an image in header/footer

Image (Base64 string with .jpeg format) can be added in the exported document in header/footer using the [`pdfExportProperties`](../api/grid/pdfExportProperties).

```typescript

const exportProperties: PdfExportProperties = {
    header: {
        fromTop: 0,
        height: 130,
        contents: [
            {
                type: 'Image',
                src: image,
                position: { x: 40, y: 10 },
                size: { height: 100, width: 250 },
            }
        ]
    }
}

```

The below code illustrates the pdf export customization.

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, PdfExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';
import { image } from './image';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions' height='272px'
              [allowPaging]='true' [allowPdfExport]='true' (toolbarClick)='toolbarClick($event)'>
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
        this.toolbarOptions = ['PdfExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_pdfexport') { // 'Grid_pdfexport' -> Grid component id + _ + toolbar item name
            const pdfExportProperties: PdfExportProperties = {
                header: {
                    fromTop: 0,
                    height: 130,
                    contents: [
                        {
                            type: 'Image',
                            src: image,
                            position: { x: 40, y: 10 },
                            size: { height: 100, width: 250 },
                        }
                    ]
                },
                footer: {
                    fromBottom: 160,
                    height: 150,
                    contents: [
                        {
                            type: 'PageNumber',
                            pageNumberType: 'Arabic',
                            format: 'Page {$current} of {$total}',
                            position: { x: 0, y: 25 },
                            style: { textBrushColor: '#ffff80', fontSize: 15 }
                        }
                    ]
                }
            };
            this.grid.pdfExport(pdfExportProperties);
        }
    }
}


```

{% endtab %}

### How to change page orientation

Page orientation can be changed Landscape(Default Portrait) for the exported document using the [`pdfExportProperties`](../api/grid/pdfExportProperties).

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, PdfExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [allowPaging]='true' [toolbar]='toolbarOptions'
               height='220px' [allowPdfExport]='true' (toolbarClick)='toolbarClick($event)'>
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
        this.toolbarOptions = ['PdfExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_pdfexport') { // 'Grid_pdfexport' -> Grid component id + _ + toolbar item name
            const pdfExportProperties: PdfExportProperties = {
                pageOrientation: 'Landscape',
            };
            this.grid.pdfExport(pdfExportProperties);
        }
    }
}


```

{% endtab %}

### How to change page size

Page size can be customized for the exported document using the [`pdfExportProperties`](../api/grid/pdfExportProperties).

Supported page sizes are:
* Letter
* Note
* Legal
* A0
* A1
* A2
* A3
* A5
* A6
* A7
* A8
* A9
* B0
* B1
* B2
* B3
* B4
* B5
* Archa
* Archb
* Archc
* Archd
* Arche
* Flsa
* HalfLetter
* Letter11x17
* Ledger

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, PdfExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [allowPaging]='true' [toolbar]='toolbarOptions'
              height='220px' [allowPdfExport]='true' (toolbarClick)='toolbarClick($event)'>
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
        this.toolbarOptions = ['PdfExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_pdfexport') { // 'Grid_pdfexport' -> Grid component id + _ + toolbar item name
            const pdfExportProperties: PdfExportProperties = {
                pageSize: 'Letter'
            };
            this.grid.pdfExport(pdfExportProperties);
        }
    }
}

```

{% endtab %}

### Export current page

PDF export provides an option to export the current page into PDF. To export current page, define the [`exportType`](../api/grid/pdfExportProperties/#exporttype) to **CurrentPage**.

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, PageService, PdfExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [allowPaging]='true' [toolbar]='toolbarOptions'
         height='220px' [allowPaging]='true' [allowPdfExport]='true' (toolbarClick)='toolbarClick($event)'>
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
        this.toolbarOptions = ['PdfExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_pdfexport') { // 'Grid_pdfexport' -> Grid component id + _ + toolbar item name
            const pdfExportProperties: PdfExportProperties = {
                exportType: 'CurrentPage'
            };
            this.grid.pdfExport(pdfExportProperties);
        }
    }
}

```

{% endtab %}

### Export hidden columns

PDF export provides an option to export hidden columns of Grid by defining the [`includeHiddenColumn`](../api/grid/pdfExportProperties/#includehiddencolumn) as **true**.

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, PdfExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [allowPaging]='true' [toolbar]='toolbarOptions' height='272px'
               [allowPdfExport]='true' (toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' [visible]='false'  width=150></e-column>
                    <e-column field='ShipCountry' headerText='ShipCountry' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['PdfExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_pdfexport') { // 'Grid_pdfexport' -> Grid component id + _ + toolbar item name
            const pdfExportProperties: PdfExportProperties = {
                includeHiddenColumn: true
            };
            this.grid.pdfExport(pdfExportProperties);
        }
    }
}

```

{% endtab %}

### Show or Hide columns on Exported PDF

You can show a hidden column or hide a visible column while exporting the grid using [`toolbarClick`](../api/grid/#toolbarclick) and [`pdfExportComplete`](../api/grid/#pdfExportComplete) events.

In the [`toolbarClick`](../api/grid/#toolbarclick) event, based on **args.item.id** as **Grid_pdfexport**. We can show or hide columns by setting [`column.visible`](../api/grid/column/#visible) property to **true** or **false** respectively.

In the pdfExportComplete event, We have reversed the state back to the previous state.

In the below example, we have **CustomerID** as a hidden column in the grid. While exporting, we have changed **CustomerID** to visible column and **ShipCity** as hidden column.

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, Column } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [allowPaging]='true'
    [toolbar]='toolbarOptions' height='272px' [allowPdfExport]='true'
    (pdfExportComplete)='pdfExportComplete()' (toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' [visible]='false' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipCountry' headerText='ShipCountry' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['PdfExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_pdfexport') {
            (this.grid.columns[1] as Column).visible = true;
            (this.grid.columns[2] as Column ).visible = false;
            this.grid.pdfExport();
        }
    }

    pdfExportComplete(): void {
        (this.grid.columns[1] as Column).visible = false;
        (this.grid.columns[2] as Column).visible = true;
    }
}

```

{% endtab %}

### Conditional Cell Formatting

Grid cells in the exported PDF can be customized or formatted using [`pdfQueryCellInfo`](../api/grid/#pdfquerycellinfo) event. In this event, we can format the grid cells of exported PDF document based on the column cell value.

In the below sample, we have set the background color for **Freight** column in the exported document by **args.cell** and **backgroundColor** property.

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions' height='272px'
            [allowPdfExport]='true' (queryCellInfo)='queryCellInfo($event)'
    (pdfQueryCellInfo)='pdfQueryCellInfo($event)' (toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='Freight' headerText='Freight' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    @ViewChild('grid')
    public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['PdfExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_pdfexport') {
            this.grid.pdfExport();
        }
    }

    pdfQueryCellInfo(args: any): void {
        if (args.column.field === 'Freight') {
            if (args.value < 30) {
                args.style = { backgroundColor: '#99ffcc' };
            } else if (args.value < 60) {
                args.style = { backgroundColor: '#ffffb3' };
            } else {
                args.style = { backgroundColor: '#ff704d' };
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

PDF export provides an option to include theme for exported PDF document.

To apply theme in exported PDF, define the [`theme`](../api/grid/pdfExportProperties/#theme) in [`pdfExportProperties`](../api/grid/pdfExportProperties/) .

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, PageService, PdfExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [allowPaging]='true' [toolbar]='toolbarOptions' height='220px'
     [allowPaging]='true' [allowPdfExport]='true' (toolbarClick)='toolbarClick($event)'>
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
        this.toolbarOptions = ['PdfExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_pdfexport') { // 'Grid_pdfexport' -> Grid component id + _ + toolbar item name
            const pdfExportProperties: PdfExportProperties = {
                theme: {
                    header: {
                        fontColor: '#64FA50', fontName: 'Calibri', fontSize: 17, bold: true,
                        border: { color: '#64FA50', dashStyle: 'Solid' }
                    },
                    record: {
                        fontColor: '#64FA50', fontName: 'Calibri', fontSize: 17, bold: true
                    },
                    caption: {
                        fontColor: '#64FA50', fontName: 'Calibri', fontSize: 17, bold: true
                    }
                }
            };
            this.grid.pdfExport(pdfExportProperties);
        }
    }
}

```

{% endtab %}

> By default, material theme is applied to exported PDF document.

## Custom data source

PDF export provides an option to define datasource dynamically before exporting. To export data dynamically, define the [`dataSource`](../api/grid/pdfExportProperties/#datasource) in [`pdfExportProperties`](../api/grid/pdfExportProperties/)

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, PageService, PdfExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [allowPaging]='true' [toolbar]='toolbarOptions'
              height='220px' [allowPaging]='true' [allowPdfExport]='true' (toolbarClick)='toolbarClick($event)'>
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
        this.toolbarOptions = ['PdfExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_pdfexport') { // 'Grid_pdfexport' -> Grid component id + _ + toolbar item name
            const pdfExportProperties: PdfExportProperties = {
                dataSource: data,
            };
            this.grid.pdfExport(pdfExportProperties);
        }
    }
}

```

{% endtab %}

## Export the hierarchy grid

The grid have an option to export the hierarchy grid to pdf document. By default, grid will exports the master grid with expanded child grids alone. you can change the exporting option by using the **PdfExportProperties.hierarchyExportMode** property. The available options are,

| Mode     | Behavior    |
|----------|-------------|
| Expanded | Exports the master grid with expanded child grids. |
| All      | Exports the master grid with all the child grids. |
| None     | Exports the master grid alone. |

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data, employeeData } from './datasource';
import { DetailRowService, GridModel, GridComponent, PdfExportProperties } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='pData' height='265px' [allowPdfExport]='true' [childGrid]='childGrid'
          [toolbar]='["PdfExport"]' (toolbarClick)="toolbarClick($event)">
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

        if (args.item.text === 'PDF Export') {
            const exportProperties: PdfExportProperties = {
                hierarchyExportMode: 'Expanded'
            };
            this.grid.pdfExport(exportProperties);
        }
    }
}


```

{% endtab %}

## Repeat column header on every page

By default, column header will be placed on the first page of the pdf document but you can display column header on every page using **repeatHeader** property of **pdfGrid**.

In the below sample, we have enabled **repeatHeader** property in [`pdfHeaderQueryCellInfo`](../api/grid/#pdfheaderquerycellinfo) event to show the header on every page.

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript


import { Component, OnInit, ViewChild } from '@angular/core';
import { purchaseData } from './datasource';
import { GridComponent, ToolbarItems } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions' height='272px'
             [allowPdfExport]='true' (pdfHeaderQueryCellInfo)='pdfHeaderQueryCellInfo($event)' (toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='Freight' headerText='Freight' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    @ViewChild('grid')
    public grid: GridComponent;

    ngOnInit(): void {
        this.data = purchaseData;
        this.toolbarOptions = ['PdfExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_pdfexport') {
            this.grid.pdfExport();
        }
    }

    pdfHeaderQueryCellInfo(args: any): void {
         args.cell.row.pdfGrid.repeatHeader = true;
    }

}

```

{% endtab %}

## Exporting Grid in server

The Grid have an option to export the data to PDF in server side using Grid server export library.

### Server Dependencies

The Server side export functionality is shipped in the Syncfusion.EJ2.GridExport package, which is available in Essential Studio and [nuget.org](https://www.nuget.org/).The following list of dependencies is required for Grid server side PDF exporting action.

* Syncfusion.EJ2
* Syncfusion.EJ2.GridExport

### Server Configuration

The following code snippet shows server configuration using ASP.NET Core Controller Action.

To Export the Grid in server side, You need to call the
 [`serverPdfExport`](../api/grid/#serverpdfexport) method for passing the Grid properties to server exporting action.

```typescript

        public ActionResult PdfExport([FromForm] string gridModel)
        {
            GridPdfExport exp = new GridPdfExport();
            Grid gridProperty = ConvertGridObject(gridModel);
            return exp.PdfExport<OrdersDetails>(gridProperty, orddata);
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
        this.toolbar = ['PdfExport'];
    }
    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_pdfexport') { // 'Grid_pdfexport' -> Grid component id + _ + toolbar item name
            this.grid.serverPdfExport('Home/PdfExport');
        }
    }
}

```

## See Also

* [Exporting Grid in Cordova application](./how-to/exporting-grid-in-cordova-application)
