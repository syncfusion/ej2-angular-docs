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

## Remote Data

You can also bind remote data to the chart using `DataManager`. The DataManager requires minimal information
like webservice URL, adaptor and crossDomain to interact with service endpoint properly. Assign the instance
 of DataManager to the [`dataSource`](../api/stock-chart/seriesDirective/#datasource) property in series and map
 the fields of data to [`xName`](../api/stock-chart/seriesDirective/#xname) and
[`yName`](../api/stock-chart/seriesDirective/#yname) properties. You can also use the
[`query`](../api/stock-chart/seriesDirective/#query) property of the series to filter the data.

{% tab template="stock-chart/datasource", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="stockChartSpline" [enablePeriodSelector]="enable" [chartArea]="chartArea"[primaryXAxis]="primaryXAxis" [primaryYAxis]="primaryYAxis" [seriesType]="seriesType"
      [indicatorType]="indicatorType">
      <e-stockchart-series-collection>
        <e-stockchart-series [dataSource]="dataManager" [query]="query" type="Spline" xName="ShippedDate"
          yName="Freight" >
        </e-stockchart-series>
      </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
  public dataManager: DataManager = new DataManager({
    url: "https://ej2services.syncfusion.com/production/web-services/api/Orders"
  });
  public query: Query = new Query()
    .take(5)
    .where("Estimate", "lessThan", 50, false);
  public primaryXAxis: Object = {
    valueType: "DateTime",
    crosshairTooltip: { enable: true },
    majorGridLines: { width: 0 }
  };
  public primaryYAxis: Object = {
    lineStyle: { width: 0 },
    majorTickLines: { width: 0 }
  };
  public seriesType: string[] = [];
  public indicatorType: string[] = [];
  public periods: object[] = [];
  public enable: boolean = false;
}
```

{% endtab %}

## See Also

* [Series Types](./series-types/)