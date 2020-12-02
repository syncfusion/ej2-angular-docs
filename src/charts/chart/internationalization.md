---
title: " Chart Internationalization | Angular "

component: "Chart"

description: "Chart provides the support for internationalization for dataLabel, axis label and tooltip elements."
---

# Internationalization

Chart provide supports for internationalization for below chart elements.

* Datalabel.
* Axis label.
* Tooltip.

For more information about number and date formatter you can refer
[`internationalization`](https://ej2.syncfusion.com/angular/documentation/chart/internationalization/?no-cache=1).

<!-- markdownlint-disable MD036 -->
**Globalization**

Globalization is the process of designing and developing an component that works in different
cultures/locales.  Internationalization  library is used to globalize number, date, time values in
Chart component using  `labelFormat` property in axis.

**Numeric Format**

In the below example axis, point  and tooltip labels are globalized to EUR.

{% tab template="chart/number-format", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { loadCldr, L10n, setCulture, setCurrencyCode } from '@syncfusion/ej2-base';
setCurrencyCode('EUR');

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'[tooltip]='tooltip'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Product X' [marker]='marker'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y1' name='Product Y ' [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public tooltip: Object;
    public marker: Object;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = [
                { x: 1900, y: 4, y1: 2.6, y2: 2.8 }, { x: 1920, y: 3.0, y1: 2.8, y2: 2.5 },
                { x: 1940, y: 3.8, y1: 2.6, y2: 2.8 }, { x: 1960, y: 3.4, y1: 3, y2: 3.2 },
                { x: 1980, y: 3.2, y1: 3.6, y2: 2.9 }, { x: 2000, y: 3.9, y1: 3, y2: 2 }
        ];
        this.primaryXAxis = {
            title: 'Year',
            edgeLabelPlacement: 'Shift'
        };
        this.primaryYAxis = {
           title: 'Sales Amount in Millions',
           labelFormat: 'c'
        };
        this.tooltip = {
            enable: true, format: '${series.name} <br>${point.x} : ${point.y}'
        };
        this.marker = {
            dataLabel: {
                visible: true
            }
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}