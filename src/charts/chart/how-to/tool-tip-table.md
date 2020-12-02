---
title: " Chart How To | Angular "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Create a table in tooltip

You can show the tooltip as table by using template property in tooltip.

Follow the given steps to show the table tooltip,

**Step 1**:

Initialize the tooltip template div as shown in the following html page,

```html
   <script id="Female-Material" type="text/x-template">
    <div id='templateWrap'>
        <table style="width:100%;  border: 1px solid black;">
        <tr><th colspan="2" bgcolor="#00FFFF">Female</th></tr>
        <tr><td bgcolor="#00FFFF">${x}:</td><td bgcolor="#00FFFF">${y}</td></tr>
        </table>
    </div>
   </script>

```

**Step 2**:

To show that tooltip template, set the element id to the `template` property in tooltip.

{% tab template="chart/table", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IPointRenderEventArgs } from '@syncfusion/ej2-angular-charts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'  [tooltip]='tooltip'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='Female' width=2 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    public tooltip: Object;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData =[
                    { x: 2010, y: 990 }, { x: 2011, y: 1010 },
                    { x: 2012, y: 1030 }, { x: 2013, y: 1070 },
                    { x: 2014, y: 1105 }, { x: 2015, y: 1138 },
                    { x: 2016, y: 1155 }
                ];
        this.primaryXAxis = {
           minimum: 2010, maximum: 2016,
          edgeLabelPlacement: 'Shift',
        };
        this.primaryYAxis = {
            minimum: 900, maximum: 1300,
            labelFormat: '{value}M',
        };
        this.marker = { visible: true, width: 10, height: 10, shape: 'Rectangle'};
        this.tooltip = {
            enable: true,
            template:'#Female-Material'
            }
        this.title = 'Population of India ( 2010 - 2016 )';
    }
}
```

{% endtab %}
