---
title: " Stock Chart Axis Types | Angular "

component: "Stock Chart"

description: "Date time axis uses date time scale and displays the date time values as axis labels in the specified format. "
---
<!-- markdownlint-disable MD036 -->

# DateTime and Logarithmic Axis

## DateTime Axis

Date time axis uses date time scale and displays the date time values as axis labels in the specified format and set the [`valueType`](../api/stock-chart/stockChartAxisModel/#valuetype) of axis to DateTime.

{% tab template="stock-chart/axis", sourceFiles="app/**/*.ts" %}

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
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = chartData;
        this.title = 'Efficiency of oil-fired power production';
        this.primaryXAxis = {
           valueType: 'DateTime'
        };
    }

}
```

{% endtab %}

## Logarithmic Axis

<!-- markdownlint-disable MD033 -->

Logarithmic axis uses logarithmic scale and it is very useful in visualizing data, when it has numerical values in both lower order of magnitude (eg: 10<sup>-6</sup>) and higher order of magnitude (eg: 10<sup>6</sup>) and set the [`valueType`](../api/stock-chart/stockChartAxisModel/#valuetype) of axis to `Lograthmic`.

{% tab template="stock-chart/axis", sourceFiles="app/**/*.ts" %}

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
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = chartData;
        this.title = 'Efficiency of oil-fired power production';
        this.primaryXAxis = {
           valueType: 'DateTime'
        };
        this.primaryYAxis = {
           valueType: 'Logarithmic'
        };
    }

}
```

{% endtab %}

## See Also

* [Axis Customization](./axis-customization/)
