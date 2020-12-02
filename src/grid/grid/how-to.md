---
title: "How To"
component: "Grid"
description: "Learn how to refresh the datasource, exporting filtered data, enable and disable grid actions, customize the pager dropdown in Essential JS 2 DataGrid."
---

# How To

## Refresh the Datasource

You can add/delete the datasource records through an external button. To reflect the datasource changes in grid,
you need to invoke the [`refresh`](../../api/grid/#refresh) method.

Please follow the below steps to refresh the grid after datasource change.

**Step 1**:

Add/delete the datasource record by using the following code.

```typescript
    this.grid.dataSource.unshift(data); // Add a new record.

    this.grid.dataSource.splice(selectedRow, 1); // Delete a record.

```

**Step 2**:

Refresh the grid after the datasource change by using the [`refresh`](../../api/grid/#refresh) method.

```typescript
    this.grid.refresh(); // Refresh the Grid.

```

{% tab template="grid/change-headertext", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts"%}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { GridComponent } from '@syncfusion/ej2-angular-grids';
import { data } from './datasource';


@Component({
    selector: 'app-root',
    template: `<button ej-button class='e-flat' (click)='add()'> Add </button>
               <button ej-button class='e-flat' (click)='delete()'> Delete </button>
                <ejs-grid #grid [dataSource]='data' [height]='280' >
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=120 ></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
    }
    add(): void {
        const rdata: object = { OrderID: 10247, CustomerID: 'ASDFG', Freight: 40.4, OrderDate: new Date(8367642e5) };
        (this.grid.dataSource as object[]).unshift(rdata);
        this.grid.refresh();
    }
    delete(): void {
        const selectedRow: number = this.grid.getSelectedRowIndexes()[0];
        if (this.grid.getSelectedRowIndexes().length) {
            (this.grid.dataSource as object[]).splice(selectedRow, 1);
        } else {
            alert('No records selected for delete operation');
        }
        this.grid.refresh();
    }
}

```

{% endtab %}

## Enable/Disable Grid and its actions

You can enable/disable the Grid and its actions by applying/removing corresponding CSS styles.

To enable/disable the grid and its actions, follow the given steps:

**Step 1**:

Create CSS class with custom style to override the default style of Grid.

```css
    .disablegrid {
        pointer-events: none;
        opacity: 0.4;
    }
    .wrapper {
        cursor: not-allowed;
    }

```

**Step 2**:

Add/Remove the CSS class to the Grid in the click event handler of Button.

```typescript
    public btnClick():void {
      if (this.Grid.element.classList.contains('disablegrid')) {
          this.Grid.element.classList.remove('disablegrid');
          document.getElementById("GridParent").classList.remove('wrapper');
      }
      else {
          this.Grid.element.classList.add('disablegrid');
          document.getElementById("GridParent").classList.add('wrapper');
      }
    }

```

In the below demo, the button click will enable/disable the Grid and its actions.

{% tab template="grid/edit", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { EditSettingsModel, ToolbarItems, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<button ejs-button (click)="btnClick()"  cssClass="e-flat">Enable/Disable Grid</button>
               <div id="GridParent">
                    <ejs-grid #Grid [dataSource]='data' [editSettings]='editSettings' [toolbar]='toolbar' height='273px'>
                        <e-columns>
                            <e-column field='OrderID' headerText='Order ID' textAlign='Right' isPrimaryKey='true' width=100></e-column>
                            <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                            <e-column field='Freight' headerText='Freight' textAlign= 'Right'
                             editType= 'numericedit' width=120 format= 'C2'></e-column>
                            <e-column field='ShipCountry' headerText='Ship Country' editType= 'dropdownedit' width=150></e-column>
                        </e-columns>
                    </ejs-grid>
               </div>`
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('Grid') public Grid: GridComponent;
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];

    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowAdding: true, allowEditing: true, allowDeleting: true };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }
    public btnClick(): void {
        if (this.Grid.element.classList.contains('disablegrid')) {
            this.Grid.element.classList.remove('disablegrid');
            document.getElementById('GridParent').classList.remove('wrapper');
        } else {
            this.Grid.element.classList.add('disablegrid');
            document.getElementById('GridParent').classList.add('wrapper');
        }
    }
}

```

{% endtab %}

## Print the expanded state from other pages

By default, the expanded child grids will be printed from the current page alone. You can print the expanded child grids from other pages by using the [`actionBegin`](../../api/grid/#actionbegin) event.

In the following example, we have printed expanded child grids form other pages.

{% tab template="grid/default", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data, employeeData } from './datasource';
import { DetailRowService, GridComponent, getPrintGridModel, Row, Column,
     ToolbarService, printGridInit, GridModel, HierarchyGridPrintMode } from '@syncfusion/ej2-angular-grids';
import { extend } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='pData' [childGrid]='childGrid' [toolbar]='["Print"]'
     hierarchyPrintMode='Expanded' allowPaging=true [pageSettings]="{pageSize: 4}" (actionBegin)="actionBegin($event)" >
                    <e-columns>
                        <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                        <e-column field='FirstName' headerText='FirstName' width=150></e-column>
                        <e-column field='LastName' headerText='Last Name' width=150></e-column>
                        <e-column field='City' headerText='City' width=150></e-column>
                    </e-columns>
                </ejs-grid>
                `,
    providers: [DetailRowService, ToolbarService]
})
export class AppComponent implements OnInit {

    public pData: object[];
    public expandedChildGrid: object = {};
    public childGrid: GridModel = {
        dataSource: data,
        queryString: 'EmployeeID',
        columns: [
            { field: 'OrderID', headerText: 'Order ID', textAlign: 'Right', width: 120 },
            { field: 'CustomerID', headerText: 'Customer ID', width: 150 },
            { field: 'ShipCity', headerText: 'Ship City', width: 150 },
            { field: 'ShipName', headerText: 'Ship Name', width: 150 }
        ]
    };
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.pData = employeeData;
        this.grid.on(printGridInit, this.printInit, this);
    }

    actionBegin(args) {
        if (args.requestType === 'paging') {
            this.expandedChildGrid = extend({}, this.expandedChildGrid, this.getExpandedState(this.grid, 'Expanded', args.previousPage));
        }
    }

    printInit(gridModel) {
        gridModel.printgrid.expandedRows = extend({}, this.expandedChildGrid, gridModel.expandedRows);
    }

    getExpandedState(gObj: GridComponent, hierarchyPrintMode: HierarchyGridPrintMode, currentPage: number): object {
        const obj: object = {};
        const rows: Row<Column>[] = gObj.getRowsObject();
        for (const row of rows) {
            if (row.isExpand && !row.isDetailRow) {
                const index: number = gObj.allowPaging ? row.index +
                    (currentPage * gObj.pageSettings.pageSize) - gObj.pageSettings.pageSize : row.index;
                obj[index] = {};
                obj[index].isExpand = true;
                obj[index].gridModel = getPrintGridModel(row.childGrid, hierarchyPrintMode);
            }
        }
        return obj;
    }
}

```

{% endtab %}

## Columns

### Change Column Header Text Dynamically

You can change the column [`headerText`](../../api/grid/column/#headertext) dynamically through an external button.

Follow the given steps to change the header text dynamically:

**Step 1**:

Get the column object corresponding to the field name by using the [`getColumnByField`](../../api/grid/#getcolumnbyfield) method.
Then change the header Text value.

```typescript
let column = this.grid.getColumnByField('ShipCity'); // Get column object.
column.headerText = 'Changed Text';

```

**Step 2**:

To reflect the changes in the grid header, invoke the [`refreshHeader`](../../api/grid/#refreshheader) method.

```typescript
this.grid.refreshHeader();

```

{% tab template="grid/change-headertext", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts"%}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { GridComponent } from '@syncfusion/ej2-angular-grids';
import { data } from './datasource';


@Component({
    selector: 'app-root',
    template: `<button ej-button class='e-flat' (click)='click()'>Change Header Text</button>
                <ejs-grid #grid [dataSource]='data' [height]='280' >
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=120 ></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
    }
    click(): void {
        const column = this.grid.getColumnByField('ShipCity'); // get the JSON object of the column corresponding to the field name
        column.headerText = 'Changed Text'; // assign a new header text to the column
        this.grid.refreshHeader();
    }
}

```

{% endtab %}

### Customize Column Styles

You can customise the appearance of header and content of the particular column using the
[`customAttributes`](../../api/grid/column/#customattributes) property.

To customize the grid column, follow the given steps:

**Step 1**:

Create a css class with custom style to override the default style for rowcell and headercell.

```css
.e-grid .e-rowcell.customcss{
    background-color: #ecedee;
    color: 'red';
    font-family: 'Bell MT';
    font-size: 20px;
}

.e-grid .e-headercell.customcss{
    background-color: #2382c3;
    color: white;
    font-family: 'Bell MT';
    font-size: 20px;
}

```

**Step 2**:

Add the custom css class to particular column by using [`customAttributes`](../../api/grid/column/#customattributes) property.

{% tab template="grid/custom-column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [height]='315'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' [customAttributes]='customAttributes' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                        <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=120></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit{

    public data: object[];
    public customAttributes: object;

    ngOnInit(): void{
        this.data = data;
        this.customAttributes = {class: 'customcss'};
    }
}

```

{% endtab %}

### Custom Tooltip for Columns

You can achieve the custom tooltip([`EJ2 Tooltip`](../../../tooltip/getting-started)) for Grid by using the
[`queryCellInfo`](../../api/grid/#querycellinfo) event.

Render the ToolTip component for the grid cells by using the following code in the
[`queryCellInfo`](../../api/grid/#querycellinfo) event.

```typescript
tooltip (args: QueryCellInfoEventArgs) {
    let tooltip: Tooltip = new Tooltip({
        content: args.data[args.column.field].toString();
    }, args.cell);
}

```

{% tab template="grid/custom-tooltip", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { QueryCellInfoEventArgs } from '@syncfusion/ej2-angular-grids';
import { Tooltip } from '@syncfusion/ej2-popups';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='315' (queryCellInfo)='tooltip($event)' >
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                        <e-column field='ShipName' headerText='Ship Name' width=120></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
    tooltip(args: QueryCellInfoEventArgs) {
        const tooltip: Tooltip = new Tooltip({
            content: args.data[args.column.field].toString()
        }, args.cell as HTMLTableCellElement);
    }
}


```

{% endtab %}

### Render other components in a column

You can render any component in a grid column using the [`template`](../../api/grid/column/#template) property.

Initialize the column template for your custom component. The [`template`](../../api/grid/column/#template) property
renders the custom component.

```html
    <div>
        <ejs-dropdownlist value='Order Placed' [dataSource]='dropData' [popupHeight]='150' [popupWidth]='150' ></ejs-dropdownlist>
    </div>

```

{% tab template="grid/column-sync-comp", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='300'>
                    <e-columns>
                        <e-column headerText='Order Status'width='200'>
                            <ng-template #template let-data>
                                <div>
                                    <ejs-dropdownlist value='Order Placed' [dataSource]='dropData' [popupHeight]='150' [popupWidth]='150' >
                                    </ejs-dropdownlist>
                                </div>
                            </ng-template>
                        </e-column>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                        <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=120></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public dropData: string[];

    ngOnInit(): void {
        this.data = data;
        this.dropData = ['Order Placed', 'Processing', 'Delivered'];
    }
}

```

{% endtab %}

### Change the Orientation of Header Text

You can change the orientation of the header text by using the [`customAttributes`](../../api/grid/column/#customattributes) property.

To change the Orientation of Header Text, Ensure the following steps:

**Step 1**:

Create a css class with orientation style for grid header cell.

```css
.orientationcss .e-headercelldiv {
    transform: rotate(90deg);
}

```

**Step 2**:

Add the custom css class to particular column by using [`customAttributes`](../../api/grid/column/#customattributes) property.

```typescript
    <e-column field='Freight' headerText='Freight' textAlign='Center' format='C2' [customAttributes]='customAttributes' width=80></e-column>

```

**Step 3**:

Resize the header cell height by using the following code.

```typescript
setHeaderHeight(args) {
    let textWidth: number = document.querySelector('.orientationcss > div').scrollWidth;//Obtain the width of the headerText content.
    let headerCell: NodeList = document.querySelectorAll('.e-headercell');
    for(let i: number = 0; i < headerCell.length; i++) {
        (<HTMLElement>headerCell.item(i)).style.height = textWidth + 'px'; //Assign the obtained textWidth as the height of the headerCell.
    }
}

```

{% tab template="grid/header-orientation", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='240' (created)='setHeaderHeight($event)' >
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Center'
                         format='C2' [customAttributes]='customAttributes' width=80></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=100 ></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public customAttributes: object;

    ngOnInit(): void {
        this.data = data;
        this.customAttributes = { class: 'orientationcss' };
    }
    setHeaderHeight(args) {
        const textWidth = document.querySelector('.orientationcss > div').scrollWidth; // Obtain the width of the headerText content.
        const headerCell: NodeList = document.querySelectorAll('.e-headercell');
        for (let i = 0; i < headerCell.length; i++) {
            // Assign the obtained textWidth as the height of the headerCell.
            (headerCell.item(i) as HTMLElement).style.height = textWidth + 'px';
        }
    }
}

```

{% endtab %}

### Customize the icon for column menu

You can customize the column menu icon by overriding the default grid class **.e-icons.e-columnmenu** with a custom property **content** as mentioned below.

```css
.e-grid .e-columnheader .e-icons.e-columnmenu::before {
              content: "\e941";
      }
```

In the below sample, grid is rendered with a customized column menu icon.

{% tab template="grid/custom-column-menu-icon", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { ColumnMenuService } from '@syncfusion/ej2-angular-grids';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='315' showColumnMenu='true' >
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' width=90></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' format='C2' width=90></e-column>
                        <e-column field='ShipName' headerText='Ship Name' width=120></e-column>
                    </e-columns>
                </ejs-grid>`,
   providers: [ColumnMenuService]
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
}


```

{% endtab %}

## Editing

### Editing with template column

You can edit template column value by defining [`field`](../api/grid/column/#field) for that particular column.

In the below demo, the **ShipCountry** column is rendered with the template.

{% tab template="grid/edit", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [editSettings]='editSettings' [toolbar]='toolbar' height='273px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' isPrimaryKey='true' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign= 'Right'
                    editType= 'numericedit' width=120 format= 'C2'></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' editType= 'dropdownedit' width=150>
                        <ng-template #template let-data>
                            <a href="#">{{data.ShipCountry}}</a>
                        </ng-template>
                    </e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];

    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }
}

```

{% endtab %}

### Customize the Edit Dialog

You can customize the appearance of the edit dialog in the [`actionComplete`](../../api/grid/#actioncomplete) event based on **requestType** as **beginEdit** or **add**.

In the below example, we have changed the dialog's header text for editing and adding records.

{% tab template="grid/edit", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [editSettings]='editSettings' [toolbar]='toolbar'
     (actionComplete)="actionComplete($event)" height='273px'>
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
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog' };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }

    actionComplete(args) {
        if ((args.requestType === 'beginEdit' || args.requestType === 'add')) {
            const dialog = args.dialog;
            const CustomerID = 'CustomerID';
            // change the header of the dialog
            dialog.header = args.requestType === 'beginEdit' ? 'Record of ' + args.rowData[CustomerID] : 'New Customer';
        }
    }
}


```

{% endtab %}

### Show or Hide columns in Dialog editing

You can show hidden columns or hide visible column's editor in the dialog while editing the grid record using [`actionBegin`](../../api/grid/#actionbegin) and [`actionComplete`](../../api/grid/#actioncomplete) events.

In the [`actionBegin`](../../api/grid/#actionbegin) event, based on **requestType** as **beginEdit** or  **add**. We can show or hide the editor by using [`column.visible`](../api/grid/column/#visible) property.

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

### Cascading DropDownList with Grid editing

You can achieve the Cascading DropDownList with grid Editing by using the Cell Edit Template feature.

In the below demo, Cascading DropDownList rendered for **ShipCountry** and **ShipState** column.

{% tab template="grid/edit", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DropDownList } from '@syncfusion/ej2-dropdowns';
import { Query, DataManager } from '@syncfusion/ej2-data';
import { cascadeData } from './datasource';
import { EditSettingsModel, ToolbarItems, IEditCell } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [editSettings]='editSettings' [toolbar]='toolbar' height='273px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' isPrimaryKey='true' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' editType= 'dropdownedit'
                     [edit]='countryParams' width=150></e-column>
                    <e-column field='ShipState' headerText='Ship State' editType= 'dropdownedit' [edit]='stateParams' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];
    public countryParams: IEditCell;
    public stateParams: IEditCell;

    public countryElem: HTMLElement;
    public countryObj: DropDownList;

    public stateElem: HTMLElement;
    public stateObj: DropDownList;

    public country: object[] = [
        { countryName: 'United States', countryId: '1' },
        { countryName: 'Australia', countryId: '2' }
    ];
    public state: object[] = [
        { stateName: 'New York', countryId: '1', stateId: '101' },
        { stateName: 'Virginia ', countryId: '1', stateId: '102' },
        { stateName: 'Washington', countryId: '1', stateId: '103' },
        { stateName: 'Queensland', countryId: '2', stateId: '104' },
        { stateName: 'Tasmania ', countryId: '2', stateId: '105' },
        { stateName: 'Victoria', countryId: '2', stateId: '106' }
    ];

    ngOnInit(): void {
        this.data = cascadeData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
        this.countryParams = {
            create: () => {
                this.countryElem = document.createElement('input');
                return this.countryElem;
            },
            read: () => {
                return this.countryObj.text;
            },
            destroy: () => {
                this.countryObj.destroy();
            },
            write: () => {
                this.countryObj = new DropDownList({
                    dataSource: new DataManager(this.country),
                    fields: { value: 'countryId', text: 'countryName' },
                    change: () => {
                        this.stateObj.enabled = true;
                        const tempQuery: Query = new Query().where('countryId', 'equal', this.countryObj.value);
                        this.stateObj.query = tempQuery;
                        this.stateObj.text = null;
                        this.stateObj.dataBind();
                    },
                    placeholder: 'Select a country',
                    floatLabelType: 'Never'
                });
                this.countryObj.appendTo(this.countryElem);
            }
        };
        this.stateParams = {
            create: () => {
                this.stateElem = document.createElement('input');
                return this.stateElem;
            },
            read: () => {
                return this.stateObj.text;
            },
            destroy: () => {
                this.stateObj.destroy();
            },
            write: () => {
                this.stateObj = new DropDownList({
                    dataSource: new DataManager(this.state),
                    fields: { value: 'stateId', text: 'stateName' },
                    enabled: false,
                    placeholder: 'Select a state',
                    floatLabelType: 'Never'
                });
                this.stateObj.appendTo(this.stateElem);
            }
        };
    }
}

```

{% endtab %}

### Provide custom data source and enabling filtering to DropDownList

You can provide data source to the DropDownList by using the [`columns.edit.params`](../../api/grid/column/#edit) property.

While setting new data source using edit params, you must specify a new [`query`](../api/drop-down-list#query) property too for the DropDownList as follows,

```typescript
{
    this.countryParams = {
        params:   {
            allowFiltering: true,
            dataSource: this.country,
            fields: {text:'countryName',value:'countryName'},
            query: new Query(),
            actionComplete: () => false
            }
        }
}

```

You can also enable filtering for the DropDownList by passing the [`allowFiltering`](../api/drop-down-list#allowfiltering) as **true** to the edit params.

In the below demo, DropDownList is rendered with custom Datasource for the **ShipCountry** column and enabled filtering to search DropDownList items.

{% tab template="grid/edit", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DropDownList } from '@syncfusion/ej2-dropdowns';
import { Query, DataManager } from '@syncfusion/ej2-data';
import { cascadeData } from './datasource';
import { EditSettingsModel, ToolbarItems, IEditCell } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [editSettings]='editSettings' [toolbar]='toolbar' height='273px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' isPrimaryKey='true' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' editType= 'dropdownedit'
                     [edit]='countryParams' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];
    public countryParams: IEditCell;

    public country: object[] = [
        { countryName: 'United States', countryId: '1' },
        { countryName: 'Australia', countryId: '2' },
        { countryName: 'India', countryId: '3' }
    ];

    ngOnInit(): void {
        this.data = cascadeData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
        this.countryParams = {
            params: {
                allowFiltering: true,
                dataSource: new DataManager(this.country),
                fields: { text: 'countryName', value: 'countryName' },
                query: new Query(),
                actionComplete: () => false
            }
        };
    }

}

```

{% endtab %}

### Use Wizard like Dialog Editing

Wizard helps you create intuitive step-by-step forms to fill. You can achieve the wizard like editing by using the dialog template feature. It support your own editing template by defining [`editSettings.mode`](../../api/grid/editSettings/#mode) as **Dialog** and [`editSettingsTemplate`](../../api/grid/editSettings/#template) as template variable to define the editors.

The following example demonstrate the wizard like editing in the grid with the unobtrusive Validation.

{% tab template="grid/wizardtemplate", sourceFiles="app/app.component.ts,app/wizardtemplate.html,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { FormGroup } from '@angular/forms';
import { data } from './datasource';
import { DataUtil } from '@syncfusion/ej2-data';
import { EditSettingsModel, ToolbarItems, GridComponent, DialogEditEventArgs } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    templateUrl: `app/wizardtemplate.html`
})
export class AppComponent implements OnInit {

    public data: object[];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];
    public shipCountryDistinctData: object;
    public next = 'Next';
    public currentTab = 0;
    public hidden = true;
    @ViewChild('grid') grid: GridComponent;
    @ViewChild('orderForm') orderForm: FormGroup;

    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog' };
        this.toolbar = ['Add', 'Edit', 'Delete'];
        this.shipCountryDistinctData = DataUtil.distinct(data, 'ShipCountry', true);
    }

    actionComplete(args: DialogEditEventArgs) {
        if ((args.requestType === 'beginEdit' || args.requestType === 'add')) {
            args.form.ej2_instances[0].rules = {}; // Disable deafault valdation.
            // Set initail Focus
            if (args.requestType === 'beginEdit') {
                (args.form.elements.namedItem('CustomerID') as HTMLInputElement).focus();
            }
            this.currentTab = 0;
            this.hidden = true;
            this.next = 'Next';
        }
    }

    nextBtn(args) {
        if (this.orderForm.valid) {
            if (this.next !== 'SUBMIT') {
                this.currentTab++;
                this.nextpre(this.currentTab);
            } else {
                this.grid.endEdit();
            }
        }
    }

    previousBtn(args) {
        if (this.orderForm.valid) {
            this.currentTab--;
            this.nextpre(this.currentTab);
        }
    }

    nextpre(current) {
        if (current) {
            this.hidden = false;
            this.next = 'SUBMIT';
        } else {
            this.hidden = true;
            this.next = 'NEXT';
        }
    }
}

```

{% endtab %}

### Using Tab Inside the Dialog Editing

You can use [`Tab`](../../../tab/getting-started/) component inside dialog edit UI using dialog template feature. The dialog template feature can be enabled by defining  [`editSettings.mode`](../../api/grid/editSettings/#mode) as **Dialog** and [`editSettingsTemplate`](../../api/grid/editSettings/#template) as template variable to define the editors.

To include tab components in the Dialog, please ensure the following steps:

**Step 1**:

Initialize the template for your tab component.

```html
        <div id="tab1">
        <div class="form-row">
            <div class="form-group col-md-6">
                <div class="e-float-input e-control-wrapper" [ngClass]="{'e-error': OrderID.invalid && (OrderID.dirty || OrderID.touched)}">
                    <input [(ngModel)]="data.OrderID" required id="OrderID" name="OrderID" type="text" [attr.disabled]="!data.isAdd ? '' : null" #OrderID="ngModel">
                    <span class="e-float-line"></span>
                    <label class="e-float-text e-label-top" for="OrderID"> Order ID</label>
                </div>
                <div id="OrderIDError" *ngIf='OrderID.invalid && (OrderID.dirty || OrderID.touched)'>
                    <label class="e-error" for="OrderID" id="OrderID-info" style="display: block;">*Order ID is required</label>
                </div>
            </div>
        </div>
        <div class="form-row">
            <div class="form-group col-md-6">
                <div class="e-float-input e-control-wrapper" [ngClass]="{'e-error': CustomerID.invalid && (CustomerID.dirty || CustomerID.touched)}">
                    <input [(ngModel)]="data.CustomerID" required id="CustomerID" name="CustomerID" type="text" #CustomerID="ngModel">
                    <span class="e-float-line"></span>
                    <label class="e-float-text e-label-top" for="CustomerID">Customer Name</label>
                </div>
                <div id="CustomerIDError" *ngIf='CustomerID.invalid && (CustomerID.dirty || CustomerID.touched)'>
                    <label class="e-error" for="CustomerID" id="CustomerID-info" style="display: block;">*Customer Name is required</label>
                </div>
            </div>
        </div>
        <button ejs-button type="button" cssClass="e-info e-btn" style="float: right" (click)="nextBtn($event)" >next</button>
    </div>

    <div id="tab2" style='display: none'>
        <div class="form-row" >
            <div class="form-group col-md-6">
                <ejs-dropdownlist id="ShipCountry" name="ShipCountry" [(ngModel)]="data.ShipCountry" [dataSource]='shipCountryDistinctData' [fields]="{text: 'ShipCountry', value: 'ShipCountry' }" placeholder="Ship Country" popupHeight='300px' floatLabelType='Always'></ejs-dropdownlist>
            </div>
        </div>
        <div class="form-row">
            <div class="form-group col-md-6">
                <ejs-checkbox #Verified name="Verified" id="Verified" label="Verified" [checked]="data.Verified" ></ejs-checkbox>
            </div>
        </div>
        <button ejs-button type="button" cssClass="e-info e-btn" style="float: right" (click)='submitBtn($event)'>submit</button>
    </div>

```

**Step 2**:

To render the Tab component, use the [`editSettingsTemplate`](../../api/grid/editSettings/#template) of the Grid.

```html

    <ejs-tab #tab id="tab_wizard" showCloseButton=false (selecting)='selecting($event)'>
        <e-tabitems>
            <e-tabitem [header]="{ 'text': 'Details' }" content="#tab1"></e-tabitem>
            <e-tabitem [header]="{ 'text': 'Verify' }" content="#tab2"></e-tabitem>
        </e-tabitems>
    </ejs-tab>

```

The following example, we have rendered tab control inside the edit dialog. The tab control has two tabs and once you fill the first tab and navigate to second one. The validation for first tab was done before navigate to second.

{% tab template="grid/tablikeedit", sourceFiles="app/app.component.ts,app/tablikeedit.html,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { FormGroup } from '@angular/forms';
import { DataUtil } from '@syncfusion/ej2-data';
import { data } from './datasource';
import { EditSettingsModel, ToolbarItems, GridComponent, DialogEditEventArgs } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    templateUrl: `./app/tablikeedit.html`
})
export class AppComponent implements OnInit {

    public data: object[];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];
    public shipCountryDistinctData: object;
    @ViewChild('grid')
    grid: GridComponent;
    @ViewChild('orderForm')
    orderForm: FormGroup
    @ViewChild('tab')
    tabObj: any;

    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog' };
        this.toolbar = ['Add', 'Edit', 'Delete'];
        this.shipCountryDistinctData = DataUtil.distinct(data, 'ShipCountry', true );
    }

    actionComplete(args: DialogEditEventArgs) {
        if ((args.requestType === 'beginEdit' || args.requestType === 'add')) {
            // Disable deafault valdation.
            args.form.ej2_instances[0].rules = {};
            // Set initail Focus
            if (args.requestType === 'beginEdit') {
                (args.form.elements.namedItem('CustomerID')as HTMLInputElement).focus();
            }
        }
    }

    nextBtn() {
        this.moveNext();
    }

    selecting(e) {
     if(e.isSwiped){
       e.cancel = true;
     }
     if(e.selectingIndex === 1) {
       e.cancel = !this.orderForm.valid;
     }
    }

    moveNext() {
        if (this.orderForm.valid)) {
            this.tabObj.select(1);
        }
    }
    submitBtn() {
        if (this.orderForm.valid) {
            this.grid.endEdit();
        }
    }
}

```

{% endtab %}

### Disable editing for a particular row/cell

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

### Perform Grid actions by keyboard shortcut keys

Using keyboard shortcuts, Grid performs navigation and actions.

In addition, You can also perform grid actions with custom keyboard shortcuts. This operation has to be achieved outside of the grid with the help of **keydown** event.

The following example demonstrates on **Adding** a new row when Enter key is pressed in the grid.

{% tab template="grid/edit", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { cascadeData } from './datasource';
import { EditSettingsModel, ToolbarItems, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid  #grid [dataSource]='data' (load)="load()" [editSettings]='editSettings' [toolbar]='toolbar' height='273px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' isPrimaryKey='true' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];
    @ViewChild('grid') Grid: GridComponent;
    load() {
        document.getElementsByClassName('e-grid')[0].addEventListener('keydown', this.keyDownHandler.bind(this));
    }

    keyDownHandler(e: any) {
        if (e.keyCode === 13) {
            this.Grid.addRecord();
        }
    }

    ngOnInit(): void {
        this.data = cascadeData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }

}

```

{% endtab %}

### Make a cell editable on a single click with batch editing

You can make a cell editable on a single click with **batch** mode of editing in Grid, by using the [`editCell`](../../api/grid/#editcell) method.

Bind the click event for the Grid and in the click event handler call the [`editCell`](../../api/grid/#editcell) method, based on the clicked target element.

{% tab template="grid/edit", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { EditSettingsModel, ToolbarItems, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #Grid [dataSource]='data' (click)='click($event)' [editSettings]='editSettings' [toolbar]='toolbar' height='273px'>
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
    @ViewChild('Grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowAdding: true, allowDeleting: true, allowEditing: true, mode: 'Batch' };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }

    click(event: any) {
        if ((event.target as any).classList.contains('e-rowcell')) {
            const index: number = parseInt((event.target as any).getAttribute('Index'), 10);
            const colindex: number = parseInt((event.target as any).getAttribute('aria-colindex'), 10);
            const field: string = this.grid.getColumns()[colindex].field;
            this.grid.editModule.editCell(index, field);
        }
    }
}

```

{% endtab %}

## Sort

### Perform single/multi sorting dynamically

You can perform single-column or multi-column sorting dynamically through an external button.

To perform single-column sorting, use the [`sortColumn`](../../api/grid/column/#sortcolumn) method of Grid.

```typescript
    public SingleSort():void {
      this.grid.sortColumn("OrderID","Descending")
    }

```

To perform multi-column sorting, you need to push the columns to be sorted into the [`sortSettings.columns`](../../api/grid/#sortsettings).

```typescript
    public MultiSort():void {
        this.grid.sortSettings.columns.push({ field: 'CustomerID',  direction: 'Ascending' },{ field: 'ShipName', direction: 'Descending' });
        this.grid.refresh();
    }

```

In the below demo, click on the corresponding button to perform single-column or multi-column sorting.

{% tab template="grid/edit", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<button ejs-button (click)="SingleSort()"  cssClass="e-flat">Sort <b>OrderID</b> column</button>
               <button ejs-button (click)="MultiSort()"  cssClass="e-flat">Sort <b>CustomerID</b> and <b>ShipName</b> columns</button>
               <div id="GridParent">
                    <ejs-grid #Grid [dataSource]='data' allowSorting='true' [toolbar]='toolbar' height='273px'>
                        <e-columns>
                            <e-column field='OrderID' headerText='Order ID' textAlign='Right' isPrimaryKey='true' width=100></e-column>
                            <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                            <e-column field='Freight' headerText='Freight' textAlign= 'Right'
                             editType= 'numericedit' width=120 format= 'C2'></e-column>
                            <e-column field='ShipName' headerText='Ship Name' editType= 'dropdownedit' width=150></e-column>
                        </e-columns>
                    </ejs-grid>
               </div>`
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('Grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
    }
    public SingleSort(): void {
        this.grid.sortColumn('OrderID', 'Descending');
    }
    public MultiSort(): void {
        this.grid.sortSettings.columns.push({ field: 'CustomerID', direction: 'Ascending' },
            { field: 'ShipName', direction: 'Descending' });
        this.grid.refresh();
    }
}

```

{% endtab %}

### Dynamically clear sort for particular/entire sorted columns in Grid

You can clear the sorting for a particular column or the entire sorted columns in Grid dynamically through an external button.

To clear sort for a particular column, you need to splice the particular column from the [`sortSettings.columns`](../../api/grid/#sortsettings).

```typescript
    public SingleClearSort():void {
        let column: any = this.grid.sortSettings.columns;
        for(let i=0;i < column.length;i++) {
            if(column[i].field == "OrderID") {
                column.splice(i,1);
                this.grid.refresh();
            }
        }
    }
```

To clear sorting for all the sorted columns, use the [`clearSorting`](../../api/grid/#clearsorting) method of Grid.

```typescript
    public MultiClearSort():void {
        this.grid.clearSorting();
    }

```

In the below demo, click on the corresponding button to clear sort for particular or entire sorted columns in Grid.

{% tab template="grid/edit", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<button ejs-button (click)="SingleClearSort()"  cssClass="e-flat">Clear the sort for <b>OrderID</b> column</button>
               <button ejs-button (click)="MultiClearSort()"  cssClass="e-flat">Clear sorting for entire sorted columns</button>
               <div id="GridParent">
                    <ejs-grid #Grid [dataSource]='data' [sortSettings]='sortOptions' allowSorting='true' [toolbar]='toolbar' height='273px'>
                        <e-columns>
                            <e-column field='OrderID' headerText='Order ID' textAlign='Right' isPrimaryKey='true' width=100></e-column>
                            <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                            <e-column field='Freight' headerText='Freight' textAlign= 'Right'
                             editType= 'numericedit' width=120 format= 'C2'></e-column>
                            <e-column field='ShipName' headerText='Ship Name' editType= 'dropdownedit' width=150></e-column>
                        </e-columns>
                    </ejs-grid>
               </div>`
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('Grid') public grid: GridComponent;
    public sortOptions: object;

    ngOnInit(): void {
        this.data = data;
        this.sortOptions = { columns: [{ field: 'OrderID', direction: 'Ascending' }, { field: 'CustomerID', direction: 'Descending' }] };
    }
    public SingleClearSort(): void {
        const column: any = this.grid.sortSettings.columns;
        for (let i = 0; i < column.length; i++) {
            if (column[i].field === 'OrderID') {
                column.splice(i, 1);
                this.grid.refresh();
            }
        }
    }
    public MultiClearSort(): void {
        this.grid.clearSorting();
    }
}

```

{% endtab %}

## Foreign Key

### Use Edit Template in Foreign Key Column

By default, foreign key column uses dropdown component for editing.
You can render other than the dropdown by using the [`column.edit`](../../api/grid/column/#edit) property.
The following example demonstrates the way of using edit template in foreign column.

In the following example, The **Employee Name** is a foreign key column and while editing, AutoComplete component is rendered instead of DropDownList.

{% tab template="grid/foreignkey", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { createElement } from '@syncfusion/ej2-base';
import { ForeignKeyService, EditService, IEditCell, EditSettingsModel, ToolbarService, Column } from '@syncfusion/ej2-angular-grids';
import { DataManager, Query } from '@syncfusion/ej2-data';
import { AutoComplete } from '@syncfusion/ej2-angular-dropdowns';
import { data, employeeData } from './datasource';


@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='270' [editSettings]='editoption' [toolbar]='toolbar'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' isPrimaryKey='true' textAlign='Right' width=100></e-column>
                        <e-column field='EmployeeID' headerText='Employee Name' width=120
                        foreignKeyValue='FirstName' [dataSource]='employeeData' [edit]='edit'></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' width=80></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=130></e-column>
                    </e-columns>
                </ejs-grid>`,
    providers: [ForeignKeyService, EditService, ToolbarService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public employeeData: object[];
    public editoption: EditSettingsModel = { allowEditing: true };
    public autoComplete: AutoComplete;
    toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    public edit: IEditCell = {
        create: () => { // to create input element
            return createElement('input');
        },
        read: () => { // return edited value to update data source
            const EmployeeID = 'EmployeeID';
            const value = new DataManager(employeeData).executeLocal(new Query().where('FirstName', 'equal', this.autoComplete.value));
            return value.length && value[0][EmployeeID]; // to convert foreign key value to local value.
        },
        destroy: () => { // to destroy the custom component.
            this.autoComplete.destroy();
        },
        write: (args: { rowData: object, column: Column, foreignKeyData: object,
             element: HTMLTableCellElement }) => { // to show the value for date picker
            this.autoComplete = new AutoComplete({
                dataSource: employeeData,
                fields: { value: args.column.foreignKeyValue },
                value: args.foreignKeyData[0][args.column.foreignKeyValue]
            });
            this.autoComplete.appendTo(args.element);
        }
    }

    ngOnInit(): void {
        this.data = data;
        this.employeeData = employeeData;
    }
}


```

{% endtab %}

### Customizing filter menu operators list

You can customize the default filter operator list by defining the
[`filterSettings.operators`](../../api/grid/filterSettings/#operators) property. The available options are:

* **stringOperator**- defines customized string operator list.
* **numberOperator** - defines customized number operator list.
* **dateOperator** - defines customized date operator list.
* **booleanOperator** - defines customized boolean operator list.

In the following sample, we have customized string filter operators.
{% tab template="grid/filtering1", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { FilterSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowFiltering]='true' [filterSettings]='filterOptions' height='273px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=100></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=100></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public filterOptions: FilterSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.filterOptions = {
           type: 'Menu',
           operators: {
               stringOperator: [
                   { value: 'startsWith', text: 'starts with' },
                   { value: 'endsWith', text: 'ends with' },
                   { value: 'contains', text: 'contains' }
                ],
            }
        };
    }
}

```

{% endtab %}

### Customize filter UI in foreign key column

You can create your own filtering UI by using [`column.filter`](../../api/grid/column/#filter) property.
The following example demonstrates the way to create a custom filtering UI in the foreign column.

In the following example, The **Employee Name** is a foreign key column. DropDownList is rendered using Filter UI.

{% tab template="grid/foreignkey", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { createElement } from '@syncfusion/ej2-base';
import { GridComponent, ForeignKeyService, FilterService, IFilter, FilterSettingsModel, Filter } from '@syncfusion/ej2-angular-grids';
import { DataManager } from '@syncfusion/ej2-data';
import { DropDownList } from '@syncfusion/ej2-angular-dropdowns';
import { data, fEmployeeData } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='315' [allowFiltering]='true'
        [filterSettings]='filteroption'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                        <e-column field='EmployeeID' headerText='Employee Name' width=120
                        foreignKeyValue='FirstName' [dataSource]='employeeData' [filter]='filter'></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' width=80></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=130  ></e-column>
                    </e-columns>
                </ejs-grid>`,
    providers: [ForeignKeyService, FilterService]
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('grid') public grid: GridComponent;
    public employeeData: object[];
    public dropInstance: DropDownList;
    public filteroption: FilterSettingsModel = { type: 'Menu'};
    public filter: IFilter = {
        ui: {
            create: (args: { target: Element, column: object }) => {
                const flValInput: HTMLElement = createElement('input', { className: 'flm-input' });
                args.target.appendChild(flValInput);
                this.dropInstance = new DropDownList({
                    dataSource: new DataManager(fEmployeeData),
                    fields: { text: 'FirstName', value: 'EmployeeID' },
                    placeholder: 'Select a value',
                    popupHeight: '200px'
                });
                this.dropInstance.appendTo(flValInput);
            },
            write: (args: {
                column: object, target: Element, parent: any,
                filteredValue: number | string
            }) => {
                this.dropInstance.text = args.filteredValue as string || '';
            },
            read: (args: { target: Element, column: any, operator: string, fltrObj: Filter }) => {
                args.fltrObj.filterByColumn(args.column.field, args.operator, this.dropInstance.text);
            }
        }
    };
    ngOnInit(): void {
        this.data = data;
        this.employeeData = fEmployeeData;
    }
}

```

{% endtab %}

### Use filter bar template in foreign key column

You can use the filter bar template in foreign key column by defining the
[`column.filterBarTemplate`](../../api/grid/column/#filterbartemplate) property.
The following example demonstrates the way to use filter bar template in foreign column.

In the following example, The **Employee Name** is a foreign key column.
This column header shows the custom filter bar template and you can select filter value by using the **DropDown** options.

{% tab template="grid/foreignkey", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { createElement } from '@syncfusion/ej2-base';
import { GridComponent, ForeignKeyService, FilterService, IFilterUI, Column } from '@syncfusion/ej2-angular-grids';
import { DataManager } from '@syncfusion/ej2-data';
import { DropDownList } from '@syncfusion/ej2-angular-dropdowns';
import { data, fEmployeeData } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='260' [allowFiltering]='true'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                        <e-column field='EmployeeID' headerText='Employee Name' width=120
                        foreignKeyValue='FirstName' [dataSource]='employeeData' [filterBarTemplate]='filter'></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' width=80></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=130  ></e-column>
                    </e-columns>
                </ejs-grid>`,
    providers: [ForeignKeyService, FilterService]
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('grid') public grid: GridComponent;
    public employeeData: object[];
    public filter: IFilterUI = {
        create: (args: { element: Element, column: Column }) => {
            return createElement('input', { className: 'flm-input' });
        },
        write: (args: { element: Element, column: Column }) => {
            fEmployeeData.splice(0, 0, {FirstName: 'All'}); // for clear filtering
            const dropInstance: DropDownList = new DropDownList({
                dataSource: new DataManager(fEmployeeData),
                fields: { text: 'FirstName' },
                placeholder: 'Select a value',
                popupHeight: '200px',
                index: 0,
                change: (e) => {
                    if (e.value !== 'All') {
                        this.grid.filterByColumn('EmployeeID', 'equal', e.value);
                    } else {
                        this.grid.removeFilteredColsByField('EmployeeID');
                    }
                }
            });
            dropInstance.appendTo(args.element as HTMLTableCellElement);
        }
    };
    ngOnInit(): void {
        this.data = data;
        this.employeeData = fEmployeeData;
    }
}

```

{% endtab %}

### Perform aggregation in Foreign Key Column

Default aggregations are not supported in a foreign key column.
You can achieve aggregation for the foreign key column by using custom the aggregates.
The following example demonstrates the way to achieve aggregation in foreign key column.

In the following example, The **Employee Name** is a foreign key column and the aggregation for the foreign column was calculated in customAggregateFn.

{% tab template="grid/foreignkey", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { ForeignKeyService, AggregateService, getForeignData, CustomSummaryType,
     AggregateColumnModel, GridComponent } from '@syncfusion/ej2-angular-grids';
import { data, employeeData } from './datasource';
import { getValue } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='280'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                        <e-column field='EmployeeID' headerText='Employee Name' width=120
                         foreignKeyValue='FirstName' [dataSource]='employeeData'></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' width=80></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=130  ></e-column>
                    </e-columns>
                    <e-aggregates>
                        <e-aggregate>
                            <e-columns>
                                <e-column field="EmployeeID" type="Custom" [customAggregate]= 'customAggregateFn'>
                                    <ng-template #footerTemplate let-data>
                                        Count of Margaret:  {{data.Custom}}
                                    </ng-template>
                                </e-column>
                            </e-columns>
                        </e-aggregate>
                    </e-aggregates>
                </ejs-grid>`,
    providers: [ForeignKeyService, AggregateService]
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('grid') public grid: GridComponent;
    public employeeData: object[];

    // Custom Aggregate function for foreign column
    public customAggregateFn: CustomSummaryType = (data1: any, column: AggregateColumnModel) => {
        return data1.result.filter((dObj: object) => {
            return getValue('FirstName', getForeignData(this.grid.getColumnByField(column.field), dObj)[0]) === 'Margaret';
        }).length;
    }

    ngOnInit(): void {
        this.data = data;
        this.employeeData = employeeData;
    }
}
  
```

{% endtab %}

### Bind foreign key dataSource on dropdown edit

When editing, you can bind foreign key datasource to a dropdown list by using [`column.dataSource`](../../api/grid/column/#datasource) property.

{% tab template="grid/foreignkey", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { ForeignKeyService, EditSettingsModel, ToolbarItems, EditService, ToolbarService } from '@syncfusion/ej2-angular-grids';
import { data, employeeData } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [editSettings]='editSettings' [toolbar]='toolbar' [height]='315'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                        <e-column field='EmployeeID' headerText='Employee Name' width=120
                        foreignKeyValue='FirstName' [dataSource]='employeeData'></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' width=80></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=130  ></e-column>
                    </e-columns>
                </ejs-grid>`,
    providers: [ForeignKeyService, EditService, ToolbarService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public employeeData: object[];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];

    ngOnInit(): void {
        this.data = data;
        this.employeeData = employeeData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }
}

```

{% endtab %}

> * By default, the foreign key column's **editType** will be set as **dropdownedit**.

## Exporting

### Exporting Grid in Cordova application

Cordova application does not support direct file download. So we have to use the Blob stream to export the Grid.
You can use corresponding exporting methods and exportComplete events to get the Blob stream.

{% tab template="grid/exporting", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import {
    GridComponent, ToolbarItems, ToolbarService, ExcelExportService, PdfExportService,
    ExcelExportCompleteArgs, PdfExportCompleteArgs
} from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions' height='272px' [allowExcelExport]='true'
    (excelExportComplete)='excelExpComplete($event)' (pdfExportComplete)='pdfExpComplete($event)'
      [allowPdfExport]='true' (toolbarClick)='toolbarClick($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                </e-columns>
                </ejs-grid>`,
    providers: [ToolbarService, ExcelExportService, PdfExportService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];
    @ViewChild('grid') public grid: GridComponent;
    public exportBlob = (blob: Blob) => {
        const a: HTMLAnchorElement = document.createElement('a');
        document.body.appendChild(a);
        a.style.display = 'none';
        const url: string = (window.URL as any).createobjectURL(blob);
        a.href = url;
        a.download = 'Export';
        a.click();
        (window.URL as any).revokeobjectURL(url);
        document.body.removeChild(a);
    }

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['PdfExport', 'ExcelExport'];
    }

    toolbarClick(args: ClickEventArgs) {
        if (args.item.id === 'Grid_pdfexport') {
            this.grid.pdfExport(null, null, null, true);
        }
        if (args.item.id === 'Grid_excelexport') {
            this.grid.excelExport(null, null, null, true);
        }
    }

    excelExpComplete(args: ExcelExportCompleteArgs) {
        // This event will be triggered when excel exporting.
        args.promise.then((e: { blobData: Blob }) => {
            // In this `then` function, we can get blob data through the arguments after promise resolved.
            this.exportBlob(e.blobData);
        });
    }

    pdfExpComplete(args: PdfExportCompleteArgs) {
        // This event will be triggered when pdf exporting.
        args.promise.then((e: { blobData: Blob }) => {
            // In this `then` function, we can get blob data through the arguments after promise resolved.
            this.exportBlob(e.blobData);
        });
    }
}


```

{% endtab %}

### Exporting Filtered Data Only

You can export the filtered data by defining the resulted data in [`exportProperties.dataSource`](../api/grid/excelExportProperties/#datasource) before export.

In the below Pdf exporting demo, We have gotten the filtered data by applying filter query to the grid data and then defines the resulted data in [`exportProperties.dataSource`](../api/grid/excelExportProperties/#datasource) and pass it to [`pdfExport`](../api/grid/#pdfexport) method.

{% tab template="grid/exporting-filtered-data", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, ToolbarItems, ToolbarService, PdfExportService,
 PageService, FilterService } from '@syncfusion/ej2-angular-grids';
import { ClickEventArgs } from '@syncfusion/ej2-angular-navigations';
import {DataManager} from '@syncfusion/ej2-data';

@Component({
  selector: 'app-root',
  template: `<ejs-grid #grid id='Grid' [dataSource]='data' [toolbar]='toolbarOptions'
   [allowFiltering]='true' [allowPaging]='true' [pageSettings]='initialPage' [allowPdfExport]='true'
   (toolbarClick)='toolbarClick($event)'>
              <e-columns>
                  <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                  <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                  <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
              </e-columns>
              </ejs-grid>`,
  providers: [ToolbarService, PdfExportService, PageService, FilterService]
})
export class AppComponent implements OnInit {

  public data: object[];
  public toolbarOptions: ToolbarItems[];
  public initialPage: object;
  @ViewChild('grid')
  public grid: GridComponent;
  ngOnInit(): void {
    this.data = data;
    this.toolbarOptions = ['PdfExport'];
    this.initialPage = { pageCount: 5, pageSize: 5 };
  }

  toolbarClick(args: ClickEventArgs) {
    if (args.item.id === 'Grid_pdfexport') {
      let pdfdata;
      const query = this.grid.renderModule.data.generateQuery(); // get grid corresponding query
      for (let i = 0; i < query.queries.length; i++) {
        if (query.queries[i].fn === 'onPage') {
          query.queries.splice(i, 1);       // remove page query to get all records
          break;
        }
      }
      const fdata = new DataManager({ json: data }).executeQuery(query).then((e: any) => {
        pdfdata = e.result as object[];  // get all filtered records
        const exportProperties = {
          dataSource: pdfdata,
        };
        this.grid.pdfExport(exportProperties);
      }).catch((e) => true);
    }
  }
}

```

{% endtab %}

## Pager

## Customize Pager DropDown

To customize default values of pager dropdown, you need to define [`pageSizes`](../../api/grid/pageSettingsModel/#pagesizes) as array of strings.

{% tab template="grid/custom-column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' allowPaging='true' [pageSettings]='initialPage'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                        <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=120></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public initialPage: object;

    ngOnInit(): void {
        this.data = data;
        this.initialPage = { pageSizes: ['5', '10', 'All'], };
    }
}

```

{% endtab %}

## Hide the expand/collapse icon in parent row when no records in child grid

By default, the expand/collapse icon will be visible even if the child grid is empty.

You can use [`rowDataBound`](../../api/grid/#rowdatabound) event to hide the icon when there are no records in child grid.

To hide the expand/collapse icon in parent row when no records in child grid, follow the given steps:

**Step 1**:

Create CSS class with custom style to override the default style of Grid.

```css
    .e-row[aria-selected="true"] .e-customizedExpandcell {
        background-color: #e0e0e0;
    }

    .e-grid.e-gridhover tr[role='row']:hover {
        background-color: #eee;
    }

```

**Step 2**:

Add the CSS class to the Grid in the [`rowDataBound`](../../api/grid/#rowdatabound-) event handler of Grid.

```typescript
    public rowDataBound(args:any){
        let filter:string = args.data.EmployeeID;
        let childrecord: any = new DataManager(this.Grid.childGrid.dataSource).executeLocal(new Query().where('EmployeeID', 'equal', parseInt(filter), true));
        if(childrecord.length == 0) {
            //here hide which parent row has no child records
            args.row.querySelector('td').innerHTML=' ';
            args.row.querySelector('td').className = 'e-customizedExpandcell';
        }
    }

```

In the below demo, the expand/collapse icon in the row with **EmployeeID** as **1** is hidden as it does not have record in child Grid.

{% tab template="grid/template", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { employeeData } from './datasource';
import { GridComponent, RowDataBoundEventArgs } from '@syncfusion/ej2-angular-grids';
import { DataManager, Query, DataResult } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #Grid [dataSource]='data' [childGrid]='childGrid' (rowDataBound)="rowDataBound($event)">
                    <e-columns>
                        <e-column field='EmployeeID' headerText='EmployeeID' width='120' ></e-column>
                        <e-column field='FirstName' headerText='First Name'  width='150' ></e-column>
                        <e-column field='Title' headerText='Title' width='120' textAlign='Right'></e-column>
                        <e-column field='City' headerText='City' width='120' textAlign='Right'></e-column>
                        <e-column field='Country' headerText='Country' width='120' textAlign='Right'></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('Grid') public Grid: GridComponent;
    public childGrid: object;
    public dataManger: object[] = [{Order: 100, ShipName: 'Berlin', EmployeeID: 2},
                                 {Order: 101, ShipName: 'Capte', EmployeeID: 3},
                                 {Order: 102, ShipName: 'Marlon', EmployeeID: 4},
                                 {Order: 103, ShipName: 'Black pearl', EmployeeID: 5},
                                 {Order: 104, ShipName: 'Pearl', EmployeeID: 6},
                                 {Order: 105, ShipName: 'Noth bay', EmployeeID: 7},
                                 {Order: 106, ShipName: 'baratna', EmployeeID: 8},
                                 {Order: 107, ShipName: 'Charge', EmployeeID: 9}];

    ngOnInit(): void {
      this.data = employeeData;
      this.childGrid = {
          dataSource: new DataManager(this.dataManger),
          queryString: 'EmployeeID',
          allowPaging: true,
          columns: [
              { field: 'Order', headerText: 'Order ID', textAlign: 'Right', width: 120 },
              { field: 'EmployeeID', headerText: 'Employee ID', textAlign: 'Right', width: 120 },
              { field: 'ShipName', headerText: 'Ship Name', width: 150 }
          ]
      };
    }
    public rowDataBound(args: RowDataBoundEventArgs) {
        const EmployeeID = 'EmployeeID';
        const filter: string = args.data[EmployeeID];
        const childrecord: any = new DataManager(this.Grid.childGrid.dataSource as JSON[]).
        executeLocal(new Query().where('EmployeeID', 'equal', parseInt(filter, 10), true));
        if (childrecord.length === 0) {
            // here hide which parent row has no child records
            args.row.querySelector('td').innerHTML = ' ';
            args.row.querySelector('td').className = 'e-customizedExpandcell';
        }
    }
}

```

{% endtab %}