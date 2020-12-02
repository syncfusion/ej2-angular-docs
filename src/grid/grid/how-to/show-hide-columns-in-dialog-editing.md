---
title: "Show or Hide columns in Dialog editing"
component: "Grid"
description: "Learn how to Show or Hide columns in Dialog editing."
---

# Show or Hide columns in Dialog editing

You can show hidden columns or hide visible column's editor in the dialog while editing the grid record using [`actionBegin`](../../api/grid/#actionbegin) and [`actionComplete`](../../api/grid/#actioncomplete) events.

In the [`actionBegin`](../../api/grid/#actionbegin) event, based on **requestType** as **beginEdit** or  **add**. We can show or hide the editor by using [`column.visible`](../../api/grid/column/#visible) property.

In the [`actionComplete`](../../api/grid/#actioncomplete) event, based on **requestType** as **save**. We can reset the properties back to the column state.

In the below example, we have rendered the grid columns **CustomerID** as hidden column and **ShipCountry** as visible column. In the edit mode, we have changed the **CustomerID** column to visible state and **ShipCountry** column to hidden state.

{% tab template="grid/edit", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { EditSettingsModel, ToolbarItems, GridComponent, Column, SaveEventArgs, EditEventArgs } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [editSettings]='editSettings' [toolbar]='toolbar' (actionBegin)="actionBegin($event)"
     (actionComplete)="actionComplete($event)" height='273px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' isPrimaryKey='true' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' [visible]='false' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign= 'Right'
                     editType= 'numericedit' width=120 format= 'C2'></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' editType= 'dropdownedit' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];
    @ViewChild('grid') grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog' };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }

    actionBegin(args: EditEventArgs) {
        if ((args.requestType === 'beginEdit' || args.requestType === 'add')) {
            for (const cols of this.grid.columns) {
                if ((cols as Column).field === 'CustomerID') {
                    (cols as Column).visible = true;
                } else if ((cols as Column).field === 'ShipCountry') {
                    (cols as Column).visible = false;
                }
            }
        }
    }

    actionComplete(args: SaveEventArgs) {
        if (args.requestType === 'save') {
            for (const cols of this.grid.columns) {
                if ((cols as Column).field === 'CustomerID') {
                    (cols as Column).visible = false;
                } else if ((cols as Column).field === 'ShipCountry') {
                    (cols as Column).visible = true;
                }
            }
        }
    }
}

```

{% endtab %}
