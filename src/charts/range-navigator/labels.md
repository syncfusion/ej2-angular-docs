---
title: " RangeNavigator Labels | Angular "

component: "RangeNavigator"

description: "RangeNavigator supports Multilevel label and enable grouping properties to customize axis labels."
---

# Labels

## Multilevel labels

The second level labels for the range navigator can be enabled by setting the “enableGrouping” property to true.
This is restricted to date-time axis alone.

{% tab template="rangenavigator/labels/default", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" labelPosition='Outside' valueType='DateTime' [value]='value'  intervalType='Quarter' [enableGrouping]='grouping' [dataSource]='chartData' xName='x' yName='y' tooltip='tooltip'></ejs-rangenavigator>`
})

export class AppComponent implements OnInit {
    public data: object[] = [];
    public value: number = 0;
    public point: object = {};
    public chartData: Object[];
    public value: Object[];
    public grouping: boolean;
    public tooltip: Object[];
    ngOnInit(): void {
        this.chartData =[];
        for (let j = 1; j < 1090; j++) {
            this.value += (Math.random() * 10 - 5);
            this.value = this.value < 0 ? Math.abs(this.value) : this.value;
            this.point = { x: new Date(2000, 0, j), y: this.value, z: (this.value + 10) };
            this.chartData.push(this.point);
        };
        this.value=[new Date("2001, 1,1"), new Date("2002,1,1")];
        this.grouping = true;
        this.tooltip= { enable: true };
    }
}

```

{% endtab %}

## Grouping

The second level axis labels can be grouped using “groupBy” property with the following interval types:

* Auto
* Years
* Quarter
* Months
* Weeks
* Days
* Hours
* Minutes
* Seconds

{% tab template="rangenavigator/labels/default", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" labelPosition='Outside' valueType='DateTime' [value]='value'  intervalType='Quarter' [enableGrouping]='grouping' groupBy='Years' [dataSource]='chartData' xName='x' yName='y' tooltip='tooltip'></ejs-rangenavigator>`
})

export class AppComponent implements OnInit {
    public data: object[] = [];
    public value: number = 0;
    public point: object = {};
    public chartData: Object[];
    public value: Object[];
    public grouping: boolean;
    public tooltip: Object[];
    ngOnInit(): void {
        this.chartData =[];
        for (let j = 1; j < 1090; j++) {
            this.value += (Math.random() * 10 - 5);
            this.value = this.value < 0 ? Math.abs(this.value) : this.value;
            this.point = { x: new Date(2000, 0, j), y: this.value, z: (this.value + 10) };
            this.chartData.push(this.point);
        };
        this.value=[new Date("2001, 1,1"), new Date("2002,1,1")];
        this.grouping = true;
        this.tooltip= { enable: true };
    }
}

```

{% endtab %}

## Smart labels

The “labelIntersectAction” property is used to avoid overlapping of labels.

The following code sample shows setting the labelIntersectAction property to Hide.

{% tab template="rangenavigator/axis/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value' labelIntersectAction='Hide'
    labelFormat='y/M/d'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public chartData: Object[];
    public value: Object[];
    ngOnInit(): void {
        this.chartData = datasrc;
        this.value=[new Date("2017-08-13"), new Date("2017-12-28")];
    }
}

```

{% endtab %}

## Label positioning

By default, the labels can be placed at outside of the range navigator. You can place the labels inside the range navigator
using the labelPosition property.

{% tab template="rangenavigator/axis/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value' labelPosition='Inside'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public chartData: Object[];
    public value: Object[];
    ngOnInit(): void {
        this.chartData = datasrc;
        this.value=[new Date("2017-08-13"), new Date("2017-12-28")];
    }
}

```

{% endtab %}

## Labels customization

The font size, color, family, etc. can be customized using the “labelStyle” property.

{% tab template="rangenavigator/lightweight/default", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { GetDateTimeData } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value' intervalType='Months'[labelFormat]='labelFormat' [labelStyle]='labelStyle' [dataSource]='chartData' xName='x' yName='y'></ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    public tooltip: Object[];
    public labelFormat: string;
    ngOnInit(): void {
        this.value = [new Date(2018, 5, 1), new Date(2018, 6, 1)];
        this.chartData = GetDateTimeData(new Date(2018, 0, 1), new Date(2019, 0, 1));
        this.labelFormat = 'MMM';
        this.labelStyle= { color: 'red', size:'10px'};
    }
}

```

{% endtab %}
