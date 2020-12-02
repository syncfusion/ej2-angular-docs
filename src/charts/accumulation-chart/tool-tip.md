---
title: "Accumulation Chart Tooltip | Angular "

component: "Accumulation Chart"

description: "Accumulation chart tooltip represents the x and y values of the current mouse pointer point."
---

# Tooltip

Tooltip for the accumulation chart can be enabled by using the `enable` property.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [tooltip]='tooltip'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
     public tooltip: Object;
    ngOnInit(): void {
        this.piedata = pieData;
        this.tooltip = {
                enable: true
                }
        };
    }
```

{% endtab %}

>Note: To use tooltip feature, inject the `AccumulationTooltipService` into the `@NgModule.providers`.

## Header

We can specify header for the tooltip using `header` property.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [tooltip]='tooltip'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
     public tooltip: Object;
    ngOnInit(): void {
        this.piedata = pieData;
        this.tooltip = {
              enable: true, header:"Pie Chart"
                }
        };
    }
```

{% endtab %}

## Format

By default, tooltip shows information of x and y value in points. In addition to that, you can show more
information in tooltip. For example the format `${series.name} ${point.x}` shows series name and point x value.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [tooltip]='tooltip'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
     public tooltip: Object;
    ngOnInit(): void {
        this.piedata = pieData;
        this.tooltip = {
              enable: true,  format: '${point.x} : <b>${point.y}%</b>'
                }
        };
    }
```

{% endtab %}

## Tooltip Template

Any HTML element can be displayed in the tooltip by using the `template` property.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [tooltip]='tooltip'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
     public tooltip: Object;
    ngOnInit(): void {
        this.piedata = pieData;
        this.tooltip = {
              enable: true,  template: "<div id='templateWrap' style='background-color:#bd18f9;border-radius: 3px; float: right;padding: 2px;line-height: 20px;text-align: center;'>"+
        "<img src='https://ej2.syncfusion.com/demos/src/chart/images/sunny.png' />" +
        "<div style='color:white; font-family:Roboto; font-style: medium; fontp-size:14px;float: right;padding: 2px;line-height: 20px;text-align: center;padding-right:6px'><span>${y}</span></div></div>"
                }
        };
    }
```

{% endtab %}

## Customization

The [`fill`](../api/accumulation-chart/tooltipSettings/#fill) and
[`border`](../api/accumulation-chart/tooltipSettings/#border) properties are used to customize the background
color and border of the tooltip respectively. The [`textStyle`](../api/accumulation-chart/tooltipSettings/#textstyle)
property in the tooltip is used to customize the font of the tooltip text.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
import { IAccTextRenderEventArgs, IAccTooltipRenderEventArgs } from '@syncfusion/ej2-charts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [tooltip]='tooltip'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public tooltip: Object;
    public ontooltipRender: Function;
    ngOnInit(): void {
        this.piedata = pieData;
         this.tooltip = {
              enable: true,
                format: '${series.name} ${point.x} : ${point.y}',
                fill: '#7bb4eb',
                border: {
                   width: 2,
                   color: 'grey'
                }
        };
    }
```

{% endtab %}

## Tooltip Mapping Name

By default, tooltip shows information of x and y value in points. You can show more information from datasource in tooltip by using the `tooltipMappingName` property of the tooltip.
You can use the `${point.tooltip}` as place holders to display the specified tooltip content.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
import { IAccTextRenderEventArgs, IAccTooltipRenderEventArgs } from '@syncfusion/ej2-charts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [tooltip]='tooltip'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' tooltipMappingName='text'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public tooltip: Object;
    ngOnInit(): void {
        this.piedata = [{ x: 'Jan', y: 13, text: 'Jan: 13' }, { x: 'Feb', y: 13, text: 'Feb: 13' },
                        { x: 'Mar', y: 17, text: 'Mar: 17' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' }
         ];
         this.tooltip = {
              enable: true, format: '${point.tooltip}'
                }
               };
    }
```

{% endtab %}

## To customize individual tooltip

Using `tooltipRender` event, you can customize a tooltip for particular point. event, you can customize a
tooltip for particular point.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
import { IAccTextRenderEventArgs, IAccTooltipRenderEventArgs } from '@syncfusion/ej2-charts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [tooltip]='tooltip' (tooltipRender)="ontooltipRender($event)">
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public tooltip: Object;
    public ontooltipRender: Function;
    ngOnInit(): void {
        this.piedata = pieData;
         this.tooltip = {
              enable: true
                }
        this.ontooltipRender = (args: IAccTooltipRenderEventArgs): void {
              if (args.point.index === 3) {
              args.text = args.point.x + '' + ':' + args.point.y + '' + ' ' +'customtext';
              args.textStyle.color = '#f48042';
        }
        }
        };
    }
```

{% endtab %}