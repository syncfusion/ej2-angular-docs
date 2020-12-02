---
title: " Financial charts | Angular "

component: "Chart"

description: "Financial charts are used to illustrate the movements in the price of a financial instrument over time. chart have hilo, hiloopenclose,candle."
---

# Financial Charts

Financial charts are used to illustrate the movements in the price of a financial instrument over time.

Chart supports the following financial series, to know more about financial type check the below video.

`youtube:veGoN2Ptz0M`

<!-- markdownlint-disable MD036 -->

## Hilo

Hilo Series illustrates the price movements in stock using the high and low values.
To render a Hilo series, use series [`type`](../api/chart/seriesDirective/#type) as `Hilo` and inject `HiloSeriesService` into the `@NgModule.providers`.

Hilo series requires 3 fields (x, high and low) to show the high and low price in the stock.

{% tab template="chart/series/hilo", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart style='display:block;' id='chart-container' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [title]='title' >
                <e-series-collection>
                    <e-series [dataSource]='data' type='Hilo' xName='x' high='high' low='low' name='India'> </e-series>
                </e-series-collection>
     </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];

    ngOnInit(): void {
        this.data = [
            { x: 'Jan', low: 87, high: 200 }, { x: 'Feb', low: 45, high: 135 },
            { x: 'Mar', low: 19, high: 85 }, { x: 'Apr', low: 31, high: 108 },
            { x: 'May', low: 27, high: 80 }, { x: 'June', low: 84, high: 130 },
            { x: 'July', low: 77, high: 150 }, { x: 'Aug', low: 54, high: 125 },
            { x: 'Sep', low: 60, high: 155 }, { x: 'Oct', low: 60, high: 180 },
            { x: 'Nov', low: 88, high: 180 }, { x: 'Dec', low: 84, high: 230 }
            ];
        this.primaryXAxis = {
            valueType: 'Category',
            title: 'Months'
            };
        this.primaryYAxis = {
            labelFormat: '{value}mm',
            edgeLabelPlacement: 'Shift',
            title: 'Rainfall',
            };
        this.title = 'Maximum and Minimum Rainfall';
    }
}
```

{% endtab %}

## High Low Open Close

HiloOpenClose series is used to represent the low, high, open and closing values over time.
To render a HiloOpenClose series, use series [`type`](../api/chart/seriesDirective/#type) as `HiloOpenClose` and
inject `HiloOpenCloseSeriesService` into the `@NgModule.providers`.

HiloOpenClose series requires 5 fields (x, high, low, open and close) to show the high, low, open and close price
values in the stock.

{% tab template="chart/series/hiloopenclose", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart style='display:block;' id='chart-container' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [title]='title' >
                <e-series-collection>
                    <e-series [dataSource]='data' type='HiloOpenClose' xName='x' high='high' low='low' open='open' close='close' name='SHIRPUR-G'> </e-series>
                </e-series-collection>
     </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];

    ngOnInit(): void {
        this.data = [
            { x: 'Jan', open: 120, high: 160, low: 100, close: 140 },
            { x: 'Feb', open: 150, high: 190, low: 130, close: 170 },
            { x: 'Mar', open: 130, high: 170, low: 110, close: 150 },
            { x: 'Apr', open: 160, high: 180, low: 120, close: 140 },
            { x: 'May', open: 150, high: 170, low: 110, close: 130 }
            ];
        this.primaryXAxis = {
            title: 'Date',
            valueType: 'Category',
            };
        this.primaryYAxis = {
            title: 'Price in Dollar', minimum: 100, maximum: 200, interval: 20,
            };
        this.title = 'Financial Analysis';
    }
}

```

{% endtab %}

### Customization of HiloOpenClose Series

