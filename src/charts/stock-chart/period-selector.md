---
title: " Stock Chart Period Selector | Angular "

component: "StockChart"

description: "The period selector allows to select a range with specified periods."
---

# Period selector

The period selector allows to select a range with specified periods. By default the period selector is enabled in stock chart.

## Periods

Periods is an array of objects that allows users to specify the range of [`periods`](../api/stock-chart/stockChartModel/#periods). The `interval` property specifies the count value of the button, and the `text` property specifies the text to be displayed on button. The `intervalType` property allows users to customize the intervals of the buttons. The `intervalType` property supports the following interval types:

* Auto
* Years
* Quarter
* Months
* Weeks
* Days
* Hours
* Minutes
* Seconds

{% tab template="stock-chart/period-selector", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { series1 } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis' [title]='title' [periods]='periods' [exportType]='exportType' [seriesType]='seriesType' [indicatorType]='indicatorType' [trendlineType]='trendlineType'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='India' width=2 ></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public periods: PeriodsModel[];
    public seriesType: string[] = [];
    public indicatorType: string[] = [];
    public trendlineType: string[] = [];
    public exportType: string[] = [];
    ngOnInit(): void {
        this.chartData = series1;
        this.title = 'Efficiency of oil-fired power production';
        this.primaryXAxis = {
           valueType: 'DateTime'
        };
        this.periods = [
            { intervalType: 'Minutes', interval: 1, text: '1m' },
            { intervalType: 'Minutes', interval: 30, text: '30m' },
            { intervalType: 'Hours', interval: 1, text: '1H' },
            { intervalType: 'Hours', interval: 12, text: '12H', selected: true },
            { intervalType: 'Auto', text: '1D' }
        ];
    }
}
```

{% endtab %}

## Visibility of period selector

The [`enablePeriodSelector`](../api/stock-chart/stockChartModel/#enableperiodselector) property allows users to toggle the visibility of period selector.

{% tab template="stock-chart/period-selector", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [enablePeriodSelector]='enable' [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [crosshair]='crosshair'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='chartData' type='Line' xName='date' yName='open' name='India' width=2 ></e-stockchart-series>
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