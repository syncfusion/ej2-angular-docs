---
title: " Chart How To | Angular "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Format the tooltip value

Using [`tooltipRender`](../../api/chart/chartModel/#tooltiprender) event, you can able to format the
datetime value instead of rendered value.

To format the datetime value,please follow the steps below

**Step 1**:

By using [`tooltipRender`](../../api/chart/chartModel/#tooltiprender) event we can able to get
the current point x value. Using this value to format the tooltip by using `formatDate` method.

The output will appear as follows,

{% tab template="chart/how-to", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { ITextRenderEventArgs } from '@syncfusion/ej2-angular-charts';
import { Internationalization } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [tooltip]='tooltip' (tooltipRender) = 'tooltipRender($event)'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='India' width=2 [marker]='marker'></e-series>
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
    public tooltipRender(args: ITooltipRenderEventArgs): void {
        let intl: Internationalization = new Internationalization();
        let formattedString: string = intl.formatDate(new Date((args.point.x).toString()), { skeleton: 'MMMEd'});
        args.textCollections = formattedString;
    };
    ngOnInit(): void {
        this.chartData = [
             { x: new Date(2005, 0, 1), y: 21 }, { x: new Date(2006, 0, 1), y: 24 },
             { x: new Date(2007, 0, 1), y: 30 }, { x: new Date(2008, 0, 1), y: 38 },
             { x: new Date(2009, 0, 1), y: 54 }, { x: new Date(2010, 0, 1), y: 57 },
        ];
        this.primaryXAxis = {
           title: 'Year',
           valueType: 'DateTime'
        };
        this.primaryYAxis = {
           title: 'Efficiency',
        };
        this.marker = { visible: true, width: 10, height: 10, dataLabel: { visible: true}};
        this.title = 'Inflation - Consumer Price';
        this.tooltip = {enable: true}
    }
}
```

{% endtab %}