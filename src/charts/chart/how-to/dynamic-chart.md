---
title: " Chart How To | Angular "

component: "Chart"

description: "How to section explains knowledge base samples and howto access different types properties and events of the chart."
---

# To add chart dynamically

By using html button, you can add the chart dynamically when click the button.

To add the chart dynamically through button click, follow the given steps:

**Step 1**:

Initially create the html button.

Then create chart inside of button `onClick` function. Now click the button charts will render based on click count.

The following code sample demonstrates the output.

{% tab template="chart/how-to", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-container',
  template: ` <div><button ej-button id='print' (click)='Add()'>Add Chart</button><div  *ngFor="let item of items"><ejs-chart [id]="id" [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='Germany' [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart></div></div>`,
})

export class AppComponent implements OnInit {
  public i:number = 0;
  public id:string ='chart-container';
  public chartData: Object[];
  public marker: Object;
  public title: string;
  public items:any =[];
  ngOnInit(): void {
    this.chartData = [{ x: 1, y: 21 }, { x: 2, y: 24 }, { x: 3, y: 36 },
    { x: 4, y: 38 }, { x: 5, y: 54 }, { x: 6, y: 57 }, { x: 7, y: 70 }],
      this.title = 'Inflation - Consumer Price';
    this.marker = { visible: true };
  }
  Add() {
   this.id = 'chart-container' + this.i;
    var item = {
      "id":this.id,
      }
    this.items.push(item);
     this.i++;
  }
}
```

{% endtab %}