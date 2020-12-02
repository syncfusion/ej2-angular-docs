
# User Interaction

## Tooltip

Chart will display details about the points through tooltip, when the mouse is moved over the point

<!-- markdownlint-disable MD036 -->

**Enable Tooltip for Data Point**

<!-- markdownlint-disable MD012 -->
By default, tooltip is not visible. Enable the tooltip by setting
[`enable`](../api/chart/tooltipSettingsModel/#enable) property to true and by injecting `TooltipService`
into the `NgModule.providers`.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [tooltip]='tooltip'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' width=2 name='China' [marker]='marker'></e-series>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y1' width=2 name='Australia' [marker]='marker'></e-series>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y2' width=2 name='Japan' [marker]='marker'></e-series>
        </e-series-collection>
    </ej-chart>`
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
                { x: new Date(1975, 0, 1), y: 16, y1: 10, y2: 4.5 },
                { x: new Date(1980, 0, 1), y: 12.5, y1: 7.5, y2: 5 },
                { x: new Date(1985, 0, 1), y: 19, y1: 11, y2: 6.5 },
                { x: new Date(1990, 0, 1), y: 14.4, y1: 7, y2: 4.4 },
                { x: new Date(1995, 0, 1), y: 11.5, y1: 8, y2: 5 },
                { x: new Date(2000, 0, 1), y: 14, y1: 6, y2: 1.5 },
                { x: new Date(2005, 0, 1), y: 10, y1: 3.5, y2: 2.5 },
                { x: new Date(2010, 0, 1), y: 16, y1: 7, y2: 3.7 }
        ];
        this.primaryXAxis = {
            title: 'Years',
            lineStyle: { width: 0 },
            labelFormat: 'y',
            intervalType: 'Years',
            valueType: 'DateTime',
            edgeLabelPlacement: 'Shift'
        };
        this.primaryYAxis = {
            title: 'Percentage (%)',
            minimum: 0, maximum: 20, interval: 2,
            labelFormat: '{value}%'
        };
        this.tooltip = { enable: true };
        this.marker = { visible: true, width: 10, height: 10 };
        this.title = 'Unemployment Rates 1975-2010';

}
```

{% endtab %}

**Format the Tooltip**

By default, tooltip shows information of x and y value in points. In addition to that, you can show more
information in tooltip. For example the format '${series.name} ${point.x}' shows series name and point x
value.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [tooltip]='tooltip'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' width=2 name='China' [marker]='marker'></e-series>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y1' width=2 name='Australia' [marker]='marker'></e-series>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y2' width=2 name='Japan' [marker]='marker'></e-series>
        </e-series-collection>
    </ej-chart>`
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
                { x: new Date(1975, 0, 1), y: 16, y1: 10, y2: 4.5 },
                { x: new Date(1980, 0, 1), y: 12.5, y1: 7.5, y2: 5 },
                { x: new Date(1985, 0, 1), y: 19, y1: 11, y2: 6.5 },
                { x: new Date(1990, 0, 1), y: 14.4, y1: 7, y2: 4.4 },
                { x: new Date(1995, 0, 1), y: 11.5, y1: 8, y2: 5 },
                { x: new Date(2000, 0, 1), y: 14, y1: 6, y2: 1.5 },
                { x: new Date(2005, 0, 1), y: 10, y1: 3.5, y2: 2.5 },
                { x: new Date(2010, 0, 1), y: 16, y1: 7, y2: 3.7 }
        ];
        this.primaryXAxis = {
            title: 'Years',
            lineStyle: { width: 0 },
            labelFormat: 'y',
            intervalType: 'Years',
            valueType: 'DateTime',
            edgeLabelPlacement: 'Shift'
        };
        this.primaryYAxis = {
            title: 'Percentage (%)',
            minimum: 0, maximum: 20, interval: 2,
            labelFormat: '{value}%'
        };
        this.tooltip = { enable: true, format: '${series.name} ${point.x} : ${point.y}' };
        this.marker = { visible: true, width: 10, height: 10 };
        this.title = 'Unemployment Rates 1975-2010';

}
```

{% endtab %}

<!-- markdownlint-disable MD013 -->

**Tooltip Template**

Any HTML elements can be displayed in the tooltip by using the ‘template’ property of the tooltip. You can use the ${x} and ${y} as place holders in the HTML element to display the x and y values of the corresponding data point.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [tooltip]='tooltip'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' width=2 name='China' [marker]='marker'></e-series>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y1' width=2 name='Australia' [marker]='marker'></e-series>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y2' width=2 name='Japan' [marker]='marker'></e-series>
        </e-series-collection>
    </ej-chart>`
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
                { x: new Date(1975, 0, 1), y: 16, y1: 10, y2: 4.5 },
                { x: new Date(1980, 0, 1), y: 12.5, y1: 7.5, y2: 5 },
                { x: new Date(1985, 0, 1), y: 19, y1: 11, y2: 6.5 },
                { x: new Date(1990, 0, 1), y: 14.4, y1: 7, y2: 4.4 },
                { x: new Date(1995, 0, 1), y: 11.5, y1: 8, y2: 5 },
                { x: new Date(2000, 0, 1), y: 14, y1: 6, y2: 1.5 },
                { x: new Date(2005, 0, 1), y: 10, y1: 3.5, y2: 2.5 },
                { x: new Date(2010, 0, 1), y: 16, y1: 7, y2: 3.7 }
        ];
        this.primaryXAxis = {
            title: 'Years',
            lineStyle: { width: 0 },
            labelFormat: 'y',
            intervalType: 'Years',
            valueType: 'DateTime',
            edgeLabelPlacement: 'Shift'
        };
        this.primaryYAxis = {
            title: 'Percentage (%)',
            minimum: 0, maximum: 20, interval: 2,
            labelFormat: '{value}%'
        };
        this.tooltip = { enable: true, template: '<div>${x}</div><div>${y}</div>' };
        this.marker = { visible: true, width: 10, height: 10 };
        this.title = 'Unemployment Rates 1975-2010';

}
```

{% endtab %}

**Customize the Appearance of Tooltip**

The [`fill`](../api/chart/tooltipSettingsModel/#fill) and [`border`](../api/chart/tooltipSettingsModel/#border-bordermodel) properties are used to customize the background color and border of the tooltip respectively. The [`textStyle`](../api/chart/tooltipSettingsModel/#textstyle-fontmodel) property in the tooltip is used to customize the font of the tooltip text.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [tooltip]='tooltip'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' width=2 name='China' [marker]='marker'></e-series>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y1' width=2 name='Australia' [marker]='marker'></e-series>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y2' width=2 name='Japan' [marker]='marker'></e-series>
        </e-series-collection>
    </ej-chart>`
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
                { x: new Date(1975, 0, 1), y: 16, y1: 10, y2: 4.5 },
                { x: new Date(1980, 0, 1), y: 12.5, y1: 7.5, y2: 5 },
                { x: new Date(1985, 0, 1), y: 19, y1: 11, y2: 6.5 },
                { x: new Date(1990, 0, 1), y: 14.4, y1: 7, y2: 4.4 },
                { x: new Date(1995, 0, 1), y: 11.5, y1: 8, y2: 5 },
                { x: new Date(2000, 0, 1), y: 14, y1: 6, y2: 1.5 },
                { x: new Date(2005, 0, 1), y: 10, y1: 3.5, y2: 2.5 },
                { x: new Date(2010, 0, 1), y: 16, y1: 7, y2: 3.7 }
        ];
        this.primaryXAxis = {
            title: 'Years',
            lineStyle: { width: 0 },
            labelFormat: 'y',
            intervalType: 'Years',
            valueType: 'DateTime',
            edgeLabelPlacement: 'Shift'
        };
        this.primaryYAxis = {
            title: 'Percentage (%)',
            minimum: 0, maximum: 20, interval: 2,
            labelFormat: '{value}%'
        };
        this.tooltip = {
                enable: true,
                format: '${series.name} ${point.x} : ${point.y}',
                fill: '#7bb4eb',
                border: {
                   width: 2,
                   color: 'grey'
                }
        };
        this.marker = { visible: true, width: 10, height: 10 };
        this.title = 'Unemployment Rates 1975-2010';

}
```

{% endtab %}

## Zooming  and Panning

**Enable Zooming**

Chart can be zoomed in three ways.

* Selection - By setting [`enableSelectionZooming`](../api/chart/zoomSettingsModel/#enableselectionzooming) property to true
  in `zoomSettings`, you can zoom the chart by using the rubber band selection.
* Mousewheel - By setting [`enableMouseWheelZooming`](../api/chart/zoomSettingsModel/#enablemousewheelzooming) property to true
  in `zoomSettings`, you can zoomin and zoomout the chart by scrolling the mouse wheel.
* Pinch - By setting  [`enablePinchZooming`](../api/chart/zoomSettingsModel/#enablepinchzooming) property to true in `zoomSettings`,
  you can zoom the chart through pinch gesture in touch enabled devices.

 >Pinch zooming is supported only in browsers that support multi-touch gestures. Currently IE11, Chrome and Opera browsers support multi-touch in desktop devices.

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { series1 } from './chartdata';

@Component({
    selector: 'app-container',
    template:
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [zoomSettings]='zoom' [legendSettings]='legend'>
        <e-series-collection>
            <e-series [dataSource]='series1' type='Area' xName='x' yName='y' name='Product X' [border]='border' [animation]='animation'></e-series>
        </e-series-collection>
    </ej-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public series1: Object[];
    public title: string;
    public primaryYAxis: Object;
    public border: Object;
    public zoom: Object;
    public animation: Object;
    public legend: Object;
    ngOnInit(): void {
        this.chartData = [
              { x: new Date(2016, 0, 1), y: -7.1 }, { x: new Date(2016, 1, 1), y: -3.7 },
              { x: new Date(2016, 2, 1), y: 0.8 }, { x: new Date(2016, 3, 1), y: 6.3 },
              { x: new Date(2016, 4, 1), y: 13.3 }, { x: new Date(2016, 5, 1), y: 18.0 },
              { x: new Date(2016, 6, 1), y: 19.8 }, { x: new Date(2016, 7, 1), y: 18.1 },
              { x: new Date(2016, 8, 1), y: 13.1 }, { x: new Date(2016, 9, 1), y: 4.1 },
              { x: new Date(2016, 10, 1), y: -3.8 }, { x: new Date(2016, 11, 1), y: -6.8 }
        ];
        this.primaryXAxis = {
            title: 'Years',
            valueType: 'DateTime',
            labelFormat: 'yMMM',
            edgeLabelPlacement: 'Shift',
            majorGridLines : { width : 0 }
        };
        this.primaryYAxis = {
            title: 'Profit ($)',
            rangePadding: 'None',
            lineStyle : { width: 0 },
            majorTickLines : {width : 0}
        };
        this.zoom = {
            enableMouseWheelZooming: true,
            enablePinchZooming: true,
            enableSelectionZooming: true
        };
        this.animation = { enable: false};
        this.series1 = series1;
        this.legend = { visible: false };
        this.border = { width: 0.5, color: '#00bdae' };
        this.title = 'Sales History of Product X';
    }

}

```

{% endtab %}

After zooming the chart, a zooming toolbar will appear with `zoom`,`zoomin`, `zoomout`, `pan` and `reset` buttons.
Selecting the Pan option will allow to pan the chart and selecting the Reset option will reset the zoomed chart.

**Modes of Zooming**

The [`mode`](../api/chart/zoomSettingsModel/#mode) property in zoomSettings specifies whether the chart is allowed to scale along the horizontal axis or vertical axis. The default value of the mode is XY (both axis).

There are three types of mode.

* X - Allows us to zoom the chart horizontally.
* Y - Allows us to zoom the chart vertically.
* XY - Allows us to zoom the chart both vertically and horizontally.

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { series1 } from './chartdata';

@Component({
    selector: 'app-container',
    template:
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [zoomSettings]='zoom' [legendSettings]='legend'>
        <e-series-collection>
            <e-series [dataSource]='series1' type='Area' xName='x' yName='y' name='Product X' [border]='border' [animation]='animation'></e-series>
        </e-series-collection>
    </ej-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public series1: Object[];
    public title: string;
    public primaryYAxis: Object;
    public border: Object;
    public zoom: Object;
    public animation: Object;
    public legend: Object;
    ngOnInit(): void {
        this.chartData = [
              { x: new Date(2016, 0, 1), y: -7.1 }, { x: new Date(2016, 1, 1), y: -3.7 },
              { x: new Date(2016, 2, 1), y: 0.8 }, { x: new Date(2016, 3, 1), y: 6.3 },
              { x: new Date(2016, 4, 1), y: 13.3 }, { x: new Date(2016, 5, 1), y: 18.0 },
              { x: new Date(2016, 6, 1), y: 19.8 }, { x: new Date(2016, 7, 1), y: 18.1 },
              { x: new Date(2016, 8, 1), y: 13.1 }, { x: new Date(2016, 9, 1), y: 4.1 },
              { x: new Date(2016, 10, 1), y: -3.8 }, { x: new Date(2016, 11, 1), y: -6.8 }
        ];
        this.primaryXAxis = {
            title: 'Years',
            valueType: 'DateTime',
            labelFormat: 'yMMM',
            edgeLabelPlacement: 'Shift',
            majorGridLines : { width : 0 }
        };
        this.primaryYAxis = {
            title: 'Profit ($)',
            rangePadding: 'None',
            lineStyle : { width: 0 },
            majorTickLines : {width : 0}
        };
        this.zoom = {
             enableSelectionZooming: true,
             mode: 'X'
        };
        this.animation = { enable: false};
        this.series1 = series1;
        this.legend = { visible: false };
        this.border = { width: 0.5, color: '#00bdae' };
        this.title = 'Sales History of Product X';
    }

}

```

{% endtab %}

**Customizing Zooming Toolbar**

By default, zoomin, zoomout, pan and reset buttons will be displayed for zoomed chart. You can customize to show your desire tools in the toolbar using [`toolbarItems`](../api/chart/zoomSettingsModel/#toolbaritems) property.

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { series1 } from './chartdata';

@Component({
    selector: 'app-container',
    template:
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [zoomSettings]='zoom' [legendSettings]='legend'>
        <e-series-collection>
            <e-series [dataSource]='series1' type='Area' xName='x' yName='y' name='Product X' [border]='border' [animation]='animation'></e-series>
        </e-series-collection>
    </ej-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public series1: Object[];
    public title: string;
    public primaryYAxis: Object;
    public border: Object;
    public zoom: Object;
    public animation: Object;
    public legend: Object;
    ngOnInit(): void {
        this.chartData = [
              { x: new Date(2016, 0, 1), y: -7.1 }, { x: new Date(2016, 1, 1), y: -3.7 },
              { x: new Date(2016, 2, 1), y: 0.8 }, { x: new Date(2016, 3, 1), y: 6.3 },
              { x: new Date(2016, 4, 1), y: 13.3 }, { x: new Date(2016, 5, 1), y: 18.0 },
              { x: new Date(2016, 6, 1), y: 19.8 }, { x: new Date(2016, 7, 1), y: 18.1 },
              { x: new Date(2016, 8, 1), y: 13.1 }, { x: new Date(2016, 9, 1), y: 4.1 },
              { x: new Date(2016, 10, 1), y: -3.8 }, { x: new Date(2016, 11, 1), y: -6.8 }
        ];
        this.primaryXAxis = {
            title: 'Years',
            valueType: 'DateTime',
            labelFormat: 'yMMM',
            edgeLabelPlacement: 'Shift',
            majorGridLines : { width : 0 }
        };
        this.primaryYAxis = {
            title: 'Profit ($)',
            rangePadding: 'None',
            lineStyle : { width: 0 },
            majorTickLines : {width : 0}
        };
        this.zoom = {
            enableSelectionZooming: true,
            toolbarItems: ['Zoom', 'Pan', 'Reset']
        };
        this.animation = { enable: false};
        this.series1 = series1;
        this.legend = { visible: false };
        this.border = { width: 0.5, color: '#00bdae' };
        this.title = 'Sales History of Product X';
    }

}

```

{% endtab %}

>Note: To use zooming feature, we need to inject `ZoomService` into the `NgModule.providers`.

## Crosshair

Crosshair has a vertical and horizontal line to view the value of the axis at mouse or touch position.

**Enable Crosshair**

Crosshair lines can be enabled by using [`enable`](../api/chart/crosshairTooltip/#enable) property in the `crosshair`. Likewise tooltip label for an axis can be enabled by using [`enable`](../api/chart/crosshairTooltipModel/#enable) property of `crosshairTooltip` in the corresponding axis.



{% tab template="chart/user-interaction/crosshair", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { ChartData } from './chartdata';

@Component({
    selector: 'app-container',
    template:
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [legendSettings]='legend' [crosshair]='crosshair'>
        <e-axes>
            <e-axis [majorGridLines]='majorGridLines'[crosshairTooltip]='crosshair' rowIndex=0 opposedPosition='true'
                [minimum]='0' [maximum]='160' [interval]='20' name='yAxis' title='Rainfall (MM)'>
            </e-axis>
        </e-axes>
        <e-series-collection>
            <e-series [dataSource]='series1' type='Line' xName='x' yName='y' name='Temperature'></e-series>
            <e-series [dataSource]='series2' type='Line' xName='x' yName='y' name='Rainfall' yAxisName='yAxis'></e-series>
        </e-series-collection>
    </ej-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public series1: Object[];
    public series2: Object[];
    public majorGridLines: Object;
    public crosshair: Object;
    public title: string;
    public primaryYAxis: Object;
    public legend: Object;
    ngOnInit(): void {
        this.primaryXAxis = {
            majorGridLines: { width: 0 },
            valueType: 'DateTime',
            crosshairTooltip: { enable: true },
            labelFormat: 'yMMM'
        };
        this.primaryYAxis = {
            minimum: 10, maximum: 90, interval: 10,
            title: 'Temperature (°F)',
            rowIndex: 0,
            crosshairTooltip: { enable: true }
        };
        this.majorGridLines = { width: 0 };
        this.crosshair = { enable: true };
        this.series1 = ChartData.prototype.getCrosshairData().series1;
        this.series2 = ChartData.prototype.getCrosshairData().series2;
        this.legend = { visible: true };
        this.title = 'Weather Condition';
    }

}

```

{% endtab %}

**Customization**

The [`fill`](../api/chart/crosshairTooltip/#fill) and [`textStyle`](../api/chart/crosshairTooltip/#textstyle) property of the `crosshairTooltip` is used to customize the background color and font style of the crosshair label respectively.
Color and width of the crosshair line can be customized by using the [`line`](../api/chart/crosshairSettingsModel/#line) property in the crosshair.

{% tab template="chart/user-interaction/crosshair", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { ChartData } from './chartdata';

@Component({
    selector: 'app-container',
    template:
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [legendSettings]='legend' [crosshair]='crosshair'>
        <e-axes>
            <e-axis [majorGridLines]='majorGridLines' [crosshairTooltip]='crosshair' rowIndex=0 opposedPosition='true'
                [minimum]='0' [maximum]='160' [interval]='20' name='yAxis' title='Rainfall (MM)'>
            </e-axis>
        </e-axes>
        <e-series-collection>
            <e-series [dataSource]='series1' type='Line' xName='x' yName='y' name='Temperature'></e-series>
            <e-series [dataSource]='series2' type='Line' xName='x' yName='y' name='Rainfall' yAxisName='yAxis'></e-series>
        </e-series-collection>
    </ej-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public series1: Object[];
    public series2: Object[];
    public majorGridLines: Object;
    public crosshair: Object;
    public title: string;
    public primaryYAxis: Object;
    public legend: Object;
    ngOnInit(): void {
        this.primaryXAxis = {
           majorGridLines: { width: 0 },
            valueType: 'DateTime',
            crosshairTooltip: { enable: true, fill: 'green' },
            labelFormat: 'yMMM'
        };
        this.primaryYAxis = {
            minimum: 10, maximum: 90, interval: 10,
            title: 'Temperature (°F)',
            rowIndex: 0,
            crosshairTooltip: { enable: true, fill: 'green' }
        };
        this.majorGridLines = { width: 0 };
        this.crosshair = { enable: true, line: {width: 2, color: 'green'}, fill: 'green' };
        this.series1 = ChartData.prototype.getCrosshairData().series1;
        this.series2 = ChartData.prototype.getCrosshairData().series2;
        this.legend = { visible: true};
        this.title = 'Weather Condition';
    }

}

```

{% endtab %}

>Note: To use crosshair feature, we need to inject `CrosshairService` into the `NgModule.providers`.

## Trackball

Trackball is used to track a data point closest to the mouse or touch position. Trackball marker indicates the closest point and trackball tooltip displays the information about the point. To use trackball feature, we need to inject `CrosshairService` and `TooltipService` into the `NgModule.providers`.

Trackball can be enabled by setting the [`enable`](../api/chart/crosshairSettings/#enable) property of the crosshair to true and
[`shared`](../api/chart/tooltipSettings/#shared) property in `tooltip` to true in chart.

{% tab template="chart/user-interaction/trackball", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { series1, series2 } from './chartdata';

@Component({
    selector: 'app-container',
    template:
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [crosshair]='crosshair' [tooltip]='tooltip'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='John' width=2 [marker]='marker'></e-series>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y1' name='Andrew' width=2 [marker]='marker'></e-series>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y2' name='Thomas' width=2 [marker]='marker'></e-series>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y3' name='Mark' width=2 [marker]='marker'></e-series>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y4' name='William' width=2 [marker]='marker'></e-series>
        </e-series-collection>
    </ej-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public crosshair: Object;
    public title: string;
    public primaryYAxis: Object;
    public tooltip: Object;
    public marker: Object;
    ngOnInit(): void {
        this.chartData = [
            { x: new Date(2000, 2, 11), y: 15, y1: 39, y2: 60, y3: 75, y4: 85 },
            { x: new Date(2000, 9, 14), y: 20, y1: 30, y2: 55, y3: 75, y4: 83 },
            { x: new Date(2001, 2, 11), y: 25, y1: 28, y2: 48, y3: 68, y4: 85 },
            { x: new Date(2001, 9, 16), y: 21, y1: 35, y2: 57, y3: 75, y4: 87 },
            { x: new Date(2002, 2, 7), y: 13, y1: 39, y2: 62, y3: 71, y4: 82 },
            { x: new Date(2002, 9, 7), y: 18, y1: 41, y2: 64, y3: 69, y4: 74 },
            { x: new Date(2003, 2, 11), y: 24, y1: 45, y2: 57, y3: 81, y4: 73 },
            { x: new Date(2003, 9, 14), y: 23, y1: 48, y2: 53, y3: 84, y4: 75 },
            { x: new Date(2004, 2, 6), y: 19, y1: 54, y2: 63, y3: 85, y4: 73 },
            { x: new Date(2004, 9, 6), y: 31, y1: 55, y2: 50, y3: 87, y4: 60 },
            { x: new Date(2005, 2, 11), y: 39, y1: 57, y2: 66, y3: 75, y4: 48 },
            { x: new Date(2005, 9, 11), y: 50, y1: 60, y2: 65, y3: 70, y4: 55 },
            { x: new Date(2006, 2, 11), y: 24, y1: 60, y2: 79, y3: 85, y4: 40 }
        ];
        this.primaryXAxis = {
            title: 'Years',
            minimum: new Date(2000, 1, 1), maximum: new Date(2006, 2, 11),
            intervalType: 'Years',
            valueType: 'DateTime',
            lineStyle: { width: 0 },
            majorGridLines: { width: 0 },
            edgeLabelPlacement: 'Shift'
        };
        this.primaryYAxis = {
            title: 'Revenue in Millions',
            labelFormat: '{value}M',
            majorTickLines: { width: 0 },
            minimum: 10, maximum: 90,
            lineStyle: { width: 0 }
        };
        this.tooltip = { enable: true, shared: true, format: '${series.name} : ${point.x} : ${point.y}' };
        this.crosshair = { enable: true, lineType: 'Vertical' };
        this.marker = { visible: true };
        this.title = 'Average Sales per Person';
    }

}

```

{% endtab %}

## Selection

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

**Point**

 You can select a point, by setting `selectionMode` to point.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' selectionMode='Point'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze' ></e-series>
        </e-series-collection>
    </ej-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = [
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.primaryYAxis = {
           minimum: 0, maximum: 80,
           interval: 20, title: 'Medals',
        };
        this.title = 'Olympic Medals';
    }

}

```

{% endtab %}

**Series**

 You can select a series, by setting `selectionMode` to series.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' selectionMode='Series'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze' ></e-series>
        </e-series-collection>
    </ej-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = [
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.primaryYAxis = {
           minimum: 0, maximum: 80,
           interval: 20, title: 'Medals',
        };
        this.title = 'Olympic Medals';
    }

}

```

{% endtab %}

**Cluster**

You can select the points that corresponds to the same index in all the series, by setting `selectionMode` to cluster.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' selectionMode='Cluster'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze' ></e-series>
        </e-series-collection>
    </ej-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = [
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.primaryYAxis = {
           minimum: 0, maximum: 80,
           interval: 20, title: 'Medals',
        };
        this.title = 'Olympic Medals';
    }

}

```

{% endtab %}

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
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' selectionMode='DragXY'>
        <e-series-collection>
            <e-series [dataSource]='series1' type='Scatter' xName='x' yName='y' name='Male' opacity=0.7 [marker]='marker'></e-series>
            <e-series [dataSource]='series2' type='Scatter' xName='x' yName='y' name='Female' opacity=0.7 [marker]='marker'></e-series>
        </e-series-collection>
    </ej-chart>`
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
        this.chartData = [
              { x: 'Jan', y: 6, y1: 6, y2: -1 }, { x: 'Feb', y: 8 , y1: 8, y2: -1.5 },
              { x: 'Mar', y: 12, y1: 11, y2: -2 }, { x: 'Apr', y: 15, y1: 16, y2: -2.5 },
              { x: 'May', y: 20, y1: 21, y2: -3 }, { x: 'Jun', y: 24, y1: 25, y2: -3.5 },
              { x: 'Jul', y: 28, y1: 27, y2: -4 }, { x: 'Aug', y: 32, y1: 31, y2: -4.5 },
              { x: 'Sep', y: 33, y1: 34, y2: -5 }, { x: 'Oct', y: 35, y1: 34, y2: -5.5 },
              { x: 'Nov', y: 40, y1: 41, y2: -6 }, { x: 'Dec', y: 42, y1: 42, y2: -6.5 }
        ];
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

**Selection Type**

You can select multiple points or series, by enabling the [`isMultiSelect`](../api/chart/#ismultiselect) property.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' selectionMode='Point' isMultiSelect='true'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze' ></e-series>
        </e-series-collection>
    </ej-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = [
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.primaryYAxis = {
           minimum: 0, maximum: 80,
           interval: 20, title: 'Medals',
        };
        this.title = 'Olympic Medals';
    }

}

```

{% endtab %}

**Customizing Selection Style**

You can apply custom style to selected points or series with [`selectionStyle`](../api/chart/series/#selectionstyle) property.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' selectionMode='Point' isMultiSelect='true'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' selectionStyle='chartSelection1'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver' selectionStyle='chartSelection2'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze' selectionStyle='chartSelection3'></e-series>
        </e-series-collection>
    </ej-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = [
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.primaryYAxis = {
           minimum: 0, maximum: 80,
           interval: 20, title: 'Medals',
        };
        this.title = 'Olympic Medals';
    }

}

```

{% endtab %}

**Selection on Load**

You can able to select a point or series programmatically on a chart using [`selectedDataIndexes`](../api/chart/#selecteddataindexes) property.

{% tab template="chart/user-interaction/selection", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'
            selectionMode='Point' isMultiSelect='true' [selectedDataIndexes]='selectedData'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' selectionStyle='chartSelection1' [animation]='animation'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver' selectionStyle='chartSelection2' [animation]='animation'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze' selectionStyle='chartSelection3' [animation]='animation'></e-series>
        </e-series-collection>
    </ej-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public animation: Object;
    public selectedData: Object[];
    ngOnInit(): void {
        this.chartData = [
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.primaryYAxis = {
           minimum: 0, maximum: 80,
           interval: 20, title: 'Medals',
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

>Note: To use select feature, we need to Inject `SelectionService` into the `NgModule.providers`.

## Data Editing

We can use the data editing support using `DataEditingService` in the angular chart. It provides drag and drop support to the rendered points. Now, we can change the location or value of the point based on its `y` value.  To enable the data editing, set the `enable` property to true in the drag settings of the series. Also, we can set color using `fill` property and set the data editing minimum and maximum range using `minY` and `maxY` properties.

{% tab template="chart/user-interaction/data-editing", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'
            [chartArea]="chartArea">
        <e-series-collection>
            <e-series [dataSource]='columnData' type='Column' xName='x' yName='y' width="2" [marker]="marker" [dragSettings]="dragSettings"></e-series>
            <e-series [dataSource]='lineData' type='Line' xName='x' yName='y' width="2" [marker]="marker" [dragSettings]="dragSettings"></e-series>
        </e-series-collection>
    </ej-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public columnData: Object[];
    public lineData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public chartArea: Object;
    public marker: Object;
    public dragSettings: Object;
    ngOnInit(): void {
        this.columnData = [
                 { x: '2005', y: 21 }, { x: '2006', y: 60 },
                 { x: '2007', y: 45 }, { x: '2008', y: 50 },
                { x: '2009', y: 74 }, { x: '2010', y: 65 },
                { x: '2011', y: 85 }
        ];
        this.lineData = [
                 { x: '2005', y: 21 }, { x: '2006', y: 22 },
                    { x: '2007', y: 36 }, { x: '2008', y: 34 },
                    { x: '2009', y: 54 }, { x: '2010', y: 55 },
                    { x: '2011', y: 60 }
        ];
        this.primaryXAxis = {
            valueType: 'Category',
            minimum: -0.5,
            maximum: 6.5,
            labelPlacement: 'OnTicks',
            majorGridLines: { width: 0 },
        };
        this.primaryYAxis = {
           rangePadding: 'None',
            minimum: 0,
            title : 'Sales',
            labelFormat: '{value}%',
            maximum: 100,
            interval: 20,
            lineStyle: { width: 0 },
            majorTickLines: { width: 0 },
            minorTickLines: { width: 0 }
        };
        this.chartArea: {
            border: {
                width: 0
            }
        };
        this.title = 'Inflation - Consumer Price';
        this.marker = {
             visible: true,
             width: 10,
             height: 10
        };
        this.dragSettings = {
            enable: true
        };
    }
}

```

{% endtab %}


