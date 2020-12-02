---
title: "Selection"
component: "TreeGrid"
description: "Learn how to select rows and cells, use range selection, and use check box selection in the Essential JS 2 TreeGrid control."
---

# Selection

Selection provides an option to highlight a row or cell.
Selection can be done through simple Mouse down or Arrow keys.
To disable selection in the TreeGrid, set the [`allowSelection`](../api/treegrid/#allowselection) to false.

The treegrid supports two types of selection that can be set by using the
[`selectionSettings.type`](../api/treegrid/selectionSettings/#type).They are:

* **`Single`** - The `Single` value is set by default. Allows you to select only a single row or cell.
* **`Multiple`** - Allows you to select multiple rows or cells.
To perform the multi-selection, press and hold CTRL key and click the desired rows or cells.
To select range of rows or cells, press and hold the SHIFT key and click the rows or cells.

{% tab template="treegrid/selection", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { SelectionSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'  [treeColumnIndex]='1' [allowPaging]='true' [selectionSettings]='selectionOptions' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public selectionOptions: SelectionSettingsModel;

    ngOnInit(): void {
        this.data = sampleData;
        this.selectionOptions = { type: 'Multiple' };
    }
}

```

{% endtab %}

## Selection Mode

TreeGrid supports three types of selection mode which can be set by using
[`selectionSettings.mode`](../api/treegrid/selectionSettings/#mode). They are:

* **`Row`** - The `row` value is set by default. Allows you to select rows only.
* **`Cell`** - Allows you to select cells only.
* **`Both`** - Allows you to select rows and cells at the same time.

{% tab template="treegrid/selection", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { SelectionSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='265' [treeColumnIndex]='1' [allowPaging]='true' [selectionSettings]='selectionOptions' childMapping='subtasks' >
        <e-columns>
                <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public selectionOptions: SelectionSettingsModel;

    ngOnInit(): void {
        this.data = sampleData;
        this.selectionOptions = { mode: 'Both' };
    }
}

```

{% endtab %}

## Cell Selection

Cell Selection can be done through simple Mouse down or Arrow keys(up, down, left and right).

TreeGrid supports two types of cell selection mode which can be set by using
[`selectionSettings.cellSelectionMode`](../api/treegrid/selectionSettings/#cellselectionmode). They are:

* **`Flow`** - The `Flow` value is set by default.
Select range of cells between the start index and end index which includes in between cells of rows.
* **`Box`** - Select range of cells within the start and end column indexes which includes
in between cells of rows within the range.

{% tab template="treegrid/selection", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { SelectionSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' height=250 [treeColumnIndex]='1' [allowPaging]='true' childMapping='subtasks' [selectionSettings]='selectionOptions'>
        <e-columns>
                <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public selectionOptions: SelectionSettingsModel;

    ngOnInit(): void {
        this.data = sampleData;
        this.selectionOptions = { cellSelectionMode: 'Box', type: 'Multiple', mode: 'Cell' };
    }
}

```

{% endtab %}

> Cell Selection requires the [`selectionSettings.mode`](../api/grid/selectionSettings/#mode) to be `Cell` or  `Both`.

## Checkbox Selection

Checkbox Selection provides an option to select multiple TreeGrid records with help of checkbox in each row.

To render checkbox in each treegrid row, you need to use checkbox column with type as `CheckBox` using
column [`type`](../api/treegrid/column/#type) property.

{% tab template="treegrid/selection", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' [treeColumnIndex]='2' childMapping='subtasks'
    height='315px' >
        <e-columns>
                <e-column type='checkbox' width='50'></e-column>
                <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;
    }
}

```

{% endtab %}

> By default selection is allowed by clicking a treegrid row or checkbox in that row. To allow Selection only through checkbox, you can set
[`selectionSettings.checkboxOnly`](../api/treegrid/selectionSettings/#checkboxonly) property to true.
> Selection can be persisted on all the operations
using [`selectionSettings.persistSelection`](../api/treegrid/selectionSettings/#persistselection) property.
For persisting selection on the TreeGrid, any one of the column should be defined as a primary key
using [`columns.isPrimaryKey`](../api/treegrid/column/#isprimarykey) property.

## Checkbox selection Mode

In checkbox selection, selection can also be done by clicking on rows. This selection provides two types of Checkbox Selection mode which can be set by using the following API,
[`selectionSettings.checkboxMode`](../api/treegrid/selectionSettings/#checkboxmode). The modes are;

* **`Default`**: This is the default value of the checkboxMode. In this mode, user can select multiple rows by clicking rows one by one.
* **`ResetOnRowClick`**: In ResetOnRowClick mode, when user clicks on a row it will reset previously selected row. Also you can perform multiple-selection in this mode by press
and hold CTRL key and click the desired rows. To select range of rows, press and hold the SHIFT key and click the rows.

{% tab template="treegrid/selection", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { SelectionSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' [treeColumnIndex]='2' childMapping='subtasks'
    height='315px' [selectionSettings]='selectionOptions' >
        <e-columns>
                <e-column type='checkbox' width='50'></e-column>
                <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public selectionOptions: SelectionSettingsModel;

    ngOnInit(): void {
        this.data = sampleData;
        this.selectionOptions = { checkboxMode: 'ResetOnRowClick'};
    }
}

```

{% endtab %}

## Toggle Selection

The Toggle selection allows to perform selection and unselection of the particular row or cell. To [`enable toggle`](../api/treegrid/selectionSettings/#enabletoggle) selection, set enableToggle property of the selectionSettings as true. If you click on the selected row or cell then it will be unselected and vice versa.

{% tab template="treegrid/selection", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { SelectionSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' [treeColumnIndex]='1' childMapping='subtasks'
    height='315px' [selectionSettings]='selectionOptions' >
        <e-columns>
                <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public selectionOptions: SelectionSettingsModel;

    ngOnInit(): void {
        this.data = sampleData;
        this.selectionOptions = { enableToggle: true};
    }
}

```

{% endtab %}

>If multi selection is enabled, then first click on any selected row (without pressing Ctrl key), it will clear the multi selection and in second click on the same row, it will be unselected.