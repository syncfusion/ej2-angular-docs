---
title: "Passing additional parameters to the server when Exporting"
component: "Grid"
description: "Learn how to pass additional parameters to server when Exporting."
---

# Passing additional parameters to the server when Exporting

You can pass the additional parameter in the [`query`](../../api/grid/#query) property by invoking **addParams** method. In the [`toolbarClick`](../../api/grid/#toolbarclick) event, you can define params as key and value pair so it will receive at the server side when exporting.

In the below example, we have passed **recordcount** as **12** using **addParams** method

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, ToolbarService, PdfExportService, ExcelExportService } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';
import { Query } from '@syncfusion/ej2-data';

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
    providers: [ToolbarService, PdfExportService, ExcelExportService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    @ViewChild('grid') public grid: GridComponent;
    public queryClone: any;

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['PdfExport', 'ExcelExport'];
    }

    toolbarClick(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_pdfexport') {
            this.queryClone = this.grid.query;
            this.grid.query = new Query().addParams('recordcount', '12');
            this.grid.pdfExport();
        } else if (args.item.id === 'Grid_excelexport') {
            this.queryClone = this.grid.query;
            this.grid.query = new Query().addParams('recordcount', '12');
            this.grid.excelExport();
        }
    }

    pdfExportComplete(): void {
        this.grid.query = this.queryClone;
    }
    excelExportComplete(): void {
        this.grid.query = this.queryClone;
    }
}

```

{% endtab %}