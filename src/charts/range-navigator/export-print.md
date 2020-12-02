---
title: " RangeNavigator Export and Print | Angular "

component: "RangeNavigator"

description: "The rendered rangenavigator can be printed or exported directly from the browser by calling the public method print and export."
---

# Export and print

## Export

The rendered range navigator can be exported to `JPEG`, `PNG`, `SVG`, or `PDF` format using the export method in the range navigator. The input parameters for this method are Export Type for format and fileName for result.

{% tab template="rangenavigator/export-print/default", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { bitCoinData } from 'datasource.ts';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';
import { RangeNavigatorComponent } from '@syncfusion/ej2-angular-charts';

@Component({
    selector: 'app-container',
    template:
    `<button ej-button id='print' (click)='export()'>Export</button>
    <ejs-rangenavigator #range id="range" valueType='DateTime' [value]='value'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    @ViewChild('range')
    public RangeObj: RangeNavigatorComponent;

    public periodsValue: Object[];
    public chartData: Object[];
    public value: Object[];
    ngOnInit(): void {
        this.chartData = bitCoinData;
        this.value=[new Date(2017, 8, 1), new Date(2018, 1, 1)];
    }
    export() {
         this.RangeObj.export('PNG', 'result',  null, [this.RangeObj]);
    }
}

```

{% endtab %}

## Print

The rendered range navigator can be printed directly from the browser by calling the public method print. The ID of the range navigator div element must be passed as argument to that method.

{% tab template="rangenavigator/export-print/default", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { bitCoinData } from 'datasource.ts';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';
import { RangeNavigatorComponent } from '@syncfusion/ej2-angular-charts';

@Component({
    selector: 'app-container',
    template:
    `<button ej-button id='print' (click)='print()'>Print</button>
    <ejs-rangenavigator #range id="range" valueType='DateTime' [value]='value'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    @ViewChild('range')
    public RangeObj: RangeNavigatorComponent;

    public periodsValue: Object[];
    public chartData: Object[];
    public value: Object[];
    ngOnInit(): void {
        this.chartData = bitCoinData;
        this.value=[new Date(2017, 8, 1), new Date(2018, 1, 1)];
    }
    print() {
        this.RangeObj.print();
    }
}

```

{% endtab %}