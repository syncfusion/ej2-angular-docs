---
title: " Chart Trendlines | Angular "

component: "Chart"

description: "Trendlines are used to show the direction and speed of price. Chart supports 6 types of trendlines and also provides trendlines customization."
---

<!-- markdownlint-disable MD036 -->

# Trendlines

Trendlines are used to show the direction and speed of price.

Trendlines can be generated for Cartesian type series (Line, Column, Scatter, Area, Candle, Hilo etc.)
except bar type series. You can add more than one trendline to a series.

Chart supports 6 types of trendlines.

## Linear

A linear trendline is a best fit straight line that is used with simpler data sets. To render a linear trendline,
use trendline [`type`](../api/chart/trendline/#type) as `Linear` and inject
`TrendLines` .

{% tab template="chart/trendlines/linear", sourceFiles="app/**/*.ts" %}

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
            `<ejs-chart id='chartcontainer'  [title]='title' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [chartArea]= 'chartArea'>
            <e-series-collection>
                <e-series [dataSource]='data' type='Scatter' xName='x' yName='y' fill="#0066FF">
                     <e-trendlines>
                        <e-trendline type='Linear' width=3  name='Linear' fill='#C64A75'>
                        </e-trendline>
                    </e-trendlines>
                    </e-series>
            </e-series-collection>
        </ejs-chart>`
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

    public title: string = 'Historical Indian Rupee Rate (INR USD)';
    constructor() {
        //code
    };
}
```

{% endtab %}

## Exponential

An exponential trendline is a curved line that is most useful when data values rise or fall
at increasingly higher rates. You cannot create an exponential trendline, if your data contains zero or negative values.

To render a exponential trendline,
use trendline [`type`](../api/chart/trendline/#type) as `Exponential` and inject
`TrendLines`.

{% tab template="chart/trendlines/exponential", sourceFiles="app/**/*.ts" %}

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
            `<ejs-chart id='chartcontainer'  [title]='title' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [chartArea]= 'chartArea'>
            <e-series-collection>
                <e-series [dataSource]='data' type='Scatter' xName='x' yName='y' fill="#0066FF">
                     <e-trendlines>
                        <e-trendline type='Linear' width=3  name='Exponential' fill='#C64A75'>
                        </e-trendline>
                    </e-trendlines>
                    </e-series>
            </e-series-collection>
        </ejs-chart>`
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

    public title: string = 'Historical Indian Rupee Rate (INR USD)';
    constructor() {
        //code
    };
}
```

{% endtab %}

## Logarithmic

A logarithmic trendline is a best-fit curved line that is most useful when the rate of change
in the data increases or decreases quickly and then levels out.

A logarithmic trendline can use negative and/or positive values.

To render a logarithmic trendline, use trendline [`type`](../api/chart/trendline/#type) as `Logarithmic` and inject
`TrendLines` .

{% tab template="chart/trendlines/logarithmic", sourceFiles="app/**/*.ts" %}

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
            `<ejs-chart id='chartcontainer'  [title]='title' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [chartArea]= 'chartArea'>
            <e-series-collection>
                <e-series [dataSource]='data' type='Scatter' xName='x' yName='y' fill="#0066FF">
                     <e-trendlines>
                        <e-trendline type='Linear' width=3  name='Logarithmic' fill='#C64A75'>
                        </e-trendline>
                    </e-trendlines>
                    </e-series>
            </e-series-collection>
        </ejs-chart>`
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

    public title: string = 'Historical Indian Rupee Rate (INR USD)';
    constructor() {
        //code
    };
}
```

{% endtab %}

## Polynomial

A polynomial trendline is a curved line that is used when data fluctuates.

To render a polynomial trendline,
use trendline [`type`](../api/chart/trendline/#type) as `Polynomial` and inject
`TrendLines`.

`polynomialOrder` used to define the polynomial value.

{% tab template= "chart/trendlines/polynomial",  sourceFiles="app/**/*.ts" %}

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
            `<ejs-chart id='chartcontainer'  [title]='title' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [chartArea]= 'chartArea'>
            <e-series-collection>
                <e-series [dataSource]='data' type='Scatter' xName='x' yName='y' fill="#0066FF">
                     <e-trendlines>
                        <e-trendline type='Linear' width=3  name='Linear' fill='#C64A75'>
                        </e-trendline>
                    </e-trendlines>
                    </e-series>
            </e-series-collection>
        </ejs-chart>`
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

    public title: string = 'Historical Indian Rupee Rate (INR USD)';
    constructor() {
        //code
    };
}
```

{% endtab %}

## Power

