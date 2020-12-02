---
title: " RangeNavigator Series Types | Angular "

component: "RangeNavigator"

description: "Essential JS 2 Range navigator supports 3 types of series, to render the data."
---

# Series Types

Essential JS 2 Range navigator supports 3 types of series, to render the data.

<!-- markdownlint-disable MD036 -->

## Line

<!-- markdownlint-disable MD036 -->

To render a line series, set the series `type` to `Line`, and inject the `LineSeriesService` into the `@NgModule.providers`.

{% tab template="rangenavigator/series-types/line", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Line' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    public tooltip: Object[];
    public labelFormat: string;
    ngOnInit(): void {
        this.value = [new Date('2017-09-01'), new Date('2018-02-01')];
        this.chartData = datasrc;
        this.labelFormat = 'MMM-yy';
    }
}

```

{% endtab %}

## Area

To render a step line series, use series `type` as `Area` and inject `AreaSeriesService` into the `@NgModule.providers`.

{% tab template="rangenavigator/series-types/area", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    public tooltip: Object[];
    public labelFormat: string;
    ngOnInit(): void {
        this.value = [new Date('2017-09-01'), new Date('2018-02-01')];
        this.chartData = datasrc;
        this.labelFormat = 'MMM-yy';
    }
}

```

{% endtab %}

## StepLine

To render a step line series, use series `type` as `StepLine` and
inject `StepLineSeries` into the `@NgModule.providers`.

{% tab template="rangenavigator/series-types/stepline", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" [value]='value'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    public tooltip: Object[];
    public labelFormat: string;
    ngOnInit(): void {
        this.value = [12,30];
        this.chartData = datasrc;
        this.labelFormat = 'MMM-yy';
    }
}

```

{% endtab %}
