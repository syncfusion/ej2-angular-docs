---
title: " Stock Chart Appearance | Angular "

component: "StockChart"

description: "We can customize stock chart appearance by using title and tooltip customizations."
---

# Appearance

## Stock Chart Title

StockChart can be given a title using [`title`](../api/stock-chart/#title-string) property, to show the information about the data plotted.

{% tab template="stock-chart/chart-title", sourceFiles="app/**/*.ts" %}

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

<!-- markdownlint-disable MD036 -->

**Title Customization**

The `textStyle` property of stockchart title provides options to customize the `size`, `color`, `fontFamily`, `fontWeight`, `fontStyle`, `opacity`, `textAlignment` and `textOverflow`.

{% tab template="stock-chart/chart-title", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [titleStyle]='titleStyle'>
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
        this.titleStyle = {
            fontFamily: "Arial",
            fontStyle: 'italic',
            fontWeight: 'regular',
            color: "#E27F2D",
            size: '23px',
            textOverflow: 'Wrap'
        }
    }
}
```

{% endtab %}

## Stock Chart Theme

Changing Stock Chart theme will affect background color, grid lines, tooltip colors and appearance.

[`theme`](../api/stock-chart/stockChartModel/#theme) property of Stock chart is shipped with several built-in themes such as `Material`, `Fabric`, `Bootstrap` , `HighContrastLight`, `MaterialDark`, `FabricDark`, `FabricDark`, `HighContrast` and `BootstrapDark`.

{% tab template="stock-chart/chart-title", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [theme]='theme'>
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
        this.theme = 'HighContrast';
    }
}
```

{% endtab %}

## See Also

* [Axis Customization](./axis-customization/)
