---
title: "Change Column Header Text Dynamically"
component: "TreeGrid"
description: "Learn how to change column header text dynamically."
---

# Change column header Text dynamically

You can change the column [`headerText`](https://ej2.syncfusion.com/angular/documentation/api/treegrid/column/#headertext) dynamically through an external button.

Follow the given steps to change the header text dynamically:

**Step 1**:

Get the column object corresponding to the field name by using the [`getColumnByField`](https://ej2.syncfusion.com/angular/documentation/api/treegrid#getcolumnbyfield) method.
Then change the header Text value.

```typescript
      /** get the JSON object of the column corresponding to the field name */
      const column = this.treegridObj.getColumnByField("Duration");
      /** assign a new header text to the column */
      column.headerText = "Changed Text";
```

**Step 2**:

To reflect the changes in the Tree Grid header, invoke the [`refreshColumns`](https://ej2.syncfusion.com/angular/documentation/api/treegrid#refreshcolumns) method.

```typescript

      this.treegridObj.refreshColumns();

```

{% tab template="treegrid/refresh", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { projectData } from './datasource';
import { TreeGridComponent } from '@syncfusion/ej2-angular-treegrid';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';

@Component({
    selector: 'app-container',
    template: `<button #btn1 ejs-button cssClass="e-flat" [isToggle]="true"  (click)="click()">Change Header Text</button>

    <ejs-treegrid #treegridObj [dataSource]='data' idMapping='TaskID' parentIdMapping='parentID' [treeColumnIndex]='1' [height]='210'>
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' width='70' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='100' ></e-column>
            <e-column field='StartDate' headerText='Start Date' width='90' format="yMd" textAlign='Right'></e-column>
            <e-column field='EndDate' headerText='End Date' width='90' format="yMd" textAlign='Right'></e-column>
            <e-column field='Duration' headerText='Duration' width='90' textAlign='Right'></e-column>
            <e-column field='Priority' headerText='Priority' width='90'></e-column>
        </e-columns>
    </ejs-treegrid>`,
})
export class AppComponent implements OnInit {

    public data: Object[] = [];
    @ViewChild('treegridObj')
    public treegridObj: TreeGridComponent;

    ngOnInit(): void {
        this.data = projectData;
    }
    click() {
        const column = this.treegridObj.getColumnByField('Duration'); // get the JSON object of the column corresponding to the field name
        column.headerText = 'Changed Text'; // assign a new header text to the column
        this.treegridObj.refreshColumns();
    }
}

```

{% endtab %}
