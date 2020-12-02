---
title: " Chart How To | Angular "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Visualize the data that returned by grid in chart

You can visualize the data that returned by grid in chart.

To visualize the data in chart, follow the given steps:

**Step 1**:

Initialize the grid with datasource.

**Step 2**:

By using the grid’s `actionComplete` event and `getCurrentViewRecords` method, you can get the current page records.
By using the grid’s `databound` event, you can update the current page records into the chart’s datasource and visualize the grid data in chart.

{% tab template= "chart/grid-visual" , sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { IDragCompleteEventArgs, ChartComponent } from '@syncfusion/ej2-angular-charts';
import { GridComponent, ActionEventArgs } from '@syncfusion/ej2-angular-grids';
import { Query, DataManager } from '@syncfusion/ej2-data';
import { orderData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-grid #grid [dataSource]='data' [allowPaging]="true" [pageSettings]='pageSettings' (dataBound)='dataBound()'
    (actionComplete)='actionComplete($event)'>
                 <e-columns>
                    <e-column field='OrderDate' headerText='Order Date' width=130 format='yMd' textAlign='right'></e-column>
                    <e-column field='Freight' width=120 format='C2' textAlign='right'></e-column>
                </e-columns>
    </ejs-grid>
    <ejs-chart #chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series  type='Line' xName='OrderDate' yName='Freight' name='dataview' [marker]='marker'></e-series>>
        </e-series-collection>
         </ejs-chart>`

})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public data: Object[];
    public title: string;
    public marker: Object;
    public primaryYAxis: Object;
    public pageSettings: Object;
    @ViewChild('chart')
    public chart: ChartComponent;
     @ViewChild('grid')
    public grid: GridComponent;
    ngOnInit(): void {
        this.data = new DataManager(orderData as JSON[]).executeLocal(new Query().take(100));
        this.pageSettings = { pageSize: 10 };
    }
    dataBound() {
           this.chart.primaryXAxis = {
            valueType: 'DateTime',
           };
          this.chart.series[0].marker = { visible: true}
          this.chart.series[0].xName = 'OrderDate';
          this.chart.series[0].yName = 'Freight';
          this.chart.series[0].dataSource = this.grid.getCurrentViewRecords();
    }
  public actionComplete(args: ActionEventArgs):void {
                if (args.requestType === 'paging') {
                 this.chart.series[0].dataSource =  this.grid.getCurrentViewRecords();
                 this.chart.refresh();
    }
}
}
```

{% endtab %}