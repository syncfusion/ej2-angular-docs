---
title: " Chart Numeric Axis | Angular "

component: "Chart"

description: "Numeric axis used to represent numeric values data in chart. we can customize the range, label format and ranga padding in numeric axis. "
---

<!-- markdownlint-disable MD036 -->

# Numeric Axis

You can use [numeric axis](https://www.syncfusion.com/angular-ui-components/angular-charts/chart-axis) to represent numeric values of data in chart. By default, the `valueType` of an axis is `Double`.

To known about numeric axis, you can check on this video:

`youtube:OWDrA0M8j7Q`

{% tab template="chart/axis/double", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' name='England'></e-series>
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
    { x: 1, y: 7 }, { x: 2, y: 1 }, { x: 3, y: 1 }, { x: 4, y: 14 }, { x: 5, y: 1 }, { x: 6, y: 10 },
    { x: 7, y: 8 }, { x: 8, y: 6 }, { x: 9, y: 10 }, { x: 10, y: 10 }, { x: 11, y: 16 }, { x: 12, y: 6 },
    { x: 13, y: 14 }, { x: 14, y: 7 }, { x: 15, y: 5 }, { x: 16, y: 2 }, { x: 17, y: 14 }, { x: 18, y: 7 },
    { x: 19, y: 7 }, { x: 20, y: 10 }];
        this.title = 'England - Run Rate';
    }

}
```

{% endtab %}

## Range

Range for an axis, will be calculated automatically based on the provided data, you can also customize the range
of the axis using [`minimum`](../api/chart/axisDirective/#minimum), [`maximum`](../api/chart/axisDirective/#maximum)
and [`interval`](../api/chart/axisDirective/#interval) property of the axis.

{% tab template="chart/axis/double", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' name='England'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.primaryXAxis = {
            valueType: 'Double',
            minimum: 1,
            maximum: 20,
            interval: 5,
            title: 'Overs'
        };
        this.chartData = chartData;
        this.title = 'England - Run Rate';
    }

}
```

{% endtab %}

## Range Padding

Padding can be applied to the minimum and maximum extremes of the axis range by using the
[`rangePadding`](../api/chart/axisDirective/#rangepadding) property. Numeric axis supports following types of padding.

* None
* Round
* Additional
* Normal
* Auto

**Numeric - None**

When the [`rangePadding`](../api/chart/axisDirective/#rangepadding) is set to `None`, minimum and maximum of an axis is based on the data.

{% tab template="chart/axis/double", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' name='England'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = chartData;
        this.primaryXAxis = {
            valueType: 'Double',
            title: 'Overs'
        };
        this.primaryYAxis = {
           title: 'Runs',
           valueType: 'Double',
           rangePadding: 'None'
        };
        this.title = 'England - Run Rate';
    }

}
```

{% endtab %}

**Numeric - Round**

When the [`rangePadding`](../api/chart/axisDirective/#rangepadding) is set to `Round`, minimum and maximum will be
rounded to the nearest possible value divisible by interval. For example, when the minimum is 3.5 and the interval
is 1, then the minimum will be rounded to 3.

{% tab template="chart/axis/double", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' name='England'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = chartData;
        this.primaryXAxis = {
            valueType: 'Double',
            title: 'Overs'
        };
        this.primaryYAxis = {
           title: 'Runs',
           valueType: 'Double',
           rangePadding: 'Round'
        };
        this.title = 'England - Run Rate';
    }

}
```

{% endtab %}

**Numeric - Additional**

When the [`rangePadding`](../api/chart/axisDirective/#rangepadding) is set to `Additional`, interval of an axis will
be padded to the minimum and maximum of the axis.

{% tab template="chart/axis/double", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' name='England'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = chartData;
        this.primaryXAxis = {
            valueType: 'Double',
            title: 'Overs'
        };
        this.primaryYAxis = {
           title: 'Runs',
           valueType: 'Double',
           rangePadding: 'Additional'
        };
        this.title = 'England - Run Rate';
    }

}
```

{% endtab %}

**Numeric - Normal**

When the [`rangePadding`](../api/chart/axisDirective/#rangepadding) is set to `Normal`, padding is applied to the axis
based on default range calculation.

{% tab template="chart/axis/double", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' name='England'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = chartData;
        this.primaryXAxis = {
            valueType: 'Double',
            title: 'Overs'
        };
        this.primaryYAxis = {
           title: 'Runs',
           valueType: 'Double',
           rangePadding: 'Normal'
        };
        this.title = 'England - Run Rate';
    }

}
```

{% endtab %}

**Numeric - Auto**

When the [`rangePadding`](../api/chart/axisDirective/#rangepadding) is set to `Auto`,horizontal numeric axis takes
None as padding calculation, while the vertical numeric axis takes Normal as padding calculation.

{% tab template="chart/axis/double", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' name='England'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = chartData;
        this.primaryXAxis = {
            valueType: 'Double',
            title: 'Overs'
        };
        this.primaryYAxis = {
           title: 'Runs',
           valueType: 'Double',
           rangePadding: 'Auto'
        };
        this.title = 'England - Run Rate';
    }

}
```

{% endtab %}

## Label Format

**Numeric Label Format**

Numeric labels can be formatted by using the [`labelFormat`](../api/chart/axisDirective/#labelformat) property.
Numeric labels supports all globalize format.

{% tab template="chart/axis/double", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { formatData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='formatData' type='Area' xName='x' yName='y' name='Product X' opacity=0.6></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public formatData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.formatData = formatData;
        this.primaryXAxis = {
            title: 'Year',
            edgeLabelPlacement: 'Shift'
        };
        this.primaryYAxis = {
           title: 'Sales Amount in Millions',
           labelFormat: 'c'
        };
        this.title = 'Average Sales Comparison';
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
<td>$1000.0</td>
<td>The Currency symbol is appended to number and number is rounded to 1 decimal place</td>
</tr>
<tr>
<td>1000</td>
<td>c2</td>
<td>$1000.00</td>
<td>The Currency symbol is appended to number and number is rounded to 2 decimal place</td>
</tr>
</table>

## GroupingSeparator

To separate groups of thousands, use [`useGroupingSeparator`](../api/chart/chartModel/#usegroupingseparator)
property in chart.

{% tab template="chart/axis/double", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { groupingData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'
     useGroupingSeparator=true>
        <e-series-collection>
            <e-series [dataSource]='groupingData' type='Column' xName='x' yName='y' name='Product X' opacity=0.6></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public groupingData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.groupingData = groupingData;
        this.primaryXAxis = {
            title: 'Quantity',
            edgeLabelPlacement: 'Shift'
        };
        this.primaryYAxis = {
           title: 'Sales Amount in Millions',
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}

## Custom Label Format

Axis also supports custom label format using placeholder like {value}°C, in which the value represent the axis
label e.g 20°C.

{% tab template="chart/axis/double", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { formatData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='formatData' type='Area' xName='x' yName='y' name='Product X' opacity=0.6></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public formatData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.formatData = formatData;
        this.primaryXAxis = {
            title: 'Year',
            edgeLabelPlacement: 'Shift'
        };
        this.primaryYAxis = {
           title: 'Sales Amount in Millions',
           labelFormat: '${value}k'
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}