---
title: "Provide custom data source and enabling filtering to DropDownList"
component: "TreeGrid"
description: "Learn how to Provide custom data source and enabling filtering to DropDownList."
---

# Provide custom data source and enabling filtering to DropDownList

You can provide data source to the DropDownList by using the **params** of [`columns.edit`](../api/treegrid/column/#edit) property.

While setting new data source using edit params, you must specify a new **query** property for the DropDownList as follows,

```typescript
  public priorityParams : IEditCell = {
    params:   {
      actionComplete: () => false,
      allowFiltering: true,
      dataSource: new DataManager(this.priorityData),
      fields: { text: "countryName", value: "countryName"},
      query: new Query()
    }
  };
```

You can also enable filtering for the DropDownList by passing the [`allowFiltering`](../../api/drop-down-list/#allowfiltering) as **true** to the edit params.

In the below demo, DropDownList is rendered with custom [`dataSource`](../../api/drop-down-list/#datasource) for the *Priority* column and enabled filtering to search DropDownList items.

{% tab template="treegrid/refresh", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { projectData } from './datasource';
import { TreeGridComponent, EditService, ToolbarService } from '@syncfusion/ej2-angular-treegrid';
import { DropDownList } from '@syncfusion/ej2-dropdowns';
import { Query, DataManager } from '@syncfusion/ej2-data';
import { IEditCell } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-container',
    providers: [EditService, ToolbarService],
    template: `<ejs-treegrid #treegrid [dataSource]='data' idMapping='TaskID' parentIdMapping='parentID' [treeColumnIndex]='1' [height]='265' [editSettings]='editSettings' (queryCellInfo)='tooltip($event)' >
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' isPrimaryKey='true'  width='70' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='100' ></e-column>
            <e-column field='StartDate' headerText='Start Date' width='100' [format]='formatOptions' editType= 'datepickeredit' textAlign='Right'></e-column>
            <e-column field='EndDate'  headerText='End Date' width='100' [format]='formatOptions' editType= 'datepickeredit' textAlign='Right'></e-column>
            <e-column field='Duration' headerText='Duration' width='90' textAlign='Right'></e-column>
            <e-column field='Priority' headerText='Priority' width='90' editType= 'dropdownedit'
                     [edit]='priorityParams'></e-column>
        </e-columns>
    </ejs-treegrid>`,
})
export class AppComponent implements OnInit {

    public data: Object[] = [];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];
    public editOptions: Object;
    public formatOptions: Object;
    public priorityParams: IEditCell;

    public priorityData : object[] = [
        { priorityName: 'Normal', priorityId: '1' },
        { priorityName: 'High', priorityId: '2' },
        { priorityName: 'Low', priorityId: '3' },
        { priorityName: 'Critical', priorityId: '4' },
        { priorityName: 'Breaker', priorityId: '5' }
    ];

    ngOnInit(): void {
        this.data = projectData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Row' };
        this.toolbar = ['Add', 'Edit', 'Delete'];
        this.editOptions = { params: { format: 'y/M/d' } };
        this.formatOptions = { format: 'y/M/d', type: 'date' };
        this.priorityParams = {
            params: {
                actionComplete: () => false,
                allowFiltering: true,
                dataSource: new DataManager(this.priorityData),
                fields: { text: 'priorityName', value: 'priorityName' },
                query: new Query()
            }
        };
    }

```

{% endtab %}