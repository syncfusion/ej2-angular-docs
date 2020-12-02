---
title: "Funnel | Angular "

component: "Accumulation Chart"

description: "The funnel chart displays series value as progressively decreasing amount to hundred percent in total"
---

# Funnel Chart

To render a funnel series, use the series [`type`](../api/accumulation-chart/accumulationSeries/#type) as `Funnel` and
inject, the `FunnelSeries` module  into the `@NgModule.providers`.

To known about funnel charts, you can check on this video:

`youtube:ckgEx9oNUXw`

{% tab template="chart/series/funnel", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { funnelData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series width='330px' type='Funnel' [dataSource]='funneldata' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public funneldata: Object[];
    ngOnInit(): void {
        this.funneldata = funnelData;
    }

}

```

{% endtab %}

## Size

The size of the funnel chart can be customized by using the  `width` and `height` properties.

{% tab template="chart/series/funnel", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { funnelData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series  width='60%'  height='80%' type='Funnel' [dataSource]='funneldata' xName='x' yName='y' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public funneldata: Object[];
    ngOnInit(): void {
        this.datalabel = { visible: true, name: 'text', position: 'Inside' };
        this.funneldata = funnelData;
    }

}

```

{% endtab %}

## Neck Size

The funnel's neck size can be customized by using the `neckWidth` and `neckHeight` properties.

{% tab template="chart/series/funnel", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { funnelData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series type='Funnel' [dataSource]='funneldata' xName='x' yName='y' [dataLabel]='datalabel' [neckWidth]='neckWidth'
             [neckHeight]='neckHeight'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public funneldata: Object[];
    public neckWidth: string = '25%';
    public neckHeight:'5%'
    ngOnInit(): void {
        this.funneldata = funnelData;
    }

}

```

{% endtab %}

## Gap between the segments

Funnel chart provides options to customize the space between the segments by using the `gapRatio` property of the
series. It ranges from 0 to 1.

{% tab template="chart/series/funnel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { funnelData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series  type='Funnel' [dataSource]='funneldata' xName='x' yName='y' [dataLabel]='datalabel' [gapRatio]="gapRatio"></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public funneldata: Object[];
    public gapRatio: number = 0.08;
    ngOnInit(): void {
        this.funneldata = funnelData;
    }

}

```

{% endtab %}

## Explode

Points can be exploded on mouse click by setting the `explode` property to true. You can also explode the point
on load using `explodeIndex`. Explode distance can be set by using `explodeOffset` property.

{% tab template="chart/series/funnel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { funnelData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series  type='Funnel'[dataSource]='funnelData' xName='x' yName='y' [explode]='explode' [explodeAll]='explodeAll'
            [explodeIndex]='explodeIndex'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public funnelData: Object[];
    public explode: boolean;
    public explodeIndex: number;
    public explodeAll: boolean;
    ngOnInit(): void {
        this.explode = true;
        this.explodeIndex = 3;
        this.explodeOffset = '30px';
        this.explodeAll = false;
        this.funnelData = funnelData;
    }

}
```

{% endtab %}

## Smart Data Label

It provides the data label smart arrangement of the funnel and pyramid series. The overlap data label will be placed on left side of the funnel/pyramid series.

{% tab template="chart/series/funnel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { funnelDataSource } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]="legendSettings" [tooltip]="tooltip" title="Top population countries in the world 2017">
        <e-accumulation-series-collection>
            <e-accumulation-series  type='Funnel' [dataSource]='funnelData' xName='x' yName='y' neckWidth='15%'
            neckHeight='18%' [dataLabel]='dataLabel' name="2017 Population" explode="false"></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public funnelData: Object[];
    public dataLabel: Object;
    public legendSettings: Object;
    public tooltip: Object;
    ngOnInit(): void {
        this.funnelData = funnelDataSource;
        this.dataLabel = {
            visible: true, position: 'Outside',
            connectorStyle: { length: '6%' }, name: 'text',
        };
        this.legendSettings = {visible = false};
        this.tooltip = {
            enable: true, format: '${point.x} : <b>${point.y}</b>'
        };
    }
}

```

{% endtab %}

## Customization

Individual points can be customized using the `pointRender` event.

{% tab template="chart/series/funnel", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { funnelData } from 'datasource.ts';
import { IAccTextRenderEventArgs, IAccPointRenderEventArgs } from '@syncfusion/ej2-charts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" (pointRender)="onPointRender($event)">
        <e-accumulation-series-collection>
            <e-accumulation-series  type='Funnel' [dataSource]='funneldata' xName='x' yName='y' [dataLabel]='datalabel' [gapRatio]="gapRatio"
             ></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public funneldata: Object[];
    public gapRatio: number = 0.08;
    public onPointRender: Function;
    ngOnInit(): void {
        this.onPointRender = (args: IAccPointRenderEventArgs): void {
            if ((args.point.x as string).indexOf('Downloaded') > -1) {
                args.fill = '#D3D3D3';
            }
            else {
            args.fill = '#597cf9';
        }
        }
        this.funneldata = funnelData;
    }

}

```

{% endtab %}

## See Also

* [Data label](./data-label/)
* [Grouping](./grouping/)