---
title: "Conditional Formatting"
component: "Pivot Table"
description: "Conditional formatting allowing the users to highlighting the value cells based on its value."
---

# Conditional Formatting

Allows end user to change the appearance of the pivot table value cells with its background color, font color, font family, and font size based on specific conditions.

The conditional formatting can be applied at runtime through the built-in dialog, invoked from the toolbar. To do so, set [`allowConditionalFormatting`](https://ej2.syncfusion.com/angular/documentation/api/pivotview#allowconditionalformatting) and [`showToolbar`](https://ej2.syncfusion.com/angular/documentation/api/pivotview#showtoolbar) properties in pivot table to **true**. Also, include the item **ConditionalFormatting** within the [`toolbar`](https://ej2.syncfusion.com/angular/documentation/api/pivotview#toolbar) property in pivot table. End user can now see the "Conditional Formatting" icon in toolbar UI automatically, which on clicking will invoke the formatting dialog to perform necessary operations.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { IDataOptions, ConditionalFormattingService, PivotView,
    FieldListService, ToolbarService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';
import { Button } from '@syncfusion/ej2-buttons';

@Component({
  selector: 'app-container',
  providers: [FieldListService, ToolbarService, ConditionalFormattingService,],
  template: `<div style="height: 480px;"><ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings allowConditionalFormatting='true' width=width showToolbar='true' [toolbar]='toolbarOptions'></ejs-pivotview></div>`
})
export class AppComponent implements OnInit {
  public dataSourceSettings: IDataOptions;
  public width: string;

    @ViewChild('pivotview', {static: false})
    public pivotGridObj: PivotView;
    public toolbarOptions: ToolbarItems[];
    ngOnInit(): void {
        this.toolbarOptions = ['ConditionalFormatting'] as ToolbarItems[];
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
            drilledMembers: [{ name: 'Country', items: ['France'] }],
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: [],
            conditionalFormatSettings: [
                {
                    measure: 'In_Stock',
                    value1: 5000,
                    conditions: 'LessThan',
                    style: {
                        backgroundColor: '#80cbc4',
                        color: 'black',
                        fontFamily: 'Tahoma',
                        fontSize: '12px'
                    }
                },
                {
                    value1: 3400,
                    value2: 40000,
                    measure: 'Sold',
                    conditions: 'Between',
                    style: {
                        backgroundColor: '#f48fb1',
                        color: 'black',
                        fontFamily: 'Tahoma',
                        fontSize: '12px'
                    }
                }
            ]
        };
        this.width = '100%';
    }
}

