---
title: "Accumulation Chart Appearance | TypeScript "

component: "Accumulation Chart"

description: "We can customize chart appearance by using color palette, point level customization, chart area cutomization, title and margin customizations."
---

# Appearance

## Custom Color Palette

You can customize the default color of series or points by providing a custom color palette of your choice by
using the [`palettes`](../api/accumulation-chart/accumulationSeries/#palettes) property.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' type='Pie' [palettes]='palette'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    public palette: string[];
    ngOnInit(): void {
        this.piedata = data;
        this.legendSettings = {
            visible: false
        };
        this.palette = ["#E94649", "#F6B53F", "#6FAAB0", "#FF33F3","#228B22","#3399FF"]
    }

}
```

{% endtab %}

## Animation

### Fluid Animation

Fluid animation used to animate series with updated dataSource continues animation rather than animation whole series. You can customize animation for a particular series using [`animate`] method.

{% tab template="chart/series/radius", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild, ViewEncapsulation } from '@angular/core';
import {
    AccumulationChart, AccumulationChartComponent,
     IAccLoadedEventArgs, Selection
} from '@syncfusion/ej2-angular-charts';

@Component({
    selector: 'app-container',
    template:
      `<ejs-accumulationchart id="donut-container" #pie [title]="title"  (loaded)='loaded($event)'>
            <e-accumulation-series-collection>
                <e-accumulation-series name='Revenue' [dataSource]='data' xName='x' yName='y' [startAngle]="startAngle" [endAngle]="endAngle" innerRadius="40%" [dataLabel]="dataLabel"> </e-accumulation-series>
            </e-accumulation-series-collection>
        </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public data ,dataLabel: Object[];
    public count ;
    public startAngle: number ;
    public endAngle: number ;
    public title: string ;
    public pie: AccumulationChartComponent | AccumulationChart;
    public loaded: Function;
    ngOnInit(): void {
        this.data = [
        { 'x': 'Net-tution and Fees', y: 21, text: '21%' },
        { 'x': 'Self-supporting Operations', y: 21, text: '21%' },
        { 'x': 'Private Gifts', y: 8, text: '8%' },
        { 'x': 'All Other', y: 8, text: '8%' },
        { 'x': 'Local Revenue', y: 4, text: '4%' },
        { 'x': 'State Revenue', y: 21, text: '21%' },
        { 'x': 'Federal Revenue', y: 16, text: '16%' }
    ];
      this.dataLabel = {
        visible: true, position: 'Inside',
        name: '${point.y}',
        font: {
            color: 'white',
            fontWeight: 'Bold',
            size: '14px'
        }
    };
      this.loaded = (args: IAccLoadedEventArgs): void {
        if (this.execute) {
            return;
        }
        let pieinterval = setInterval(
            () => {
                if (document.getElementById('donut-container')) {
                    if (this.count === 0) {
                        this.pie.series[0].dataSource = [{ 'x': 'Net-tution and Fees', y: 10 },
                        { 'x': 'Self-supporting Operations', y: 10 },
                        { 'x': 'Private Gifts', y: 13 }, { 'x': 'All Other', y: 14 },
                        { 'x': 'Local Revenue', y: 9 }, { 'x': 'State Revenue', y: 13 },
                        { 'x': 'Federal Revenue', y: 8 }
                        ];
                        this.execute = true;
                        this.pie.animate();
                        this.count++;
                    } else if (this.count === 1) {
                        this.pie.series[0].dataSource = [
                            { 'x': 'Net-tution and Fees', y: 120 }, { 'x': 'Self-supporting Operations', y: 31 },
                            { 'x': 'Private Gifts', y: 6 }, { 'x': 'All Other', y: 12 },
                            { 'x': 'Local Revenue', y: 25 }, { 'x': 'State Revenue', y: 11 },
                            { 'x': 'Federal Revenue', y: 12 }
                        ];
                        this.execute = true;
                        this.pie.animate();
                        this.count++;
                    } else if (this.count === 2) {
                        this.pie.series[0].dataSource = [
                            { 'x': 'Net-tution and Fees', y: 6 }, { 'x': 'Self-supporting Operations', y: 22 },
                            { 'x': 'Private Gifts', y: 11 }, { 'x': 'All Other', y: 15 },
                            { 'x': 'Local Revenue', y: 13 }, { 'x': 'State Revenue', y: 10 },
                            { 'x': 'Federal Revenue', y: 8 }
                        ];
                        this.execute = true;
                        this.pie.animate();
                        this.count++;
                    } else if (this.count === 3) {
                        this.pie.series[0].dataSource = [
                            { 'x': 'Net-tution and Fees', y: 15 }, { 'x': 'Self-supporting Operations', y: 10 },
                            { 'x': 'Private Gifts', y: 18 }, { 'x': 'All Other', y: 20 },
                            { 'x': 'Local Revenue', y: 30 }, { 'x': 'State Revenue', y: 20 },
                            { 'x': 'Federal Revenue', y: 25 }
                        ];
                        this.execute = true;
                        this.pie.animate();
                        this.count++;
                    } else if (this.count === 4) {
                        this.pie.series[0].dataSource = [
                            { 'x': 'Net-tution and Fees', y: 21 }, { 'x': 'Self-supporting Operations', y: 10 },
                            { 'x': 'Private Gifts', y: 15 }, { 'x': 'All Other', y: 15 },
                            { 'x': 'Local Revenue', y: 11 }, { 'x': 'State Revenue', y: 20 },
                            { 'x': 'Federal Revenue', y: 60 }
                        ];
                        this.execute = true;
                        this.pie.animate();
                        this.count = 0;
                    }
                } else {
                    clearInterval(pieinterval);
                }
            },
            3000);
    }
    this.count = 0;
    this.startAngle = 0;
    this.endAngle = 360;
    this.title = 'Education Institutional Revenue';
    }
}
```

{% endtab %}
