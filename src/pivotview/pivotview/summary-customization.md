---
title: "Summary Customization"
component: "Pivot Table"
description: "Show/hide sub-totals and grand totals for the pivot table"
---

# Show or hide totals

## Show or hide grand totals

Allows to show or hide grand totals in rows and columns using the [`showGrandTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showgrandtotals) property. To hide the grand totals in rows and columns, set the property [`showGrandTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showgrandtotals) in [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/) to **false**.
End user can also hide grand totals for row or columns separately by setting the property [`showRowGrandTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showrowgrandtotals) or [`showColumnGrandTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showcolumngrandtotals) in [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/) to **false** respectively.

> By default, [`showGrandTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showgrandtotals), [`showRowGrandTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showgrandtotals) and [`showColumnGrandTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showgrandtotals) properties in [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/) are set as **true**.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions, FieldListService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [FieldListService],
  // specifies the template string for the pivot table component
  template: `<div style="height: 480px;"><ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings showFieldList='true'
  width=width></ejs-pivotview></div>`
})
export class AppComponent implements OnInit {
    public width: string;
    public dataSourceSettings: IDataOptions;

    ngOnInit(): void {

        this.width = "100%";

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            drilledMembers: [{ name: 'Country', items: ['France'] }],
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: [],
            showGrandTotals: false
        };
    }
}

```

{% endtab %}

## Show or hide sub-totals

Allows to show or hide sub-totals in rows and columns using the [`showSubTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showsubtotals) property. To hide all the sub-totals in rows and columns, set the property [`showSubTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showsubtotals) in [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/) to **false**. End user can also hide sub-totals for rows or columns separately by setting the property [`showRowSubTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showrowsubtotals) or [`showColumnSubTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showcolumnsubtotals) in [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/)  to **false** respectively.

> By default, [`showSubTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showsubtotals), [`showRowSubTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showrowsubtotals) and [`showColumnSubTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showcolumnsubtotals) properties in [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showsubtotals) are set as **true**.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { IDataOptions, PivotView, FieldListService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [FieldListService],
  // specifies the template string for the pivot table component
  template: `<div style="height: 480px;"><ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings showFieldList='true' width=width></ejs-pivotview></div>`
})

export class AppComponent {

    public width: string;
    public dataSourceSettings: IDataOptions;

    ngOnInit(): void {

        this.width = "100%";

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            allowLabelFilter: true,
            allowValueFilter: true,
            enableSorting: true,
            drilledMembers: [{ name: 'Country', items: ['France'] }],
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: [],
            showSubTotals: false
        };
    }
 }

```

{% endtab %}

## Show or hide sub-totals for specific fields

Allows to show or hide sub-totals for specific fields in rows and columns using the [`ShowSubTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showsubtotals) property. To hide sub-totals for a specific field in row or column axis, set the property [`showSubTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showsubtotals) in [`rows`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#rows) or [`columns`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#columns) to **false** respectively.

> By default, [`showSubTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showsubtotals) property in [`rows`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#rows) or [`columns`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#columns) is set as **true**.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions, FieldListService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [FieldListService],
  // specifies the template string for the pivot table component
  template: `<div style="height: 480px;"><ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings showFieldList='true'
  width=width></ejs-pivotview></div>`
})
export class AppComponent implements OnInit {
    public width: string;
    public dataSourceSettings: IDataOptions;

    ngOnInit(): void {

        this.width = "100%";

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            drilledMembers: [{ name: 'Country', items: ['France'] }],
            columns: [{ name: 'Year', caption: 'Production Year', showSubTotals: false }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country', showSubTotals: false }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: []
        };
    }
}

```

{% endtab %}

## Show or hide totals using toolbar

It can also be achieved using built-in toolbar options by setting the [`showToolbar`](https://ej2.syncfusion.com/angular/documentation/api/pivotview#showtoolbar) property in pivot table to **true**. Also, include the items **GrandTotal** and **SubTotal** within the [`toolbar`](https://ej2.syncfusion.com/angular/documentation/api/pivotview#toolbar) property in pivot table. End user can now see "Show/Hide Grand totals" and "Show/Hide Sub totals" icons in toolbar UI automatically.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import {
    IDataOptions, PivotView, FieldListService, CalculatedFieldService, NumberFormattingService,
    ToolbarService, ConditionalFormattingService, ToolbarItems, DisplayOption, IDataSet
} from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [CalculatedFieldService, ToolbarService, ConditionalFormattingService, FieldListService, NumberFormattingService],
  // specifies the template string for the pivot table component
  template: `<div style="height: 480px;"><ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings width='100%' showToolbar='true' height='350' [toolbar]='toolbarOptions' ></ejs-pivotview></div>`
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    public toolbarOptions: ToolbarItems[];
    public displayOption: DisplayOption;

    @ViewChild('pivotview', {static: false})
    public pivotGridObj: PivotView;

    ngOnInit(): void {
        this.displayOption = { view: 'Both' } as DisplayOption;

        this.toolbarOptions = [ 'SubTotal', 'GrandTotal' ] as ToolbarItems[];
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
    }
 }
```

{% endtab %}