---
title: " Chart Other Types | Angular "

component: "Chart"

description: "Chart contains box and wishker, errorbar, waterfall and histogram charts and also supports different customization"
---

<!-- markdownlint-disable MD036 -->

# Box and whisker

To render a box and whisker chart, use series[`type`](../api/chart/seriesModel/#type) as `BoxAndWhisker` and inject
`BoxAndWhiskerSeriesService` into the `@NgModule.providers`. The field y requires n number of data or it should
contains minimum of five values to plot a segment.
>
{% tab template="chart/series/box", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chart-container' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='BoxAndWhisker' xName='x' yName='y' [marker]='marker'> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public data: Object[];
    public marker: Object;
    public tooltip: Object;
    ngOnInit(): void {
        this.data = data;
        this.primaryXAxis = {
            valueType: 'Category',
            };
        this.title = 'Company Revenue and Profit';
        this.marker = { visible: true }

    }
}

```

{% endtab %}

## Customization of Box and Whisker series

### boxPlotMode

You can change the rendering mode of the Box and Whisker series using the `boxPlotMode` property.
The default boxPlotMode is `exclusive`.The other boxPlotMode available are `inclusive` and `normal`.

To render a box and whisker chart, use series[`type`](../api/chart/seriesModel/#type) as `BoxAndWhisker` and
inject `BoxAndWhiskerSeriesService` into the `@NgModule.providers`. The field y requires n number of data or it
should contains minimum of five values to plot a segment.
>
{% tab template="chart/series/box", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chart-container' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='BoxAndWhisker' xName='x' yName='y' [marker]='marker' boxPlotMode='Normal'> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];
    public marker: Object;
    public tooltip: Object;
    ngOnInit(): void {
        this.data = data;
        this.primaryXAxis = {
            valueType: 'Category',
            };
        this.title = 'Company Revenue and Profit';
        this.marker = { visible: true };

    }
}

```

{% endtab %}

### showMean

In Box and Whisker series `showMean` property is used to show the box and whisker average value. The default value of `showMean` is false.

{% tab template="chart/series/box", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='BoxAndWhisker' xName='x' yName='y' [marker]='marker' [showMean]='showMean'> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];
    public marker: Object;
    public tooltip: Object;
    public showMean: boolean = false;

    ngOnInit(): void {
        this.data = data;
        this.primaryXAxis = {
            valueType: 'Category',
            };
        this.marker = {
            visible: true
            };
        this.title = 'Company Revenue and Profit';

    }
}

```

{% endtab %}

## Waterfall Chart

Waterfall chart helps to understand the cumulative effect of the sequentially introduced positive
and negative values. To render a Waterfall series, use series [`type`](../api/chart/seriesDirective/#type) as
`Waterfall` and inject `WaterfallSeriesService` into the `@NgModule.providers`.
[`intermediateSumIndexes`](../api/chart/seriesDirective/#intermediateSumIndexes) property of waterfall is used
to represent the in between the sum values and [`sumIndexes`](../api/chart/seriesDirective/#sumIndexes)
is used to represent the cumulative sum values.

{% tab template="chart/series/waterfall", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart style='display:block;' id='chart-container' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [title]='title' >
                <e-series-collection>
                    <e-series [dataSource]='data' type='Waterfall' xName='x' yName='y' name='USA' [columnWidth]='columnWidth'
                [connector]='connector' [intermediateSumIndexes]='intermediate' [sumIndexes]='sum' [marker]='marker'> </e-series>
                </e-series-collection>
     </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];
    public marker: Object;
    public connector: Object;
    public sum: number[] = [8];
    public intermediate: number[] = [4, 7];
    public columnWidth: number = 0.6;

    ngOnInit(): void {
        this.data = [
            { x: 'Income', y: 4711 }, { x: 'Sales', y: -1015 },
            { x: 'Development', y: -688 },
            { x: 'Revenue', y: 1030 }, {x: 'Balance'},
            { x: 'Administrative', y: -780 },
            { x: 'Expense', y: -361 }, { x: 'Tax', y: -695 },
            { x: 'Net Profit'}
            ];
        this.primaryXAxis = {
            majorGridLines: {width: 0},
            valueType: 'Category',
            };
        this.primaryYAxis = {
            labelFormat: '${value}M',
            minimum: 0, maximum: 5500, interval: 500,
            majorGridLines: {width: 0},
            lineStyle: { width: 0},
            majorTickLines: { width: 0}
            };
        this.marker = {
            dataLabel: { visible: true, position: 'Outer' }
            };
        this.connector = { color: '#5F6A6A', width: 1.5 };
        this.title = 'Company Revenue and Profit';
    }
}
```

