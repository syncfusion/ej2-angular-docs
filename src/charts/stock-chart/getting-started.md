---
title: " Stock Chart Getting Started | Angular "

component: "Stock Chart"

description: "Getting started file explains how to configure and install chart packages and also how to create basic stock chart, module injections."
---

# Getting started

This section explains you the steps required to create a simple StockChart and demonstrate the basic usage of the StockChart component in an Angular environment.

## Setup Angular Environment

You can use [`Angular CLI`](https://github.com/angular/angular-cli) to setup your Angular applications.
To install Angular CLI use the following command.

```bash
npm install -g @angular/cli
```

## Create an Angular Application

Start a new Angular application using below Angular CLI command.

```bash
ng new my-app
cd my-app
```

## Adding Syncfusion Chart package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Chart component, use the following command.

```bash
npm install @syncfusion/ej2-angular-charts --save
```

> The **--save** will instruct NPM to include the chart package inside of the `dependencies` section of the `package.json`.

## Registering StockChart Module

Import Chart module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-charts` [src/app/app.module.ts].

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the StockChartModule for the StockChart component
import { StockChartModule } from '@syncfusion/ej2-angular-charts';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of StockChartModule into NgModule
  imports:      [ BrowserModule, StockChartModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

* Modify the template in `app.component.ts` file to render the `ej2-angular-charts` component
`[src/app/app.component.ts]`.

```javascript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'app-container',
  // specifies the template string for the Charts component
  template: `<ejs-stockchart id='chart-container'></ejs-stockchart>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent  { }
```

<!-- markdownlint-disable MD033 -->

Now use the <code>app-container</code> in the index.html instead of default one.

```html
<app-container></app-container>
```

* Now run the application in the browser using the below command.

```cmd
npm start
```

## Module Injection

Chart component are segregated into individual feature-wise modules. In order to use a particular feature,
you need to inject its feature service in the AppModule. In the current application, we are
going to modify the above basic chart to visualize sales stock value of a company.
For this application we are going to use  candle series, tooltip, data label, datetime axis and legend
feature of the chart. Please find relevant
feature service name and description as follows.

* `CandleSeriesService` - Inject this provider to use candle series.
* `LegendService` - Inject this provider to use legend feature.
* `TooltipService` - Inject this provider to use tooltip feature.
* `DataLabelService` - Inject this provider to use datalabel feature.
* `DateTimeService`  - Inject this provider to use datetime feature.

These modules should be injected to the provider section as follows,

 ```javascript
    import { NgModule } from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';
    import { AppComponent } from './app.component';
    import { ChartComponent } from '@syncfusion/ej2-angular-charts';
    import { DateTimeService, LegendService, TooltipService } from '@syncfusion/ej2-angular-charts';
    import { DataLabelService, CandleSeriesService} from '@syncfusion/ej2-angular-charts';

    @NgModule({
        imports: [
            BrowserModule,
        ],
        declarations: [AppComponent, ChartComponent],
        bootstrap: [AppComponent],
        providers: [ DateTimeService, LegendService, TooltipService, DataLabelService, CandleSeriesService ]
    })

 ```

## Populate Chart with Data

This section explains how to plot below JSON data to the chart.

```javascript
    export class AppComponent implements OnInit {
    public chartData: Object[];
    ngOnInit(): void {
        // Data for chart series
        this.chartData = [{
            "x": new Date('2012-04-02T00:00:00.000Z'),
            "open": 320.705719,
            "high": 324.074066,
            "low": 317.737732,
            "close": 323.783783,
            "volume": 45638000
        }, {
            "x": new Date('2012-04-03T00:00:00.000Z'),
            "open": 323.028015,
            "high": 324.299286,
            "low": 319.639648,
            "close": 321.631622,
            "volume": 40857000
        }, {
            "x": new Date('2012-04-04T00:00:00.000Z'),
            "open": 319.544556,
            "high": 319.819824,
            "low": 315.865875,
            "close": 317.892883,
            "volume": 32519000
        }, {
            "x": new Date('2012-04-05T00:00:00.000Z'),
            "open": 316.436432,
            "high": 318.533539,
            "low": 314.599609,
            "close": 316.476471,
            "volume": 46327000
        }]

    }

}

 ```

 Add a series object to the chart by using [`series`](../api/stock-chart/stockChartSeriesDirective/) property and then set the JSON data to [`dataSource`](../api/stock-chart/stockChartSeriesDirective/#datasource-any) property.

Since the JSON contains datetime data, set the [`valueType`](../api/stock-chart/stockChartAxisDirective/#valuetype-any)for horizontal axis to `DateTime`. By default, the axis valueType is `Numeric`.

{% tab template="stock-chart/getting-started/datasource", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from './datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" >
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='stockchartData' type='Candle' xName='date' High='high' Low='low' Open='open' Close ='close' Name='Apple'></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
    public stockchartData: Object[];
    ngOnInit(): void {
        // Title for stock chart
        this.stockchartData = chartData;
    }
}


```

{% endtab %}

## Add Stock Chart Title

You can add a title using [`title`](../api/stock-chart/#title) property to the chart to provide
quick information to the user about the data plotted in the chart.

{% tab template="stock-chart/getting-started/title", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { chartData } from './datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container"
    [title]='title'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='stockchartData' type='Candle' xName='date' High='high' Low='low' Open='open' Close ='close' Name='Apple'></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
    public stockchartData: Object[];
    public title: string;
    ngOnInit(): void {
        // Title for chart
        this.title = 'AAPL Stock Price';
        this.stockchartData = chartData;
    }
}

```

{% endtab %}

## Add Stock Chart Crosshair

Crosshair has a vertical and horizontal line to view the value of the axis at mouse or touch position.

Crosshair lines can be enabled by using [`enable`](../api/chart/crosshairSettings/#enable) property in the `crosshair`. Likewise tooltip label for an axis can be enabled by using [`enable`](../api/chart/crosshairTooltip/#enable) property of `crosshairTooltip` in the corresponding axis.

{% tab template="stock-chart/getting-started/crosshair", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { chartData } from './datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container"
    [title]='title' [crosshair]='crosshair'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='stockchartData' type='Candle' xName='date' High='high' Low='low' Open='open' Close ='close' Name='Apple'></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
    public stockchartData: Object[];
    public title: string;
    ngOnInit(): void {
        // Title for chart
        this.title = 'AAPL Historical';
        this.crosshair = { enable: true };
        this.stockchartData = chartData;
    }
}

```

{% endtab %}

## Trackball

Trackball is used to track a data point closest to the mouse or touch position. Trackball marker indicates the
closest point and trackball tooltip displays the information about the point. To use trackball feature,
we need to inject `CrosshairService` and `TooltipService` into the `NgModule.providers`.

Trackball can be enabled by setting the [`enable`](../api/chart/crosshairSettings/#enable) property of the crosshair to true and
[`shared`](../api/chart/tooltipSettings/#shared) property in `tooltip` to true in chart.

{% tab template="stock-chart/getting-started/trackball", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [crosshair]='crosshair' [tooltip]='tooltip'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='John' width=2 [marker]='marker'></e-stockchart-series>
            <e-stockchart-series [dataSource]='chartData' type='Line' xName='x' yName='y1' name='Andrew' width=2 [marker]='marker'></e-stockchart-series>
            <e-stockchart-series [dataSource]='chartData' type='Line' xName='x' yName='y2' name='Thomas' width=2 [marker]='marker'></e-stockchart-series>
            <e-stockchart-series [dataSource]='chartData' type='Line' xName='x' yName='y3' name='Mark' width=2 [marker]='marker'></e-stockchart-series>
            <e-stockchart-series [dataSource]='chartData' type='Line' xName='x' yName='y4' name='William' width=2 [marker]='marker'></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public crosshair: Object;
    public title: string;
    public tooltip: Object;
    public marker: Object;
    ngOnInit(): void {
        this.chartData = [
            { x: new Date(2000, 2, 11), y: 15, y1: 39, y2: 60, y3: 75, y4: 85 },
            { x: new Date(2000, 9, 14), y: 20, y1: 30, y2: 55, y3: 75, y4: 83 },
            { x: new Date(2001, 2, 11), y: 25, y1: 28, y2: 48, y3: 68, y4: 85 },
            { x: new Date(2001, 9, 16), y: 21, y1: 35, y2: 57, y3: 75, y4: 87 },
            { x: new Date(2002, 2, 7), y: 13, y1: 39, y2: 62, y3: 71, y4: 82 },
            { x: new Date(2002, 9, 7), y: 18, y1: 41, y2: 64, y3: 69, y4: 74 },
            { x: new Date(2003, 2, 11), y: 24, y1: 45, y2: 57, y3: 81, y4: 73 },
            { x: new Date(2003, 9, 14), y: 23, y1: 48, y2: 53, y3: 84, y4: 75 },
            { x: new Date(2004, 2, 6), y: 19, y1: 54, y2: 63, y3: 85, y4: 73 },
            { x: new Date(2004, 9, 6), y: 31, y1: 55, y2: 50, y3: 87, y4: 60 },
            { x: new Date(2005, 2, 11), y: 39, y1: 57, y2: 66, y3: 75, y4: 48 },
            { x: new Date(2005, 9, 11), y: 50, y1: 60, y2: 65, y3: 70, y4: 55 },
            { x: new Date(2006, 2, 11), y: 24, y1: 60, y2: 79, y3: 85, y4: 40 }
        ];
        this.primaryXAxis = {
            title: 'Years',
            minimum: new Date(2000, 1, 1), maximum: new Date(2006, 2, 11),
            intervalType: 'Years',
            valueType: 'DateTime',
        };
        this.tooltip = { enable: true, shared: true, format: '${series.name} : ${point.x} : ${point.y}' };
        this.crosshair = { enable: true, lineType: 'Vertical' };
        this.marker = { visible: true };
        this.title = 'Average Sales per Person';
    }

}

```

{% endtab %}