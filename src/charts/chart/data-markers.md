---
title: " Chart Marker | Angular "

component: "Chart"

description: "Data markers are used to provide information about the data points in the series. You can add a shape to adorn each data point."
---

# Data Markers

Data markers are used to provide information about the data points in the series. You can add a shape to adorn
each data point.

<!-- markdownlint-disable MD036 -->

## Marker

<!-- markdownlint-disable MD036 -->

Markers can be added to the points by enabling the [`visible`](../api/chart/markerSettingsModel/#visible)
option of the marker property.

{% tab template="chart/data-marker/marker", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { markerData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='December 2007' width=2 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    ngOnInit(): void {
        this.chartData = markerData;
        this.primaryXAxis = {
            valueType: 'Category', interval: 1,
        };
        this.marker = { visible: true };
        this.title = 'FB Penetration of Internet Audience';
    }

}
```

{% endtab %}

## Shape

Markers can be assigned with different shapes such as Rectangle, Circle, Diamond etc using the `shape`property.

{% tab template="chart/data-marker/marker", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { markerData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='December 2007' width=2 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    ngOnInit(): void {
        this.chartData = markerData;
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.marker = { visible: true, width: 10, height: 10, shape: 'Diamond' };
        this.title = 'FB Penetration of Internet Audience';
    }

}
```

{% endtab %}

>Note : To know more about the marker shape type refer the [`shape`](../api/chart/markerSettings/#shape).

## Images

Apart from the shapes, you can also add custom images to mark the data point using the
[`imageUrl`](../api/chart/markerSettingsModel/#imageurl) property.

{% tab template="chart/data-marker/marker", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { imageData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='India' width=2 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    ngOnInit(): void {
        this.chartData = imageData;
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.marker = { visible: true,
                        width: 10, height: 10, shape: 'Image',
                        imageUrl:'./sun_annotation.png'
        };
        this.title = 'Temperature flow over months';
    }

}
```

{% endtab %}

## Customization

Marker's color and border can be customized using `fill` and `border` properties.

{% tab template="chart/data-marker/marker", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { markerData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='December 2007' width=2 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    ngOnInit(): void {
        this.chartData = markerData;
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.marker = { visible: true,  fill: 'Red', height: 10, width: 10,
                    border:{width: 2, color: 'blue'} };
        this.title = 'FB Penetration of Internet Audience';
    }

}
```

{% endtab %}

## Customizing Specific Point

You can also customize the specific marker and label using
[`pointRender`](../api/chart/iPointRenderEventArgs/) event.
`pointRender` event allows you to change the shape, color and border for a point.

{% tab template="chart/data-marker/marker", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { markerData } from 'datasource.ts';
import { IPointRenderEventArgs, ITextRenderEventArgs } from '@syncfusion/ej2-angular-charts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' (pointRender)='pointRender($event)' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='December 2007' width=2 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    public pointRender(args: IPointRenderEventArgs): void {
        if(args.point.index === 3) {
                args.fill = 'red'
        }
    };
    ngOnInit(): void {
        this.chartData = markerData;
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.marker = {  visible: true,
                    height: 10, width: 10 };
        this.title = 'FB Penetration of Internet Audience';
    }

}
```

{% endtab %}

## See Also

* [Customize the marker with different shape](./how-to/marker-customization/#customize-the-marker-with-different-shape)