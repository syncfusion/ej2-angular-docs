---
title: " StockChart Selecting Range | Angular "

component: "StockChart"

description: "we can able to select the particular range data by dragging thumbs or by tapping on the labels or by setting the start and end value properties. "
---

# Selecting Range

The left and right thumb of RangeNavigator are used to indicate the selected range in the large collection of data. Following are the ways you can select a range.

* By dragging the thumbs.
* By tapping on the labels.
* By setting the start and end through Date Range button.

{% tab template="stock-chart/range-selector", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [crosshair]='crosshair'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='chartData' type='Candle' xName='date' yName='open' name='India' width=2 ></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public primaryYAxis: Object;
    public chartData: Object[];
    public title: string;
    public crosshair: Object;
    ngOnInit(): void {
        this.chartData = chartData;
        this.title = 'Efficiency of oil-fired power production';
        this.primaryXAxis = {
           valueType: 'DateTime',
           crosshairTooltip: {enable:true}
        };
        this.primaryYAxis = {
           majorTickLines: { color: 'transparent', width: 0 },
           crosshairTooltip: {enable:true}
        };
        this.crosshair= {
            enable: true
        };
    }

}
```

{% endtab %}

## Visibility of range selector

The [`enableSelector`](../api/stock-chart/stockChartModel/#enableselector) property allows users to toggle the visibility of range selector.

{% tab template="stock-chart/range-selector", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [enableSelector]='enable' [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [crosshair]='crosshair'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='chartData' type='Candle' xName='date' yName='open' name='India' width=2 ></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public primaryYAxis: Object;
    public chartData: Object[];
    public title: string;
    public crosshair: Object;
    public enable: boolean = false;
    ngOnInit(): void {
        this.chartData = chartData;
        this.title = 'Efficiency of oil-fired power production';
        this.primaryXAxis = {
           valueType: 'DateTime',
           crosshairTooltip: {enable:true}
        };
        this.primaryYAxis = {
           majorTickLines: { color: 'transparent', width: 0 },
           crosshairTooltip: {enable:true}
        };
        this.crosshair= {
            enable: true
        };
    }

}
```

{% endtab %}