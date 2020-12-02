---
title: " Stock Chart Crosshair | Angular "

component: "StockChart"

description: "Crosshair has a vertical and horizontal line to view the value of the axis at mouse position.The trackball used to display data collections"
---

# Crosshair

Crosshair has a vertical and horizontal line to view the value of the axis at mouse or touch position.

Crosshair lines can be enabled by using [`enable`](../api/chart/crosshairSettings/#enable) property in the `crosshair`. Likewise tooltip label for an axis can be enabled by using [`enable`](../api/chart/crosshairTooltip/#enable) property of `crosshairTooltip` in the corresponding axis.

{% tab template="stock-chart/cross-hair", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis' [title]='title' [crosshair]='crosshair'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='chartData' type='Candle' xName='date' yName='open' name='India' width=2 ></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public crosshair: Object;
    ngOnInit(): void {
        this.chartData = chartData;
        this.title = 'Efficiency of oil-fired power production';
        this.primaryXAxis = {
           valueType: 'DateTime'
        };
        this.crosshair= {
            enable: true
        };
    }

}
```

{% endtab %}

## Tooltip for axis

Tooltip label for an axis can be enabled by using [`enable`](../api/chart/crosshairSettings/#enable) property of `crosshairTooltip` in the corresponding axis.

{% tab template="stock-chart/cross-hair", sourceFiles="app/**/*.ts" %}

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

## Customization

The [`fill`](../api/chart/crosshairSettings/#fill-string) and [`textStyle`](../api/chart/crosshairSettings/#textstyle-fontmodel)
property of the `crosshairTooltip` is used to customize the background color and font style of the crosshair label respectively.
Color and width of the crosshair line can be customized by using the
[`line`](../api/chart/crosshairSettingsModel/#line) property in the crosshair.

{% tab template="stock-chart/cross-hair", sourceFiles="app/**/*.ts" %}

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
            enable: true,
            line: {width: 2, color: 'green'}
        };
    }

}
```

{% endtab %}
