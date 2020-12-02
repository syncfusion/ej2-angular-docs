---
title: " RangeNavigator Data | Angular "

component: "RangeNavigator"

description: "Range navigator supports double, datetime and logarithmic data values for rendering.Also supports labels and range Customization."
---

<!-- markdownlint-disable MD036 -->

# Types of data

## Numeric

Numeric scale is used to represent the numeric values of data in a chart. By default, the valueType of a range navigator is Double.

{% tab template="rangenavigator/axis/numeric", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { double } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" [value]='value'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    ngOnInit(): void {
        this.value = [12,30];
        this.chartData = double;
    }
}

```

{% endtab %}

### Range

Minimum and maximum of the Range navigator will be calculated automatically based on the provided data. You can also customize the range using the minimum, maximum, and interval properties.

{% tab template="rangenavigator/axis/numeric", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" [value]='value' [minimum]='minimum' [maximum]='maximum' [interval]='interval'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='StepLine' xName='xData' yName='yData' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    public minimum: number;
    public maximum: number;
    public interval: number;
    ngOnInit(): void {
        this.value = [60,100];
        this.chartData = [
                            { xData: 10, yData: 35 }, { xData: 20, yData: 28 },
                            { xData: 30, yData: 34 }, { xData: 40, yData: 32 },
                            { xData: 50, yData: 40 }, { xData: 60, yData: 30 },
                            { xData: 70, yData: 4 }, { xData: 80, yData: 22 },
                            { xData: 90, yData: 30 }, { xData: 100, yData: 43 },
                            { xData: 110, yData: 60 }, { xData: 120, yData: 33 },
                            { xData: 130, yData: 40 }, { xData: 140, yData: 29 },
                            { xData: 150, yData: 10 }, { xData: 160, yData: 16 },
                         ];
        this.minimum= 10;
        this.maximum= 160;
        this.interval= 10;
    }
}

```

{% endtab %}

### Label Format

Numeric labels can be formatted using the labelFormat property.

Numeric labels support all globalized formats.

{% tab template="rangenavigator/axis/numeric", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { double } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" [value]='value' labelFormat='n1'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    ngOnInit(): void {
        this.value = [12,30];
        this.chartData = double;
    }
}

```

{% endtab %}

The following table describes the result of applying some commonly used label formats on numeric values.

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td><b>Label Value</b></td>
<td><b>Label Format property value</b></td>
<td><b>Result </b></td>
<td><b>Description </b></td>
</tr>
<tr>
<td>1000</td>
<td>n1</td>
<td>1000.0</td>
<td>The Number is rounded to 1 decimal place</td>
</tr>
<tr>
<td>1000</td>
<td>n2</td>
<td>1000.00</td>
<td>The Number is rounded to 2 decimal place</td>
</tr>
<tr>
<td>1000</td>
<td>n3</td>
<td>1000.000</td>
<td>The Number is rounded to 3 decimal place</td>
</tr>
<tr>
<td>0.01</td>
<td>p1</td>
<td>1.0%</td>
<td>The Number is converted to percentage with 1 decimal place</td>
</tr>
<tr>
<td>0.01</td>
<td>p2</td>
<td>1.00%</td>
<td>The Number is converted to percentage with 2 decimal place</td>
</tr>
<tr>
<td>0.01</td>
<td>p3</td>
<td>1.000%</td>
<td>The Number is converted to percentage with 3 decimal place</td>
</tr>
<tr>
<td>1000</td>
<td>c1</td>
<td>$1,000.0</td>
<td>The Currency symbol is appended to number and number is rounded to 1 decimal place</td>
</tr>
<tr>
<td>1000</td>
<td>c2</td>
<td>$1,000.00</td>
<td>The Currency symbol is appended to number and number is rounded to 2 decimal place</td>
</tr>
</table>

### Custom Label Format

The range navigator also supports custom label formats using placeholders such as {value}$, in which, the value
represent the axis label, e.g. 20$.

{% tab template="rangenavigator/axis/numeric", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { double } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" [value]='value' labelFormat='{value}$'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    ngOnInit(): void {
        this.value = [12,30];
        this.chartData = double;
    }
}

```

