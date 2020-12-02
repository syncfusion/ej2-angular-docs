---
title: " Accumulation Chart Print and Export | Angular "

component: "Accumulation Chart"

description: "Accumultion chart have a public methods for print or export the rendered chart"
---

# Print and Export

## Print

The rendered chart can be printed directly from the browser by calling the public method print.

{% tab template="chart/series/radius", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<div class="col-md-8">
    <button ej-button id='print' (click)='print()'>Print</button>
    <ejs-accumulationchart #chart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' radius="100%"></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>
    </div> `
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    @ViewChild('chart')
    public chartObj: ChartComponent;
    ngOnInit(): void {
        this.piedata = [
                { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
                { x: 'Mar', y: 7, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
                { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
                { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: 25, text: 'Aug: 25' },
                { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' }];
        }
        print() {
            this.chartObj.print();
       }
    }
```

{% endtab %}

## Export

The rendered chart can be exported to `Image`(jpeg or png) or `SVG` or `PDF` format by using the export method.
Input parameters for this method are `Export` Type for `format` and `fileName` of result.

{% tab template="chart/series/radius", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<div class="col-md-8">
    <ejs-accumulationchart #chart id="chart-container" (loaded)='loaded($event)'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' radius="100%"></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>
    </div> `
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public loaded;
    @ViewChild('chart');
    public chart: Chart;
    ngOnInit(): void {
        this.piedata = [
                { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
                { x: 'Mar', y: 7, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
                { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
                { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: 25, text: 'Aug: 25' },
                { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' }];
        this.loaded = (args: IAccLoadedEventArgs): void {
                args.accumulation.exportModule.export('PNG', 'export');
        }
    }
}
```

{% endtab %}