---
title: "Enable editing in single click"
component: "Grid"
description: "Learn how to enable single click editing in the Essential JS 2 DataGrid control."
---

# Enable editing in single click

## Normal Editing

You can make a row editable on a single click with **Normal** mode of editing in Grid, by using the [`startEdit`](../../api/grid/#startedit) and [`endEdit`](../../api/grid/#endedit) methods.

Bind the **mouseup** event for Grid and in the event handler call the [`startEdit`](../../api/grid/#startedit) and [`endEdit`](../../api/grid/#endedit), based on the clicked target element.

{% tab template="grid/single-click-batch-editing", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { EditSettingsModel, ToolbarItems, GridComponent } from '@syncfusion/ej2-angular-grids';
import { MouseEventArgs } from '@syncfusion/ej2-base';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [editSettings]='editSettings' [toolbar]='toolbar' allowPaging='true' (load)='load($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100 isPrimaryKey='true'></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign= 'Right' width=120 format= 'C2'></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})

export class AppComponent implements OnInit {

    public data: object[];
    public toolbar: ToolbarItems[];
    @ViewChild('grid')
    public grid: GridComponent;
    public editSettings: EditSettingsModel;
    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Normal' };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }
    load(args){
        this.grid.element.addEventListener('mouseup', (e: MouseEventArgs) => {
        if ((e.target as HTMLElement).classList.contains("e-rowcell")) {
        if (this.grid.isEdit)
            this.grid.endEdit();
            let index: number = parseInt((e.target as HTMLElement).getAttribute("Index"));
            this.grid.selectRow(index);
            this.grid.startEdit();
        };
        });
    }
}

```

{% endtab %}

### Open dropdown edit popup on single click

You can open the default dropdown edit popup with single click edit by focusing the dropdown element and calling the EJ2 dropdown list's [`showPopup`](../../api/drop-down-list/#showpopup) method in the Grid's [`actionComplete`](../../api/grid/#actioncomplete) event. In this demo we have used a global flag variable in the **mouseup** event to ensure if the dropdown column is the clicked edit target.

{% tab template="grid/open-dropdown-popup", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { EditSettingsModel, ToolbarItems, GridComponent } from '@syncfusion/ej2-angular-grids';
import { MouseEventArgs } from '@syncfusion/ej2-base';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [editSettings]='editSettings' [toolbar]='toolbar' allowPaging='true' (load)='load($event)' (actionComplete)='onActionComplete($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100 isPrimaryKey='true'></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign= 'Right' width=120 format= 'C2'></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' editType='dropdownedit' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})

export class AppComponent implements OnInit {

    public data: object[];
    public toolbar: ToolbarItems[];
    @ViewChild('grid')
    public grid: GridComponent;
    public editSettings: EditSettingsModel;
    public isDropdown = false;

    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Normal' };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }
    load(args){
        this.grid.element.addEventListener('mouseup', (e: MouseEventArgs) => {
            if ((e.target as HTMLElement).classList.contains("e-rowcell")) {
              if (this.grid.isEdit)
                  this.grid.endEdit();
              let rowInfo = this.grid.getRowInfo(e.target);
              if (rowInfo.column.field === "ShipCountry")
                  this.isDropdown = true;
              this.grid.selectRow(rowInfo.rowIndex);
              this.grid.startEdit();
            }
        });
    }

    onActionComplete(args) {
        if (args.requestType =="beginEdit" && this.isDropdown) {
            this.isDropdown = false;
            let dropdownObj = args.form.querySelector('.e-dropdownlist').ej2_instances[0];
            dropdownObj.element.focus();
            dropdownObj.showPopup();
        }
    }

}

```

{% endtab %}

## Batch Editing

You can make a cell editable on a single click with **Batch** mode of editing in Grid, by using the [`editCell`](../../api/grid/edit/#editcell) method.

Bind the **mouseup** event for Grid and in the event handler call the [`editCell`](../../api/grid/edit/#editcell) method, based on the clicked target element.

{% tab template="grid/single-click-inline-editing", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { EditSettingsModel, ToolbarItems, GridComponent } from '@syncfusion/ej2-angular-grids';
import { MouseEventArgs } from '@syncfusion/ej2-base';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [editSettings]='editSettings' [toolbar]='toolbar' allowPaging='true' (load)='load($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100 isPrimaryKey='true'></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign= 'Right' width=120 format= 'C2'></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})

export class AppComponent implements OnInit {

    public data: object[];
    public toolbar: ToolbarItems[];
    @ViewChild('grid')
    public grid: GridComponent;
    public editSettings: EditSettingsModel;
    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Batch' };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }
    load(args){
        this.grid.element.addEventListener('mouseup', (e: MouseEventArgs) => {
        if ((e.target as HTMLElement).classList.contains("e-rowcell")) {
            let index: number = parseInt((e.target as HTMLElement).getAttribute("Index"));
            let colindex: number = parseInt((e.target as HTMLElement).getAttribute("aria-colindex"));
            let field: string = this.grid.getColumns()[colindex].field;
            this.grid.editModule.editCell(index, field);
        };
        });
    }
}

```

{% endtab %}