{% endtab %}

**Customization of Waterfall Series**

The negative changes of waterfall charts is
represented by using [`negativeFillColor`](../api/chart/seriesDirective/#negativeFillColor) and the summary changes are
represented by using [`summaryFillColor`](../api/chart/seriesDirective/#summaryFillColor) properties.

By default, the negativeFillColor as ‘#E94649’ and the summaryFillColor as ‘#4E81BC’.

{% tab template="chart/series/waterfall", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { waterfallData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart style='display:block;' id='chart-container' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [title]='title' >
                <e-series-collection>
                    <e-series [dataSource]='data' type='Waterfall' xName='x' yName='y' name='USA' [columnWidth]='columnWidth' summaryFillColor='#e56590' negativeFillColor='#f8b883'
                [connector]='connector' [intermediateSumIndexes]='intermediate' [sumIndexes]='sum' [marker]='marker'> </e-series>
                </e-series-collection>
     </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];
    public marker: Object;
    public connector: Object;
    public sum: number[] = [8];
    public intermediate: number[] = [4, 7];
    public columnWidth: number = 0.6;

    ngOnInit(): void {
        this.data = waterfallData;
        this.primaryXAxis = {
            valueType: 'Category',
            };
        this.primaryYAxis = {
            labelFormat: '${value}M',
            minimum: 0, maximum: 5500, interval: 500,
            };
        this.marker = {
            dataLabel: { visible: true, position: 'Outer' }
            };
        this.connector = { color: '#5F6A6A', width: 1.5 };
        this.title = 'Company Revenue and Profit';
    }
}

```

{% endtab %}

## Histogram Series

Histogram type charts can provide a visual display of large amounts of data that are difficult to understand in a tabular or spreadsheet form. To render a histogram chart, use series [`type`](../api/chart/seriesDirective/#type) as `Histogram`and inject `HistogramSeriesService` into the `@NgModule.providers`.

{% tab template="chart/series/histogram", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart style='display:block;' align='center' id='chart-container' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis' (load)='load($event)'>
            <e-series-collection>
                <e-series [dataSource]='data' type='Histogram' yName='y' name='Score' width=2 [binInterval]='binInterval' showNormalDistribution='showNormalDistribution'
                [columnWidth]='columnWidth'> </e-series>
            </e-series-collection>
        </ejs-chart>`
})
export class AppComponent implements OnInit {
    public data: Object[] = [];
    public primaryXAxis: Object = {
        minimum: 0, maximum: 100
    };
    public primaryYAxis: Object = {
            minimum: 0, maximum: 50, interval: 10,
    };
    public load(args: ILoadedEventArgs): void {
        let points: number[] = [5.250, 7.750, 0, 8.275, 9.750, 7.750, 8.275, 6.250, 5.750,
        5.250, 23.000, 26.500, 27.750, 25.025, 26.500, 26.500, 28.025, 29.250, 26.750, 27.250,
        26.250, 25.250, 34.500, 25.625, 25.500, 26.625, 36.275, 36.250, 26.875, 40.000, 43.000,
        46.500, 47.750, 45.025, 56.500, 56.500, 58.025, 59.250, 56.750, 57.250,
        46.250, 55.250, 44.500, 45.525, 55.500, 46.625, 46.275, 56.250, 46.875, 43.000,
        46.250, 55.250, 44.500, 45.425, 55.500, 56.625, 46.275, 56.250, 46.875, 43.000,
        46.250, 55.250, 44.500, 45.425, 55.500, 46.625, 56.275, 46.250, 56.875, 41.000, 63.000,
        66.500, 67.750, 65.025, 66.500, 76.500, 78.025, 79.250, 76.750, 77.250,
        66.250, 75.250, 74.500, 65.625, 75.500, 76.625, 76.275, 66.250, 66.875, 80.000, 85.250,
        87.750, 89.000, 88.275, 89.750, 97.750, 98.275, 96.250, 95.750, 95.250
    ];
    points.map((value: number) => {
        this.data.push({
            y: value
        });
    });
    };
    public binInterval: number = 20;
    public columnWidth: number = 0.99;
    public showNormalDistribution: boolean = true;

