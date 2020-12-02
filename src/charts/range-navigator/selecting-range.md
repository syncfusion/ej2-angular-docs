---
title: " RangeNavigator Selecting Range | Angular "

component: "RangeNavigator"

description: "we can able to select the particular range data by dragging thumbs or by tapping on the labels or by setting the start and end value properties. "
---

# Selecting Range

The left and right thumb of RangeNavigator are used to indicate the selected range in the large collection of data. Following are the ways you can select a range.

<!-- markdownlint-disable MD010 -->

*	By dragging the thumbs.
*	By tapping on the labels.
*	By setting the start and end through value properties.

Following code example shows how to configure the selected range using value  property of RangeNavigator.

{% tab template="rangenavigator/selecting-range/default", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value' [tooltip]='tooltip'
    [labelFormat]='labelFormat'>
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
    public labelFormat: string;
    ngOnInit(): void {
        this.value = [new Date('2017-09-01'), new Date('2018-02-01')];
        this.chartData = datasrc;
        this.tooltip = { enable: true, displayMode: 'Always' };
        this.labelFormat = 'MMM-yy';
    }
}

```

{% endtab %}
