---
title: "Accumulation Chart Customization | Angular "

component: "AccumulationChart"

description: "Accumulation charts provides option to customize radius, datalabel template, angles, explode, legend, annotation"
---

<!-- markdownlint-disable MD036 -->

# Customization

**Radius customization**

By default, radius of the pie series will be 80 % of the size (minimum of height and width of the chart).
You can customize this, by using [`radius`](../api/accumulation-chart/accumulationSeries/#radius) property of the
series.

{% tab template="chart/series/radius", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' radius="100%"></e-accumulation-series>
        </e-accumulation-series-collection>
    </ej-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    ngOnInit(): void {
        this.piedata = [
                { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
                { x: 'Mar', y: 7, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
                { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
                { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: 25, text: 'Aug: 25' },
                { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' }];
    }

}
```

{% endtab %}

**Doughnut Series**

In order, to achieve a doughnut in pie, you need to customize the
[`innerRadius`](../api/accumulation-chart/accumulationSeries/#innerradius) property of the series. By default, the
value is 0%.  By setting value greater than 0%, a doughnut will appear. `innerRadius` property takes value
from 0% to 100% of the pie radius.

{% tab template="chart/series/doughnut", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' innerRadius='40%'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ej-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    ngOnInit(): void {
        this.piedata = [
                { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
                { x: 'Mar', y: 7, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
                { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
                { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: 25, text: 'Aug: 25' },
                { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' }];
    }

}
```

{% endtab %}

**Smart Labels**

As like in chart, you can also enable labels for the points in accumulation chart using
[`dataLabel`](../api/accumulation-chart/accumulationSeries/#datalabel) property in series. This label will arrange smartly
without overlapping with each other. You can enable or disable this feature using
[`enableSmartLabels`](../api/accumulation-chart/accumulationChartModel/#enablesmartlabels)property.

{% tab template="chart/series/smartlabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-accumulationchart id="chart-container" [enableSmartLabels]='enableSmartLabels'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ej-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public datalabel: Object;
    public enableSmartLabels: boolean;
    ngOnInit(): void {
        this.datalabel = { visible: true, name: 'text', position: 'Outside' };
        this.enableSmartLabels = true;
        this.piedata = [
                { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
                { x: 'Mar', y: 7, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
                { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
                { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: 25, text: 'Aug: 25' },
                { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' }];
    }

}
```

{% endtab %}

## Datalabel template

As like in chart, you can use datalabel template for the points in accumulation chart using
[`dataLabel`](../api/accumulation-chart/accumulationSeries/#datalabel) property in series.

{% tab template="chart/series/smartlabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-accumulationchart id="chart-container" [enableSmartLabels]='enableSmartLabels'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ej-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public datalabel: Object;
    public enableSmartLabels: boolean;
    ngOnInit(): void {
        this.datalabel = { visible: true, name: 'text', position: 'Outside', template: '<div>${point.x}</div><div>${point.y}</div>' };
        this.enableSmartLabels = true;
        this.piedata = [
                { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
                { x: 'Mar', y: 7, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
                { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
                { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: 25, text: 'Aug: 25' },
                { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' }];
    }

}
```

{% endtab %}

## Grouping

You can club/group few points of the series based on
[`groupTo`](../api/accumulation-chart/accumulationSeries/#groupto) property. For example, if the club
value is 11, then the points with value less than 11 is grouped together and will be showed as a single
point with label `others`.  You can customize the label for that point using
[`textRender`](../api/accumulation-chart/accumulationChartModel/#textrender) event. The
 property also takes value in percentage (percentage of total data points value).

{% tab template="chart/series/clubpoint", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IAccTextRenderEventArgs, IAccPointRenderEventArgs } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template:
    `<ej-accumulationchart id="chart-container" (textRender)="onTextRender($event)" (pointRender)="onPointRender($event)">
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' groupTo='11' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ej-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public datalabel: Object;
    public onTextRender: Function;
    public onPointRender: Function;
    ngOnInit(): void {
        this.datalabel = { visible: true, name: 'text', position: 'Outside' };
        this.onTextRender = (args: IAccTextRenderEventArgs): void {
            if (args.text.indexOf('Others') > -1) {
                args.color = 'red';
                args.border.width = 1;
            }
        }
        this.onPointRender = (args: IAccPointRenderEventArgs): void {
            if ((args.point.x as string).indexOf('Others') > -1) {
                args.fill = '#D3D3D3';
            }
        }
        this.piedata = [
                { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
                { x: 'Mar', y: 7, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
                { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
                { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: 25, text: 'Aug: 25' },
                { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' }];
    }

}
```

{% endtab %}

**Start and End angles**

You can customize the start and end angle of the pie series using
[`startAngle`](../api/accumulation-chart/accumulationSeries/#startangle) and
[`endAngle`](../api/accumulation-chart/accumulationSeries/#endangle) properties. By default, `startAngle` is 0
degree and `endAngle` is 360 degree. By customizing this, we can achieve a semi pie series.

{% tab template="chart/series/startangle", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' [startAngle]='startAngle' [endAngle]='endAngle' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ej-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public startAngle: number;
    public endAngle: number;
    public datalabel: Object;
    ngOnInit(): void {
        this.startAngle = 270;
        this.endAngle = 90;
        this.datalabel = { visible: true, name: 'text', position: 'Outside' };
        this.piedata = [
                { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
                { x: 'Mar', y: 7, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
                { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
                { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: 25, text: 'Aug: 25' },
                { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' }];
    }

}
```

{% endtab %}

**Explode**

By setting [`explode`](../api/accumulation-chart/accumulationSeries/#explode) property to true, you can explode a point in series on mouse click.
Points can also be exploded on load, by using
[`explodeIndex`](../api/accumulation-chart/accumulationSeries/#explodeindex),[`explodeOffset`](../api/accumulation-chart/accumulationSeries/#explodeoffset) and
[`explodeAll`](../api/accumulation-chart/accumulationSeries/#explodeall) property.
`explodeIndex` takes the value of the point index to be exploded, while `explodeAll` property takes the value in boolean,
when it’s true, all the points will be exploded on initial render itself.
`explodeOffset` property specifies the distance about which the slice has to be moved, when it is exploded.

{% tab template="chart/series/explode", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' [explode]='explode'
            [explodeIndex]='explodeIndex'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ej-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public explode: boolean;
    public explodeIndex: number;
    ngOnInit(): void {
        this.explode = true;
        this.explodeIndex = 4;
        this.explodeOffset = '30px';
        this.piedata = [
                { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
                { x: 'Mar', y: 7, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
                { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
                { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: 25, text: 'Aug: 25' },
                { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' }];
    }

}
```

{% endtab %}

**Legend**

  As like chart, legend is also available for accumulation, which gives information about the points. But
  by default, the legend will be placed on right hand side, if the width of the chart is high or will be
  placed on the bottom, if the height of the chart is high. Other customization regarding the legend
  element are same as
  [`chart legend`](http://ej2.syncfusion.com/documentation/chart/legend.html#position-and-alignment).
  Here legend for a point can be collapsed by giving empty string to the x value of the point.

{% tab template="chart/series/legend", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-accumulationchart id="chart-container" [legendSettings]='legendSettings'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ej-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    ngOnInit(): void {
        this.legendSettings = {
            position: 'Right',
            visible: true,
            height: '40',
            width: '160'
        };
        this.piedata = [
                { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
                { x: 'Mar', y: 7, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
                { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
                { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: 25, text: 'Aug: 25' },
                { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' },
                { x: 'Nov', y: 9, text: 'Nov: 9' }, { x: 'Dec', y: 3.5, text: 'Dec: 3.5' }];
    }

}
```

{% endtab %}

## Annotation

Annotations are used to mark the specific area of interest in the chart area with texts, shapes or images.

<!-- markdownlint-disable MD033 -->

You can add annotations to the chart by using the <code>annotations</code> option.
By using the <code>content</code> option of annotation object,
you can specify the id of the element that needs to be displayed in the chart area.

{% tab template="chart/series/accumulationAnnotation", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-accumulationchart id="chart-container">
        <e-accumulation-annotations>
            <e-accumulation-annotation content='Feb-3.5' region='Series' coordinateUnits='Point' x='Feb' y=3.5>
            </e-accumulation-annotation>
        </e-accumulation-annotations>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ej-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    ngOnInit(): void {
        this.piedata = [
                { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
                { x: 'Mar', y: 7, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
                { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
                { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: 25, text: 'Aug: 25' },
                { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' },
                { x: 'Nov', y: 9, text: 'Nov: 9' }, { x: 'Dec', y: 3.5, text: 'Dec: 3.5' }];
    }

}
```

{% endtab %}

>Note: To use annotation feature in accumulation chart, we need to inject `AccumulationAnnotationService` into the `@NgModule.providers`.

## Empty Points

The Data points that uses the null or undefined as value are considered as empty points.
Empty data points are ignored and not plotted in the Chart. You can customize those points, using `emptyPointSettings` property in series.
Default mode of the empty point is Gap. Others mode supported here are 'Average' and 'Zero'.

{% tab template="chart/series/radius", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' radius="100%"></e-accumulation-series>
        </e-accumulation-series-collection>
    </ej-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    ngOnInit(): void {
        this.piedata = [
                { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
                { x: 'Mar', y: null, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
                { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
                { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: undefined, text: 'Aug: 25' },
                { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' }];
    }

}
```

{% endtab %}

**Customizing empty point**

Specific color for empty point can be set by `fill` property in `emptyPointSettings`. Border for a empty point can be set by
`border` property.

{% tab template="chart/series/radius", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' [emptyPointSettings]='empty'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ej-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    ngOnInit(): void {
        this.piedata = [
                { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
                { x: 'Mar', y: null, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
                { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
                { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: undefined, text: 'Aug: 25' },
                { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' }];
        this.empty = {
            mode: 'Average', fill: 'pink', border: { width: 2, color: 'black'}
        }
    }

}
```

{% endtab %}