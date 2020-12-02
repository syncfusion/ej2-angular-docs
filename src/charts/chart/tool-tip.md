---
title: " Chart Tooltip | Angular "

component: "Chart"

description: "Tooltip is used to show the data value when mouse hover on the chart.We can able to customize format,template and appearance."
---

# Tooltip

<!-- markdownlint-disable MD036 -->

Chart will display details about the points through tooltip, when the mouse is moved over the point.

## Default Tooltip

By default, tooltip is not visible. Enable the tooltip by setting
[`enable`](../api/chart/tooltipSettingsModel/#enable) property to true and by injecting `TooltipService`
into the `NgModule.providers`.

To known about tooltip, you can check on this video:

`youtube:GaJ16060GZ8`

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { toolData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [tooltip]='tooltip'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' width=2 name='China' [marker]='marker'></e-series>
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
        this.chartData = toolData;
        this.primaryXAxis = {
            valueType: 'DateTime',
        };
        this.tooltip = { enable: true };
        this.marker = { visible: true, width: 10, height: 10 };
        this.title = 'Unemployment Rates 1975-2010';

}
```

{% endtab %}

<!-- markdownlint-disable MD013 -->

## Format the Tooltip

<!-- markdownlint-disable MD013 -->

By default, tooltip shows information of x and y value in points. In addition to that, you can show more
information in tooltip. For example the format '${series.name} ${point.x}' shows series name and point x
value.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { toolData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [tooltip]='tooltip'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' width=2 name='China' [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    public tooltip: Object;
    ngOnInit(): void {
        this.chartData = toolData;
        this.primaryXAxis = {
            valueType: 'DateTime'
        };
        this.tooltip = { enable: true, header: 'Unemployment', format: '<b>${point.x} : ${point.y}</b>' };
        this.marker = { visible: true, width: 10, height: 10 };
        this.title = 'Unemployment Rates 1975-2010';

}
```

{% endtab %}

<!-- markdownlint-disable MD013 -->

## Individual Series Format

<!-- markdownlint-disable MD013 -->

 You can format the each series tooltip separately using series `tooltipFormat` property.

 >Note: If series `tooltipFormat` is given, it shows the tooltip for that series in that format, or else it will take tooltip format.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { toolData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [tooltip]='tooltip'>
        <e-series-collection>
            <e-series [dataSource]='chartData1' type='Spline' xName='x' yName='y' width=2 name='Max Temp' [marker]='marker' tooltipFormat='${point.x}'></e-series>
            <e-series [dataSource]='chartData2' type='Spline' xName='x' yName='y' width=2 name='Avg Temp' [marker]='marker' tooltipFormat='${point.y}'></e-series>
            <e-series [dataSource]='chartData3' type='Spline' xName='x' yName='y' width=2 name='Min Temp' [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData1: Object[];
    public chartData2: Object[];
    public chartData3: Object[];
    public tooltipFormat1: string;
    public tooltipFormat2: string;
    public title: string;
    public marker: Object;
    public tooltip: Object;
    ngOnInit(): void {
        this.chartData1 = [
                { x: 'Sun', y: 15 }, { x: 'Mon', y: 22 },
                { x: 'Tue', y: 32 },
                { x: 'Wed', y: 31 },
                { x: 'Thu', y: 29 }, { x: 'Fri', y: 24 },
                { x: 'Sat', y: 18 },
            ];
        this.chartData2 = [
                { x: 'Sun', y: 10 }, { x: 'Mon', y: 18 },
                { x: 'Tue', y: 28 },
                { x: 'Wed', y: 28 },
                { x: 'Thu', y: 26 }, { x: 'Fri', y: 20 },
                { x: 'Sat', y: 15 }
            ];
        this.chartData3 = [
                { x: 'Sun', y: 2 }, { x: 'Mon', y: 12 },
                { x: 'Tue', y: 22 },
                { x: 'Wed', y: 23 },
                { x: 'Thu', y: 19 }, { x: 'Fri', y: 13 },
                { x: 'Sat', y: 8 },
            ];
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.tooltip = { enable: true, header: 'Unemployment', format: '<b>${point.x} : ${point.y}</b>' };
        this.marker = { visible: true, width: 10, height: 10 };
        this.title = 'NC Weather Report - 2016';

}
```

{% endtab %}

<!-- markdownlint-disable MD013 -->

## Tooltip Template

Any HTML elements can be displayed in the tooltip by using the ‘template’ property of the tooltip. You can use the ${x} and ${y} as place holders in the HTML element to display the x and y values of the corresponding data point.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { toolData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [tooltip]='tooltip'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' width=2 name='China' [marker]='marker'></e-series>
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
        this.chartData = toolData;
        this.primaryXAxis = {
            valueType: 'DateTime'
        };
        this.tooltip = { enable: true, template: '#Unemployment' };
        this.marker = { visible: true, width: 10, height: 10 };
        this.title = 'Unemployment Rates 1975-2010';

}
```

{% endtab %}

## Tooltip Mapping Name

By default, tooltip shows information of x and y value in points. You can show more information from data source in tooltip by using the `tooltipMappingName` property of the tooltip. You can use the `${point.tooltip}` as place holders to display the specified tooltip content.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { toolData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis' [title]='title' [tooltip]='tooltip'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' width=2 tooltipMappingName='country'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public tooltip: Object;
    ngOnInit(): void {
        this.chartData =  [
                    { x: 'Germany', y: 72, country: 'GER: 72'},
                    { x: 'Russia', y: 103.1, country: 'RUS: 103.1'},
                    { x: 'Brazil', y: 139.1, country: 'BRZ: 139.1'},
                    { x: 'India', y: 462.1, country: 'IND: 462.1'},
                    { x: 'China', y: 721.4, country: 'CHN: 721.4'},
                    { x: 'United States Of America', y: 286.9, country: 'USA: 286.9'},
                    { x: 'Great Britain', y: 115.1, country: 'GBR: 115.1'},
                    { x: 'Nigeria', y: 97.2, country: 'NGR: 97.2'},
        ];
        this.primaryXAxis = {
             valueType: 'Category',
        };
        this.tooltip = {
               enable: true, format: '${point.tooltip}'
        };
        this.title = 'Internet Users in Million – 2016';

}
```

{% endtab %}

## Customize the Appearance of Tooltip

The [`fill`](../api/chart/tooltipSettingsModel/#fill) and [`border`](../api/chart/tooltipSettingsModel/#border) properties are used to customize the background color and border of the tooltip respectively. The [`textStyle`](../api/chart/tooltipSettingsModel/#textstyle) property in the tooltip is used to customize the font of the tooltip text.

{% tab template="chart/user-interaction/tooltip", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { toolData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [tooltip]='tooltip'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' width=2 name='China' [marker]='marker'></e-series>
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
        this.chartData = toolData;
        this.primaryXAxis = {
            valueType: 'DateTime'
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

## See Also

* [Format the tooltip value](./how-to/tool-tip-format/#format-the-tooltip-value)
* [Create a table in tooltip](./how-to/tool-tip-table/#create-a-table-in-tooltip)