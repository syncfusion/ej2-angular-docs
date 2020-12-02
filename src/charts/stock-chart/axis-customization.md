---
title: " Stock Chart Axis Customization | Angular "

component: "Stock Chart"

description: " Stock Chart axis contains different customization and types like axis crossing, multiple axis, inversed axis, tick and grid, title customizations"
---

# Axis Customization

## Axis Crossing

An axis can be positioned in the Stock Chart area using [`crossesAt`](../api/stock-chart/stockChartAxisModel/#crossesat) and [`crossesInAxis`](../api/stock-chart/stockChartAxisModel/#crossesinaxis) properties. The [`crossesAt`](../api/stock-chart/stockChartAxisModel/#crossesat) property specifies the values (datetime, numeric, or logarithmic) at which the axis line has to be intersected with the vertical axis or vice-versa, and the [`crossesInAxis`](../api/stock-chart/stockChartAxisModel/#crossesinaxis) property specifies the axis name with which the axis line has to be crossed.

{% tab template="stock-chart/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis' [title]='title'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='chartData' type='Candle' xName='date' yName='open' name='India' width=2 ></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = chartData;
        this.title = 'Efficiency of oil-fired power production';
        this.primaryXAxis = {
           valueType: 'DateTime',
           crossesAt: 90
        };
    }

}
```

{% endtab %}

## Title

You can add a title to the axis using [`title`](../api/stock-chart/stockChartAxisModel/#title) property to provide quick
information to the user about the data plotted in the axis. Title style can be customized using [`titleStyle`](../api/stock-chart/stockChartAxisModel/#titlestyle) property of the axis.

{% tab template="stock-chart/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis' [title]='title'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='chartData' type='Candle' xName='date' yName='open' name='India' width=2 ></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = chartData;
        this.title = 'Efficiency of oil-fired power production';
        this.primaryXAxis = {
           valueType: 'DateTime',
           title: 'AAPL Historical',
        };
    }

}
```

{% endtab %}

## Tick Lines Customization

