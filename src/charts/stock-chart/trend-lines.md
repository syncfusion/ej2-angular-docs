---
title: " StockChart Trendlines | Angular "

component: "StockChart"

description: "Trendlines are used to show the direction and speed of price. StockChart supports 6 types of trendlines."
---

<!-- markdownlint-disable MD036 -->

# Trendlines

Trendlines are used to show the direction and speed of price.

StockChart supports 6 types of trendlines namely `Linear`,`Exponential`,`Logarithmic`,`Polynomial`,`Power`,`Moving Average`. By using trendline dropdown button you can add or remove the required trendline type.

## Linear

A linear trendline is a best fit straight line that is used with simpler data sets. To render a linear trendline,
use trendline [`type`](../api/stock-chart/stockChartTrendlineModel/#type) as `Linear` and inject
`TrendLines` .

## Exponential

An exponential trendline is a curved line that is most useful when data values rise or fall
at increasingly higher rates. You cannot create an exponential trendline, if your data contains zero or negative values.

To render a exponential trendline,
use trendline [`type`](../api/stock-chart/stockChartTrendlineModel/#type) as `Exponential` and inject
`TrendLines`.

## Logarithmic

A logarithmic trendline is a best-fit curved line that is most useful when the rate of change in the data increases or decreases quickly and then levels out. A logarithmic trendline can use negative and/or positive values.

To render a logarithmic trendline, use trendline [`type`](../api/stock-chart/stockChartTrendlineModel/#type) as `Logarithmic` and inject
`Trendlines` .

## Polynomial

A polynomial trendline is a curved line that is used when data fluctuates.

To render a polynomial trendline,
use trendline [`type`](../api/stock-chart/stockChartTrendlineModel/#type) as `Polynomial` and inject
`Trendlines` .

`polynomialOrder` used to define the polynomial value.

## Power

A power trendline is a curved line that is best used with data sets that compare measurements that increase at a specific rate.

To render a power trendline, use trendline [`type`](../api/stock-chart/stockChartTrendlineModel/#type) as `Power` and inject
`Trendlines` .

## Moving Average

A moving average trendline smoothen out fluctuations in data to show a pattern or trend more clearly.

To render a moving average trendline, use trendline [`type`](../api/stock-chart/stockChartTrendlineModel/#type) as `MovingAverage` and inject `Trendlines`.

`period` property defines the period to find the moving average.

{% tab template="stock-chart/trendlines/movingaverage", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
let series1 : any[] =[];
let yValue = [7.66, 8.03, 8.41, 8.97, 8.77, 8.20, 8.16, 7.89, 8.68, 9.48, 10.11, 11.36, 12.34, 12.60, 12.95,
    13.91, 16.21, 17.50, 22.72, 28.14, 31.26, 31.39, 32.43, 35.52, 36.36,
    41.33, 43.12, 45.00, 47.23, 48.62, 46.60, 45.28, 44.01, 45.17, 41.20, 43.41, 48.32, 45.65, 46.61, 53.34, 58.53];
let point1; let i; let j = 0;
for (i = 1973; i <= 2013; i++) {
    point1 = { x: i, y: yValue[j] };
    series1.push(point1); j++;
}
@Component({
    selector: 'app-container',
    template:
            `<ejs-stockchart id='chartcontainer'  [title]='title' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [chartArea]= 'chartArea'>
            <e-stockchart-series-collection>
                <e-stockchart-series [dataSource]='data' type='Scatter' xName='x' yName='y' fill="#0066FF">
                     <e-stockchart-trendlines>
                        <e-stockchart-trendline type='MovingAverage' width=3  name='Linear' fill='#C64A75' [backwardForecast]='backwardForecast'>
                        </e-stockchart-trendline>
                    </e-stockchart-trendlines>
                    </e-stockchart-series>
            </e-stockchart-series-collection>
        </ejs-stockchart>`
})

export class AppComponent implements OnInit {
    public data: Object[] = series1;
    public primaryXAxis: Object = {
        title: 'Months',
        majorGridLines: { width : 0}
    };
    public primaryYAxis: Object = {
       title: 'Rupees against Dollars',
       interval: 10, lineStyle: {width: 0}, majorTickLines: { width: 0 }
    };
    public chartArea : Object = {
      border: { width : 0}
    };
    public backwardForecast: number = 5;
    public title: string = 'Historical Indian Rupee Rate (INR USD)';
    constructor() {
        //code
    };
}
```

{% endtab %}