{% endtab %}

## Logarithmic Axis

Logarithmic supports logarithmic scale, and it is used to visualize data when the Range navigator has numerical values in both lower (e.g.: 10-6) and higher (e.g.: 106) orders of magnitude.

{% tab template="rangenavigator/axis/logarithmic", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" [value]='value' valueType='Logarithmic' [interval]='interval'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})

export class AppComponent implements OnInit {

    public value: Object[];
    public chartData: Object[];
    public interval: number;
    ngOnInit(): void {
        this.value = [4,6];
        this.chartData = [];
        for (let i = 0; i < 100; i++) {
            this.chartData.push({
                x: Math.pow(10, i * 0.1),
                y: Math.floor(Math.random() * (80 - 30 + 1)) + 30
            });
        }
        this.interval = 1;
    }
}

```

{% endtab %}

>Note: To use logarithmic scale,  inject the `LogarithmicService` into the `@NgModule.providers`, and then set the valueType to Logarithmic.

**Range**

Minimum and maximum of the Range navigator will be calculated automatically based on the provided data. You can also customize the range using the minimum, maximum, and interval properties.

{% tab template="rangenavigator/axis/logarithmic", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" [value]='value' valueType='Logarithmic' [interval]='interval'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})

export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    public interval: number;
    ngOnInit(): void {
        this.value = [4,6];
        this.chartData = [];
        for (let i = 0; i < 100; i++) {
            this.chartData.push({
                x: Math.pow(10, i * 0.1),
                y: Math.floor(Math.random() * (80 - 30 + 1)) + 30
            });
        }
        this.interval = 1;
    }
}

```

{% endtab %}

### Logarithmic Base

Logarithmic base can be customized using the logBase property. The default value of the logBase property is 10.

{% tab template="rangenavigator/axis/logarithmic", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" [value]='value' valueType='Logarithmic' [logBase]='log'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})

export class AppComponent implements OnInit {

    public value: Object[];
    public chartData: Object[];
    public log: number;
    ngOnInit(): void {
        this.value = [4,6];
        this.chartData = [];
        for (let i = 0; i < 100; i++) {
            this.chartData.push({
                x: Math.pow(10, i * 0.1),
                y: Math.floor(Math.random() * (80 - 30 + 1)) + 30
            });
        }
        this.log = 2;
    }
}

```

{% endtab %}

## Date-time

Date-time Range navigator supports date-time scale and displays date-time values as a labels in the specified format.

{% tab template="rangenavigator/axis/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public periodsValue: Object[];
    public chartData: Object[];
    public value: Object[];
    ngOnInit(): void {
        this.chartData = datasrc;
        this.value=[new Date("2017-08-13"), new Date("2017-12-28")];
    }
}

```

{% endtab %}

>Note: To use date-time scale,  inject the `DateTimeService` into the `@NgModule.providers`.

### Interval Customization

Date-time intervals can be customized using the interval and intervalType properties of the range navigator.
For example, when you set interval as 2 and intervalType as years, the interval is considered as 2 years.
Date-time supports the following interval types:
* Auto
* Years
* Quarter
* Months
* Weeks
* Days
* Hours
* Minutes

{% tab template="rangenavigator/axis/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value' intervalType='Months' [interval]='interval'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public chartData: Object[];
    public value: Object[];
    public interval:number;
    ngOnInit(): void {
        this.chartData = datasrc;
        this.value=[new Date("2017-08-13"), new Date("2017-12-28")];
        this.interval = 2;
    }
}

```

{% endtab %}

**Label Format**

You can format and parse the date to all globalize format using `labelFormat` property in an axis.

{% tab template="rangenavigator/axis/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value' labelFormat='y/M/d'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public chartData: Object[];
    public value: Object[];
    ngOnInit(): void {
        this.chartData = datasrc;
        this.value=[new Date("2017-08-13"), new Date("2017-12-28")];
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
