---
title: " Chart How To | Angular "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Mark a threshold in chart

You can mark a threshold in chart by using the `stripline`.

To mark a threshold in chart, follow the given steps:

**Step 1**:

By using the start and end properties in `striplines` object, you can mark the threshold line in horizontal
axis to the chart as follows,

{% tab template= "chart/how-to" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='Runs' [marker]='marker'></e-series>>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = [
                 {x: 1, y: 5},{x: 2, y: 22},{x: 3, y: 10},{x: 4, y: 12},{x: 5, y: 5},
                 {x: 6, y: 15},{x: 7, y: 6},{x: 8, y: 12},{x: 9, y: 20},{x: 10, y: 7}];
        this.primaryXAxis={
            title: 'Overs'
        };
        this.primaryYAxis = {
           title: 'Runs',
            stripLines:[
           { start: 15, end: 15.1, color: '#ff512f', visible: true }
           ]
        };
        this.marker={visible: true}
        this.title = 'India Vs Australia 1st match';
    }
}
```

{% endtab %}