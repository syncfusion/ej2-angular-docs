---
title: "Pie and Doughnut | Angular "

component: "Accumulation Chart"

description: "Pie and doughnut charts are used to presents the relationship of different parts of data and also known biggest data easily"
---

# Pie & Doughnut

## Pie Chart

To render a pie series, use the series [`type`](../api/accumulation-chart/accumulationSeriesModel/#type) as `Pie` and
inject the `PieSeriesService` module  into the `@NgModule.providers`. If the `PieSeries` module is not
injected, this module will be loaded by default.

To known about circular and triangular charts, you can check on this video:

`youtube:ckgEx9oNUXw`

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' type='Pie'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    ngOnInit(): void {
        this.piedata = pieData;
        this.legendSettings = {
            visible: false
        };
    }

}
```

{% endtab %}

## Radius Customization

By default, radius of the pie series will be 80% of the size (minimum of chart width and height).
You can customize this using [`radius`](../api/accumulation-chart/accumulationSeries/#radius) property of the series.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' radius="100%"></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    ngOnInit(): void {
        this.piedata = pieData;
        this.legendSettings = {
            visible: false
        };
    }

}
```

{% endtab %}

## Pie Center

The center position of the pie can be changed by Center X and Center Y. By default, center value of the pie series x and y is 50%. You can customize this using [`center`](../api/accumulation-chart/accumulationChartModel/#center) property of the series.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="container" width='92%' [legendSettings]="legendSettings" [title]="title" [enableAnimation]= 'enableAnimation' [center]='center'>
            <e-accumulation-series-collection>
                <e-accumulation-series name='Browser' [dataSource]='pieData' xName='x' yName='y' [startAngle]="startAngle" [endAngle]="endAngle" innerRadius="0%" radius="70%" [explode]='explode' explodeOffset='10%' [explodeIndex]='0'>
                </e-accumulation-series>
            </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public pieData: Object[];
    public startAngle: number;
    public endAngle: number;
    public center: Object ;
    public explode: boolean ;
    public enableAnimation: boolean ;
    public title: string ;
    public legendSettings: Object;
    ngOnInit(): void {
    this.pieData = data;
        this.legendSettings = {
            visible: false
        };
    this.center = {x: '60%', y: '60%'};
    this.startAngle = 0;
    this.endAngle = 360;
    this.explode = true;
    this.enableAnimation = false;
    this.title = 'Mobile Browser Statistics';
    }

}
```

{% endtab %}

## Various Radius Pie Chart

You can use radius mapping to render the slice with different [`radius`](../api/accumulation-chart/accumulationSeries/#radius) pie and also use [`border`](../api/accumulation-chart/accumulationSeries/#border) , fill properties to customize the point. dataLabel is used to represent individual data and its value.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { variespiedata } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="container" width='92%' [legendSettings]="legendSettings" [title]="title" [enableAnimation]= 'enableAnimation'>
            <e-accumulation-series-collection>
                <e-accumulation-series name='Browser' [dataSource]='pieData' xName='x' yName='y' [startAngle]="startAngle" [endAngle]="endAngle" innerRadius="20%" radius="r">
                </e-accumulation-series>
            </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public pieData: Object[];
    public startAngle: number;
    public endAngle: number;
    public center: Object ;
    public explode: boolean ;
    public enableAnimation: boolean ;
    public title: string ;
    public radius: string ;
    public legendSettings: Object;
    ngOnInit(): void {
    this.pieData = variespiedata;
        this.legendSettings = {
            visible: false
        };
    this.startAngle = 0;
    this.endAngle = 360;
    this.radius = 'r';
    this.enableAnimation = true;
    this.title = 'Mobile Browser Statistics';
    }

}
```

{% endtab %}

## Doughnut Chart

To achieve a doughnut in pie series, customize the [`innerRadius`](../api/accumulation-chart/accumulationSeries/#innerradius)
property of the series. By setting value greater than 0%, a doughnut will appear. The `innerRadius` property takes value from 0% to 100%
of the pie radius.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' innerRadius='40%'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    ngOnInit(): void {
        this.piedata = pieData;
         this.legendSettings = {
            visible: false
        };
    }

}
```

{% endtab %}

## Start and End angles

You can customize the start and end angle of the pie series using the
[`startAngle`](../api/accumulation-chart/accumulationSeries/#startangle) and
[`endAngle`](../api/accumulation-chart/accumulationSeries/#endangle) properties. The default value of  `startAngle` is 0 degree,
 and `endAngle` is 360 degrees. By customizing this, you can achieve a semi pie series.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' [startAngle]='startAngle' [endAngle]='endAngle' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public startAngle: number;
    public endAngle: number;
    public datalabel: Object;
    public legendSettings: Object;
    ngOnInit(): void {
        this.startAngle = 270;
        this.endAngle = 90;
        this.datalabel = { visible: true, name: 'text', position: 'Outside' };
        this.piedata = pieData;
         this.legendSettings = {
            visible: false
        };
    }

}
```

{% endtab %}

## Color & Text Mapping

The fill color and the text in the data source can be mapped to the chart using `pointColorMapping` in series and
`name` in datalabel respectively.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { dataMapping } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' [pointColorMapping]= 'map' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public map: Object = 'fill';
    public datalabel: Object;
    public legendSettings: Object;
    ngOnInit(): void {
        this.piedata = dataMapping;
        this.datalabel = { visible: true, name: 'text', position: 'Outside' };
        this.legendSettings = {
            visible: false
        };
    }

}
```

{% endtab %}

## Hide pie or doughnut border

By default, the border will appear in the pie/doughnut chart while mouse hover on the chart. You can disable the the border by
setting `enableBorderOnMouseMove` property is `false`.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { dataMapping } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings' [enableBorderOnMouseMove]='enableBorderOnMouseMove'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public datalabel: Object;
    public legendSettings: Object;
    public enableBorderOnMouseMove: boolean;
    ngOnInit(): void {
        this.enableBorderOnMouseMove = false;
        this.piedata = dataMapping;
        this.datalabel = { visible: true, name: 'text', position: 'Outside' };
        this.legendSettings = {
            visible: false
        };
    }

}
```

{% endtab %}