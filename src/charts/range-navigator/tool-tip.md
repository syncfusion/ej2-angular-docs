---
title: " RangeNavigator Tooltip | Angular "

component: "RangeNavigator"

description: "The range navigator supports tooltips for sliders.Tooltips  display the selected start and end values."
---

# Tooltip

The range navigator supports tooltips for sliders. Sliders are used to select data at a range in the range navigator.
Tooltips  display the selected start and end values.

## Customization

Tooltips can be customized using the following properties:

* tooltip: Customizes the text displayed in tooltip.
* enable: Customizes the visibility of the tooltip.
* fill: Customizes the background color of the tooltip.
* opacity: Customizes the opacity of the tooltip.
* textStyle: Customizes the font size, color, family, style, weight, alignment, and overflow of the tooltip.

{% tab template="rangenavigator/getting-started/tooltip", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'data.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value' [tooltip]='tooltip'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    public tooltip: Object[];
    ngOnInit(): void {
        this.value = [new Date('2017-09-01'), new Date('2018-02-01')];
        this.chartData = datasrc;
        this.tooltip = { enable: true, displayMode: 'Always', fill:'red', opacity: 0.6, textStyle:{ style: 'Italic', color:'blue', size:'12px'} };
    }
}

```

{% endtab %}

## Label Format

You can format and parse the date to all globalize format using `labelFormat` property in an axis.

{% tab template="rangenavigator/getting-started/tooltip", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'data.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value' [tooltip]='tooltip'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    public tooltip: Object[];
    ngOnInit(): void {
        this.value = [new Date('2017-09-01'), new Date('2018-02-01')];
        this.chartData = datasrc;
        this.tooltip = { enable: true, displayMode: 'Always', labelFormat: 'y/M/d' };
    }
}

```

{% endtab %}

The following table describes the result of applying some common date time formats to the `labelFormat` property

<!-- markdownlint-disable MD033 -->

<table>
<tr>
<td><b>Label Value</b></td>
<td><b>Label Format Property Value</b></td>
<td><b>Result </b></td>
<td><b>Description </b></td>
</tr>
<tr>
<td>new Date(2000, 03, 10)</td>
<td>EEEE</td>
<td>Monday</td>
<td>The Date is displayed in day format</td>
</tr>
<tr>
<td>new Date(2000, 03, 10)</td>
<td>yMd</td>
<td>04/10/2000</td>
<td>The Date is displayed in month/date/year format</td>
</tr>
<tr>
<td>new Date(2000, 03, 10)</td>
<td> MMM </td>
<td>Apr</td>
<td>The Shorthand month for the date is displayed</td>
</tr>
<tr>
<td>new Date(2000, 03, 10)</td>
<td>hm</td>
<td>12:00 AM</td>
<td>Time of the date value is displayed as label</td>
</tr>
<tr>
<td>new Date(2000, 03, 10)</td>
<td>hms</td>
<td>12:00:00 AM</td>
<td>The Label is displayed in hours:minutes:seconds format</td>
</tr>
</table>
