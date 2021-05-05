---
title: " Chart How To | Angular "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# Customize column width and spacing

By using the [`columnWidth`](https://ej2.syncfusion.com/documentation/api/chart/series/#columnwidth) and [`columnSpacing`](https://ej2.syncfusion.com/documentation/api/chart/series/#columnspacing) property in the series of the chart, you can customize the column width and column spacing value for all points of the column series.

To customize the column width and spacing in column series of the chart, follow the given steps:

**Step 1**:

By setting [`columnWidth`](https://ej2.syncfusion.com/documentation/api/chart/series/#columnwidth) value between 0 to 1 you can customize the width for every point in the column series.

{% tab template= "chart/how-to" , sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IAccTooltipRenderEventArgs } from '@syncfusion/ej2-ng-charts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart style="display:block;" [chartArea]="chartArea" [width]="width" align="center"
      id="chartcontainer" [primaryXAxis]="primaryXAxis" [primaryYAxis]="primaryYAxis"
      [title]="title" [tooltip]="tooltip" (load)="load($event)" >
      <e-series-collection>
        <e-series [dataSource]="data" type="Column" xName="x" yName="y" name="Gold"
          width="2" columnWidth="0.4">
        </e-series>
      </e-series-collection>
    </ejs-chart>`
})
export class AppComponent {
    public data: Object[] = [
    { x: "USA", y: 4 },
    { x: "GBR", y: 5 },
    { x: "CHN", y: 6 }
  ];
  //Initializing Primary X Axis
  public primaryXAxis: Object = {
    valueType: "Category",
    interval: 1,
    majorGridLines: { width: 0 }
  };
  //Initializing Primary Y Axis
  public primaryYAxis: Object = {
    majorGridLines: { width: 0 },
    majorTickLines: { width: 0 },
    lineStyle: { width: 0 }
  };
  public marker: Object = {
    dataLabel: {
      visible: true,
      position: "Top",
      font: { fontWeight: "600", color: "#ffffff" }
    }
  };
  public title: string = "Olympic Medal Counts - RIO";
  public tooltip: Object = {
    enable: true
  };
  // custom code start
  public load(args: ILoadedEventArgs): void {
    let selectedTheme: string = location.hash.split("/")[1];
    selectedTheme = selectedTheme ? selectedTheme : "Material";
    args.chart.theme = <ChartTheme>(
      (selectedTheme.charAt(0).toUpperCase() + selectedTheme.slice(1)).replace(
        /-dark/i,
        "Dark"
      )
    );
    if (selectedTheme === "highcontrast") {
      args.chart.series[0].marker.dataLabel.font.color = "#000000";
      args.chart.series[1].marker.dataLabel.font.color = "#000000";
      args.chart.series[2].marker.dataLabel.font.color = "#000000";
    }
  }
  // custom code end
  public chartArea: Object = {
    border: {
      width: 0
    }
  };
  public width: string = Browser.isDevice ? "100%" : "60%";

  constructor() {
    //code
  }

}
```

{% endtab %}
