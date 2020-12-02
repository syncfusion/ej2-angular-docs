---
title: " Chart Multiple-panes | Angular "

component: "Chart"

description: "Chart can be divided multiple rows and columns. Axes are rendering based on row index or column index in pane."
---

# Multiple Panes

Chart area can be divided into multiple panes using [`rows`](../api/chart/rowDirective/) and [`columns`](../api/chart/columnDirective/).

## Rows

To split the chart area vertically into number of rows, use [`rows`](../api/chart/rowDirective/) property of the chart.

* You can allocate space for each row by using the [`height`](../api/chart/rowDirective/#height) property. The value can be either in
 percentage or in pixel.
* To associate a vertical axis to a particular row, specify its index to
[`rowIndex`](../api/chart/axisDirective/#rowindex-number) property of the axis.
* To customize each row’s bottom line, use [`border`](../api/chart/rowDirective/#border-bordermodel) property.

{% tab template="chart/axis/multiple-panes", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-axes>
            <e-axis rowIndex=1 name='yAxis1' opposedPosition='true' title='Temperature (Celsius)' [majorGridLines]='majorGridLines' labelFormat='{value}°C'
                   [minimum]='24' [maximum]='36' [interval]='2' [lineStyle]='lineStyle'>
            </e-axis>
        </e-axes>
        <e-rows>
             <e-row height=50%></e-row>
             <e-row height=50%></e-row>
        </e-rows>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Germany'></e-series>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y1' name='Japan' yAxisName='yAxis1' [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
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
                { x: 'Jan', y: 15, y1: 33 }, { x: 'Feb', y: 20, y1: 31 }, { x: 'Mar', y: 35, y1: 30 },
                { x: 'Apr', y: 40, y1: 28 }, { x: 'May', y: 80, y1: 29 }, { x: 'Jun', y: 70, y1: 30 },
                { x: 'Jul', y: 65, y1: 33 }, { x: 'Aug', y: 55, y1: 32 }, { x: 'Sep', y: 50, y1: 34 },
                { x: 'Oct', y: 30, y1: 32 }, { x: 'Nov', y: 35, y1: 32 }, { x: 'Dec', y: 35, y1: 31 }
        ];
        this.primaryXAxis = {
            title: 'Months',
            valueType: 'Category',
            interval: 1
        };
        this.primaryYAxis = {
            minimum: 0, maximum: 90, interval: 20,
            lineStyle: { width: 0 },
            title: 'Temperature (Fahrenheit)',
            labelFormat: '{value}°F'
        };
        this.majorGridLines = { width: 0};
        this.lineStyle = { width: 0};
        this.marker = {
            visible: true, width: 10, height: 10, border: { width: 2, color: '#F8AB1D' }
        }
        this.title = 'Weather Condition';
    }

}
```

{% endtab %}

For spanning the vertical axis along multiple row, you can use [`span`](../api/chart/axisDirective/#span) property of an axis.

{% tab template="chart/axis/multiple-panes", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-axes>
            <e-axis rowIndex=1 name='yAxis1' opposedPosition='true' title='Temperature (Celsius)' [majorGridLines]='majorGridLines' labelFormat='{value}°C'
                   [minimum]='24' [maximum]='36' [interval]='2' [lineStyle]='lineStyle'>
            </e-axis>
        </e-axes>
        <e-rows>
             <e-row height=50%></e-row>
             <e-row height=50%></e-row>
        </e-rows>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Germany'></e-series>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y1' name='Japan' yAxisName='yAxis1' [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
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
                { x: 'Jan', y: 15, y1: 33 }, { x: 'Feb', y: 20, y1: 31 }, { x: 'Mar', y: 35, y1: 30 },
                { x: 'Apr', y: 40, y1: 28 }, { x: 'May', y: 80, y1: 29 }, { x: 'Jun', y: 70, y1: 30 },
                { x: 'Jul', y: 65, y1: 33 }, { x: 'Aug', y: 55, y1: 32 }, { x: 'Sep', y: 50, y1: 34 },
                { x: 'Oct', y: 30, y1: 32 }, { x: 'Nov', y: 35, y1: 32 }, { x: 'Dec', y: 35, y1: 31 }
        ];
        this.primaryXAxis = {
            title: 'Months',
            valueType: 'Category',
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
        this.title = 'Weather Condition';
    }

}
```

{% endtab %}

## Columns

To split the chart area horizontally into number of columns, use [`columns`](../api/chart/columnDirective/) property of the chart.

* You can allocate space for each column by using the [`width`](../api/chart/columnDirective/#width)
property. The given width can be either in percentage or in pixel.
* To associate a horizontal axis to a particular column, specify its index to
[`columnIndex`](../api/chart/axisDirective/#columnindex) property of the axis.
* To customize each column’s bottom line, use [`border`](../api/chart/columnDirective/#border) property.

{% tab template="chart/axis/multiple-panes", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-axes>
            <e-axis columnIndex=1 name='xAxis1' opposedPosition='true' [majorGridLines]='majorGridLines'
                  valueType='Category' [lineStyle]='lineStyle'>
            </e-axis>
        </e-axes>
        <e-columns>
             <e-column width=50%></e-column>
             <e-column width=50%></e-column>
        </e-columns>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Germany'></e-series>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y1' name='Japan' xAxisName='xAxis1' [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
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
                { x: 'Jan', y: 15, y1: 33 }, { x: 'Feb', y: 20, y1: 31 }, { x: 'Mar', y: 35, y1: 30 },
                { x: 'Apr', y: 40, y1: 28 }, { x: 'May', y: 80, y1: 29 }, { x: 'Jun', y: 70, y1: 30 },
                { x: 'Jul', y: 65, y1: 33 }, { x: 'Aug', y: 55, y1: 32 }, { x: 'Sep', y: 50, y1: 34 },
                { x: 'Oct', y: 30, y1: 32 }, { x: 'Nov', y: 35, y1: 32 }, { x: 'Dec', y: 35, y1: 31 }
        ];
        this.primaryXAxis = {
            title: 'Months',
            valueType: 'Category',
            interval: 1
        };
        this.primaryYAxis = {
            minimum: 0, maximum: 90, interval: 20,
            lineStyle: { width: 0 },
            title: 'Temperature (Fahrenheit)',
            labelFormat: '{value}°F'
        };
        this.majorGridLines = { width: 0};
        this.lineStyle = { width: 0};
        this.marker = {
            visible: true, width: 10, height: 10, border: { width: 2, color: '#F8AB1D' }
        }
        this.title = 'Weather Condition';
    }

}
```

{% endtab %}

For spanning the horizontal axis along multiple column, you can use [`span`](../api/chart/axisDirective/#span) property of an axis.

{% tab template="chart/axis/multiple-panes", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-axes>
            <e-axis columnIndex=1 name='xAxis1' opposedPosition='true' [majorGridLines]='majorGridLines'
                  valueType='Category' [lineStyle]='lineStyle'>
            </e-axis>
        </e-axes>
        <e-columns>
             <e-column width=50%></e-column>
             <e-column width=50%></e-column>
        </e-columns>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Germany'></e-series>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y1' xAxisName='xAxis1' name='Japan' [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
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
                { x: 'Jan', y: 15, y1: 33 }, { x: 'Feb', y: 20, y1: 31 }, { x: 'Mar', y: 35, y1: 30 },
                { x: 'Apr', y: 40, y1: 28 }, { x: 'May', y: 80, y1: 29 }, { x: 'Jun', y: 70, y1: 30 },
                { x: 'Jul', y: 65, y1: 33 }, { x: 'Aug', y: 55, y1: 32 }, { x: 'Sep', y: 50, y1: 34 },
                { x: 'Oct', y: 30, y1: 32 }, { x: 'Nov', y: 35, y1: 32 }, { x: 'Dec', y: 35, y1: 31 }
        ];
        this.primaryXAxis = {
            title: 'Months',
            valueType: 'Category',
            interval: 1,
            span: 2
        };
        this.primaryYAxis = {
            minimum: 0, maximum: 90, interval: 20,
            lineStyle: { width: 0 },
            title: 'Temperature (Fahrenheit)',
            labelFormat: '{value}°F'
        };
        this.majorGridLines = { width: 0};
        this.lineStyle = { width: 0};
        this.marker = {
            visible: true, width: 10, height: 10, border: { width: 2, color: '#F8AB1D' }
        }
        this.title = 'Weather Condition';
    }

}
```

{% endtab %}
