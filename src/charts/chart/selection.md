---
title: " Chart Selection | Angular "

component: "Chart"

description: "Strip Lines are vertical or horizontal lines used to highlight/mark a certain region on the plot area."
---

<!-- markdownlint-disable MD036 -->

# Selection

Chart provides selection support for the series and its data points on mouse click.

>When Mouse is clicked on the data points, the corresponding series legend will also be selected.

We have different type of selection mode for selecting the data. They are,

* None
* Point
* Series
* Cluster
* DragXY
* DragX
* DragY

## Point

 You can select a point, by setting `selectionMode` to point.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { selectionData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' selectionMode='Point'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze' ></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = selectionData;
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.title = 'Olympic Medals';
    }

}

```

{% endtab %}

>Note: To use select feature, we need to Inject `SelectionService` into the `NgModule.providers`.

## Series

 You can select a series, by setting `selectionMode` to series.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { selectionData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' selectionMode='Series'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze' ></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = selectionData;
        this.primaryXAxis = {
           valueType: 'Category'
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

## Cluster

You can select the points that corresponds to the same index in all the series, by setting `selectionMode` to
cluster.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { selectionData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' selectionMode='Cluster'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze' ></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = selectionData;
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.title = 'Olympic Medals';
    }

}

```

{% endtab %}

## Rectangular selection

**DragXY, DragX and DragY**

To fetch the collection of data under a particular region, you have to set `selectionMode` as `DragXY`.

* DragXY - Allows us to select data with respect to horizontal and vertical axis.
* DragX - Allows us to select data with respect to horizontal axis.
* DragY - Allows us to select data with respect to vertical axis.

The selected data’s are returned as an array collection in the [`dragComplete`]
(../api/chart/iDragCompleteEventArgs/) event.

{% tab template="chart/user-interaction/drag", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { ChartData } from './chartdata.service';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' selectionMode='DragXY'>
        <e-series-collection>
            <e-series [dataSource]='series1' type='Scatter' xName='x' yName='y' name='Male' opacity=0.7 [marker]='marker'></e-series>
            <e-series [dataSource]='series2' type='Scatter' xName='x' yName='y' name='Female' opacity=0.7 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public series1: Object;
    public series2: Object;
    public marker: Object;
    ngOnInit(): void {
        this.primaryXAxis = {
            title: 'Height (cm)',
            minimum: 120, maximum: 180,
            edgeLabelPlacement: 'Shift',
            labelFormat: '{value}cm'
        };
        this.primaryYAxis = {
            title: 'Weight (kg)',
            minimum: 60, maximum: 90,
            labelFormat: '{value}kg',
            rangePadding: 'None'
        };
        this.title = 'Height Vs Weight';
        this.marker = {  width: 10, height: 10 };
        this.series1 = ChartData.prototype.getScatterData().series1;
        this.series2 = ChartData.prototype.getScatterData().series2;
    }

}

```

{% endtab %}

## Lasso selection

To select a region by drawing freehand shapes to fetch a collection of data use `selectionMode` as `Lasso`. You can also select multiple regions on the chart through this mode.

{% tab template="chart/user-interaction/drag", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { ChartData } from './chartdata.service';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' selectionMode='Lasso'>
        <e-series-collection>
            <e-series [dataSource]='series1' type='Scatter' xName='x' yName='y' name='Male' opacity=0.7 [marker]='marker'></e-series>
            <e-series [dataSource]='series2' type='Scatter' xName='x' yName='y' name='Female' opacity=0.7 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public series1: Object;
    public series2: Object;
    public marker: Object;
    ngOnInit(): void {
        this.primaryXAxis = {
            title: 'Height (cm)',
            minimum: 120, maximum: 180,
            edgeLabelPlacement: 'Shift',
            labelFormat: '{value}cm'
        };
        this.primaryYAxis = {
            title: 'Weight (kg)',
            minimum: 60, maximum: 90,
            labelFormat: '{value}kg',
            rangePadding: 'None'
        };
        this.title = 'Height Vs Weight';
        this.marker = {  width: 10, height: 10 };
        this.series1 = ChartData.prototype.getScatterData().series1;
        this.series2 = ChartData.prototype.getScatterData().series2;
    }

}

```

