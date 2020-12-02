---
title: "Value filtering"
component: "Pivot Table"
description: "Value filtering allows user to view pivot table with particular records based on value fields."
---

# Value filtering

Value filtering allows you to perform filtering operation to be performed based on the aggregate values. For example, to show the data where the total sum of units sold for each country exceeds 2000, apply a value filter **2000** with filter operator **GreaterThan** on the country field.

Value filtering can be enabled by setting the `allowValueFilter` property to **true**.

## Value filtering through UI

Value filtering can also be performed through the UI option available in the [`grouping bar`](./grouping-bar) and [`field list`](./field-list) at runtime.

## Value filtering through code

It can be configured using the `filterSettings` option through the code-behind. The settings required to filter at initial rendering are:

* `name`: Sets the normal field name.
* `type`: Sets the filter type as **Value** to the field.
* `measure`: Sets the value field name.
* `condition`: Sets the operator type such as equals, greater than, less than, etc.
* `value1`: Sets the start value.
* `value2`: Sets the end value. It is applicable only for the operator such as 'Between' and 'NotBetween'.

Operators that can be used in label filtering are:

| Operator | Description |
|------|-------------|
| Equals| Displays the pivot table that matches with the value.|
| DoesNotEquals| Displays the pivot table that does not match with the given value.|
| GreaterThan| Displays the pivot table when the value is greater.|
| GreaterThanOrEqualTo| Displays the pivot table when the value is greater than or equal.|
| LessThan| Displays the pivot table when the value is lesser.|
| LessThanOrEqualTo| Displays the pivot table when the value is lesser than or equal.|
| Between| Displays the pivot table that records between start and end values.|
| NotBetween| Displays the pivot table that does not record between start and end values.|

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
          allowValueFilter: true,
          drilledMembers: [{ name: 'Country', items: ['France'] }],
          filterSettings: [{ name: 'Country', measure: 'Sold', type: 'Value', condition: 'GreaterThan', value1: '2000' }],
          columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
          values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
          rows: [{ name: 'Country' }, { name: 'Products' }],
          filters: []
        };
    }
}

```

{% endtab %}

## See Also

* [Member Filtering](./member-filtering)
* [Label Filtering](./label-filtering)