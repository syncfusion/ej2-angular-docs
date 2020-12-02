---
title: " Chart Series | Angular "

component: "Chart"

description: "Chart supports to render collection of series like multiple series or combination series."
---

# Chart Series

## Multiple Series

You can add multiple series to the chart by using [`series`](../api/chart/seriesDirective/) property.
The series are rendered in the order as it is added to the series array.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='gold'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze'></e-series>
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
              { country: "USA", gold: 50, silver: 70, bronze: 45 },
              { country: "China", gold: 40, silver: 60, bronze: 55 },
              { country: "Japan", gold: 70, silver: 60, bronze: 50 },
              { country: "Australia", gold: 60, silver: 56, bronze: 40 },
              { country: "France", gold: 50, silver: 45, bronze: 35 },
              { country: "Germany", gold: 40, silver: 30, bronze: 22 },
              { country: "Italy", gold: 40, silver: 35, bronze: 37 },
              { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
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

## Combination Series

Combination of different types like Line, column etc, can be rendered in a chart.

>Bar series cannot be combined with any other series as the axis orientation is different from other series.

{% tab template="chart/series/combination", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StackingColumn' xName='x' yName='y' name='Private Consumption'></e-series>
            <e-series [dataSource]='chartData' type='StackingColumn' xName='x' yName='y1' name='Government Consumption'></e-series>
            <e-series [dataSource]='chartData' type='StackingColumn' xName='x' yName='y2' name='Investment'></e-series>
            <e-series [dataSource]='chartData' type='StackingColumn' xName='x' yName='y3' name='Net Foreign Trade'></e-series>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y4' name='GDP' [marker]='marker' opacity=0.6></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public marker: Object;
    ngOnInit(): void {
        this.chartData = [
              { x: '2005', y: 1.2, y1: 0.5, y2: 0.7, y3: -0.8, y4: 1.5 },
              { x: '2006', y: 1, y1: 0.5, y2: 1.4, y3: 0, y4: 2.3 },
              { x: '2007', y: 1, y1: 0.5, y2: 1.5, y3: -1, y4: 2 },
              { x: '2008', y: 0.25, y1: 0.35, y2: 0.35, y3: -.35, y4: 0.1 },
              { x: '2009', y: 0.1, y1: 0.9, y2: -2.7, y3: -0.3, y4: -2.7 },
              { x: '2010', y: 1, y1: 0.5, y2: 0.5, y3: -0.5, y4: 1.8 },
              { x: '2011', y: 0.1, y1: 0.25, y2: 0.25, y3: 0, y4: 2 },
              { x: '2012', y: -0.25, y1: -0.5, y2: -0.1, y3: -0.4, y4: 0.4 },
              { x: '2013', y: 0.25, y1: 0.5, y2: -0.3, y3: 0, y4: 0.9 },
              { x: '2014', y: 0.6, y1: 0.6, y2: -0.6, y3: -0.6, y4: 0.4 },
              { x: '2015', y: 0.9, y1: 0.5, y2: 0, y3: -0.3, y4: 1.3 }
        ];
        this.primaryXAxis = {
            title: 'Years',
            interval: 1,
            labelIntersectAction : 'Rotate45',
            valueType: 'Category'
        };
        this.primaryYAxis = {
            title: 'Growth',
            minimum: -3, maximum: 3, interval: 1
        };
        this.marker = { visible: true, width: 10, opacity: 0.6, height: 10 };
        this.title = 'Annual Growth GDP in France';
    }

}
```

{% endtab %}

## Enable Complex Property in Series

By setting `enableComplexProperty` value as `true` in series you can bind complex data to the chart.

{% tab template="chart/series/combination", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart style='display:block;' align='center' id='chart-container' [primaryXAxis]='primaryXAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='data' type='Column' xName='group.x' yName='group.y' name='Gold' width=2 enableComplexProperty=true> </e-series>
            <e-series [dataSource]='data' type='Column' xName='group.x' yName='y' name='Silver' width=2  enableComplexProperty=true> </e-series>
        </e-series-collection>
    </ejs-chart>`
})

export class AppComponent implements OnInit {
public data: Object[] = [
  {group: { x: 'USA', y: 10}, y: 20},
  {group: { x: 'China', y: 30}, y: 10}
];
    //Initializing Primary X Axis
    public primaryXAxis: Object = {
        valueType: 'Category'
    };
    public title: string = 'Olympic Medal Counts - RIO';

}
```

{% endtab %}