In HiloOpenClose series, [`bullFillColor`](../api/chart/seriesDirective/#bullFillColor) is used to fill the
 segment when the open value is greater than the close value and
[`bearFillColor`](../api/chart/seriesDirective/#bearFillColor) is used to fill the segment when the open
value is less than the close value.

By default, bullFillColor is set as red and bearFillColor is set as green.

{% tab template="chart/series/hiloopenclose", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { openData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart style='display:block;' id='chart-container' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [title]='title' >
                <e-series-collection>
                    <e-series [dataSource]='data' type='HiloOpenClose' xName='x' high='high' low='low' open='open' close='close' name='SHIRPUR-G' bearFillColor= '#e56590' bullFillColor= '#f8b883'> </e-series>
                </e-series-collection>
     </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];

    ngOnInit(): void {
        this.data = openData;
        this.primaryXAxis = {
            title: 'Date',
            valueType: 'Category',
            };
        this.primaryYAxis = {
            title: 'Price in Dollar', minimum: 100, maximum: 200, interval: 20,
            };
        this.title = 'Financial Analysis';
    }
}

```

{% endtab %}

## Candle

Candle series are similar to Hilo Open Close series, are used to represent the low,
high, open and closing price over time. To render a candle series, use series
[`type`](../api/chart/seriesDirective/#type) as `Candle` and inject `CandleSeriesService` into the
`@NgModule.providers`.

{% tab template="chart/series/candle", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart style='display:block;' id='chart-container' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis' [title]='title' >
                <e-series-collection>
                    <e-series [dataSource]='data' type='Candle' xName='x' high='high' low='low' open='open' close='close' name='SHIRPUR-G'> </e-series>
                </e-series-collection>
     </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];

    ngOnInit(): void {
        this.data = [
            { x: 'Jan', open: 120, high: 160, low: 100, close: 140 },
            { x: 'Feb', open: 150, high: 190, low: 130, close: 170 },
            { x: 'Mar', open: 130, high: 170, low: 110, close: 150 },
            { x: 'Apr', open: 160, high: 180, low: 120, close: 140 },
            { x: 'May', open: 150, high: 170, low: 110, close: 130 }
            ];
        this.primaryXAxis = {
            title: 'Date',
            valueType: 'Category',
            };
        this.primaryYAxis = {
            title: 'Price in Dollar', minimum: 100, maximum: 200, interval: 20,
            };
        this.title = 'Financial Analysis';
    }
}

```

{% endtab %}

**Hollow Candles**

Candle charts allow to visually compare the current price with previous price by customizing the appearance.

Candles are filled/left as hollow based on the following criteria.

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td><b>States</b></td>
<td><b>Description </b></td>
</tr>
<tr>
<td>Filled</td>
<td>candle sticks are filled when the close value is lesser than the open value</td>
</tr>
<tr>
<td>Unfilled</td>
<td>candle sticks are unfilled when the close value is greater than the open value</td>
</tr>
</table>

The color of the candle will be defined by comparing with previous values.

Bear color  will be applied when the current closing value is greater than the previous closing value.
Bull color will be applied when the current closing value is less than the previous closing value.

By default, bullFillColor is set as red and bearFillColor is set as green.

**Solid Candles**

[`enableSolidCandles`](../api/chart/seriesDirective/#enableSolidCandles) is used to enable/disable the solid
candles. By default is set to be false. The fill color of the candle will be defined by its opening and closing values.

[`bearFillColor`](../api/chart/seriesDirective/#bearFillColor) will be applied when the opening value is less than the closing value.
[`bullFillColor`](../api/chart/seriesDirective/#bullFillColor) will be applied when the opening value is greater than closing value.

{% tab template="chart/series/candle", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { candleData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart style='display:block;' id='chart-container' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [title]='title'>
                <e-series-collection>
                    <e-series [dataSource]='data' type='Candle' xName='x' high='high' low='low' open='open' close='close' name='SHIRPUR-G' bearFillColor= '#e56590' bullFillColor= '#f8b883'
                     [enableSolidCandles]='enableSolidCandles'> </e-series>
                </e-series-collection>
     </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];
    public enableSolidCandles: Object = { enable: true };
    ngOnInit(): void {
        this.data = candleData;
        this.primaryXAxis = {
            title: 'Date',
            valueType: 'Category',
            };
        this.primaryYAxis = {
            title: 'Price in Dollar', minimum: 100, maximum: 200, interval: 20,
            };
        this.title = 'Financial Analysis';
    }
}

```

{% endtab %}

## See Also

* [Data label](./data-labels/)
* [Tooltip](./tool-tip/)
