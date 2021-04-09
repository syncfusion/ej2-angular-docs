---
title: " StockChart Series Types | Angular "

component: "StockChart"

description: "Essential JS 2 StockChart  StockChart supports 6 major types of series and also supports different tpes customizations for each type of StockChart."
---

# StockChart Series Types

Essential JS 2 StockChart supports 7 major types of series namely `Line`, `Spline`, `Area`, `Hilo`, `HiloOpenClose`, `Hollow Candle` and `Candle` . By using the series dropdown button you can navigate between the above listed series types.

<!-- markdownlint-disable MD036 -->

## Line

To render a line series, use series [`type`](../api/stock-chart/stockSeriesModel/#type) as `Line` and
inject `LineSeriesService` into the `@NgModule.providers`.

## Spline

To render a spline series, use series [`type`](../api/stock-chart/stockSeriesModel/#type) as `Spline` and inject `SplineSeriesService` into the `@NgModule.providers`.

## Area

To render a area series, use series [`type`](../api/stock-chart/stockSeriesModel/#type) as `Area` and inject `AreaSeriesService` into the `@NgModule.providers`.

## Hilo

To render a hilo series, use series [`type`](../api/stock-chart/stockSeriesModel/#type) as `Hilo` and
inject `HiloSeries` into the `@NgModule.providers`.

## HiloOpenClose

To render a hiloOpenClose series, use series [`type`](../api/stock-chart/stockSeriesModel/#type) as `HiloOpenClose` and inject `HiloOpenCloseSeries` into the `@NgModule.providers`..

## HollowCandle

To render a hollowcandle series, use series [`type`](../api/stock-chart/stockSeriesModel/#type) as `Candle` and set `enableSolidCandle` as false. Now inject `CandleSeries` into the `@NgModule.providers`.

## Candle

To render a candle series, use series [`type`](../api/stock-chart/stockSeriesModel/#type) as `Candle` and
inject `CandleSeries` into the `@NgModule.providers`.

{% tab template="stock-chart/series-types/candle", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='chartData' type='Candle' xName='date' yName='open' name='India' width=2 ></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = chartData;
        this.title = 'Efficiency of oil-fired power production';
    }

}
```

{% endtab %}