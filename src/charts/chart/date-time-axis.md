---
title: " Chart Datetime Axis | Angular "

component: "Chart"

description: "Date time axis uses date time scale and displays the date time values as axis labels in the specified format."
---

<!-- markdownlint-disable MD036 -->

# DateTime and DateTimeCategory Axis

## DateTime Axis

 Date time axis uses date time scale and displays the date time values as axis labels in the specified format.

To known about dateTime axis, you can check on this video:

`youtube:AoxGQlE_WtE`

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = [
                 { x: new Date(2000, 6, 11), y: 10 }, { x: new Date(2002, 3, 7), y: 30 },
                 { x: new Date(2004, 3, 6), y: 15 }, { x: new Date(2006, 3, 30), y: 65 },
                 { x: new Date(2008, 3, 8), y: 90 }, { x: new Date(2010, 3, 8), y: 85 }
        ];
        this.primaryXAxis = {
            valueType: 'DateTime',
            title: 'Sales Across Years',
            labelFormat: 'yMMM'
        };
        this.primaryYAxis = {
           title: 'Sales Amount in millions(USD)'
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}

>Note: To use datetime axis, we need to inject `DateTimeService` into the `@NgModule.providers` and
set the [`valueType`](../api/chart/axisDirective/#valuetype) of axis to `DateTime`.

## DateTimeCategory Axis

Date-time category axis is used to display the date-time values with non-linear intervals. For example, the
business days alone have been depicted in a week here.

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = data;
        this.primaryXAxis = {
              valueType: 'DateTimeCategory'
        };
        this.primaryYAxis = {
           title: 'Sales Amount in millions(USD)'
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}

>Note: To use datetime axis, we need to inject `DateTimeCategoryService` into the `@NgModule.providers` and
set the [`valueType`](../api/chart/axisDirective/#valuetype) of axis to `DateTimeCategory`.

### Range

Range for an axis, will be calculated automatically based on the provided data, you can also customize the range
of the axis using [`minimum`](../api/chart/axisDirective/#minimum), [`maximum`](../api/chart/axisDirective/#maximum)
and [`interval`](../api/chart/axisDirective/#interval) property of the axis.

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { dateData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = dateData;
        this.primaryXAxis = {
            valueType: 'DateTime',
            title: 'Sales Across Years',
            labelFormat: 'yMMM',
            minimum: new Date(2000, 6, 1),
            maximum: new Date(2010, 6, 1)
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}

### Interval Customization

Date time intervals can be customized by using the [`interval`](../api/chart/axisDirective/#interval) and
[`intervalType`](../api/chart/axisDirective/#intervaltype) properties of the axis.
For example, when you set interval as 2 and intervalType as years, it considers 2 years as interval.
DateTime axis supports following interval types,

* Auto
* Years
* Months
* Days
* Hours
* Minutes
* Seconds

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { dateData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = dateData;
        this.primaryXAxis = {
            valueType: 'DateTime',
            intervalType: 'Years'
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}

**Applying Padding to the Range**

Padding can be applied to the minimum and maximum extremes of the range by using the
[`rangePadding`](../api/chart/axisDirective/#rangepadding) property. Date time axis supports the following types
of padding,

* None
* Round
* Additional

**DateTime - None**

When the [`rangePadding`](../api/chart/axisDirective/#rangepadding) is set to `None`, minimum and maximum of the axis is based on the data.

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { dateData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = dateData;
        this.primaryXAxis = {
            valueType: 'DateTime',
            title: 'Sales Across Years',
            labelFormat: 'yMMM',
            rangePadding: 'None'
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}

**DateTime - Round**

When the [`rangePadding`](../api/chart/axisDirective/#rangepadding) is set to `Round`, minimum and maximum will be
rounded to the nearest possible value divisible by interval. For example, when the minimum is 15th Jan, interval is
1 and the interval type is ‘month’, then the axis minimum will be Jan 1st.

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { dateData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = dateData;
        this.primaryXAxis = {
            valueType: 'DateTime',
            title: 'Sales Across Years',
            labelFormat: 'yMMM',
            rangePadding: 'Round'
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}

**DateTime - Additional**

When the [`rangePadding`](../api/chart/axisDirective/#rangepadding) is set to `Additional`, interval of an axis will
be padded to the minimum and maximum of the axis.

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { dateData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = dateData;
        this.primaryXAxis = {
            valueType: 'DateTime',
            title: 'Sales Across Years',
            labelFormat: 'yMMM',
            rangePadding: 'Additional'
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}

## Label Format

You can format and parse the date to all globalize format using [`labelFormat`](../api/chart/axisDirective/#labelformat) property in an axis.

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { dateData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = dateData;
        this.primaryXAxis = {
            valueType: 'DateTime',
            title: 'Sales Across Years',
            labelFormat: 'yMd'
        };
        this.primaryYAxis = {
           title: 'Sales Amount in millions(USD)'
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}

The following table describes the result of applying some common date time formats to the labelFormat property

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

<!-- markdownlint-disable MD033 -->