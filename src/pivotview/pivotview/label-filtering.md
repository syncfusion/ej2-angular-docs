---
title: "Label filtering"
component: "Pivot Table"
description: "Label filtering allows user to view pivot table with particular records based on field headers."
---

# Label filtering

Label filtering allows you to view the pivot table with particular records of a field based on headers. Label filtering can be enabled by setting the `allowLabelFilter` property to **true**. The following are the three different types of available label filtering:

* Text or label filtering.
* Date filtering.
* Number filtering.

## Label filtering through UI

Label filtering can be performed through the UI option available in the [`grouping bar`](./grouping-bar) and [`field list`](./field-list) at runtime.

## Text or label filtering through code

Text or label filtering allows you to view the pivot table with particular records of a field based on text. For example, to show only the groups for France, apply the text **france** with filter operator **Equals** on the country field.

Label filtering can be configured using the `filterSettings` option through code-behind. The settings required to filter at initial rendering are:

* `name`: Sets the field name.
* `type`: Sets the filter type as **Label** to the field.
* `condition`: Sets the operator type such as equals, greater than, less than, etc.
* `value1`: Sets the start value.
* `value2`: Sets the end value. It is applicable only for the operator such as 'Between' and 'NotBetween'.

Operators that can be used in label filtering are:

| Operator | Description |
|------|-------------|
| Equals| Displays the pivot table that matches with the text.|
| DoesNotEquals| Displays the pivot table that does not match with the given text.|
| BeginWith| Displays the pivot table that begins with text.|
| DoesNotBeginWith| Displays the pivot table that does not begins with text.|
| EndsWith| Displays the pivot table that ends with text.|
| DoesNotEndsWith| Displays the pivot table that does not ends with text.|
| Contains| Displays the pivot table that contains text.|
| DoesNotContains| Displays the pivot table that does not contain text.|
| GreaterThan| Displays the pivot table when the text is greater.|
| GreaterThanOrEqualTo| Displays the pivot table when the text is greater than or equal.|
| LessThan| Displays the pivot table when the text is lesser.|
| LessThanOrEqualTo| Displays the pivot table when the text is lesser than or equal.|
| Between| Displays the pivot table that records between the start and end text.|
| NotBetween| Displays the pivot table that does not record between the start and end text.|

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions, IDataSet } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  // specifies the template string for the pivot table component
  template: `<ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings width=width height='350'></ejs-pivotview>`
})
export class AppComponent implements OnInit {
    public width: string;
    public dataSourceSettings: IDataOptions;

    ngOnInit(): void {

        this.width = '100%';

        this.dataSourceSettings = {
        dataSource: Pivot_Data as IDataSet[],
        expandAll: false,
        allowLabelFilter: true,
        filterSettings: [{ name: 'Country', type: 'Label', condition: 'GreaterThan', value1: 'United Kingdom' }],
        columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
        values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
        rows: [{ name: 'Country' }, { name: 'Products' }],
        filters: []
        };
    }
}

```

{% endtab %}

## Date filtering through code

Date filtering allows you to view the pivot table with particular records of a field based on date. For example, to show only the groups for the year 2016, apply the value as **2016** with the filter operator **Equals** on the year field.

Date filtering can be configured using the `filterSettings` option through code-behind. The settings required to filter at initial rendering are:

* `name`: Sets the field name.
* `type`: Sets the filter type as **Date** to the field.
* `condition`: Sets the operator type such as equals, before, after, etc.
* `value1`: Sets the start date.
* `value2`: Sets the end date. It is applicable only for the operator such as 'Between' and 'NotBetween'.

Operators that can be used in date filtering are:

| Operator | Description |
|------|-------------|
| Equals| Displays the pivot table that matches with the given date.|
| DoesNotEquals| Displays the pivot table that does not match with the given date.|
| Before| Displays the records on the pivot table before to the given date.|
| BeforeOrEqualTo| Displays the records on the pivot table before or equal to the given date.|
| After| Displays the records on the pivot table after to the given date.|
| AfterOrEqualTo| Display the records on the pivot table after or equal to the given date.|
| Between| Displays the pivot table that records between the start and end dates.|
| NotBetween| Displays the pivot table that does not record between the start and end dates.|

> Date filtering option is enabled only when the field has **date** type `formatsettings`.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions, IDataSet } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  // specifies the template string for the pivot table component
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings width=width></ejs-pivotview>`
})
export class AppComponent implements OnInit {
    public width: string;
    public dataSourceSettings: IDataOptions;

    ngOnInit(): void {

        this.width = '100%';

        this.dataSourceSettings = {
        dataSource: Pivot_Data as IDataSet[],
        expandAll: false,
        allowLabelFilter: true,
        formatSettings: [{ name: 'Year', format: 'dd/MM/yyyy-hh:mm', type: 'date' }],
        filterSettings: [{ name: 'Year', type: 'Date', condition: 'Before', value1: new Date('2016') }],
        columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
        values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
        rows: [{ name: 'Country' }, { name: 'Products' }],
        filters: []
        };
    }
}

```

{% endtab %}

## Number filtering through code

Number filtering allows you to view the pivot table with particular records of a field based on numbers. For example, to show only the groups less than the value 40000, apply the value as **40000** with filter operator **LessThan** on the amount field.

Number filtering can be configured using the `filterSettings` option through the code-behind. The settings required to filter at initial rendering are:

* `name`: Sets the field name.
* `type`: Sets the filter type as **Number** to the field.
* `condition`: Sets the operator type such as equals, greater than, less than, etc.
* `value1`: Sets the start value.
* `value2`: Sets the end value. It is applicable only for the operator such as 'Between' and 'NotBetween'.

Operators that can be used in date filtering are:

| Operator | Description |
|------|-------------|
| Equals| Displays the pivot table that matches with the number.|
| DoesNotEquals| Displays the pivot table that does not match with the given number.|
| GreaterThan| Displays the pivot table when the number is greater.|
| GreaterThanOrEqualTo| Displays the pivot table when the number is greater than or equal.|
| LessThan| Displays the pivot table when the number is lesser.|
| LessThanOrEqualTo| Displays the pivot table when the number is lesser than or equal.|
| Between| Displays the pivot table that records between start and end numbers.|
| NotBetween| Displays the pivot table that does not record between the start and end numbers.|

> Number filtering option is enabled only when the field contains the **number** format.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions, IDataSet } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  // specifies the template string for the pivot table component
  template: `<ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings width=width height='350'></ejs-pivotview>`
})
export class AppComponent implements OnInit {
    public width: string;
    public height: number;
    public dataSourceSettings: IDataOptions;

    ngOnInit(): void {

        this.width = '100%';

        this.dataSourceSettings = {
        dataSource: Pivot_Data as IDataSet[],
        expandAll: false,
        allowLabelFilter: true,
        filterSettings: [{ name: 'Amount', type: 'Number', condition: 'LessThan', value1: '40000' }],
        columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
        values: [{ name: 'Sold', caption: 'Units Sold' }],
        rows: [{ name: 'Amount', caption: 'Sold Amount' }],
        filters: [{ name: 'Country' }, { name: 'Products' }]
        };
    }
}

```

{% endtab %}

## See Also

* [Member Filtering](./member-filtering)
* [Value Filtering](./value-filtering)