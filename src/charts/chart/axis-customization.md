---
title: " Chart Axis Customization | Angular "

component: "Chart"

description: "Chart axis contains different customization and types like axis crossing, multiple axis, inversed axis, tick and grid, title customizations"
---

# Axis Customization

To known about axis customization, you can check on this video:

`youtube:6e5YbVZw-nI`

## Axis Crossing

An axis can be positioned in the chart area using `crossesAt` and `crossesInAxis` properties. The `crossesAt`
property specifies the values (datetime, numeric, or logarithmic) at which the axis line has to be intersected
with the vertical axis or vice-versa, and the `crossesInAxis` property specifies the axis name with which the
axis line has to be crossed.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { categoryData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = categoryData
        this.primaryXAxis = {
           valueType: 'Category',
           crossesAt : 15
        };
        this.primaryYAxis = {
          crossesAt : 5
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

## Title

You can add a title to the axis using [`title`](../api/chart/axisDirective/#title) property to provide quick
information to the user about the data plotted in the axis.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { categoryData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = categoryData;
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.primaryYAxis = {
           minimum: 0, maximum: 80,
           interval: 20, title: 'Medals',
           labelFormat: '${value}K',
           titleStyle: {
            size: '16px', color: 'grey',
            fontFamily : 'Segoe UI', fontWeight : 'bold'
           }
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

## Tick Lines Customization

You can customize the  `width`, `color` and `size` of the minor and major tick lines, using
[`majorTickLines`](../api/chart/axisModel/#majorticklines) and
[`minorTickLines`](../api/chart/axisModel/#minorticklines) properties in the axis.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { tickData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = tickData;
        this.primaryXAxis = {
            valueType: 'Category',
            majorTickLines : {
               color : 'blue',
               width : 5
            },
            minorTickLines : {
               color : 'red',
               width : 0
            }
        };
        this.primaryYAxis = {
           title: 'Temperature (Fahrenheit)',
           majorTickLines : {
              color : 'blue',
              width : 5
           },
           minorTickLines : {
              color : 'red',
              width : 0
           }
        };
        this.title = 'Temperature flow over months';
    }

}
```

{% endtab %}

## Grid Lines Customization

You can customize the `width`, `color` and `dashArray` of the minor and major grid lines,
using [`majorGridLines`](../api/chart/axisModel/#majorgridlines) and
[`minorGridLines`](../api/chart/axisModel/#minorgridlines) properties in the axis.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { tickData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = tickData;
        this.primaryXAxis = {
            valueType: 'Category',
            majorGridLines : {
               color : 'blue',
               width : 1
            },
            minorGridLines : {
               color : 'red',
               width : 0
            }
        };
        this.primaryYAxis = {
           title: 'Temperature (Fahrenheit)',
           majorGridLines : {
              color : 'blue',
              width : 1
           },
           minorGridLines : {
              color : 'red',
              width : 0
           }
        };
        this.title = 'Temperature flow over months';
    }

}
```

{% endtab %}

## Multiple Axis

In addition to primary X and Y axis, we can add n number of axis to the chart. Series can be associated with
this axis, by mapping with axis's unique name.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { multipleData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-axes>
            <e-axis rowIndex=0 name='yAxis1' opposedPosition='true' title='Temperature (Celsius)' [majorGridLines]='majorGridLines' labelFormat='{value}°C'
                   [minimum]='24' [maximum]='36' [interval]='2' [lineStyle]='lineStyle'>
            </e-axis>
        </e-axes>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Germany'></e-series>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y1' yAxisName='yAxis1' name='Japan' [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    ngOnInit(): void {
        this.chartData = multipleData;
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.marker = {
            visible: true, width: 10, height: 10, border: { width: 2, color: '#F8AB1D' }
        }
        this.title = 'Weather Condition';
    }

}
```

{% endtab %}

## Inversed Axis

<!-- markdownlint-disable MD033 -->

When an axis is inversed, highest value of the axis comes closer to origin and vice versa. To place an axis in inversed manner set this property
 [`isInversed`](../api/chart/axisModel/#isinversed) to true.

 {% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { inverseData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
     `<ejs-chart id="chart-container" [title]='title' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
         [legendSettings]='legend'>
            <e-series-collection>
                <e-series [dataSource]='data' type='Column' xName='x' yName='y' name='Years' [marker]='marker'>
                </e-series>
           </e-series-collection>
       </ejs-chart>`
       })

 export class AppComponent {
    public primaryXAxis: Object;
    public primaryYAxis: Object;
    public data: Object[];
    public title: string

    ngOnInit(): void {
    this.primaryYAxis = {
        isInversed: true
    };
    this.data= inverseData;
    this.title= 'Exchange Rate';
    }

}

```

{% endtab %}

## Opposed Position

<!-- markdownlint-disable MD012 -->
To place an axis opposite from its original position, set [`opposedPosition`](../api/chart/axisModel/#opposedposition)
property of the axis to true.
<!-- markdownlint-disable MD012 -->

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { tickData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = tickData;
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.primaryYAxis = {
           title: 'Temperature (Fahrenheit)',
           opposedPosition: true
        };
        this.title = 'Temperature flow over months';
    }

}
```

{% endtab %}


