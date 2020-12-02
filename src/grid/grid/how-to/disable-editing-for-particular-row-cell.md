---
title: "Disable editing for a particular row/cell"
component: "Grid"
description: "Learn how to Disable editing for a particular row/cell."
---

# Disable editing for a particular row/cell

You can disable the editing for a particular row by using the [`actionBegin`](../../api/grid/#actionbegin) event of Grid based on **requestType** as **beginEdit**.

In the below demo, the rows which are having the value for **ShipCountry** column as "France" is prevented from editing.

{% tab template="grid/edit", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [editSettings]='editSettings' [toolbar]='toolbar'
               (actionBegin)="actionBegin($event)" height='273px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' isPrimaryKey='true' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign= 'Right' editType= 'numericedit'
                     width=120 format= 'C2'></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' editType= 'dropdownedit' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];

    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowEditing: true };
        this.toolbar = ['Edit', 'Update', 'Cancel'];
    }

    actionBegin(args) {
        if (args.requestType === 'beginEdit') {
            if (args.rowData.ShipCountry === 'France') {
                args.cancel = true;
            }
        }
    }
}

```

{% endtab %}

For batch mode of editing, you can use [`cellEdit`](../../api/grid/#celledit) event of Grid. In the below demo, the cells which are having the value as "France" is prevented from editing.

{% tab template="grid/edit", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { EditSettingsModel, ToolbarItems, CellEditArgs } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [editSettings]='editSettings' [toolbar]='toolbar' (cellEdit)="cellEdit($event)" height='273px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' isPrimaryKey='true' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
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

    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowEditing: true, mode: 'Batch' };
        this.toolbar = ['Edit', 'Update', 'Cancel'];
    }

    cellEdit(args: CellEditArgs) {
        if (args.value === 'France') {
            args.cancel = true;
        }
    }
}

```

{% endtab %}
