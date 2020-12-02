---
title: "Show Spinner while Exporting"
component: "Grid"
description: "Learn how to Show spinner while exporting the grid."
---

# Show Spinner on Grid when Exporting

You can show/ hide spinner component while exporting the grid using **showSpinner**/ **hideSpinner** methods. You can use [`toolbarClick`](../../api/grid/#toolbarclick) event to show spinner before exporting and hide a spinner in the [`pdfExportComplete`](https://ej2.syncfusion.com/angular/documentation/api/grid/#pdfexportcomplete) or [`excelExportComplete`](https://ej2.syncfusion.com/angular/documentation/api/grid/#excelexportcomplete) event after the exporting.

In the [`toolbarClick`](../../api/grid/#toolbarclick) event, based on the parameter **args.item.id** as **Grid_pdfexport** or **Grid_excelexport** we can call the **showSpinner** method from grid instance.

In the [`pdfExportComplete`](https://ej2.syncfusion.com/angular/documentation/api/grid/#pdfexportcomplete) or [`excelExportComplete`](https://ej2.syncfusion.com/angular/documentation/api/grid/#excelexportcomplete) event, We can call the **hideSpinner** method.

In the below demo, we have rendered the default spinner component when exporting the grid.

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, ExcelExportService } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [allowPaging]='true'
    [toolbar]='toolbarOptions' height='272px' [allowPdfExport]='true' [allowExcelExport]='true'
    (excelExportComplete)='excelExportComplete()' (pdfExportComplete)='pdfExportComplete()'
    (toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' [visible]='false' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipCountry' headerText='ShipCountry' width=150></e-column>
                </e-columns>
                </ejs-grid>`,
    providers: [ExcelExportService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    @ViewChild('grid')  public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['PdfExport', 'ExcelExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_pdfexport') {
            this.grid.showSpinner();
            this.grid.pdfExport();
        } else if (args.item.id === 'Grid_excelexport') {
            this.grid.showSpinner();
            this.grid.excelExport();
        }
    }

    pdfExportComplete(): void {
        this.grid.hideSpinner();
    }
    excelExportComplete(): void {
        this.grid.hideSpinner();
    }
}


```

{% endtab %}