    ngOnInit(): void {

    }
}
```

{% endtab %}

## Error Bar Chart

Error bars are graphical representations of the variability of data and used on graphs to indicate the error or uncertainty in a reported
measurement. To render the error bar for the series, set [`visible`](../api/chart/seriesDirective/#type)
as `true` in error bar object and inject `ErrorBar` module into the `@NgModule.providers`.

{% tab template="chart/series/errorbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='India' width=2 [marker]='marker' [errorBar]='errorBar'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    public errorBar: Object;
    ngOnInit(): void {
        this.chartData = [
            { x: 2006, y: 7.8 }, { x: 2007, y: 7.2 },
            { x: 2008, y: 6.8 }, { x: 2009, y: 10.7 },
            { x: 2010, y: 10.8 }, { x: 2011, y: 9.8 }
        ];
        this.primaryXAxis = {
            minimum: 2005, maximum: 2012, interval: 1,
            title: 'Year'
        };
        this.marker = { visible: true };
        this.errorBar = { visible: true };
        this.title = 'Unemployment rate (%)';
    }

}

```

{% endtab %}

**Changing Error Bar Type**

To change the error bar rendering type using [`type`](../api/chart/errorBarSettingsModel/#type)
option of error bar. To change the error bar line length you can use [`verticalError`](../api/chart/errorBarSettingsModel/#verticalError)
property.

{% tab template="chart/series/errorbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { errorData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='India' width=2 [marker]='marker' [errorBar]='errorBar'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public chartData: Object[];
    public title: string;
    public marker: Object;
    public errorBar: Object;
    ngOnInit(): void {
        this.chartData = errorData;
        this.marker = { visible: true };
        this.errorBar = { visible: true,  type: 'Percentage', verticalError:4 };
        this.title = 'Unemployment rate (%)';
    }

}

```

{% endtab %}

**Customizing Error Bar Type**

To customize the error bar type, set error bar [`type`](../api/chart/errorBarSettingsModel/#type) as `Custom` and
then change the horizontal/vertical positive and negative error of error bar.

{% tab template="chart/series/errorbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { errorData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='India' width=2 [marker]='marker' [errorBar]='errorBar'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public chartData: Object[];
    public title: string;
    public marker: Object;
    public errorBar: Object;
    ngOnInit(): void {
        this.chartData = errorData;
        this.marker = { visible: true };
        this.errorBar = { visible: true, type: 'Custom',
            mode:'Both'
            verticalPostiveError:3,
            horizontalPositiveError:2,
            verticalNegativeError:3,
            horizontalNegativeError:2
        };
        this.title = 'Unemployment rate (%)';
    }

}

```

{% endtab %}

**Changing Error Bar Mode**

Error bar mode is used to define whether the error bar line has to be drawn horizontally, vertically or in both side.
To change the error bar mode use [`mode`](../api/chart/errorBarSettingsModel/#mode) option.

{% tab template="chart/series/errorbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { errorData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='India' width=2 [marker]='marker' [errorBar]='errorBar'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public chartData: Object[];
    public title: string;
    public marker: Object;
    public errorBar: Object;
    ngOnInit(): void {
        this.chartData = errorData;
        this.marker = { visible: true };
        this.errorBar = { visible: true, mode: 'Horizontal' };
        this.title = 'Unemployment rate (%)';
    }

}

```

{% endtab %}

**Changing Error Bar Direction**

To change the error bar direction to plus, minus or both side using [`direction`](../api/chart/errorBarSettingsModel/#direction) option.

{% tab template="chart/series/errorbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { errorData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='India' width=2 [marker]='marker' [errorBar]='errorBar'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    public errorBar: Object;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = errorData;
        this.marker = { visible: true };
        this.errorBar = { visible: true,  mode:'Vertical', direction:'Minus' };
        this.title = 'Unemployment rate (%)';
    }

}

```

{% endtab %}

**Customizing Error Bar Cap**

To customize the error bar cap length, width and fill color, you can use [`errorBarCap`](../api/chart/errorBarCapSettingsModel/) option.

{% tab template="chart/series/errorbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { errorData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='India' width=2 [marker]='marker' [errorBar]='errorBar'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    public errorBar: Object;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = errorData;
        this.primaryXAxis = {
            minimum: 2005, maximum: 2012, interval: 1,
            title: 'Year'
        };
        this.marker = { visible: true };
        this.errorBar = { visible: true, errorBarCap:{ length:10, width:10, color:'#0000ff'
} };
        this.title = 'Unemployment rate (%)';
    }

}

```

{% endtab %}

## Vertical Chart

In EJ2 chart, you can draw a chart in vertical manner by changing orientation of the axis. All series types support this feature.
You can use `isTransposed` property in chart to render a chart in vertical manner.

{% tab template="chart/series/line", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { splineData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' isTransposed='true'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Spline' xName='x' yName='y' name='London' width=2 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public marker: Object;
    ngOnInit(): void {
        this.chartData = splineData;
        this.primaryXAxis = {
           title: 'Month',
           valueType: 'Category'
        };
        this.marker = { visible: true, width: 10, height: 10 };
        this.primaryYAxis = {
            minimum: -5, maximum: 35, interval: 5,
            title: 'Temperature in Celsius',
            labelFormat: '{value}C'
        };
        this.title = 'Climate Graph-2012';
    }

}
```

{% endtab %}

## Pareto chart

Pareto charts are used to find the cumulative values of data in different categories. It is a combination of Column and Line series.
The initial values are represented by column chart and the cumulative values are represented by Line chart.
To render a pareto chart, use series [`type`](../api/chart/seriesModel/#type) as
`Pareto` and inject `ParetoSeries` `ColumnSeries` and  `LineSeries` module.

{% tab template="chart/series/line", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { splineData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [tooltip]='tooltip'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Pareto' xName='x' yName='y' name='Defect' width=2 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public marker: Object;
    public tooltip: Object;
    ngOnInit(): void {
        this.chartData = [
                    { x: 'Traffic', y: 56 }, { x: 'Child Care', y: 44.8 },
                    { x: 'Transport', y: 27.2 }, { x: 'Weather', y: 19.6 },
                    { x: 'Emergency', y: 6.6 }
                ];
        this.primaryXAxis = {
            title: 'Defects',
            valueType: 'Category',
        };
        this.marker = { visible: true, width: 10, height: 10 };
        this.primaryYAxis = {
         title: 'Frequency',
            minimum: 0,
            maximum: 150,
            interval: 30,

        };
        this.tooltip = { enable: true, shared: true }
        this.title = 'Climate Graph-2012';
    }

}
```

{% endtab %}

## See Also

* [Data label](./data-labels/)
* [Tooltip](./tool-tip/)
