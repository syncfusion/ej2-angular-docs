---
title: " Chart How To | Angular "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Show series based on respective legend click

By using the `chartMouseClick` event, you can show the series based on respective legend click. In this event, you can get the legend target id, using which you can get the current series index. Based on the index, you can set value of `visible` to `true` or `false`.

{% tab template="chart/how-to" , sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { ILoadedEventArgs, Series, IMouseEventArgs } from '@syncfusion/ej2-angular-charts';

@Component({
    selector: 'app-container',
    template:
    `  <ejs-chart style='display:block;' #chart [chartArea]='chartArea' [width]='width' align='center' id='chartcontainer' [primaryXAxis]='primaryXAxis'
            [primaryYAxis]='primaryYAxis' [title]='title' [tooltip]='tooltip' (chartMouseClick)='chartMouseClick($event)'>
            <e-series-collection>
                <e-series [dataSource]='data' type='Column' xName='x' yName='y' name='Gold' width=2 fill="red" opacity=0.7> </e-series>
                <e-series [dataSource]='data1' type='Column' xName='x' yName='y' name='Silver' width=2 fill="orange" opacity=0.7> </e-series>
                <e-series [dataSource]='data2' type='Column' xName='x' yName='y' name='Bronze' width=2 fill="grey" opacity=0.7> </e-series>
            </e-series-collection>
        </ejs-chart>`
})
export class AppComponent implements OnInit {
    @ViewChild('chart')
    public chart1:ChartComponent;
    public previousTarget = null;
    public data: Object[] = [
        { x: 'USA', y: 46 }, { x: 'GBR', y: 27 }, { x: 'CHN', y: 26 }
    ];
    public data1: Object[] = [
        { x: 'USA', y: 37 }, { x: 'GBR', y: 23 }, { x: 'CHN', y: 18 }
    ];
    public data2: Object[] = [
        { x: 'USA', y: 38 }, { x: 'GBR', y: 17 }, { x: 'CHN', y: 26 }
    ];
    public primaryXAxis: Object = {
        valueType: 'Category', interval: 1,
    };
    public title: string = 'Olympic Medal Counts - RIO';
    public tooltip: Object = {
        enable: true
    };
    public chartMouseClick(args: IMouseEventArgs): void {
       var flag = false;
    if (((args.target).indexOf('chart_legend_text') > -1) || ((args.target).indexOf('chart_legend_shape') > -1) ||
      (args.target).indexOf('chart_legend_shape_marker_') && !(args.target).indexOf('chart_legend_element')) {
      var ids = ((args.target).indexOf('chart_legend_text') > -1) ?
        (args.target).split('chart_legend_text_')[1] : args.target.split('chart_legend_shape_marker_')[1] || args.target.split('chart_legend_shape_')[1];
      for (var i = 0; i < this.chart1.series.length; i++) {
        this.chart1.series[i].visible = false;
      }
      if (ids == this.previousTarget) {
        for (var j = 0; j < this.chart1.series.length; j++)
          this.chart1.series[j].visible = true;
        this.chart1.series[ids].visible = false;
        this.previousTarget = null;
        flag = true;
      }
      if (!flag)
        this.previousTarget = ids;
    }
    };
}
```

{% endtab %}