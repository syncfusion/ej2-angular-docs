---
title: "Get specific row and cell index in Tree Grid"
component: "TreeGrid"
description: "Learn how to get specific row and cell index in Tree Grid."
---

# Get specific row and cell index in Tree Grid

You can get the specific row and cell index of the Tree Grid by using [`rowSelected`](../api/treegrid/#rowselected) event of the treegrid. Here, we can get the row and cell index by using *aria-rowindex* (get row Index from *tr* element) and *aria-colindex* (column index from *td* element) attribute.

{% tab template="treegrid/refresh", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { projectData } from './datasource';
import { TreeGridComponent  } from '@syncfusion/ej2-angular-treegrid';
import { RowSelectEventArgs } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegridObj [dataSource]='data' idMapping='TaskID' parentIdMapping='parentID' [treeColumnIndex]='1'  (rowSelected)='rowSelected($event)' [height]='267'>
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' width='70' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='150' ></e-column>
            <e-column field='StartDate' headerText='Start Date' textAlign='Right' [format]='formatOptions' width='90'></e-column>
            <e-column field='EndDate' headerText='Start Date' textAlign='Right' [format]='formatOptions'width='90'></e-column>
            <e-column field='Duration' headerText='Duration' width='80' textAlign='Right'></e-column>
            <e-column field='Progress' headerText='Progress' width='80' textAlign='Right'></e-column>
            <e-column field='Priority' headerText='Priority' width='90'></e-column>
        </e-columns>
    </ejs-treegrid>`,
})
export class AppComponent implements OnInit {

    public data: Object[] = [];
    public formatOptions: Object;

    ngOnInit(): void {
        this.data = projectData;
        this.formatOptions = { format: 'y/M/d', type: 'date' };
    }
    rowSelected(args: RowSelectEventArgs) {
        alert("row index: "+ " " + (args.row as HTMLTableRowElement).getAttribute('aria-rowindex'));
        alert("column index: "+ " " + args.target.closest('td').getAttribute('aria-colindex'));
    }

```

{% endtab %}