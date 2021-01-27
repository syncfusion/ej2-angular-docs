---
title: "Aggregation"
component: "Pivot Table"
description: "Aggregation allows user to summarize the measure values."
---

# Aggregation

> This feature is applicable only for the relational data source.

End user can perform calculations over a group of values (exclusively for value fields bound in value axis) using the aggregation option. By default, values are added (summed) together. The other aggregation types are explained below.

> The fields with data type such as number support all aggregation types mentioned below except for **"CalculatedField"**. The fields with data type such as string, date, datetime, boolean, etc., support **"Count"** and **"DistinctCount"** aggregation types alone.

| Operator | Description |
|------|-------------|
| Sum| Displays the pivot table values with sum.|
| Product| Displays the pivot table values with product.|
| Count| Displays the pivot table values with count.|
| DistinctCount| Displays the pivot table values with distinct count.|
| Min| Displays the pivot table with minimum value.|
| Max| Displays the pivot table with maximum value.|
| Avg| Displays the pivot table values with average.|
| Median| Displays the pivot table values with median.|
| Index| Displays the pivot table values with index.|
| PopulationStDev| Displays the pivot table values with standard deviation of population.|
| SampleStDev| Displays the pivot table values with sample standard deviation.|
| PopulationVar| Displays the pivot table values with variance of population.|
| SampleVar| Displays the pivot table values with sample variance.|
| RunningTotals| Displays the pivot table values with running totals.|
| DifferenceFrom| Displays the pivot table values with difference from the value of the base item in the base field.|
| PercentageOfDifferenceFrom| Displays the pivot table values with percentage difference from the value of the base item in the base field.|
| PercentageOfGrandTotal| Displays the pivot table values with percentage of grand total of all values.|
| PercentageOfColumnTotal| Displays the pivot table values in each column with percentage of total values for the column.|
| PercentageOfRowTotal| Displays the pivot table values in each row with percentage of total values for the row.|
| PercentageOfParentTotal| Displays the pivot table values with percentage of total of all values based on selected field.|
| PercentageOfParentColumnTotal| Displays the pivot table values with percentage of its parent total in each column.|
| PercentageOfParentRowTotal| Displays the pivot table values with percentage of its parent total in each row.|
| CalculatedField| Displays the pivot table with calculated field values. It allows user to create a new calculated field alone.|

## Assigning aggregation type for value fields through API

