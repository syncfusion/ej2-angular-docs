---
title: "Refresh the data source"
component: "TreeGrid"
description: "Learn how to customize the Essential JS 2 Tree Grid."
---

# How To

## How to refresh the datasource

You can add/delete the datasource records through an external button. To reflect the datasource changes in Tree Grid, you need to assign the modified data to dataSource property.

Please follow the below steps to refresh the Tree Grid after datasource change.

**Step 1**:

Add/delete the datasource record by using the following code.

```typescript

    const dataSource: object = extendArray((this.treegridObj as TreeGridComponent).dataSource as object[]);

    // Added New Record.
    (dataSource as object[]).unshift({ TaskID: 99, TaskName: "New Data", StartDate: new Date('02/03/2017'), Duration: 10 });

    // Delete record.
    (dataSource as object[]).splice(selectedRowIndex, 1);

```

**Step 2**:

Refresh the Tree Grid after the datasource change by assign the modified data to dataSource property.

```typescript
    (this.treegridObj as TreeGridComponent).dataSource = dataSource; // Refresh the TreeGrid.

```

{% tab template="treegrid/refresh-datasource", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { projectData } from './datasource';
import { TreeGridComponent , extendArray  } from '@syncfusion/ej2-angular-treegrid';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';

@Component({
    selector: 'app-container',
    template: `<button #btn1 ejs-button cssClass="e-flat"  (click)="add()">Add</button>
    <button #btn2 ejs-button cssClass="e-flat" (click)="delete()">Delete</button>
    <ejs-treegrid #treegridObj [dataSource]='data' idMapping='TaskID' parentIdMapping='parentID' [treeColumnIndex]='1'[height]='280'>
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' width='70' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='100'></e-column>
            <e-column field='StartDate' headerText='Start Date' width='90' format="yMd" textAlign='Right'></e-column>
            <e-column field='EndDate' headerText='End Date' width='90' format="yMd" textAlign='Right'></e-column>
            <e-column field='Duration' headerText='Duration' width='90' textAlign='Right'></e-column>
            <e-column field='Priority' headerText='Priority' width='90'></e-column>
        </e-columns>
    </ejs-treegrid>`,
})
export class AppComponent implements OnInit {

    public data: Object[];
    @ViewChild('treegridObj')
    public treegridObj: TreeGridComponent;

    ngOnInit(): void {
        this.data = projectData;
    }
    add() {
        const dataSource = extendArray((this.treegridObj as TreeGridComponent).dataSource as object[]);
        (dataSource as object[]).unshift({ TaskID: 99, TaskName: "New Data", StartDate: new Date('02/03/2017'), EndDate: new Date('04/04/2017'), Duration: 10, Priority: "High" }); // Add record.
        (this.treegridObj as TreeGridComponent).dataSource = dataSource; // Refresh the TreeGrid.
    }
    delete() {
        const selectedRow = (this.treegridObj as TreeGridComponent).getSelectedRowIndexes().length;
        const selectedRowIndex = (this.treegridObj as TreeGridComponent).getSelectedRowIndexes()[0];
        const dataSource = extendArray((this.treegridObj as TreeGridComponent).dataSource as object[]);
        if (selectedRow > 0) {
            (dataSource as object[]).splice(selectedRowIndex, 1); // Delete record.
        }
        else {
            alert("No records selected for delete operation");
        }
        (this.treegridObj as TreeGridComponent).dataSource = dataSource; // Refresh the TreeGrid.
    }
}

```

{% endtab %}