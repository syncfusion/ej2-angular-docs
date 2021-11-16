---
title: "Selection"
component: "Grid"
description: "Learn how to select rows and cells, use range selection, and use check box selection in the Essential JS 2 DataGrid control."
---

# Selection

Selection provides an option to highlight a row or cell or column.
Selection can be done through simple Mouse down or Arrow keys.
To disable selection in the Grid, set the [`allowSelection`](../api/grid/#allowselection) to false.

The grid supports two types of selection that can be set by using the
[`selectionSettings.type`](../api/grid/selectionSettings/#type).They are:

* **Single** - The **Single** value is set by default. Allows you to select only a single row or cell or column.
* **Multiple** - Allows you to select multiple rows or cells or columns.
To perform the multi-selection, press and hold CTRL key and click the desired rows or cells  or columns.
To select range of rows or cells or columns, press and hold the SHIFT key and click the rows or cells or columns.

{% tab template="grid/selection", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { SelectionSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [selectionSettings]='selectionOptions' height='315px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public selectionOptions: SelectionSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.selectionOptions = { type: 'Multiple' };
    }
}

```

{% endtab %}

## Selection Mode

Grid supports three types of selection mode which can be set by using
[`selectionSettings.mode`](../api/grid/selectionSettings/#mode). They are:

* **Row** - The **row** value is set by default. Allows you to select rows only.
* **Cell** - Allows you to select cells only.
* **Both** - Allows you to select rows and cells at the same time.

{% tab template="grid/selection", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { SelectionSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [selectionSettings]='selectionOptions' height='315px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public selectionOptions: SelectionSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.selectionOptions = { mode: 'Both' };
    }
}

```

{% endtab %}

## Cell Selection

Cell Selection can be done through simple Mouse down or Arrow keys(up, down, left and right).

Grid supports two types of cell selection mode which can be set by using
[`selectionSettings.cellSelectionMode`](../api/grid/selectionSettings/#cellselectionmode). They are:

* **Flow** - The **Flow** value is set by default.
Select range of cells between the start index and end index which includes in between cells of rows.
* **Box** - Select range of cells within the start and end column indexes which includes
in between cells of rows within the range.

{% tab template="grid/selection", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { SelectionSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [selectionSettings]='selectionOptions' height='315px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public selectionOptions: SelectionSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.selectionOptions = { cellSelectionMode: 'Box', type: 'Multiple', mode: 'Cell' };
    }
}

```

{% endtab %}

> Cell Selection requires the [`selectionSettings.mode`](../api/grid/selectionSettings/#mode) to be **Cell** or  **Both** and
[`type`](../api/grid/selectionSettings/#type) should be **Multiple**.

## Column selection

Column selection can be done through simple mouse down or arrow keys.

You can enable column selection by setting the [`selectionSettings.allowColumnSelection`](../api/grid/selectionSettings/#allowcolumnselection) property as true.

{% tab template="grid/selection", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { SelectionSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [selectionSettings]='selectionOptions' height='315px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public selectionOptions: SelectionSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.selectionOptions = { allowColumnSelection: true, type: 'Multiple' };
    }
}

```

{% endtab %}

## Checkbox Selection

Checkbox Selection provides an option to select multiple Grid records with help of checkbox in each row.

To render checkbox in each grid row, you need to use checkbox column with type as **CheckBox** using
column [`type`](../api/grid/column/#type) property.

{% tab template="grid/selection", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { SelectionSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height='315px'>
                <e-columns>
                    <e-column type='checkbox' width='50'></e-column>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public selectionOptions: SelectionSettingsModel;

    ngOnInit(): void {
        this.data = data;
    }
}

```

{% endtab %}

> By default selection is allowed by clicking a grid row or checkbox in that row. To allow Selection only through checkbox, you can set
[`selectionSettings.checkboxOnly`](../api/grid/selectionSettings/#checkboxonly) property to true.
> Selection can be persisted on all the operations
using [`selectionSettings.persistSelection`](../api/grid/selectionSettings/#persistselection) property.
For persisting selection on the Grid, any one of the column should be defined as a primary key
using [`columns.isPrimaryKey`](../api/grid/column/#isprimarykey) property.

## Toggle selection

The Toggle selection allows to perform selection and unselection of the particular row or cell or column. To enable toggle selection, set [`enableToggle`](../api/grid/selectionSettings/#enabletoggle) property of the selectionSettings as true. If you click on the selected row or cell or column then it will be unselected and vice versa.

{% tab template="grid/selection", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { SelectionSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height='315px' [selectionSettings]='selectionOptions'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public selectionOptions: SelectionSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.selectionOptions = { type: 'Multiple', mode: 'Both' };
    }
}

```

{% endtab %}

> If multi selection is enabled, then first click on any selected row (without pressing Ctrl key), it will clear the multi selection and in second click on the same row, it will be unselected.

## Select row at Initial rendering

To select a row at initial rendering, set the [`selectedRowIndex`](../api/grid/#selectedrowindex) value.

{% tab template="grid/selection", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { SelectionSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [selectedRowIndex]=1 [selectionSettings]='selectionOptions' height='315px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public selectionOptions: SelectionSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.selectionOptions = { type: 'Multiple', mode: 'Both' };
    }
}

```

{% endtab %}

## Get Selected Row Indexes

You can get the selected row indexes by using the [`getSelectedRowIndexes`](../api/grid/#getselectedrowindexes) method.

{% tab template="grid/selection", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, RowSelectEventArgs } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' height='315px' (rowSelected)='rowSelected($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    @ViewChild('grid')
    public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
    }

    rowSelected(args: RowSelectEventArgs) {
        const selectedrowindex: number[] = this.grid.getSelectedRowIndexes();  // Get the selected row indexes.
        alert(selectedrowindex); // To alert the selected row indexes.
        const selectedrecords: object[] = this.grid.getSelectedRecords();  // Get the selected records.
    }
}

```

{% endtab %}

## Touch Interaction

When you tap Grid row on touch screen devices, then the tapped row is selected.
Also, it will show a popup ![Multi row selection](images/selection.jpg)  for multi-row-selection.
To select multiple rows or cells, tap the popup![Multi row or cell selection](images/mselection.jpg)  and then tap the desired rows or cells.

> For multi-selection, It requires the selection [`type`](../api/grid/selectionSettings/#type) to be **Multiple**.

The following screenshot represents a Grid touch selection in the device.

![Touch Interaction](images/touch-selection.jpg)

## Checkbox selection Mode

In checkbox selection, selection can also be done by clicking on rows. This selection provides two types of Checkbox Selection mode which can be set by using the following API,
[`selectionSettings.checkboxMode`](../api/grid/selectionSettings/#checkboxmode). The modes are;

* **Default**: This is the default value of the checkboxMode. In this mode, user can select multiple rows by clicking rows one by one.
* **ResetOnRowClick**: In ResetOnRowClick mode, when clicking on row it will reset previously selected row. Also you can perform multiple-selection in this mode by press
and hold CTRL key and click the desired rows. To select range of rows, press and hold the SHIFT key and click the rows.

{% tab template="grid/selection", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { SelectionSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [selectionSettings]='selectionOptions' height='315px'>
                <e-columns>
                    <e-column type='checkbox' width='50'></e-column>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public selectionOptions: SelectionSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.selectionOptions = { checkboxMode: 'ResetOnRowClick'};
    }
}

```

{% endtab %}

## Simple Multiple Row selection

You can select multiple rows by clicking on rows one by one. This will not deselect the previously selected rows. To deselect the previously selected row, you can click on the  selected row. You can enable this behavior by using [`selectionSettings.enableSimpleMultiRowSelection`](../api/grid/selectionSettings/#enablesimplemultirowselection) property.

{% tab template="grid/selection", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { SelectionSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [selectionSettings]='selectionOptions' height='315px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public selectionOptions: SelectionSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.selectionOptions = { type: 'Multiple', enableSimpleMultiRowSelection: true };
    }
}

```

{% endtab %}

## See Also

* [Animate the Grid selected row in Angular Grid](https://www.syncfusion.com/forums/156448/animate-the-grid-selected-row-in-angular-grid)
* [How can I disable the row selection on context menu click in Angular Grid](https://www.syncfusion.com/forums/143449/how-can-i-disable-the-row-selection-on-context-menu-click-in-angular-grid)
* [How to retrieve the selected records in the Grid in Angular Grid](https://www.syncfusion.com/forums/150200/how-to-retrieve-the-selected-records-in-the-grid-in-angular-grid)
* [How to prevent tab to focus on a cell when inside a grid in Angular Grid](https://www.syncfusion.com/forums/156333/how-to-prevent-tab-to-focus-on-a-cell-when-inside-a-grid-in-angular-grid)
* [How to select the first row of the Grid, after the grid refreshed in Angular Grid](https://www.syncfusion.com/forums/152715/how-to-select-the-first-row-of-the-grid-after-the-grid-refreshed-in-angular-grid)
* [How to select the multiple row at initial render in Angular Grid](https://www.syncfusion.com/forums/156142/how-to-select-the-multiple-row-at-initial-render-in-angular-grid)
* [How to cancel the selection of first record while adding a new record in Angular Grid](https://www.syncfusion.com/forums/163325/how-to-cancel-the-selection-of-first-record-while-adding-a-new-record-in-angular-grid)