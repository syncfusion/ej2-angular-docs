---
title: " RangeNavigator Customization | Angular "

component: "RangeNavigator"

description: "Range navigator can be customized using the navigatorBorder, navigatorStyleSettings, seleced or unselected region color properties."
---

# Customization

## Navigator appearance

The navigator can be customized using the `navigatorStyleSettings` property. The `selectedRegionColor` property is used to specify the color for selected region whereas the `unSelectedRegionColor` property is used to specify the color for unselected region.

{% tab template="rangenavigator/getting-started/default", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value' [navigatorStyleSettings]='navigatorStyle' labelFormat='MMM-yy'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    public navigatorStyle: Object;
    ngOnInit(): void {
        this.value = [new Date('2017-09-01'), new Date('2018-02-01')];
        this.chartData = datasrc;
        this.navigatorStyle = {  unselectedRegionColor: 'skyblue', selectedRegionColor: 'pink' };
    }
}

```

{% endtab %}

## Thumb

The thumb property provides options to customize the border, fill, size, and type of thumb. The types of thumb can be `Circle` and `Rectangle`.

{% tab template="rangenavigator/getting-started/default", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value' [navigatorStyleSettings]='navigatorStyle' labelFormat='MMM-yy'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    public navigatorStyle: Object;
    ngOnInit(): void {
        this.value = [new Date('2017-09-01'), new Date('2018-02-01')];
        this.chartData = datasrc;
        this.navigatorStyle = { thumb:{ type: 'Rectangle', border: { width: 2, color: 'red'}, fill: 'pink' }};

    }
}

```

{% endtab %}

## Border customization

Using the `navigatorBorder` property, you can customize the `width` and `color` of the range navigator.

{% tab template="rangenavigator/getting-started/default", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value' [navigatorBorder]='navigatorBorder' labelFormat='MMM-yy'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    public navigatorBorder: Object;
    ngOnInit(): void {
        this.value = [new Date('2017-09-01'), new Date('2018-02-01')];
        this.chartData = datasrc;
        this.navigatorBorder = {  width: 4, color: 'green'};

    }
}

```

{% endtab %}

## Deferred update

If the `enableDeferredUpdate` property is set to true, then the changed event will be fired after dragging the slider. If the `enableDeferredUpdate` is false, then the changed event will be fired when dragging the slider. By default, the `enableDeferredUpdate` is set to false.

{% tab template="rangenavigator/deferred", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { datasrc } from 'datasource.ts';
import { IChangedEventArgs }  from "@syncfusion/ej2-charts";

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value' [tooltip]='tooltip' [enableDeferredUpdate]='enableDeferredUpdate' (changed)='changed($event)'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>
          <ejs-chart #chart style='display:block;' id='chart' height='350' [primaryXAxis]='primaryXAxis' [tooltip]= 'tooltip'>
                <e-series-collection>
                    <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                    </e-series>
                </e-series-collection>`
})
export class AppComponent implements OnInit {
     @ViewChild('chart')
    public chart: Chart;
    public periodsValue: Object[];
    public chartData: Object[];
    public value: Object[];
    public tooltip: Object;
    public enableDeferredUpdate: booloean;
    public changed: IChangedEventArgs;
    public primaryXAxis: object;
    public legendSettings: object;
    ngOnInit(): void {
        this.primaryXAxis = {
            valueType: 'DateTime',
            edgeLabelPlacement: 'Shift'
        };
        this.legendSettings= { visible: false };
        this.chartData = datasrc;
        this.value=[new Date('2017-09-01'), new Date('2018-02-01')];
        this.tooltip={ enable: true };
        this.enableDeferredUpdate = true;
        this.changed = function(args) {
            this.chart.primaryXAxis.zoomFactor = args.zoomFactor;
            this.chart.primaryXAxis.zoomPosition = args.zoomPosition;
            this.chart.dataBind();

        }
    }
}

```

{% endtab %}

## Allow snapping

The `allowSnapping` property toggles the placement of the slider exactly to the left or on the nearest interval.

{% tab template="rangenavigator/getting-started/default", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value' labelFormat='MMM-yy' [allowSnapping]='allowSnapping'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    public allowSnapping: boolean;
    ngOnInit(): void {
        this.value = [new Date('2017-09-01'), new Date('2018-02-01')];
        this.chartData = datasrc;
        this.allowSnapping= true;

    }
}

```

{% endtab %}

## Animation

The speed of the animation can be controlled using the `animationDuration` property. The default value of the `animationDuration` property is 500 milliseconds.

{% tab template="rangenavigator/getting-started/default", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value' labelFormat='MMM-yy' [animationDuration]='animationDuration'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    public animationDuration: number;
    ngOnInit(): void {
        this.value = [new Date('2017-09-01'), new Date('2018-02-01')];
        this.chartData = datasrc;
        this.animationDuration=2000;

    }
}

```

{% endtab %}

## See Also

* [Grid and Tick Lines](./grid-tick/)
* [Labels](./labels/)