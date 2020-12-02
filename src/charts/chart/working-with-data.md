---
title: " Chart Working With Data | Angular "

component: "Chart"

description: "Chart can be rendered by using different types of data source. They are called local data, remote data and empty points. "
---

<!-- markdownlint-disable MD036 -->

# Working with Data

Chart can visualise data bound from local or remote data.

## Local Data

You can bind a simple JSON data to the chart using
[`dataSource`](../api/chart/seriesDirective/#datasource) property in series. Now map the fields in JSON to
[`xName`](../api/chart/seriesDirective/#xname) and [`yName`](../api/chart/seriesDirective/#yname)
properties.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='month' yName='sales' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    ngOnInit(): void {
        this.chartData = [
            { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
            { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
            { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
            { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
            { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
            { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
        ];
        this.primaryXAxis = {
            valueType: 'Category'
        };
    }

}
```

{% endtab %}

### Common Datasource

You can also bind a JSON data common to all series using
[`dataSource`](../api/chart/series/#datasource) property in chart.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis' [dataSource]='chartData'>
        <e-series-collection>
            <e-series type='Column' xName='month' yName='sales' name='Sales'></e-series>
            <e-series type='Column' xName='month' yName='sales1' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    ngOnInit(): void {
        this.chartData = [
      { month: 'Jan', sales: 35, sales1: 28 }, { month: 'Feb', sales: 28, sales1: 35 },
      { month: 'Mar', sales: 34, sales1: 32 }, { month: 'Apr', sales: 32, sales1: 34 },
      { month: 'May', sales: 40, sales1: 32 }, { month: 'Jun', sales: 32, sales1: 40 },
      { month: 'Jul', sales: 35, sales1: 55 }, { month: 'Aug', sales: 55, sales1: 35 },
      { month: 'Sep', sales: 38, sales1: 30 }, { month: 'Oct', sales: 30, sales1: 38 },
      { month: 'Nov', sales: 25, sales1: 32 }, { month: 'Dec', sales: 32, sales1: 25 }

        ];
        this.primaryXAxis = {
            valueType: 'Category'
        };
    }

}
```

{% endtab %}

## Lazy loading

Lazy loading allows you to load data for chart on demand. Chart will fire the scrollEnd event, in that we can
get the minimum and maximum range of the axis, based on this, we can upload the data to chart.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { ChartComponent } from '@syncfusion/ej2-angular-charts';
import { Internationalization, DateFormatOptions } from '@syncfusion/ej2-base';
import { ChangeEventArgs as NumericChange } from '@syncfusion/ej2-inputs';
import { NumericTextBoxComponent } from '@syncfusion/ej2-angular-inputs';
import { IScrollEventArgs, ILoadedEventArgs } from '@syncfusion/ej2-charts';
import { ChangeEventArgs } from '@syncfusion/ej2-dropdowns';
import { DropDownListComponent } from '@syncfusion/ej2-angular-dropdowns';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart style='display:block;' #chart [legendSettings]='legend' id='container' [primaryXAxis]='primaryXAxis'
            [tooltip]='tooltip' [height]='height' [width]='width' (scrollEnd)='scrollEnd($event)'
            [primaryYAxis]='primaryYAxis' [crosshair]='crosshair' [chartArea]='chartArea' [title]='title'>
            <e-series-collection>
                <e-series [dataSource]='data' [animation]='animation' type='Line' xName='x' yName='y'>
                </e-series>
            </e-series-collection>
        </ejs-chart>`
})
export class AppComponent implements OnInit {
    public intl: Internationalization = new Internationalization();
    @ViewChild('point')
    private pointslength: NumericTextBoxComponent;
    public value: number = 1000;
    public step: number = 100;
    public enabled: boolean = false;
    public format: string = 'n';
    public dropValue: string = 'Range';
    public minValue: Date = new Date(2009, 0, 1);
    public maxValue: Date = new Date(2014, 0, 1);
    public dropDownData: Object = [
        { value: 'Range' },
        { value: 'Points Length' }

    ];
    public fields: Object = { text: 'value', value: 'value' };
    public data: Object[] = this.GetNumericData(new Date(2009, 0, 1));
    @ViewChild('chart')
    public chart: ChartComponent;
    // Initializing Primary X Axis
    public primaryXAxis: Object = {
        title: 'Day',
        valueType: 'DateTime',
        edgeLabelPlacement: 'Shift',
        skeleton: 'yMMM',
        skeletonType: 'Date',
        scrollbarSettings: {
            range: {
                minimum: new Date(2009, 0, 1),
                maximum: new Date(2014, 0, 1)
            },
            enable: true,
            pointsLength: 1000
        }
    };
    public height: string = '450';
    public width: string = '100%';
    //Initializing Primary Y Axis
    public primaryYAxis: Object = {
        title: 'Server Load',
        labelFormat: '{value}MB'
    };
    public tooltip: Object = {
        enable: true, shared: true,
        header : "<b>${point.x}</b>", format : "Server load : <b>${point.y}</b>"
    };
    public legend: Object = {
        visible: false
    };
    public title: string = 'Network Load';
    public animation: Object = { enable: false };
    public chartArea: Object = {
        border: {
            width: 0
        }
    };
    public scrollEnd(args: IScrollEventArgs): void {
        this.chart.series[0].dataSource = this.GetNumericData(new Date(args.currentRange.maximum));
        this.chart.dataBind();
    };
    public GetNumericData(date: Date): {x: Date, y: number}[] {
        var series1 = [];
        var value = 30;
        for (var i = 0; i <= 60; i++) {
            if (Math.random() > .5) {
                value += (Math.random() * 10 - 5);
            }
            else {
                value -= (Math.random() * 10 - 5);
            }
            if (value < 0) {
                value = this.getRandomInt(20, 40);
            }
            date = new Date(date.setMinutes(date.getMinutes() + 1));
            var point = { x: date, y: Math.round(value) };
            series1.push(point);
        }
        return series1;
    }
    public getRandomInt(min, max) {
        return Math.floor(Math.random() * (max - min + 1)) + min;
    }
};

```

{% endtab %}

## Remote Data

You can also bind remote data to the chart using `DataManager`. The DataManager requires minimal information
like webservice URL, adaptor and crossDomain to interact with service endpoint properly. Assign the instance
 of DataManager to the [`dataSource`](../api/chart/seriesDirective/#datasource) property in series and map
 the fields of data to [`xName`](../api/chart/seriesDirective/#xname) and
[`yName`](../api/chart/seriesDirective/#yname) properties. You can also use the
[`query`](../api/chart/seriesDirective/#query) property of the series to filter the data.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'>
        <e-series-collection>
            <e-series [dataSource]='dataManager' type='Column' [query]='query' xName='CustomerID' yName='Freight' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public primaryYAxis: Object;
    public dataManager: DataManager = new DataManager({
    url: 'https://ej2services.syncfusion.com/production/web-services/api/Orders'
    });
    public query: Query = new Query().take(5).where('Estimate', 'lessThan', 3, false);
    ngOnInit(): void {
        this.primaryXAxis = {
            rangePadding: 'Additional',
            valueType: 'Category',
            title: 'Assignee'
        };
        this.primaryYAxis = {
            title: 'Estimate'
        };
    }

}
```

{% endtab %}

## Empty points

The Data points that uses the `null` or `undefined` as value are considered as empty points.
Empty data points are ignored and not plotted in the Chart.
When the data is provided by using the points property,
By using `emptyPointSettings` property in series, you can customize the empty point. Default `mode` of the empty point is `Gap`.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='month' yName='sales' name='Sales' [emptyPointSettings]='emptySeries1'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public marker: Object;
    public emptySeries1: Object;
    public emptySeries2: Object;
        ngOnInit(): void {
        this.chartData = [
            { month: 'Jan', sales: 35 }, { month: 'Feb', sales: null },
            { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
            { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
            { month: 'Jul', sales: undefined }, { month: 'Aug', sales: 55 },
            { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
            { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
        ];
        this.primaryXAxis = {
            valueType: 'Category'
        }
        this.marker: {
            visible : true
        }
        this.emptySeries1 = {
            mode: 'Gap'
        }
        this.emptySeries2 = {
            mode:'Average'
        }
    }

}
```

{% endtab %}

**Customizing empty point**

Specific color for empty point can be set by `fill` property in `emptyPointSettings`. Border for a empty point can be set by
`border` property.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='month' yName='sales' name='Sales' [emptyPointSettings]='emptySeries1'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public marker: Object;
    public emptySeries1: Object;
    public emptySeries2: Object;
        ngOnInit(): void {
        this.chartData = [
            { month: 'Jan', sales: 35 }, { month: 'Feb', sales: null },
            { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
            { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
            { month: 'Jul', sales: undefined }, { month: 'Aug', sales: 55 },
            { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
            { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
        ];
        this.primaryXAxis = {
            valueType: 'Category'
        }
        this.marker: {
            visible : true
        }
        this.emptySeries1 = {
            mode:'Average',
            fill: 'red',
            border: { width: 2, color: 'violet'}
        }
    }

}
```

{% endtab %}
