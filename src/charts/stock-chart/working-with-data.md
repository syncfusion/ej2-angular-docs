---
title: " Stock Chart Working With Data | TypeScript "

component: "Stock Chart"

description: "Stock Chart can be rendered by using different types of data source. They are called local data, remote data and empty points."
---
<!-- markdownlint-disable MD036 -->

# Working with Data

Stock Chart can visualise data bound from local or remote data.

## Local Data

You can bind a simple JSON data to the chart using
[`dataSource`](../api/stock-chart/stockSeriesModel/#datasource) property in series.

{% tab template="stock-chart/datasource", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from './datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [crosshair]='crosshair'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='stockchartData' type='Candle' xName='date' yName='open' name='India' width=2 ></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public primaryYAxis: Object;
    public stockchartData: Object[];
    public title: string;
    public crosshair: Object;
    ngOnInit(): void {
        this.stockchartData = chartData;
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

## See Also

* [Series Types](./series-types/)