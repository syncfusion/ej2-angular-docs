---
title: " Accumulation Chart Data Label | Angular "

component: "Accumulation Chart"

description: "Data labels are names of the data points that are displayed on the x-axis of a chart and also used to highlight important data points"
---

# Data Label

Data label can be added to a chart series by enabling the [`visible`](../api/accumulation-chart/accumulationDataLabelSettings/#visible)
option in the dataLabel property.

{% tab template="chart/series/smartlabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { labelData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public datalabel: Object;
    ngOnInit(): void {
        this.datalabel = { visible: true };
        this.piedata = labelData;
    }

}
```

{% endtab %}

>Note: To use the data label feature, inject the `DataLabel` into the `@NgModule.providers`.

## Positioning

Accumulation chart provides support for placing the data label either `inside` or `outside` the chart.

{% tab template="chart/series/smartlabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { labelData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public datalabel: Object;
    ngOnInit(): void {
        this.datalabel = { visible: true, position: 'Outside' };
        this.piedata = labelData;
    }

}
```

{% endtab %}

## DataLabel Rotation

Using `angle` property, you can rotate the data label by its given angle.

{% tab template="chart/series/smartlabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { labelData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public datalabel: Object;
    ngOnInit(): void {
        this.datalabel = { visible: true, angle: 90, enableRotation: true },
        this.piedata = labelData;
    }

}
```

{% endtab %}

>Note: when the `enableRotation` is true, the datalabel is rotated along the slice.

## Smart Labels

Datalabels will be arranged smartly without overlapping with each other. You can enable or disable this feature using
the [`enableSmartLabels`](../api/accumulation-chart/accumulationChartModel/#enablesmartlabels) property.

{% tab template="chart/series/smartlabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { labelData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [enableSmartLabels]='enableSmartLabels'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public datalabel: Object;
    public enableSmartLabels: boolean;
    ngOnInit(): void {
        this.datalabel = { visible: true, name: 'text', position: 'Outside' };
        this.enableSmartLabels = true;
        this.piedata = labelData;
    }

}
```

{% endtab %}

## Datalabel template

Label content can be formatted by using the template option. Inside the template, you can add the placeholder text
`${point.x}` and `${point.y}` to display corresponding data points x & y value. Using
[`template`](../api/accumulation-chart/accumulationDataLabelSettings/#template)property, you can set data label
template in chart.

{% tab template="chart/series/smartlabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { labelData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [enableSmartLabels]='enableSmartLabels'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public datalabel: Object;
    public enableSmartLabels: boolean;
    ngOnInit(): void {
        this.datalabel = { visible: true, name: 'text', position: 'Outside', template: '<div>${point.x}</div><div>${point.y}</div>' };
        this.enableSmartLabels = true;
        this.piedata = labelData;
    }

}
```

{% endtab %}

## Connector Line

Connector line will be visible when the data label is placed `outside` the chart.
The connector line can be customized using the `type`, `color`, `width`, `length` and `dashArray` properties

{% tab template="chart/series/smartlabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { labelData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [enableSmartLabels]='enableSmartLabels'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public datalabel: Object;
    public enableSmartLabels: boolean;
    ngOnInit(): void {
        this.datalabel = { visible: true, name: 'text', position: 'Outside',
                         connectorStyle:{
                    //Length of the connector line in pixels
                    length: '50px',
                    //Width of the connector line in pixels
                    width: 2,
                    //dashArray of the connector line
                    dashArray: '5,3',
                    //Color of the connector line
                    color: '#f4429e',
                    //Specifies the type of the connector line either Line or Curve
                    type: 'Curve'
                } };
        this.enableSmartLabels = true;
        this.piedata = labelData;
    }

}
```

{% endtab %}

## Text Mapping

The fill color and the text in the data source can be mapped to the chart using `pointColorMapping` in series and
`name` in datalabel respectively.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { dataMapping } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public datalabel: Object;
    ngOnInit(): void {
        this.piedata = dataMapping;
        this.datalabel = { visible: true, name: 'text', position: 'Outside' };
    }

}
```

{% endtab %}

## Customization

Individual text can be customized using the `textRender` event.

{% tab template="chart/series/smartlabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { labelData } from 'datasource.ts';
import { IAccTextRenderEventArgs } from '@syncfusion/ej2-charts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" (textRender)="onTextRender($event)">
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public datalabel: Object;
    public onTextRender: Function;
    ngOnInit(): void {
        this.datalabel = { visible: true };
        this.piedata = labelData;
        this.onTextRender = (args: IAccTextRenderEventArgs): void {
             if (args.text === '13.5') {
            args.color = 'red';
            args.border.width = 1;
        }
        }
    }

}
```

{% endtab %}
