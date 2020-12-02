---
title: "Custom Tooltip for columns"
component: "TreeGrid"
description: "Learn how to Custom Tooltip for columns."
---

# Custom Tooltip for columns

You can achieve the custom tooltip([`EJ2 Tooltip`](https://ej2.syncfusion.com/angular/documentation/tooltip/getting-started)) for Tree Grid by using the [`queryCellInfo`](../api/treegrid/#querycellinfo) event.

Render the ToolTip component for the Tree Grid cells by using the following code in the
[`queryCellInfo`](../api/treegrid/#querycellinfo) event.

```typescript

  public tooltip(args: QueryCellInfoEventArgs){
    const tooltip: Tooltip = new Tooltip({
      content: args.data[args.column.field].toString()
    });
    tooltip.appendTo(args.cell as HTMLElement);
  }

```

{% tab template="treegrid/refresh", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { projectData } from './datasource';
import { TreeGridComponent } from '@syncfusion/ej2-angular-treegrid';
import { QueryCellInfoEventArgs } from '@syncfusion/ej2-angular-grids';
import { Tooltip } from '@syncfusion/ej2-popups';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegridObj [dataSource]='data' idMapping='TaskID' parentIdMapping='parentID' [treeColumnIndex]='1' [height]='317' (queryCellInfo)='tooltip($event)' >
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' width='70' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='100' ></e-column>
            <e-column field='StartDate' headerText='Start Date' width='90' format="yMd" textAlign='Right'></e-column>
            <e-column field='EndDate' headerText='End Date' width='90' format="yMd" textAlign='Right'></e-column>
            <e-column field='Duration' headerText='Duration' width='80' textAlign='Right'></e-column>
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
    tooltip(args: QueryCellInfoEventArgs) {
        const tooltip: Tooltip = new Tooltip({
            content: args.data[args.column.field].toString()
        }, args.cell as HTMLTableCellElement);  
    }

```

{% endtab %}