You can customize the  `width`, `color` and `size` of the minor and major tick lines, using
[`majorTickLines`](../api/stock-chart/stockChartAxisModel/#majorticklines) and
[`minorTickLines`](../api/stock-chart/stockChartAxisModel/#minorticklines) properties in the axis.

{% tab template="stock-chart/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis' [title]='title'>
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
    ngOnInit(): void {
        this.chartData = chartData;
        this.title = 'Efficiency of oil-fired power production';
        this.primaryXAxis = {
           valueType: 'DateTime',
        //Tick lines customization
             majorTickLines : {
                 color : 'blue',
                 width : 5
             },
             minorTickLines : {
                 color : 'red',
                 width : 0
             }
        };
        this.primaryYAxis = {
        //Tick lines customization
             majorTickLines : {
                 color : 'blue',
                 width : 5
             },
             minorTickLines : {
                 color : 'red',
                 width : 0
             }
        };
    }

}
```

{% endtab %}

## Grid Lines Customization

You can customize the `width`, `color` and `dashArray` of the minor and major grid lines, using [`majorGridLines`](../api/stock-chart/stockChartAxisModel/#majorgridlines)
and [`minorGridLines`](../api/stock-chart/stockChartAxisModel/#minorgridlines) properties in the axis.

{% tab template="stock-chart/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis' [title]='title'>
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
    ngOnInit(): void {
        this.chartData = chartData;
        this.title = 'Efficiency of oil-fired power production';
        this.primaryXAxis = {
           valueType: 'DateTime',
        //Tick lines customization
             majorGridLines : {
                 color : 'blue',
                 width : 5
             },
             minorGridLines : {
                 color : 'red',
                 width : 0
             }
        };
        this.primaryYAxis = {
        //Tick lines customization
             majorGridLines : {
                 color : 'blue',
                 width : 5
             },
             minorGridLines : {
                 color : 'red',
                 width : 0
             }
        };
    }

}
```

{% endtab %}

## Multiple Axis

In addition to primary X and Y axis, we can add n number of axis to the Stock Chart. Series can be associated with this [`axis`](../api/stock-chart/stockChartAxisModel), by mapping with axis's unique name.

{% tab template="stock-chart/multiple-axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-stockchart-axes>
            <e-stockchart-axis rowIndex=1 name='yAxis1' opposedPosition='true' title='Temperature (Celsius)' [majorGridLines]='majorGridLines' labelFormat='{value}°C'
                   [minimum]='24' [maximum]='36' [interval]='2' [lineStyle]='lineStyle'>
            </e-stockchart-axis>
        </e-stockchart-axes>
        <e-stockchart-rows>
             <e-stockchart-row height='20%'></e-stockchart-row>
             <e-stockchart-row height='20%'></e-stockchart-row>
        </e-stockchart-rows>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Germany'></e-stockchart-series>
            <e-stockchart-series [dataSource]='chartData' type='Line' xName='x' yName='y1' name='Japan' yAxisName='yAxis1' [marker]='marker'></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public majorGridLines: Object;
    public primaryYAxis: Object;
    public lineStyle: Object;
    public marker: Object;
    public rows: Object;
    ngOnInit(): void {
        this.chartData = [
                { x: new Date(2000, 2, 11), y: 15, y1: 29 },
                { x: new Date(2000, 9, 14), y: 20, y1: 30 },
                { x: new Date(2001, 2, 11), y: 25, y1: 28 },
                { x: new Date(2001, 9, 16), y: 21, y1: 35 },
                { x: new Date(2002, 2, 7), y: 13, y1: 29 },
                { x: new Date(2002, 9, 7), y: 18, y1: 31 },
                { x: new Date(2003, 2, 11), y: 24, y1: 25 },
                { x: new Date(2003, 9, 14), y: 23, y1: 28 },
                { x: new Date(2004, 2, 6), y: 19, y1: 24 },
                { x: new Date(2004, 9, 6), y: 31, y1: 25 },
                { x: new Date(2005, 2, 11), y: 39, y1: 27 },
                { x: new Date(2005, 9, 11), y: 30, y1: 30 },
                { x: new Date(2006, 2, 11), y: 24, y1: 20 }
        ];
        this.primaryXAxis = {
            title: 'Months',
            valueType: 'DateTime',
            interval: 1
        };
        this.primaryYAxis = {
            minimum: 0, maximum: 90, interval: 20,
            lineStyle: { width: 0 },
            title: 'Temperature (Fahrenheit)',
            labelFormat: '{value}°F',
            span: 2
        };
        this.majorGridLines = { width: 0};
        this.lineStyle = { width: 0};
        this.marker = {
            visible: true, width: 10, height: 10, border: { width: 2, color: '#F8AB1D' }
        }
        this.title = 'Multiple Axis';
    }

}
```

{% endtab %}

## Inversed Axis

<!-- markdownlint-disable MD033 -->

When an axis is inversed, highest value of the axis comes closer to origin and vice versa. To place an axis in inversed manner set this property
 [`isInversed`](../api/stock-chart/stockChartAxisModel/#isinversed) to true.

 {% tab template="stock-chart/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis' [title]='title'>
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
    ngOnInit(): void {
        this.chartData = chartData;
        this.title = 'Efficiency of oil-fired power production';
        this.primaryXAxis = {
           valueType: 'DateTime',
           isInversed: true
        };
        this.primaryYAxis = {
            isInversed: true
        };
    }

}
```

{% endtab %}

## Opposed Position

To place an axis opposite from its original position,
set [`opposedPosition`](../api/stock-chart/stockChartAxisModel/#opposedposition) property of the axis to true.

 {% tab template="stock-chart/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis' [title]='title'>
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
    ngOnInit(): void {
        this.chartData = chartData;
        this.title = 'Efficiency of oil-fired power production';
        this.primaryXAxis = {
           valueType: 'DateTime',
           opposedPosition: true
        };
        this.primaryYAxis = {
            opposedPosition: true
        };
    }

}
```

{% endtab %}