```

{% endtab %}

Conditional formatting can also be included in the pivot table through code-behind using the [`conditionalFormatSetting`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/conditionalFormatSettings/). The required properties to apply a new conditional formatting are,

* [`measure`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/conditionalFormatSettings/#measure): Specifies the value field name for which style will be applied.
* [`conditions`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/conditionalFormatSettings/#conditions): Specifies the operator type such as equals, greater than, less than, etc.
* [`value1`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/conditionalFormatSettings/#value1): Specifies the start value.
* [`value2`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/conditionalFormatSettings/#value2): Specifies the end value.
* [`style`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/conditionalFormatSettings/#style): Specifies the style for the cell.

The available style properties in [`style`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/style/), to set in value cells are:

* [`backgroundColor`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/style/#backgroundcolor): Specifies the background color.
* [`color`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/style/#color): Specifies the font color.
* [`fontFamily`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/style/#fontfamily): Specifies the font family.
* [`fontSize`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/style/#fontsize): Specifies the font size.

Meanwhile, user can also view conditional formatting dialog in UI by invoking `showConditionalFormattingDialog` method on an external button click which is shown in the below code sample.

To use the conditional formatting feature, User need to inject the `ConditionalFormatting` module in pivot table.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { IDataOptions, PivotView, ConditionalFormattingService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';
import { Button } from '@syncfusion/ej2-buttons';

@Component({
  selector: 'app-container',
  providers: [ConditionalFormattingService],
  // specifies the template string for the pivot table component
  template: `<div class="col-md-2"><button ej-button id='formatting'>Apply Formatting</button></div><div class="col-md-8"><ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings allowConditionalFormatting='true' [width]=width  height='350'></ejs-pivotview></div>`
})
export class AppComponent implements OnInit {
    public width: string;
    public height: number;
    public dataSourceSettings: IDataOptions;
    public button: Button;
    @ViewChild('pivotview',{static: false})
    public pivotGridObj: PivotView;

    ngOnInit(): void {

        this.width = '100%';

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
            drilledMembers: [{ name: 'Country', items: ['France', 'Germany'] }],
            columns: [{ name: 'Year' }, { name: 'Order_Source', caption: 'Order Source' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            values: [{ name: 'In_Stock', caption: 'In Stock' },
            { name: 'Sold', caption: 'Units Sold' }],
            filters: [{ name: 'Product_Categories', caption: 'Product Categories' }],
            conditionalFormatSettings: [
                {
                    measure: 'In_Stock',
                    value1: 5000,
                    conditions: 'LessThan',
                    style: {
                        backgroundColor: '#80cbc4',
                        color: 'black',
                        fontFamily: 'Tahoma',
                        fontSize: '12px'
                    }
                },
                {
                    value1: 3400,
                    value2: 40000,
                    measure: 'Sold',
                    conditions: 'Between',
                    style: {
                        backgroundColor: '#f48fb1',
                        color: 'black',
                        fontFamily: 'Tahoma',
                        fontSize: '12px'
                    }
                }
            ]
        };
        this.button = new Button({ isPrimary: true });
        this.button.appendTo('#formatting');
        this.button.element.onclick = (): void => {
            this.pivotGridObj.conditionalFormattingModule.showConditionalFormattingDialog();
        };
    }
}

```

{% endtab %}

## Conditional formatting for all fields

Allows end user to apply conditional formatting commonly for all value fields just by ignoring the [`measure`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/conditionalFormatSettings/#measure) property and setting rest of the properties in [`conditionalFormatSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/conditionalFormatSettings/).

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { IDataOptions, PivotView, ConditionalFormattingService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [ConditionalFormattingService],
  // specifies the template string for the pivot table component
  template: `<div class="col-md-8"><ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings allowConditionalFormatting='true' [width]=width  height='350'></ejs-pivotview></div>`
})
export class AppComponent implements OnInit {
    public width: string;
    public height: number;
    public dataSourceSettings: IDataOptions;
    @ViewChild('pivotview',{static: false})
    public pivotGridObj: PivotView;

    ngOnInit(): void {
        this.width = '100%';
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
            drilledMembers: [{ name: 'Country', items: ['France', 'Germany'] }],
            columns: [{ name: 'Year' }, { name: 'Order_Source', caption: 'Order Source' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            values: [{ name: 'In_Stock', caption: 'In Stock' },
            { name: 'Sold', caption: 'Units Sold' }],
            filters: [{ name: 'Product_Categories', caption: 'Product Categories' }],
            conditionalFormatSettings: [
                {
                    value1: 500,
                    conditions: 'GreaterThan',
                    style: {
                        backgroundColor: '#80cbc4',
                        color: 'black',
                        fontFamily: 'Tahoma',
                        fontSize: '12px'
                    }
                }
            ]
        };
    }
}

```

{% endtab %}

## Conditional formatting for specific value field

Allows end user to apply conditional formatting to a specific value field by setting the [`measure`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/conditionalFormatSettings/#measure) property with specific value field name in [`conditionalFormatSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/conditionalFormatSettings/#measure).

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { IDataOptions, PivotView, ConditionalFormattingService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [ConditionalFormattingService],
  // specifies the template string for the pivot table component
  template: `<div class="col-md-8"><ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings allowConditionalFormatting='true' [width]=width  height='350'></ejs-pivotview></div>`
})
export class AppComponent implements OnInit {
    public width: string;
    public height: number;
    public dataSourceSettings: IDataOptions;
    @ViewChild('pivotview', {static: false})
    public pivotGridObj: PivotView;

