---
title: " Chart Category Axis | Angular "

component: "Chart"

description: "Category axis are used to represent, the string values instead of numbers.It contains range, label placement customizations."
---

# Category Axis

<!-- markdownlint-disable MD036 -->

Category axis are used to represent, the string values instead of numbers.

To known about category axis, you can check on this video:

`youtube:7U7X1m_fBrA`

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = [
             { country: "USA", gold: 50 },
             { country: "China", gold: 40 },
             { country: "Japan", gold: 70 },
             { country: "Australia", gold: 60 },
             { country: "France", gold: 50 },
             { country: "Germany", gold: 40 },
             { country: "Italy", gold: 40 },
             { country: "Sweden", gold: 30, silver: 25 }
        ];
        this.primaryXAxis = {
            valueType: 'Category',
            title: 'Countries'
        };
        this.primaryYAxis = {
            minimum: 0, maximum: 80,
            interval: 20, title: 'Medals'
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

>Note: To use category axis, we need to inject `CategoryService` into the `@NgModule.providers` and
set the [`valueType`](../api/chart/axis/#valuetype-any) of axis to `Category`.

<!-- markdownlint-disable MD036 -->

## Labels Placement

<!-- markdownlint-disable MD036 -->

By default, category labels are placed between the ticks in an axis, this can also be placed on ticks
using [`labelPlacement`](../api/chart/axis/#labelplacement) property.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { categoryData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = categoryData;
        this.primaryXAxis = {
            valueType: 'Category',
            title: 'Countries',
            labelPlacement: 'OnTicks'
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

## Range

Range of the category axis can be customized using [`minimum`](../api/chart/axis/#minimum),
[`maximum`](../api/chart/axis/#maximum) and [`interval`](../api/chart/axis/#interval) property of
the axis.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { categoryData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = categoryData;
        this.primaryXAxis = {
            valueType: 'Category',
            minimum: 1,
            maximum: 5,
            interval: 2,
            title: 'Countries'
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

## Indexed category axis

Category axis also can be rendered based on the index values of data source. This can be achieved by defining the
`isIndexed` property to `true` in the axis.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { categoryData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData1' type='Column' xName='x' yName='y'></e-series>
            <e-series [dataSource]='chartData2' type='Column' xName='x' yName='y'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData1: Object[];
    public chartData2: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData1 =  [{ x: 'Myanmar', y: 7.3 }, { x: 'India', y: 7.9 }, { x: 'Bangladesh', y: 6.8 }, { x: 'Cambodia', y: 7.0 }, { x: 'China', y: 6.9 }];
        this.chartData2 = [{ x: 'Poland', y: 2.7 },{ x: 'Australia', y: 2.5 },{ x: 'Singapore', y: 2.0 },{ x: 'Canada', y: 1.4 },{ x: 'Germany', y: 1.8 }];
        this.primaryXAxis = {
            valueType: 'Category',
             isIndexed: true
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}