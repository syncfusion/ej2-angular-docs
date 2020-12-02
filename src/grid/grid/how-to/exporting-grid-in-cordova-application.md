---
title: "Exporting Grid in Cordova application"
component: "Grid"
description: "Learn how to Exporting Grid in Cordova application."
---

# Exporting Grid in Cordova application

Cordova application does not support direct file download. So we have to use the Blob stream to export the Grid.
You can use corresponding exporting methods and exportComplete events to get the Blob stream.

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import {
    GridComponent, ToolbarItems, ToolbarService, ExcelExportService, PdfExportService,
    ExcelExportCompleteArgs, PdfExportCompleteArgs
} from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions' height='272px' [allowExcelExport]='true'
    (excelExportComplete)='excelExpComplete($event)' (pdfExportComplete)='pdfExpComplete($event)'
      [allowPdfExport]='true' (toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                </e-columns>
                </ejs-grid>`,
    providers: [ToolbarService, ExcelExportService, PdfExportService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    @ViewChild('grid') public grid: GridComponent;
    public exportBlob = (blob: Blob) => {
        const a: HTMLAnchorElement = document.createElement('a');
        document.body.appendChild(a);
        a.style.display = 'none';
        const url: string = (window.URL as any).createobjectURL(blob);
        a.href = url;
        a.download = 'Export';
        a.click();
        (window.URL as any).revokeobjectURL(url);
        document.body.removeChild(a);
    }

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['PdfExport', 'ExcelExport'];
    }

    toolbarClick(args: ClickEventArgs) {
        if (args.item.id === 'Grid_pdfexport') {
            this.grid.pdfExport(null, null, null, true);
        }
        if (args.item.id === 'Grid_excelexport') {
            this.grid.excelExport(null, null, null, true);
        }
    }

    excelExpComplete(args: ExcelExportCompleteArgs) {
        // This event will be triggered when excel exporting.
        args.promise.then((e: { blobData: Blob }) => {
            // In this `then` function, we can get blob data through the arguments after promise resolved.
            this.exportBlob(e.blobData);
        });
    }

    pdfExpComplete(args: PdfExportCompleteArgs) {
        // This event will be triggered when pdf exporting.
        args.promise.then((e: { blobData: Blob }) => {
            // In this `then` function, we can get blob data through the arguments after promise resolved.
            this.exportBlob(e.blobData);
        });
    }
}


```

{% endtab %}