    ngOnInit(): void {
        this.width = '100%';
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
            drilledMembers: [{ name: 'Country', items: ['France', 'Germany'] }],
            columns: [{ name: 'Year' }, { name: 'Order_Source', caption: 'Order Source' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            values: [{ name: 'In_Stock', caption: 'In Stock' },
            { name: 'Sold', caption: 'Units Sold' }],
            filters: [{ name: 'Product_Categories', caption: 'Product Categories' }],
            conditionalFormatSettings: [
                {
                    measure: 'In_Stock',
                    value1: 500,
                    conditions: 'GreaterThan',
                    style: {
                        backgroundColor: '#80cbc4',
                        color: 'black',
                        fontFamily: 'Tahoma',
                        fontSize: '12px'
                    }
                }
            ]
        };
    }
}

```

{% endtab %}

## Editing and removing existing conditional format

Editing and removing existing conditional format can be done through the UI at runtime. To do so, open the conditional formatting dialog and edit the "Value", "Condition" and "Format" options based on user requirement and click "OK". To remove a conditional format, click the "Delete" icon besides the respective condition.  

![output](images/cformatting_remove.png)

## Event

### ConditionalFormatting

The event [`conditionalFormatting`](https://ej2.syncfusion.com/angular/documentation/api/pivotview#conditionalformatting) is triggered initially while clicking the “ADD CONDITION” button inside the conditional formatting dialog in-order to fill user specific condition instead of default condition at runtime. To use this event, [`allowConditionalFormatting`](https://ej2.syncfusion.com/angular/documentation/api/pivotview#allowconditionalformatting) property in PivotView must be set to **true**. It has following parameters -

* `applyGrandTotals` - boolean property, by setting this to true user can enable formatting to grand totals.
* `conditions` - condition to be filled in conditional formatting dialog.
* `label` - Label value for conditional formatting dialog.
* `measure` - measure value for the conditional formatting dialog.
* `style` - style property of the conditional formatting dialog.
* `value1` - value 1 for conditional formatting dialog.
* `value2` - value 2 for conditional formatting dialog, this is applicable only for selected conditions like **Between** and **NotBetween**.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { IDataOptions, PivotView, ConditionalFormattingService, IConditionalFormatSettings } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';
import { Button } from '@syncfusion/ej2-buttons';

@Component({
  selector: 'app-container',
  providers: [ConditionalFormattingService],
  // specifies the template string for the pivot table component
  template: `<div class="col-md-2"><button ej-button id='formatting'>Apply Formatting</button></div><div class="col-md-8"><ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings allowConditionalFormatting='true' [width]=width  height='350' (conditionalFormatting)='conditionalFormatting($event)'></ejs-pivotview></div>`
})
export class AppComponent implements OnInit {
    public width: string;
    public height: number;
    public dataSourceSettings: IDataOptions;
    public button: Button;
    @ViewChild('pivotview', {static: false})
    public pivotGridObj: PivotView;
    conditionalFormatting(args: IConditionalFormatSettings) {
        args.style.backgroundColor = "Blue";
        args.value1 = 23459;
    }

    ngOnInit(): void {

        this.width = '100%';

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
            drilledMembers: [{ name: 'Country', items: ['France', 'Germany'] }],
            columns: [{ name: 'Year' }, { name: 'Order_Source', caption: 'Order Source' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            values: [{ name: 'In_Stock', caption: 'In Stock' },
            { name: 'Sold', caption: 'Units Sold' }],
            filters: [{ name: 'Product_Categories', caption: 'Product Categories' }],
            conditionalFormatSettings: [
                {
                    measure: 'In_Stock',
                    value1: 5000,
                    conditions: 'LessThan',
                    style: {
                        backgroundColor: '#80cbc4',
                        color: 'black',
                        fontFamily: 'Tahoma',
                        fontSize: '12px'
                    }
                }
            ]
        };
        this.button = new Button({ isPrimary: true });
        this.button.appendTo('#formatting');
        this.button.element.onclick = (): void => {
            this.pivotGridObj.conditionalFormattingModule.showConditionalFormattingDialog();
        };
    }
}

```

{% endtab %}

## See Also

* [Apply conditional formatting for specific row or column](./how-to/apply-conditional-formatting-for-specific-row-or-column)