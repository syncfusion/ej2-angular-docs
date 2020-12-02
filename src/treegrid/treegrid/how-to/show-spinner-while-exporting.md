---
title: "Show Spinner on TreeGrid when Exporting"
component: "TreeGrid"
description: "Learn how to Show spinner while exporting the Tree Grid."
---

# Show Spinner on TreeGrid when Exporting

You can show/ hide spinner component while exporting the Tree Grid using [`showSpinner`](../api/treegrid/#showspinner)/ [`hideSpinner`](../api/treegrid/#hidespinner) methods. You can use  [`toolbarClick`](../api/treegrid/#toolbarclick) event to show spinner before exporting and hide a spinner in the [`pdfExportComplete`](../api/treegrid/#pdfexportcomplete) or [`excelExportComplete`](../api/treegrid/#excelexportcomplete) event after the exporting.

In the [`toolbarClick`](../../api/grid/#toolbarclick) event, based on the parameter **args.item.text** as **PDF Export** or **Excel Export** we can call the [`showSpinner`](../api/treegrid/#showspinner) method from Tree Grid instance.

In the [`pdfExportComplete`](../api/treegrid/#pdfexportcomplete) or [`excelExportComplete`](../api/treegrid/#excelexportcomplete) event, We can call the [`hideSpinner`](../api/treegrid/#hidespinner) method.

In the below demo, we have rendered the default spinner component when exporting the Tree Grid.

{% tab template="treegrid/refresh", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { projectData } from './datasource';
import { TreeGridComponent,  ToolbarItems, ToolbarService, PageService, PdfExportService, ExcelExportService  } from '@syncfusion/ej2-angular-treegrid';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-container',
    providers: [ToolbarService, PageService, PdfExportService,ExcelExportService],
    template: `<ejs-treegrid #treegridObj [dataSource]='data' idMapping='TaskID' parentIdMapping='parentID'
    [treeColumnIndex]='1' [allowPaging]='true' [pageSettings]='initialPage' [toolbar]='toolbarOptions'
    [allowPdfExport]='true' [allowExcelExport]='true' (excelExportComplete)='excelExportComplete()'
    (pdfExportComplete)='pdfExportComplete()' (toolbarClick)='toolbarClick($event)'>
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' width='70' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='100' ></e-column>
            <e-column field='StartDate' headerText='Start Date' textAlign='Right' [format]='formatOptions' width='100'></e-column>
            <e-column field='EndDate' headerText='Start Date' textAlign='Right' [format]='formatOptions'width='100'></e-column>
            <e-column field='Duration' headerText='Duration' width='90' textAlign='Right'></e-column>
            <e-column field='Priority' headerText='Priority' width='90'></e-column>
        </e-columns>
    </ejs-treegrid>`,
})
export class AppComponent implements OnInit {

    public data: Object[] = [];
    public formatOptions: Object;
    public toolbarOptions: ToolbarItems[];
    public initialPage: object;

    @ViewChild('treegridObj')
    public treegridObj: TreeGridComponent;

    ngOnInit(): void {
        this.data = projectData;
        this.formatOptions = { format: 'y/M/d', type: 'date' };
        this.toolbarOptions = ['PdfExport', 'ExcelExport'];
        this.initialPage = { pageCount: 5, pageSize: 5 };
    }
    toolbarClick(args: ClickEventArgs) {
      if (this.treegridObj && args.item.text === 'PDF Export') {
        this.treegridObj.showSpinner();
        this.treegridObj.pdfExport();
      }
      else if (this.treegridObj && args.item.text === 'Excel Export') {
        this.treegridObj.showSpinner();
        this.treegridObj.excelExport();
      }
    }
    pdfExportComplete() {
        if (this.treegridObj) {
            this.treegridObj.hideSpinner();
        }
    }
    excelExportComplete() {
        if (this.treegridObj) {
            this.treegridObj.hideSpinner();
        }
    }
  }

```

{% endtab %}