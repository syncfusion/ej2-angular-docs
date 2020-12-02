---
title: " RangeNavigator Period Selector | Angular "

component: "RangeNavigator"

description: "The period selector allows to select a range with specified periods."
---

# Period selector

The period selector allows to select a range with specified periods.

## Periods

Periods is an array of objects that allows users to specify the range of periods. The “interval” property specifies the count value of the button, and the “text” property specifies the text to be displayed on button. The “intervalType” property allows users to customize the intervals of the buttons. The “intervalType” property supports the following interval types:

* Auto
* Years
* Quarter
* Months
* Weeks
* Days
* Hours
* Minutes
* Seconds

{% tab template="rangenavigator/periodselector/periods", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [periodSelectorSettings]='periodsValue'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='close' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public periodsValue: Object[];
    public chartData: Object[];
    public tooltip: Object[];
    public labelFormat: string;
    ngOnInit(): void {
        this.periodsValue = {
                                periods: [
                                    { text: '1M', interval: 1, intervalType: 'Months' },{ text: '3M', interval: 3, intervalType:'Months'},
                                    { text: '6M', interval: 6, intervalType: 'Months' }, { text: 'YTD' },
                                    { text: '1Y', interval: 1, intervalType: 'Years' },
                                    { text: '2Y', interval: 2, intervalType: 'Years', selected: true },
                                    { text: 'All' }
                                ]
                            };
        this.chartData = chartData;
    }
}

```

{% endtab %}

>Note: To use the period selector feature, inject the `PeriodSelectorService` into the `@NgModule.providers`.

## Positioning period selector

The `position` property allows users to position the period selector either at the `top` or `bottom`.

{% tab template="rangenavigator/periodselector/position", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [periodSelectorSettings]='periodsValue'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='close' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public periodsValue: Object[];
    public chartData: Object[];
    ngOnInit(): void {
        this.periodsValue = {
                                position: 'Top',
                                periods: [
                                    { text: '1M', interval: 1, intervalType: 'Months' }, { text: '3M', interval: 3, intervalType: 'Months' },
                                    { text: '6M', interval: 6, intervalType: 'Months' }, { text: 'YTD' },
                                    { text: '1Y', interval: 1, intervalType: 'Years' },
                                    { text: '2Y', interval: 2, intervalType: 'Years', selected: true
                                    },
                                    { text: 'All' }
                                ]
                            };
        this.chartData = chartData;
    }
}

```

{% endtab %}

## Height

The `height` property allows users to specify the height for period selector. The default value of the height property is 43.

{% tab template="rangenavigator/periodselector/position", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [periodSelectorSettings]='periodsValue'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='close' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public periodsValue: Object[];
    public chartData: Object[];
    ngOnInit(): void {
        this.periodsValue = {
                                height: 65,
                                periods: [
                                    { text: '1M', interval: 1, intervalType: 'Months' }, { text: '3M', interval: 3, intervalType: 'Months' },
                                    { text: '6M', interval: 6, intervalType: 'Months' }, { text: 'YTD' },
                                    { text: '1Y', interval: 1, intervalType: 'Years' },
                                    { text: '2Y', interval: 2, intervalType: 'Years', selected: true
                                    },
                                    { text: 'All' }
                                ]
                        };
        this.chartData = chartData;
    }
}

```

{% endtab %}

## Visibility of range navigator

The `disableRangeSelector` property allows users to render the period selector without range navigator.

{% tab template="rangenavigator/periodselector/position", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [disableRangeSelector]='visibility' [periodSelectorSettings]='periodsValue'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='close' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public periodsValue: Object[];
    public chartData: Object[];
    public visibility: boolean;
    ngOnInit(): void {
        this.periodsValue = {
                               periods: [
                                        { text: '1M', interval: 1, intervalType: 'Months' }, { text: '3M', interval: 3, intervalType: 'Months' },
                                        { text: '6M', interval: 6, intervalType: 'Months' }, { text: 'YTD' },
                                        { text: '1Y', interval: 1, intervalType: 'Years' },
                                        { text: '2Y', interval: 2, intervalType: 'Years', selected: true
                                        },
                                        { text: 'All' }
                                    ]
                        };
        this.chartData = chartData;
        this.visibility = true;
    }
}

```

{% endtab %}

## See Also

* [LightWeight](./lightweight/)
