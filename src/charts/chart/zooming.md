---
title: " Chart Zooming | Angular "

component: "Chart"

description: "Chart have zooming and panning properties. Chart contains different  zoom modes, zoom toolbar items, scrollbar and auto interval zooming. "
---

# Zooming and Panning

## Enable Zooming

Chart can be zoomed in three ways.

* Selection - By setting [`enableSelectionZooming`](../api/chart/zoomSettingsModel/#enableselectionzooming) property to true
  in `zoomSettings`, you can zoom the chart by using the rubber band selection.
* Mousewheel - By setting [`enableMouseWheelZooming`](../api/chart/zoomSettingsModel/#enablemousewheelzooming) property to true
  in `zoomSettings`, you can zoomin and zoomout the chart by scrolling the mouse wheel.
* Pinch - By setting  [`enablePinchZooming`](../api/chart/zoomSettingsModel/#enablepinchzooming) property to true in `zoomSettings`,
  you can zoom the chart through pinch gesture in touch enabled devices.

 >Pinch zooming is supported only in browsers that support multi-touch gestures. Currently IE11, Chrome and Opera

 browsers support multi-touch in desktop devices.

 To known about Zooming and Panning, you can check on this video:

`youtube:B9_gRlZ5B94`

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { series1 } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [zoomSettings]='zoom' [legendSettings]='legend'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' name='Product X' [border]='border' [animation]='animation' opacity=0.3></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public border: Object;
    public zoom: Object;
    public animation: Object;
    public legend: Object;
    ngOnInit(): void {
        this.chartData = series1;
        this.primaryXAxis = {
            valueType: 'DateTime',
            labelFormat: 'yMMM',
        };
        this.zoom = {
            enableMouseWheelZooming: true,
            enablePinchZooming: true,
            enableSelectionZooming: true
        };
        this.animation = { enable: false};
        this.legend = { visible: false };

    }

}

```

{% endtab %}

>Note: To use zooming feature, we need to inject `ZoomService` into the `NgModule.providers`.

After zooming the chart, a zooming toolbar will appear with `zoom`,`zoomin`, `zoomout`, `pan` and `reset` buttons.
Selecting the Pan option will allow to pan the chart and selecting the Reset option will reset the zoomed chart.

## Modes

The [`mode`](../api/chart/zoomSettingsModel/#mode) property in zoomSettings specifies whether the chart is
allowed to scale along the horizontal axis or vertical axis. The default value of the mode is XY (both axis).

There are three types of mode.

* X - Allows us to zoom the chart horizontally.
* Y - Allows us to zoom the chart vertically.
* XY - Allows us to zoom the chart both vertically and horizontally.

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { series1 } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [zoomSettings]='zoom' [legendSettings]='legend'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' name='Product X' [border]='border' [animation]='animation' opacity=0.3></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public primaryYAxis: Object;
    public zoom: Object;
    public animation: Object;
    public legend: Object;
    ngOnInit(): void {
        this.chartData = series1;
        this.primaryXAxis = {
            valueType: 'DateTime',
            labelFormat: 'yMMM',
        };
        this.zoom = {
            enableSelectionZooming: true,
              mode: 'X'
        };
        this.animation = { enable: false};
        this.legend = { visible: false };

    }

}
```

{% endtab %}

## Toolbar

By default, zoomin, zoomout, pan and reset buttons will be displayed for zoomed chart. You can customize
to show your desire tools in the toolbar using [`toolbarItems`](../api/chart/zoomSettingsModel/#toolbaritems)
property.

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { series1 } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [zoomSettings]='zoom' [legendSettings]='legend'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' name='Product X' [border]='border' [animation]='animation' opacity=0.3></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public primaryYAxis: Object;
    public zoom: Object;
    public animation: Object;
    public legend: Object;
    ngOnInit(): void {
        this.chartData = series1;
        this.primaryXAxis = {
            valueType: 'DateTime',
            labelFormat: 'yMMM',
        };
        this.zoom = {
            enableSelectionZooming: true,
            toolbarItems: ['Zoom', 'Pan', 'Reset']
        };
        this.animation = { enable: false};
        this.legend = { visible: false };

    }

}
```

{% endtab %}

## Enable pan

Using [`enablePan`](../api/chart/zoomSettingsModel/#enablePan)
property you can able to pan the zoomed chart without help of toolbar items.

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { series1 } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [zoomSettings]='zoom' [legendSettings]='legend'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' name='Product X' [border]='border' [animation]='animation' opacity=0.3></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public primaryYAxis: Object;
    public zoom: Object;
    public animation: Object;
    public legend: Object;
    ngOnInit(): void {
        this.chartData = series1;
        this.primaryXAxis = {
            valueType: 'DateTime',
            labelFormat: 'yMMM',
            zoomFactor: 0.2, zoomPosition: 0.6
        };
        this.zoom = {
            enableSelectionZooming: true,
            enablePan: true
        };
        this.animation = { enable: false};
        this.legend = { visible: false };

    }

}
```

{% endtab %}

## Enable Scrollbar

Using `enableScrollbar` property, you can able to add scrollbar for zoomed chart. Using this scrollbar, you can pan or zoom the chart.

{% tab template="chart/user-interaction/scrollbar", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { series1 } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [zoomSettings]='zoom' [legendSettings]='legend'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' name='Product X' [border]='border' [animation]='animation' opacity=0.3></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public primaryYAxis: Object;
    public zoom: Object;
    public animation: Object;
    public legend: Object;
    ngOnInit(): void {
        this.chartData = series1;
        this.primaryXAxis = {
            valueType: 'DateTime',
            labelFormat: 'yMMM',
            zoomFactor: 0.2, zoomPosition: 0.6
        };
        this.zoom = {
            enableSelectionZooming: true,
            enableScrollbar: true
        };
        this.animation = { enable: false};
        this.legend = { visible: false };

    }

}
```

{% endtab %}

## Auto interval on zooming

By using [`enableAutoIntervalOnZooming`](../api/chart/axis/#enableAutoIntervalOnZooming) property,
the axis interval will get calculated automatically with respect to the zoomed range.

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { series1 } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [zoomSettings]='zoom' [legendSettings]='legend'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' name='Product X' [border]='border' [animation]='animation' opacity=0.3></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public primaryYAxis: Object;
    public zoom: Object;
    public animation: Object;
    public legend: Object;
    ngOnInit(): void {
        this.chartData = series1;
        this.primaryXAxis = {
            valueType: 'DateTime',
            labelFormat: 'yMMM'
        };
        this.zoom = {
            enableSelectionZooming: true,
        };
        enableAutoIntervalOnZooming: true,
        this.animation = { enable: false};
        this.legend = { visible: false };

    }

}
```

{% endtab %}