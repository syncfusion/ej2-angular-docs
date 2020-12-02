---
title: " stockchart Tooltip | Angular "

component: "stockchart"

description: "Tooltip is used to show the data value when mouse hover on the stockchart.We can able to customize format,template and appearance."
---

# Tooltip

<!-- markdownlint-disable MD036 -->

stockchart will display details about the points through tooltip, when the mouse is moved over the point.

## Default Tooltip

By default, tooltip is not visible. Enable the tooltip by setting
[`enable`](../api/chart/tooltipSettingsModel/) property to true and by injecting `TooltipService`
into the `NgModule.providers`.

{% tab template="stock-chart/tooltip", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [tooltip]='tooltip'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='chartData' type='Spline' xName='date' yName='open' width=2 name='China' [marker]='marker'></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public marker: Object;
    public tooltip: Object;
    ngOnInit(): void {
        this.chartData = chartData;
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

{% tab template="stock-chart/tooltip", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [tooltip]='tooltip'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='chartData' type='Spline' xName='date' yName='open' width=2 name='China' [marker]='marker'></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    public tooltip: Object;
    ngOnInit(): void {
        this.chartData = chartData;
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

## Tooltip Template

Any HTML elements can be displayed in the tooltip by using the ‘template’ property of the tooltip. You can use the ${x} and ${y} as place holders in the HTML element to display the x and y values of the corresponding data point.

{% tab template="stock-chart/tooltip", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [tooltip]='tooltip'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='chartData' type='Spline' xName='date' yName='open' width=2 name='China' [marker]='marker'></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public marker: Object;
    public tooltip: Object;
    ngOnInit(): void {
        this.chartData = chartData;
        this.primaryXAxis = {
            valueType: 'DateTime'
        };
        this.tooltip = { enable: true, template: '#Unemployment' };
        this.marker = { visible: true, width: 10, height: 10 };
        this.title = 'Unemployment Rates 1975-2010';

}
```

{% endtab %}

## Customize the Appearance of Tooltip

The [`fill`](../api/chart/tooltipSettingsModel/#fill) and [`border`](../api/chart/tooltipSettingsModel/#border) properties are used to customize the background color and border of the tooltip respectively. The [`textStyle`](../api/chart/tooltipSettingsModel/#textstyle) property in the tooltip is used to customize the font of the tooltip text.

{% tab template="stock-chart/tooltip", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [tooltip]='tooltip'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='chartData' type='Spline' xName='date' yName='open' width=2 name='China' [marker]='marker'></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public marker: Object;
    public tooltip: Object;
    ngOnInit(): void {
        this.chartData = chartData;
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
