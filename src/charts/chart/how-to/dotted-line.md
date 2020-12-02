---
title: " Chart How To | Angular "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# To add dotted line using annotation

By using `annotation`, you can add dotted lines in the chart.

To add dotted lines in the chart, follow the given steps:

**Step 1**:

Initialize the custom elements by using the `annotation` property.

By setting `coordinateUnits` value as `point` in annotation object you can placed dotted lines
in the chart based on point x and y values.

{% tab template="chart/how-to", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { ITooltipRenderEventArgs, Series } from '@syncfusion/ej2-angular-charts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis' [title]='title'
     [tooltip]='tooltip'>
     <e-annotations>
    <e-annotation visible = true
                    content='<div id = "test" style="border-top:3px dashed grey;border-top-width: 2px; width: 10000px"></div>'
                    x = '2014' y = 50
                    coordinateUnits='Point'>
                </e-annotation>
            </e-annotations>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='Max Temp'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    public primaryYAxis: Object;
    public tooltip: Object = {
        enable: true
    };
    ngOnInit(): void {
        this.chartData =[
        { x: '2014', y:34 }, { x: '2015', y: 38 },
        { x: '2016', y: 44 }, { x: '2017', y: 51 },
        { x: '2018', y: 61 }, { x: '2019', y: 76 },
        { x: '2020', y: 82 }
                ];
        this.primaryXAxis = {
        valueType: 'Category'
        };
        this.title =  'NC Weather Report - 2016';
    }
}
```

{% endtab %}