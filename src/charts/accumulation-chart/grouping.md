---
title: "Accumulation Chart Grouping | Angular "

component: "Accumulation Chart"

description: "By using point and value in pie chart,you can group collection of points into the single slice"
---

# Grouping

You can club/group few points of the series based on
[`groupTo`](../api/accumulation-chart/accumulationSeries/#groupto) property. For example, if the club
value is 11, then the points with value less than 11 is grouped together and will be showed as a single
point with label `others`. The property also takes value in percentage (percentage of total data points value).

{% tab template="chart/series/clubpoint", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IAccTextRenderEventArgs, IAccPointRenderEventArgs } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" >
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' groupTo='11' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public datalabel: Object;
    ngOnInit(): void {
        this.datalabel = { visible: true, name: 'text', position: 'Outside' };
        this.piedata = [
                { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
                { x: 'Mar', y: 7, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
                { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
                { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: 25, text: 'Aug: 25' },
                { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' }];
    }

}
```

{% endtab %}

## Broken slice

You can visualize all points available in club/group points by clicking on the grouped point. For example, if 5 points are grouped together it will be showed as a single slice with label `others`. If we click on `others` slice it will explode and broke into 5 seperate slices.

{% tab template="chart/series/clubpoint", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IAccTextRenderEventArgs, IAccPointRenderEventArgs } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" >
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' groupTo='11' [dataLabel]='datalabel' [explode]='explode' [explodeOffset]='explodeOffset'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public datalabel: Object;
    public explode: boolean;
    public explodeOffset: string;
    ngOnInit(): void {
        this.datalabel = { visible: true, name: 'text', position: 'Outside' };
        this.piedata = [
               { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
                { x: 'Mar', y: 7, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
                { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
                { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: 25, text: 'Aug: 25' },
                { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' },
                { x: 'Nov', y: 9, text: 'Nov: 9' }, { x: 'Dec', y: 3.5, text: 'Dec: 3.5' }
                ];
        this.explode = true;
        this.explodeOffset = '10%';
    }

}
```

{% endtab %}

## Group Mode

Slice can also be grouped based on number of points by specifying the `groupMode` to Point. For example, if the group to value is 11, accumulation chart will show 1st 11 points and will group remaining entries in the collection as a single point.

{% tab template="chart/series/clubpoint", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IAccTextRenderEventArgs, IAccPointRenderEventArgs } from '@syncfusion/ej2-charts';
import { groupData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" (textRender)="onTextRender($event)" (pointRender)="onPointRender($event)">
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' [dataLabel]='datalabel' groupTo='4' groupMode='Point'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public datalabel: Object;
    public onTextRender: Function;
    public onPointRender: Function;
    ngOnInit(): void {
        this.datalabel = { visible: true, name: 'text', position: 'Outside' };
        this.onTextRender = (args: IAccTextRenderEventArgs): void {
            if (args.text.indexOf('Others') > -1) {
                args.color = 'red';
                args.border.width = 1;
            }
        }
        this.onPointRender = (args: IAccPointRenderEventArgs): void {
            if ((args.point.x as string).indexOf('Others') > -1) {
                args.fill = '#D3D3D3';
            }
        }
        this.piedata = groupData;
    }

}
```

{% endtab %}

## Customization

You can customize the grouped point and its data label using `pointRender` and `textRender` event.

{% tab template="chart/series/clubpoint", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IAccTextRenderEventArgs, IAccPointRenderEventArgs } from '@syncfusion/ej2-charts';
import { groupData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" (textRender)="onTextRender($event)" (pointRender)="onPointRender($event)">
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' groupTo='11' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public datalabel: Object;
    public onTextRender: Function;
    public onPointRender: Function;
    ngOnInit(): void {
        this.datalabel = { visible: true, name: 'text', position: 'Outside' };
        this.onTextRender = (args: IAccTextRenderEventArgs): void {
            if (args.text.indexOf('Others') > -1) {
                args.color = 'red';
                args.border.width = 1;
            }
        }
        this.onPointRender = (args: IAccPointRenderEventArgs): void {
            if ((args.point.x as string).indexOf('Others') > -1) {
                args.fill = '#D3D3D3';
            }
        }
        this.piedata = groupData;
    }

}
```

{% endtab %}