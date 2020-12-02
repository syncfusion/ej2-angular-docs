---
title: "Exporting Filtered Data Only"
component: "TreeGrid"
description: "Learn how to customize the Essential JS 2 Tree Grid."
---

# Exporting Filtered Data Only

You can export the filtered data by defining the resulted data in [`PdfExportProperties.dataSource`](../../api/grid/pdfExportProperties/#datasource) before export.

In the below Pdf exporting demo, We have gotten the filtered data from the filteredResult of Tree Grid filterModule and then defines the resulted data in [`PdfExportProperties.dataSource`](../../api/grid/pdfExportProperties/#datasource) and pass it to [`pdfExport`](../api/treegrid/#pdfexport) method.

{% tab template="treegrid/refresh", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { projectData } from './datasource';
import { TreeGridComponent, ToolbarItems, ToolbarService, PdfExportService,
 PageService, FilterService } from '@syncfusion/ej2-angular-treegrid';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';
import { PdfExportProperties } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-container',
    providers: [ToolbarService, PdfExportService, PageService, FilterService],
    template: `<ejs-treegrid #treegridObj [dataSource]='data' idMapping='TaskID' parentIdMapping='parentID' [treeColumnIndex]='1' [allowFiltering]='true' [allowPaging]='true' [pageSettings]='initialPage' [allowPdfExport]='true' [toolbar]='toolbarOptions' (toolbarClick)='toolbarClick($event)' >
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' width='70' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='100' ></e-column>
            <e-column field='StartDate' headerText='Start Date' textAlign='Right' [format]='formatOptions' editType='datepickeredit' [edit]='editOptions' width='100'></e-column>
            <e-column field='EndDate' headerText='Start Date' textAlign='Right' [format]='formatOptions' editType='datepickeredit' [edit]='editOptions' width='100'></e-column>
            <e-column field='Duration' headerText='Duration' width='90' textAlign='Right'></e-column>
            <e-column field='Priority' headerText='Priority' width='90'></e-column>
        </e-columns>
    </ejs-treegrid>`,
})
export class AppComponent implements OnInit {

    public data: Object[] = [];
    public editOptions: Object;
    public formatOptions: Object;
    public toolbarOptions: ToolbarItems[];
    public initialPage: object;
    @ViewChild('treegridObj')
    public treegridObj: TreeGridComponent;

    ngOnInit(): void {
        this.data = projectData;
        this.editOptions = { params: { format: 'y/M/d' } };
        this.formatOptions = { format: 'y/M/d', type: 'date' };
        this.toolbarOptions = ['PdfExport'];
        this.initialPage = { pageCount: 5, pageSize: 5 };
    }
    toolbarClick(args: ClickEventArgs) {
    if (this.treegridObj && args.item.text === 'PDF Export') {
      let pdfdata;
      pdfdata = this.treegridObj.filterModule.filteredResult;
      const exportProperties = {
        dataSource: pdfdata,
     };
     if (this.treegridObj) {
         this.treegridObj.pdfExport(exportProperties);
     }
  
    }
  }

```

{% endtab %}
