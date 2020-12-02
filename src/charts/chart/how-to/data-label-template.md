---
title: " Chart How To | Angular "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Bind colors for each data label template from the data source

You can bind text and interior information for a point from dataSource other than x and y value. To change color for the background in the datalabel template, you can use `${point.text}`.
To use point.text, you have to bind the property from dataSource to name in the datalabel options.

Follow the given steps to show the table tooltip,

**Step 1**:

Initialize the datalabel template div as shown in the following html page,

```html
    <script id="index" type="text/x-template">
    <div id='templateWrap' style="background-color: ${point.text}; border-radius: 3px;"><span>${point.y}</span></div>
    </script>
```

**Step 2**:

To show that datalabel template, set the element id to the `template` property in datalabel.

{% tab template="chart/datalabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IPointRenderEventArgs } from '@syncfusion/ej2-angular-charts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='Female' width=2 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public chartData: Object[];
    public title: string;
    public marker: Object;
    ngOnInit(): void {
        this.chartData =[
                   { x: 10, y: 7000, color: 'red' },
                   { x: 20, y: 1000, color: 'yellow' },
                   { x: 30, y: 12000, color: 'orange' },
                   { x: 40, y: 14000, color: 'skyblue' },
                   { x: 50, y: 11000, color: 'blue' },
                   { x: 60, y: 5000, color: 'green' },
                   { x: 70, y: 7300, color: 'pink' },
                   { x: 80, y: 9000, color: 'white' },
                   { x: 90, y: 12000, color: 'magenta' },
                   { x: 100, y: 14000, color: 'purple' },
                   { x: 110, y: 11000, color: 'teal' },
                   { x: 120, y: 5000, color: 'gray' },
                ];
        this.marker = { visible: true, dataLabel: { visible: true, name: 'color', template: '#index' }};
        this.title = 'Sales Rate in USA';
    }
}
```

{% endtab %}
