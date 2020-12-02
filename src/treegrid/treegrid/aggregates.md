---
title: "Aggregates"
component: "TreeGrid"
description: "Learn how to aggregate rows, apply custom aggregates, and format the aggregate values in the Essential JS 2 TreeGrid control."
---

# Aggregates

Aggregate values are displayed in the TreeGrid footer and in parent row footer for child row aggregate values. It can be configured through `aggregates` property.
 [`field`](../api/treegrid/aggregateColumnModel/#field) and [`type`](../api/treegrid/aggregateColumnModel/#type)
 are the minimum properties required to represent an aggregate column.

To use the aggregate feature, you have to inject the `Aggregate` module.

By default, the aggregate value can be displayed in the treegrid footer, and footer of child rows. To show the aggregate value in one of the cells, use the [`footerTemplate`](../api/treegrid/aggregateColumnModel/#footertemplate).

You can also check this video to learn about how to use Aggregates in Angular TreeGrid.

`youtube:1dwChk61zsk`

## Built-in aggregate types

The aggregate type should be specified in the [`type`](../api/treegrid/aggregateColumnModel/#type) property to configure an aggregate column.

The built-in aggregates are,
* Sum
* Average
* Min
* Max
* Count
* Truecount
* Falsecount

> * Multiple aggregates can be used for an aggregate column by setting the [`type`](../api/treegrid/aggregateColumnModel/#type) property
with an array of aggregate types.
> * Multiple types for a column is supported only when one of the aggregate templates is used.

## Footer aggregate

Footer aggregate value is calculated for all the rows, and it is displayed in the footer cells. Use the [`footerTemplate`](../api/treegrid/aggregateColumnModel/#footertemplate) property to render the aggregate value in footer cells.

{% tab template="treegrid/aggregate", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { summaryRowData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='240' [treeColumnIndex]='0'  childMapping='children' >
        <e-columns>
                   <e-column field='FreightID' headerText='Freight ID'  width=130></e-column>
                   <e-column field='FreightName' headerText='Freight Name'  width=195></e-column>
                   <e-column field='UnitWeight' headerText='Weight Per Unit' textAlign='Right' type='number' width=130></e-column>
                   <e-column field='TotalUnits' headerText='Total Units' textAlign='Right' type='number' width=125></e-column>
        </e-columns>
        <e-aggregates>
        <e-aggregate [showChildSummary]='false'>
            <e-columns>
                <e-column field="UnitWeight" type="Max" columnName='UnitWeight'>
                    <ng-template #footerTemplate let-data>Maximum: {{data.Max}}</ng-template>
                </e-column>
                 <e-column field="TotalUnits" type="Min" columnName='TotalUnits'>
                    <ng-template #footerTemplate let-data>Minimum: {{data.Min}}</ng-template>
                </e-column>
            </e-columns>
        </e-aggregate>
        </e-aggregates>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = summaryRowData;
    }
}
```

{% endtab %}

> The aggregate values must be accessed inside the template using their corresponding [`type`](../api/treegrid/aggregateColumnModel/#type) name.

## Child aggregate

Aggregate value is calculated for child rows, and it is displayed in the parent row footer. Use the [`childSummary`](../api/treegrid/aggregateRowModel/#showchildsummary) property to render the child rows aggregate value.

{% tab template="treegrid/aggregate", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { summaryRowData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='240' [treeColumnIndex]='0'  childMapping='children' >
        <e-columns>
                   <e-column field='FreightID' headerText='Freight ID'  width=130></e-column>
                   <e-column field='FreightName' headerText='Freight Name'  width=195></e-column>
                   <e-column field='UnitWeight' headerText='Weight Per Unit' textAlign='Right' type='number' width=130></e-column>
                   <e-column field='TotalUnits' headerText='Total Units' textAlign='Right' type='number' width=125></e-column>
        </e-columns>
        <e-aggregates>
        <e-aggregate [showChildSummary]='true'>
            <e-columns>
                <e-column field="UnitWeight" type="Max">
                    <ng-template #footerTemplate let-data>Maximum: {{data.Max}}</ng-template>
                </e-column>
                <e-column field="TotalUnits" type="Min">
                    <ng-template #footerTemplate let-data>Minimum: {{data.Min}}</ng-template>
                </e-column>
            </e-columns>
        </e-aggregate>
    </e-aggregates>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = summaryRowData;
    }
}
```

{% endtab %}

## How to format aggregate value

You can format the aggregate value result by using the [`format`](../api/treegrid/aggregateColumnModel/#type) property.

{% tab template="treegrid/aggregate", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { summaryData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='260' width='auto' [treeColumnIndex]='0'  childMapping='subtasks' >
        <e-columns>
                   <e-column field='category' headerText='Category'  width=130></e-column>
                   <e-column field='units' headerText='Total Units'  textAlign='Right' type='number' Width=130></e-column>
                   <e-column field='unitPrice' headerText='Unit Price($)' format='C2' textAlign='Right' type='number' width=110 ></e-column>
                   <e-column field='price' headerText='Price($)' textAlign='Right' type='number' width=160 ></e-column>
        </e-columns>
        <e-aggregates >
        <e-aggregate >
            <e-columns>
                <e-column field="price" format='C2' type="Sum" customAggregate='customAggregateFn'>
                    <ng-template #footerTemplate let-data>Total: {{data.Sum}}</ng-template>
                </e-column>
            </e-columns>
        </e-aggregate>
    </e-aggregates>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = summaryData;
    }
}

```

{% endtab %}

## Custom aggregate

To calculate the aggregate value with your own aggregate functions, use the custom aggregate option. To use custom aggregation, specify the [`type`](../api/treegrid/aggregateColumnModel/#type) as `Custom`, and provide the custom aggregate function in the [`customAggregate`](../api/treegrid/aggregateColumnModel/#customaggregate) property.

{% tab template="treegrid/aggregate", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { summaryData } from './datasource';
import { getObject, CustomSummaryType } from '@syncfusion/ej2-grids';
@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='245' [treeColumnIndex]='0'  childMapping='subtasks' >
        <e-columns>
                   <e-column field='category' headerText='Category'  width=240></e-column>
                   <e-column field='units' headerText='Total Units'  textAlign='Right' type='number' Width=130></e-column>
                   <e-column field='unitPrice' headerText='Unit Price($)' format='C2' textAlign='Right' type='number' width=110 ></e-column>
                   <e-column field='price' headerText='Price($)' textAlign='Right' type='number' width=160 ></e-column>
        </e-columns>
        <e-aggregates >
        <e-aggregate [showChildSummary]='false' >
            <e-columns>
                <e-column field="price" format='C2' type="Custom" [customAggregate]='customAggregateFn' columnName='category' >
                    <ng-template #footerTemplate let-data>Count of Frozen seafood : {{data.Custom}}</ng-template>
                </e-column>
            </e-columns>
        </e-aggregate>
    </e-aggregates>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    ngOnInit(): void {
        this.data = summaryData;
    }
    customAggregateFn (data: Object): number {
        let sampleData: Object[] = getObject('result', data);
        let countLength: number; countLength = 0;
        sampleData.filter((item: Object) => {
            let data: string = getObject('category', item);
            if (data === 'Frozen seafood') {
                countLength++;
            }
        });
        return countLength;
    };
}

```

{% endtab %}

> To access the custom aggregate value inside the template, use the key as `Custom`.