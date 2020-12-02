---
title: " Chart How To | Angular "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart"
---

# Add or remove a series from the chart dynamically

You can add or remove the chart series dynamically by using the `addSeries` or `removeSeries` method.

To add or remove the series dynamically, follow the given steps:

**Step 1**:

To add a new series to chart dynamically, pass the series value to the `addSeries` method.

To remove the new series from chart dynamically, pass the series index to the `removeSeries` method.

{% tab template= "chart/add-series", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { ChartComponent } from '@syncfusion/ej2-angular-charts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart #chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='Column' xName='x' yName='y' > </e-series>
            </e-series-collection>
    </ejs-chart>
    <button ejs-button class='e-flat' (click)='add()'>add </button>
    <button ejs-button class='e-flat' (click)='remove()'>remove </button>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];
    @ViewChild('chart')
    public chart: ChartComponent;
    ngOnInit(): void {
        this.data =  [{ x: 'John', y: 10000 }, { x: 'Jake', y: 12000 }, { x: 'Peter', y: 18000 },
                { x: 'James', y: 11000 }, { x: 'Mary', y: 9700 }];
        this.primaryXAxis = {
           title: 'Manager',
            valueType: 'Category'
            };
        this.primaryYAxis = {
            title: 'Sales',
            minimum: 0,
            maximum: 20000
            };

        this.title = 'Sales Comparision';
    }
     add() {
                this.chart.addSeries([{
                type: 'Column',
                dataSource: [{ x: 'John', y: 11000 }, { x: 'Jake', y: 16000 }, { x: 'Peter', y: 19000 },
                { x: 'James', y: 12000 }, { x: 'Mary', y: 10700 }],
                xName: 'x', width: 2,
                yName: 'y'
            }]);
        }
     remove() {
         this.chart.removeSeries(1);
     }
}
```

{% endtab %}