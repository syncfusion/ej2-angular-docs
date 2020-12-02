---
title: " StockChart Technical Indicators | Angular "

component: "StockChart"

description: "Indicators represent a statistical approach to technical analysis as opposed to a subjective approach. we have different types of indicators."
---

<!-- markdownlint-disable MD036 -->

# Technical Indicators

A technical indicator is a mathematical calculation based on historic price, volume or open interest information
that aims to forecast financial market direction.

StockChart supports 10 types of technical indicators namely `Accumulation Distribution`, `ATR`, `EMA`,`SMA`,`TMA`,`Momentum`,`MACD`,`RSI`,`Stochastic`,`Bollinger Band`. By using indicator dropdown box you can add an remove the required indicators types.

## Accumulation Distribution

Accumulation Distribution combines price and volume to show how money may be flowing into or out of stock.
To render a Accumulation Distribution Indicator,
use indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as `AccumulationDistribution` and inject
`AccumulationDistributionIndicatorService` into the `@NgModule.providers`.
To calculate the signal line [`volume`](../api/stock-chart/stockChartIndicatorModel/#volume) field is additionally added with `dataSource`.

## Average True Range (ATR)

ATR measures the stock volatility by comparing the current value with the
previous value. To render a Average True Range (ATR) Indicator,
use indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as `Atr` and inject `AtrIndicatorService` into the `@NgModule.providers`.

## Bollinger Band

A StockChart overlay that shows the upper and lower limits of normal price movements based on the standard deviation of prices.
To render a Bollinger Band, use indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as `BollingerBand`
and inject `BollingerBandsService` into the `@NgModule.providers`.
Bollinger band will be represented by three lines (upperLine, lowerLine, signalLine).Bollinger Band
default values of the [`period`](../api/stock-chart/stockChartIndicatorModel/#period) is 14 and
[`standardDeviations`](../api/stock-chart/stockChartIndicatorModel/#standarddeviation) is 2.

## Exponential Moving Average (EMA)

Moving average Indicators are used to define the direction of the trend. To render a EMA Indicator,
use indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as `Ema` and
inject `EMAIndicatorService` into the `@NgModule.providers`.

## Momentum

Momentum shows the speed at which the price of the stock is changing. To render a Momentum indicator, use indicator
[`type`](../api/stock-chart/stockChartIndicatorModel/#type) as `Momentum`and inject `MomentumIndicatorService` into the
`@NgModule.providers`. Momentum indicator will be represented by two lines (upperLine,
signalLine).In momentum indicator the upperBand value is always render at the value 100.

## Moving Average Convergence Divergence (MACD)

MACD is based on the difference between two EMA's. To render a MACD Indicator, use indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as
`MACD` and inject `MACDIndicatorService` into the `@NgModule.providers`.MACD indicator will be represented
by MACD line,signal line, MACD histogram. MACD histogram is used to differentiate MACD line and signal line.

## Relative Strength Index (RSI)

RSI shows how strongly a stock is moving in its current direction. To render a RSI Indicator, use
indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as`Rsi` and inject `RsiIndicatorService`
into the `@NgModule.providers`.RSI indicator will be represented
by three lines (upperBand, lowerBand, signalLine). The upperBand and lowerBand values are customized by
[`overBought`](../api/stock-chart/stockChartIndicatorModel/#overbrought) and [`overSold`](../api/stock-chart/stockChartIndicatorModel/#oversold)
properties of indicator and the signalLine is calculated by RSI formula.

## Simple Moving Average (SMA)

Moving average Indicators are used to define the direction of the trend. To render a SMA Indicator,
use indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as
`Sma` and inject `SmaIndicatorService` module using `@NgModule.providers`.

## Stochastic

It shows how a stock is, when compared to previous state. To render a Stochastic indicator,
use indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as `Stochastic`
and inject `StochasticIndicatorService` module using `@NgModule.providers` method.
stochastic indicator will be represented by four lines (upperLine, lowerLine, periodLine, signalLine).
In stochastic indicator the upperBand value and lowerBand value is customized by [`overBought`](../api/stock-chart/stockChartIndicatorModel/#overbought)
and [`overSold`](../api/stock-chart/stockChartIndicatorModel/#oversold) properties of indicators and the periodLine and
signalLine is render based on stochastic formula.

## Triangular Moving Average (TMA)

Moving average indicators are used to define the direction of the trend. To render a TMA Indicator,
use indicator [`type`](../api/stock-chart/stockChartIndicatorModel/#type) as
`TMA` and inject `TmaIndicatorService` module using `@NgModule.providers`.

{% tab template= "stock-chart/technical-indicators/tma", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
            `<ejs-stockchart id='chartcontainer' style="display:block;" [title]='title' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
              [chartArea]= 'chartArea'>
            <e-stockchart-indicators>
                <e-stockchart-indicator type='Tma' [dataSource]='data' xName='x' field="Close" high='high' low='low' open='open' fill="blue"
                close='close' volume='volume'> </e-stockchart-indicator>
            </e-stockchart-indicators>
        </ejs-stockchart>`
})
export class AppComponent implements OnInit {
 public data: Object[] = chartData;
    public primaryXAxis: Object = {
        title: 'Months',
        valueType: 'DateTime',
        intervalType: 'Months',
        majorGridLines: { width: 0}
    };
    public primaryYAxis: Object = {
        title: 'Price',
        labelFormat: '${value}',
        minimum: 30, maximum: 180,
        interval: 30,
    };
    public title: string = 'AAPL 2012-2017';
    public chartArea : Object = {
      border: { width : 0}
    };
    constructor() {
        //code
    };
}
```

{% endtab %}

**Module Dependencies**
To render a Indicator, it is mandatory to inject `LineSeriesService` module..
In addition to that, MACD Indicator requires `ColumnSeriesService` and BollingerBands requires `RangeAreaSeriesService`.
