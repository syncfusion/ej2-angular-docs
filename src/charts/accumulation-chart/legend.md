---
title: "Accumulation Chart Legend | Angular "

component: "Accumulation Chart"

description: "Accumulation chart legend is used to give additional information about the chart series."
---

# Legend

As like a chart, the legend is also available for accumulation charts, which gives information about the points.
By default, the legend will be placed on the right, if the width of the chart is high or will be placed on the bottom,
if the height of the chart is high. Other customization features regarding the legend element are same as the
[`chart legend`](http://ej2.syncfusion.com/documentation/chart/legend.html#position-and-alignment).
Here, the legend for a point can be collapsed by giving the empty string to the x value of the point.
{% tab template="chart/series/legend", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    ngOnInit(): void {
        this.legendSettings = {
            visible: true
        };
        this.piedata = pieData;
    }

}
```

{% endtab %}

## Position and Alignment

By using the position property, you can position the legend at the `left`, `right`, `top` or `bottom` of the chart.
You can also align the legend to `center`, `far` or `near` of the chart using the alignment property.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    ngOnInit(): void {
        this.legendSettings = {
           position:'Top' ,alignment:'Near'
        };
        this.piedata = pieData;
    }

}
```

{% endtab %}

## Legend Shape

To change the legend icon shape, use the `legendShape` property in the `series`. By default, legend icon shape
is `seriesType`.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'  legendShape='Rectangle'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    ngOnInit(): void {
        this.legendSettings = {
          visible: true
        };
        this.piedata = pieData;
    }

}
```

{% endtab %}

## Legend Size

The legend size can be changed by using the `width` and `height` properties of the `legendSettings`.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'  legendShape='Circle'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    ngOnInit(): void {
        this.legendSettings = {
         width: '150', height: '100', border: { width: 1, color: 'pink'}
        };
        this.piedata = pieData;
    }

}
```

{% endtab %}

## Legend Item Size

You can customize the size of the legend items by using the `shapeHeight` and `shapeWidth` properties.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'  legendShape='Circle'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    ngOnInit(): void {
        this.legendSettings = {
          shapeHeight: 15, shapeWidth: 15
        };
        this.piedata = pieData;
    }

}
```

{% endtab %}

## Enable Animation

You can customize the animation while clicking legend by setting enableAnimation as true or false using `enableAnimation` property in Accumulation Chart.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings' [enableAnimation]='enableAnimation' [enableSmartLabels]='enableSmartLabels'
    [title]='title'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' groupTo='11' [dataLabel]='datalabel' [explode]='explode' [explodeOffset]='explodeOffset'
            [startAngle]='startAngle' [endAngle]='endAngle' radius='70%'  innerRadius='40%'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    public datalabel: Object;
    public startAngle: number;
    public endAngle: number;
    public explode: boolean;
    public explodeOffset: string;
    public enableSmartLabels: boolean;
    public enableAnimation: boolean;
    public title: Object = 'Project Cost Breakdown';
    ngOnInit(): void {
        this.datalabel = {   visible: true,
                    name: 'text',
                    position: 'Inside',
                    font: {
                        fontWeight: '600',
                        color: '#ffffff'
                    }
        };
        this.legendSettings = {
            visible: true, position: 'Top'
        };
        this.startAngle = 0;
        this.endAngle = 360;
        this.explode = true;
        this.explodeOffset = '10%';
        this.enableSmartLabels = true;
        this.enableAnimation = true;
        this.piedata = [{ x: 'Labour', y: 18, text: '18%' }, { x: 'Legal', y: 8, text: '8%' },
                { x: 'Production', y: 15, text: '15%' }, { x: 'License', y: 11, text: '11%' },
                { x: 'Facilities', y: 18, text: '18%' }, { x: 'Taxes', y: 14, text: '14%' },
                { x: 'Insurance', y: 16, text: '16%' }];
    }

}
```

{% endtab %}

## Paging for Legend

Paging will be enabled by default, when the legend items exceeds the legend bounds. You can view the each legend
item by navigating between the pages using the navigation buttons.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'  legendShape='Circle'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    ngOnInit(): void {
        this.legendSettings = {
         height: '150', width:'80'
        };
        this.piedata = pieData;
    }

}
```

{% endtab %}

## Legend Title

You can set title for legend using `title` property in `legendSettings`. You can also customize the `fontStyle`, `size`, `fontWeight`,
`color`, `textAlignment`, `fontFamily`, `opacity` and `textOverflow` of legend title. `titlePosition` is used to set the legend position in `Top`, `Left` and `Right` position. `maximumTitleWidth` is used to set the width of the legend title. By default, it will be `100px`.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'  legendShape='Circle'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    ngOnInit(): void {
        this.legendSettings = {
        title: 'Months', position: 'Bottom'
        };
        this.piedata = pieData;
    }

}
```

{% endtab %}

## Arrow Page Navigation

By default, the page number will be enabled while legend paging. Now, you can disable that page number and also you can get left and right arrows for page navigation. You have to set `false` value to `enablePages` to get this support.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'  legendShape='Circle'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    ngOnInit(): void {
        this.legendSettings = {
        width: '260px', height: '50px', enablePages: false, position: 'Bottom'
        };
        this.piedata = pieData;
    }

}
```

{% endtab %}