{% endtab %}

## Multi-region selection

To select multiple region on the chart, set the `allowMultiSelection` property to true.

{% tab template="chart/user-interaction/drag", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { ChartData } from './chartdata.service';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' selectionMode='DragXY' allowMultiSelection='true'>
        <e-series-collection>
            <e-series [dataSource]='series1' type='Scatter' xName='x' yName='y' name='Male' opacity=0.7 [marker]='marker'></e-series>
            <e-series [dataSource]='series2' type='Scatter' xName='x' yName='y' name='Female' opacity=0.7 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public series1: Object;
    public series2: Object;
    public marker: Object;
    ngOnInit(): void {
        this.primaryXAxis = {
            title: 'Height (cm)',
            minimum: 120, maximum: 180,
            edgeLabelPlacement: 'Shift',
            labelFormat: '{value}cm'
        };
        this.primaryYAxis = {
            title: 'Weight (kg)',
            minimum: 60, maximum: 90,
            labelFormat: '{value}kg',
            rangePadding: 'None'
        };
        this.title = 'Height Vs Weight';
        this.marker = {  width: 10, height: 10 };
        this.series1 = ChartData.prototype.getScatterData().series1;
        this.series2 = ChartData.prototype.getScatterData().series2;
    }

}

```

{% endtab %}

## Selection type

You can select multiple points or series, by enabling the [`isMultiSelect`](../api/chart/#ismultiselect) property.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { selectionData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' selectionMode='Point' isMultiSelect='true'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze' ></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = selectionData;
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.title = 'Olympic Medals';
    }

}

```

{% endtab %}

## Selection on load

You can able to select a point or series programmatically on a chart using
[`selectedDataIndexes`](../api/chart/#selecteddataindexes) property.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { selectionData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'
            selectionMode='Point' isMultiSelect='true' [selectedDataIndexes]='selectedData'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' selectionStyle='chartSelection1' [animation]='animation'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver' selectionStyle='chartSelection2' [animation]='animation'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze' selectionStyle='chartSelection3' [animation]='animation'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public animation: Object;
    public selectedData: Object[];
    ngOnInit(): void {
        this.chartData = selectionData;
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.animation = { enable: false};
        this.selectedData = [
        { series: 0, point: 1}, { series: 2, point: 3}
    ];
        this.title = 'Olympic Medals';
    }

}

```

{% endtab %}

## Selection through on legend

You can able to select a point or series through on legend using
[`toggleVisibility`](../api/chart/legendSettingsModel/#toggleVisibility) property.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { selectionData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'
       [legendSettings]='legendSettings'  selectionMode='Point'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' selectionStyle='chartSelection1' [animation]='animation'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver' selectionStyle='chartSelection2' [animation]='animation'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze' selectionStyle='chartSelection3' [animation]='animation'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public animation: Object;
    public selectedData: Object[];
    public legendSettings: Object;
    ngOnInit(): void {
        this.chartData = selectionData;
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.animation = { enable: false};
        this.legendSettings = { visible: true,  toggleVisibility: false };
        this.title = 'Olympic Medals';
    }

}

```

{% endtab %}

## Customization for selection

You can apply custom style to selected points or series with [`selectionStyle`](../api/chart/series/#selectionstyle) property.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { selectionData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' selectionMode='Point' isMultiSelect='true'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' selectionStyle='chartSelection1'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver' selectionStyle='chartSelection2'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze' selectionStyle='chartSelection3'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = selectionData;
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.title = 'Olympic Medals';
    }

}

```

{% endtab %}

## See Also

* [Display selected data for range selection](./how-to/selected-data-grid/#display-selected-data-for-range-selection)