---
title: "Editing"
component: "Pivot Table"
description: "Editing allows to perform CRUD operation in the raw items of any cells of the pivot table."
---

# Editing

> This feature is applicable only for the relational data source.

Cell edit allows to add, delete, or update the raw items of any value cell from the pivot table. The raw items can be viewed in a data grid inside a new window on double-clicking the appropriate value cell. In the data grid, CRUD operations can be performed by double-clicking the cells or using toolbar options. Once user finishes editing raw items, aggregation will be performed for the updated values in pivot table component immediately. This support can be enabled by setting the [`allowEditing`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/cellEditSettingsModel/#allowediting) property in [`editSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/cellEditSettingsModel/) to **true**.

The CRUD operations available in the data grid toolbar and command column are:

| Toolbar Button | Actions |
|----------------|---------|
| Add | Add a new row.|
| Edit | Edit the current row or cell.|
| Delete | Delete the current row.|
| Update | Update the edited row or cell.|
| Cancel | Cancel the edited state. |

The following are the supported edit types in the data grid:

* Normal
* Dialog
* Batch
* Command Columns

## Normal

In normal edit mode, when user starts editing, the state of the currently selected row alone will be completely changed to edit state. User can change the cell values and save it to the data source by clicking "Update" toolbar button. To enable the normal edit, set the [`mode`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/cellEditSettingsModel/#mode) property in [`editSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/cellEditSettingsModel/) to **Normal**.

> The normal edit mode **Normal** is set as the default mode for editing.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { IDataOptions, PivotView, CellEditSettings } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',  
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings [editSettings]=editSettings width=width></ejs-pivotview>`
})

export class AppComponent {

    public width: string;
    public editSettings: CellEditSettings
    public dataSourceSettings: IDataOptions;

    ngOnInit(): void {

        this.width = "100%";
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
            drilledMembers: [{ name: 'Country', items: ['France'] }],
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: []
        };
        this.editSettings= { allowAdding: true, allowDeleting: true, allowEditing: true, mode: 'Normal' }
    }
 }

```

{% endtab %}

## Dialog

In dialog edit mode, when user starts editing, the currently selected row data will be shown in an exclusive dialog. User can change cell values and save it to the data source by clicking "Save" button in the dialog. To enable the dialog edit, set the [`Mode`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/cellEditSettingsModel/#mode) property in [`editSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/cellEditSettingsModel/) to **Dialog**.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { IDataOptions, PivotView, CellEditSettings } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',  
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings [editSettings]=editSettings width=width></ejs-pivotview>`
})

export class AppComponent {

    public width: string;
    public editSettings: CellEditSettings
    public dataSourceSettings: IDataOptions;

    ngOnInit(): void {

        this.width = "100%";
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
            drilledMembers: [{ name: 'Country', items: ['France'] }],
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: []
        };
        this.editSettings= { allowAdding: true, allowDeleting: true, allowEditing: true, mode: 'Dialog' }
    }
 }

```

{% endtab %}

## Batch

In batch edit mode, when user double-clicks any data grid cell, the state of target cell is changed to edit state. User can perform bulk changes and finally save (added, changed, and deleted data in the single request) to the data source by clicking "Update" toolbar button. To enable the batch edit, set the [`mode`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/cellEditSettingsModel/#mode) property in [`editSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/cellEditSettingsModel/) to **Batch**. You can perform bulk save (added, changed, and deleted data in the single request) to the data source by clicking the toolbar's **Update** button.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { IDataOptions, PivotView, CellEditSettings } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',  
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings [editSettings]=editSettings width=width></ejs-pivotview>`
})

export class AppComponent {

    public width: string;
    public editSettings: CellEditSettings
    public dataSourceSettings: IDataOptions;

    ngOnInit(): void {

        this.width = "100%";
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
            drilledMembers: [{ name: 'Country', items: ['France'] }],
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: []
        };
        this.editSettings= { allowAdding: true, allowDeleting: true, allowEditing: true, mode: 'Batch' }
    }
 }

```

{% endtab %}

## Command column

An additional column appended in the data grid layout holds the command buttons to perform the CRUD operation. To enable the command columns, set the [`allowCommandColumns`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/cellEditSettingsModel/#allowcommandcolumns) property in [`editSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/cellEditSettingsModel/) to **true**.

The available built-in command buttons are:

| Command Button | Actions |
|----------------|---------|
| Edit | Edit the current row.|
| Delete | Delete the current row.|
| Save | Update the edited row.|
| Cancel | Cancel the edited state. |

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { IDataOptions, PivotView, CellEditSettings } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',  
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings [editSettings]=editSettings width=width></ejs-pivotview>`
})

export class AppComponent {

    public width: string;
    public editSettings: CellEditSettings
    public dataSourceSettings: IDataOptions;

    ngOnInit(): void {

        this.width = "100%";
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
            drilledMembers: [{ name: 'Country', items: ['France'] }],
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: []
        };
        this.editSettings= { allowAdding: true, allowDeleting: true, allowEditing: true, allowCommandColumns: true }
    }
 }

```

{% endtab %}

## Inline Editing

Allows editing of a value cell directly without the use of an external edit dialog. It is applicable if and only if a single raw data is used for the value of the cell. It is applicable to all editing modes, such as normal, batch, dialog and column commands. It can be enabled by setting the [`allowInlineEditing`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/cellEditSettings/#allowinlineediting) property in [`editSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/cellEditSettingsModel/) to **true**.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { IDataOptions, PivotView, CellEditSettings } from '@syncfusion/ej2-angular-pivotview';
import { pivot_flatdata } from './datasource.ts';

@Component({
  selector: 'app-container',  
  template: `<div class="control-section" style="overflow:auto;">
  <ejs-pivotview #pivotview id='PivotView' [gridSettings]='gridSettings'
  [dataSourceSettings]=dataSourceSettings width='100%' height='290'
  [editSettings]='editSettings'> </ejs-pivotview> </div>`
})

export class AppComponent {

    public width: string;
    public editSettings: CellEditSettings
    public dataSourceSettings: IDataOptions;

    ngOnInit(): void {

        this.width = "100%";
        this.dataSourceSettings = {
            dataSource: pivot_flatdata,
            expandAll: true,
            rows: [{ name: 'Country'}],
            columns: [{ name: 'Date' }, { name: 'Product' }],
            values: [{ name: 'Quantity' caption: 'Units Sold' },{ name: 'Amount' caption: 'Sold Amount' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            showColumnSubTotals:false
            };
        this.editSettings= { allowEditing: true, allowInlineEditing:true }
    }
 }

```

{% endtab %}

## Editing using the pivot chart

Users can also add, delete, or update the underlying raw items of any data point via pivot chart. The raw items will be shown in the data grid in the new window by clicking the appropriate data point. Then you can edit the raw items as mentioned above by any of the edit types (normal, dialog, batch and command column).

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions, DisplayOption, PivotChartService, CellEditSettings } from '@syncfusion/ej2-angular-pivotview';
import { ChartSettings } from '@syncfusion/ej2-pivotview/src/pivotview/model/chartsettings';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [PivotChartService],
  // specifies the template string for the pivot table component
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings
  [chartSettings]='chartSettings' [displayOption]='displayOption' [editSettings]=editSettings></ejs-pivotview>`
})
export class AppComponent implements OnInit {
    public dataSourceSettings: IDataOptions;
    public chartSettings: ChartSettings;
    public displayOption: DisplayOption;
    public editSettings: CellEditSettings

    ngOnInit(): void {

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: []
        };

        this.displayOption = { view: 'Chart' } as DisplayOPtion;
        this.chartSettings = { chartSeries: { type: 'Column' }} as ChartSettings;
        this.editSettings= { allowAdding: true, allowDeleting: true, allowEditing: true, mode: 'Normal' }
    }
}

```

{% endtab %}

## Events

### EditCompleted

The event [`editCompleted`](https://ej2.syncfusion.com/angular/documentation/api/pivotview#editcompleted) triggers when values cells are edited completely. The event provides edited cell(s) information along with its previous cell value. It also helps to do the CRUD operation by manually updating the database which is connected to the component. It has the following parameters.
* `currentData` - It holds the current raw data of the edited cells.
* `previousData` - It holds the previous raw data of the edited cells.
* `previousPosition` - It holds the index of the raw data whose values are edited.
* `cancel` - It is a boolean property and if it is set as **true**, the editing won’t be reflected in the pivot table.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { IDataOptions, PivotView, DrillThroughService, EditCompletedEventArgs, CellEditSettings } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [DrillThroughService],
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings [editSettings]='editSettings'
              allowDrillThrough='true' width=width (editCompleted)='editCompleted($event)'></ejs-pivotview>`
})

export class AppComponent {

    public width: string;
     public editSettings: CellEditSettings;
    public dataSourceSettings: IDataOptions;

    editCompleted(args:EditCompletedEventArgs) {
        //triggers when a value cell is edited
    },

    ngOnInit(): void {

        this.width = "100%";

        this.editSettings= { allowAdding: true, allowDeleting: true, allowEditing: true, mode: 'Normal' }

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            drilledMembers: [{ name: 'Country', items: ['France'] }],
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }]
        };
    }
 }

```

{% endtab %}

### DrillThrough

For more information [`refer`](./drill-through/#drillthrough) here.

### BeginDrillThrough

For more information [`refer`](./drill-through/#begindrillthrough) here.