A power trendline is a curved line that is best used with data sets that compare measurements that increase at a specific rate.

To render a power trendline, use trendline [`type`](../api/chart/trendline/#type) as `Power` and inject
`TrendLines`.

{% tab template="chart/trendlines/power",  sourceFiles="app/**/*.ts" %}

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
            `<ejs-chart id='chartcontainer'  [title]='title' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [chartArea]= 'chartArea'>
            <e-series-collection>
                <e-series [dataSource]='data' type='Scatter' xName='x' yName='y' fill="#0066FF">
                     <e-trendlines>
                        <e-trendline type='Linear' width=3  name='Linear' fill='#C64A75'>
                        </e-trendline>
                    </e-trendlines>
                    </e-series>
            </e-series-collection>
        </ejs-chart>`
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

    public title: string = 'Historical Indian Rupee Rate (INR USD)';
    constructor() {
        //code
    };
}

```

{% endtab %}

## Moving Average

A moving average trendline smoothen out fluctuations in data to show a pattern or trend more clearly.

To render a moving average trendline, use trendline [`type`](../api/chart/trendline/#type) as `MovingAverage` and inject
`TrendLines` .

`period` property defines the period to find the moving average.

{% tab template="chart/trendlines/movingaverage",  sourceFiles="app/**/*.ts" %}

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
            `<ejs-chart id='chartcontainer'  [title]='title' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [chartArea]= 'chartArea'>
            <e-series-collection>
                <e-series [dataSource]='data' type='Scatter' xName='x' yName='y' fill="#0066FF">
                     <e-trendlines>
                        <e-trendline type='MovingAverage' width=3  name='Linear' fill='#C64A75'>
                        </e-trendline>
                    </e-trendlines>
                    </e-series>
            </e-series-collection>
        </ejs-chart>`
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

    public title: string = 'Historical Indian Rupee Rate (INR USD)';
    constructor() {
        //code
    };
}

```

{% endtab %}

**Customization of Trendlines**

The [`fill`](../api/chart/trendline/#fill) and [`width`](../api/chart/trendline/#width)
properties are used to customize the appearance of the trendline.

{% tab template="chart/trendlines/movingaverage",  sourceFiles="app/**/*.ts" %}

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
            `<ejs-chart id='chartcontainer'  [title]='title' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [chartArea]= 'chartArea'>
            <e-series-collection>
                <e-series [dataSource]='data' type='Scatter' xName='x' yName='y' fill="#0066FF">
                     <e-trendlines>
                        <e-trendline type='MovingAverage' width=3  name='Linear' fill='#C64A75'>
                        </e-trendline>
                    </e-trendlines>
                    </e-series>
            </e-series-collection>
        </ejs-chart>`
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

    public title: string = 'Historical Indian Rupee Rate (INR USD)';
    constructor() {
        //code
    };
}
```

{% endtab %}

## Forecasting

Trendlines forecasting is the prediction of future/past situations.

Forecasting can be classified into two types as follows

Forward Forecasting
Backward Forecasting

**Forward Forecasting**

The value set for forwardForecast is used to determine the distance moving towards the future trend.

{% tab template="chart/trendlines/movingaverage",  sourceFiles="app/**/*.ts" %}

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
            `<ejs-chart id='chartcontainer'  [title]='title' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [chartArea]= 'chartArea'>
            <e-series-collection>
                <e-series [dataSource]='data' type='Scatter' xName='x' yName='y' fill="#0066FF">
                     <e-trendlines>
                        <e-trendline type='MovingAverage' width=3  name='Linear' fill='#C64A75' [forwardForecast]='forwardForecast'>
                        </e-trendline>
                    </e-trendlines>
                    </e-series>
            </e-series-collection>
        </ejs-chart>`
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
    public forwardForecast: number = 5;
    public title: string = 'Historical Indian Rupee Rate (INR USD)';
    constructor() {
        //code
    };
}

```

{% endtab %}

**Backward Forecasting**

The value set for the backwardForecast is used to determine the past trends.

{% tab template="chart/trendlines/movingaverage", sourceFiles="app/**/*.ts" %}

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
            `<ejs-chart id='chartcontainer'  [title]='title' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [chartArea]= 'chartArea'>
            <e-series-collection>
                <e-series [dataSource]='data' type='Scatter' xName='x' yName='y' fill="#0066FF">
                     <e-trendlines>
                        <e-trendline type='MovingAverage' width=3  name='Linear' fill='#C64A75' [backwardForecast]='backwardForecast'>
                        </e-trendline>
                    </e-trendlines>
                    </e-series>
            </e-series-collection>
        </ejs-chart>`
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