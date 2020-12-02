---
title: "Pyramid | Angular "

component: "Accumulation Chart"

description: "The pyramid chart displays series value as progressively decreasing amount to hundred percent in total"
---

# Pyramid Chart

To render a pyramid series, use the series [`type`](../api/accumulation-chart/accumulationSeriesModel/#type) as `Pyramid` and
inject `PyramidSeries` module into the `@NgModule.providers`.

To known about pyramid, you can check on this video:

`youtube:ckgEx9oNUXw`

{% tab template="chart/series/pyramid", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { pyramidData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series type='Pyramid' [dataSource]='pyramidData' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public pyramidData: Object[];
    public enableSmartLabels: boolean;
    ngOnInit(): void {
        this.pyramidData = pyramidData;
    }

}

```

{% endtab %}

## Mode

The Pyramid chart supports linear and surface modes of rendering. The default type of the
`pyramidMode` is `linear`.

{% tab template="chart/series/pyramid", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { pyramidData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series type='Pyramid' pyramidMode='Surface' [dataSource]='pyramidData' xName='x' yName='y' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public pyramidData: Object[];
    ngOnInit(): void {
        this.pyramidData = pyramidData;
    }
}

```

{% endtab %}

## Size

The size of the pyramid chart can be customized by using the  `width` and `height` properties.

{% tab template="chart/series/pyramid", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { pyramidData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series width='60%' height='80%' type='Pyramid' [dataSource]='pyramidData' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public pyramidData: Object[];
    ngOnInit(): void {
        this.pyramidData = pyramidData;
    }

}

```

{% endtab %}

## Gap Between the Segments

Pyramid chart provides options to customize the space between the segments by using the `gapRatio` property of the
series. It ranges from 0 to 1.

{% tab template="chart/series/pyramid", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { pyramidData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series  type='Pyramid' [dataSource]='pyramidData' xName='x' yName='y' [gapRatio]="gapRatio"></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public pyramidData: Object[];
    public gapRatio: number = 0.2;
    ngOnInit(): void {
        this.pyramidData = pyramidData;
    }

}

```

{% endtab %}

## Explode

Points can be exploded on mouse click by setting the `explode` property to true. You can also explode the point
on load using `explodeIndex`. Explode distance can be set by using `explodeOffset` property.

{% tab template="chart/series/pyramid", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pyramidData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series type='Pyramid' [dataSource]='pyramidData' xName='x' yName='y' [explode]='explode' [explodeAll]='explodeAll'
            [explodeIndex]='explodeIndex'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public pyramidData: Object[];
    public explode: boolean;
    public explodeIndex: number;
    public explodeAll: boolean;
    ngOnInit(): void {
        this.explode = true;
        this.explodeIndex = 3;
        this.explodeOffset = '30px';
        this.explodeAll = false;
        this.pyramidData = pyramidData;
    }

}

```

{% endtab %}

## Customization

Individual points can be customized using the `pointRender` event.

{% tab template="chart/series/pyramid", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pyramidData } from 'datasource.ts';
import { IAccTextRenderEventArgs, IAccPointRenderEventArgs } from '@syncfusion/ej2-charts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container"  (pointRender)="onPointRender($event)">
        <e-accumulation-series-collection>
            <e-accumulation-series  type='Pyramid' [dataSource]='pyramidData' xName='x' yName='y' [dataLabel]='datalabel' [gapRatio]="gapRatio"
            ></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public pyramidData: Object[];
    public gapRatio: number = 0.2;
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
        this.pyramidData = pyramidData;
    }

}
```

{% endtab %}