---
title: " Chart Print and Export | Angular "

component: "Chart"

description: "The rendered chart can be printed or exported directly from the browser by calling the public method print and export."
---

# Print and Export

## Print

The rendered chart can be printed directly from the browser by calling the public method print.
You can pass array of ID of elements or element to this method. By default it take element of the chart.

{% tab template= "chart/series/polar" , sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';

@Component({
    selector: 'app-container',
    template:
    `<div class="col-md-8">
    <button ej-button id='print' (click)='print()'>Print</button>
    <ejs-chart #chart id='chart-container' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='Radar' xName='x' yName='y' drawType='Line'> </e-series>
            </e-series-collection>
    </ejs-chart>
    </div> `
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];
    @ViewChild('chart')
    public chartObj: ChartComponent;

    ngOnInit(): void {
        this.data = [{ x: 2005, y: 28 }, { x: 2006, y: 25 },{ x: 2007, y: 26 }, { x: 2008, y: 27 },
                     { x: 2009, y: 32 }, { x: 2010, y: 35 }, { x: 2011, y: 30 }];
        this.primaryXAxis = {
            title: 'Year', coefficient: 90,
            minimum: 2004, maximum: 2012, interval: 1
            };
        this.primaryYAxis = {
            minimum: 20, maximum: 40, interval: 5,
            title: 'Efficiency',
            labelFormat: '{value}%'
            };

        this.title = 'Efficiency of oil-fired power production';
    }
     print() {
        this.chartObj.print();
    }
}

```

{% endtab %}

## Export

The rendered chart can be exported to `JPEG`, `PNG`, `SVG`, or `PDF` format using the export method in chart. The input parameters for this method are `Export Type` for format and `fileName` for result.

The optional parameters for this method are,
* `orientation` - either portrait or landscape,
* `controls` - pass collections of controls for multiple export,
* `width` - width of chart export, and
* `height` - height of chart export.

{% tab template= "chart/series/polar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<div class="col-md-8">
    <ejs-chart id='chart-container'  [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis' (loaded)='loaded($event)'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='Radar' xName='x' yName='y' drawType='Line'> </e-series>
            </e-series-collection>
    </ejs-chart>
    </div> `
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];
    public loaded;

    ngOnInit(): void {
        this.data = [{ x: 2005, y: 28 }, { x: 2006, y: 25 },{ x: 2007, y: 26 }, { x: 2008, y: 27 },
                     { x: 2009, y: 32 }, { x: 2010, y: 35 }, { x: 2011, y: 30 }];
        this.primaryXAxis = {
            title: 'Year', coefficient: 90,
            minimum: 2004, maximum: 2012, interval: 1
            };
        this.primaryYAxis = {
            minimum: 20, maximum: 40, interval: 5,
            title: 'Efficiency',
            labelFormat: '{value}%'
            };

        this.title = 'Efficiency of oil-fired power production';
        this.loaded = (args: ILoadedEventArgs): void {
                args.chart.exportModule.export('PNG', 'export');
        }
    }
}

```

{% endtab %}

## Multiple Chart Export

You can export the multiple charts in single page by passing the multiple chart objects in the export
method of chart.

To export multiple charts in a single page, follow the given steps:

**Step 1**:

Initially, render more than one chart to export, and then add button to export the multiple charts. In
button click, call the export private method in charts, and then pass the multiple chart objects in the
export method.

{% tab template= "chart/add-series", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { ChartComponent } from '@syncfusion/ej2-angular-charts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart #chart id='chartcontainer'
            [title]='title' (loaded)='loaded($event)'>
            <e-series-collection>
                <e-series [dataSource]='data' type='Column' xName='x' yName='y' > </e-series>
            </e-series-collection>
    </ejs-chart>
    <ejs-chart #chart1 id='chartcontainer1'
            [title]='title'>
            <e-series-collection>
                <e-series [dataSource]='data1' type='Column' xName='x' yName='y' > </e-series>
            </e-series-collection>
    </ejs-chart>
    <button ej-button id='print' (click)='export()'>Export</button>`
})
export class AppComponent implements OnInit {
    public title: string;
    public data: Object[];
    public data1: Object[];
    @ViewChild('chart')
    public chart: ChartComponent;
    @ViewChild('chart1')
    public chart1: ChartComponent;
    ngOnInit(): void {
        this.data =  [
              { x: 1, y: 20 }, { x: 2, y: 5 },
              { x: 3, y: 10 }, { x: 4, y: 40 }
              ];
        this.data1 =  [
              { x: 1, y: 20 }, { x: 2, y: 5 },
              { x: 3, y: 10 }, { x: 4, y: 40 }
              ];
        this.title = 'Chart 1';
    }
     export() {
         this.chart.exportModule.export('PNG', 'chart','Landscape',[this.chart, this.chart1]);
    }
}
```

{% endtab %}