For each value field, the aggregation type can be set using the property [`type`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#type) in [`values`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#values). Meanwhile, aggregation types like **DifferenceFrom** and **PercentageOfDifferenceFrom** can check for specific field of specific item using [`baseField`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#basefield) and [`baseItem`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#baseitem) properties. Likewise, **PercentageOfParentTotal** type can for specific field using [`baseField`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#basefield) property. For instance, the aggregation type **DifferenceFrom** would intake the specified field and its corresponding member as input and its value is compared across other members in the same field and also across different fields to formulate an appropriate output value.  

* [`type`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#type): It allows to set the aggregate type of the field.
* [`baseField`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#basefield): It allows to set the specific field to aggregate the values.
* [`baseItem`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#baseitem): It allows to set the specific member to aggregate the values.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  // specifies the template string for the pivot table component
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings width=width></ejs-pivotview>`
})
export class AppComponent implements OnInit {
    public dataSourceSettings: IDataOptions;
    public width: string;

    ngOnInit(): void {
        this.width = '100%';

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' type:'DifferenceFrom' baseField:'Country' baseItem:'France'}, { name: 'Amount', caption: 'Sold Amount', type: 'Sum' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: []
        };
    }
}

```

{% endtab %}

> By default, the aggregation will be considered as **Sum** to the value fields which had number type and for the value fields which had non-number type values such as string, date, datetime, boolean, etc., the aggregation type will be considered as **Count**.

## Modifying aggregation type for value fields at runtime

Aggregation types can be changed easily through UI at runtime. The value fields bound to grouping bar and field list appears with a dropdown icon which helps to select an appropriate aggregation type for the respective value field. On selection, the values in the pivot table will be changed dynamically.

<!-- markdownlint-disable MD012 -->
![output](images/aggregation_fl_menu.png "List of pre-defined aggregation types to be changed via Field List")
<br/>
<br/>
![output](images/aggregation_gb_menu.png "List of pre-defined aggregation types to be changed via Grouping Bar")

## Show desired aggregation types in its dropdown menu

By default, all the aggregation types are displayed in the dropdown menu available in buttons. However, based on the request for an application, we may need to show selective aggregation types on our own. This can be achieved using the [`aggregateTypes`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#aggregatetypes) property.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions, GroupingBarService, AggregateTypes } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [GroupingBarService],
  // specifies the template string for the pivot table component
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings width=width showGroupingBar='true' [aggregateTypes]='aggregateTypesOption'></ejs-pivotview>`
})
export class AppComponent implements OnInit {
    public dataSourceSettings: IDataOptions;
    public width: string;
    public aggregateTypesOption: AggregateTypes[];
    ngOnInit(): void {
        this.width = '100%';
        this.aggregateTypesOption = ['DistinctCount', 'Avg', 'Product'],
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            drilledMembers: [{ name: 'Country', items: ['France'] }],
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount', type: 'Sum' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            filters: [],
        };
    }
}

```

{% endtab %}

## Hiding aggregation type from button text

By default, in value axis each field would be displayed by its name and aggregation type together. To hide aggregation type and display field name alone, set the property [`showAggregationOnValueField`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#showaggregationonvaluefield)  in [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/) to **false**.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { IDataOptions, IDataSet, PivotView, GroupingBarService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [GroupingBarService],
  // specifies the template string for the pivot table component
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings [width]=width showGroupingBar='true'></ejs-pivotview>`
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    public width: string;
    ngOnInit(): void {
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: [],
            showAggregationOnValueField: false
        };
        this.width = "100%";
    }
 }
```

{% endtab %}

## Hiding aggregation type icon from UI

By default, the icon to set aggregation type is enabled in the grouping bar. To disable this icon, set the property [`showValueTypeIcon`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/groupingBarSettings/#showvaluetypeicon) in [`groupingBarSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/groupingBarSettings/) to **false**.

> Icon to change the aggregation type can be hidden only in Grouping Bar but not in Field List at the moment.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { IDataOptions, IDataSet, PivotView, GroupingBarService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [GroupingBarService],
  // specifies the template string for the pivot table component
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings [width]=width showGroupingBar='true' [groupingBarSettings]='groupingSettings'></ejs-pivotview>`
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    public groupingSettings: GroupingBarSettings;
    public width: string;
    ngOnInit(): void {
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: [],
            showAggregationOnValueField: false
        };
        this.width = "100%";
        this.groupingSettings = {
            showValueTypeIcon: false
        } as GroupingBarSettings;
    }
 }
```

{% endtab %}

## Event

### AggregateCellInfo

The event [`aggregateCellInfo`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#aggregatecellinfo) triggers every time while rendering value cell. This allows user to change the cell value and skip formatting if applied. It has following parameters:

* `fieldName` - It holds current cell's field name.
* `row` - It holds current cell's row value.
* `column` - It holds current cell's row value.
* `value` - It holds value of current cell.
* `cellSets` - It holds raw data for the aggregated value cell.
* `rowCellType` - It holds row cell type value.
* `columnCellType` - It holds column cell type value.
* `aggregateType` - It holds aggregate type of the cell.
* `skipFormatting` - boolean property, it allows to skip formatting if applied.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { IDataOptions, IDataSet, PivotView, GroupingBarService, AggregateEventArgs } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [GroupingBarService],
  // specifies the template string for the pivot table component
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings [width]=width showGroupingBar='true' (aggregateCellInfo)='aggregateCell($event)'></ejs-pivotview>`
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    public width: string;
    conditionalFormatting(args: AggregateEventArgs) {
        args.skipFormatting = true;
    }

    ngOnInit(): void {
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: [],
            showAggregationOnValueField: false
        };
        this.width = "100%";
    }
 }
```

{% endtab %}