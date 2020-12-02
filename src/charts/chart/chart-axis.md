
# Axis

Chart typically has two axis, which are used to measure and categorize data:
a horizontal or primary x axis and a vertical or primary y axis.

Vertical axis supports numerical and logarithmic scale. Horizontal axis supports
the following types of scale.

* Category
* Numeric
* DateTime
* Logarithmic

In addition to this, both the vertical and horizontal axis support inversed axis.

## Category Axis

Category axis are used to represent, the string values instead of numbers.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze'></e-series>
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
             { country: "USA", gold: 50, silver: 70, bronze: 45 },
             { country: "China", gold: 40, silver: 60, bronze: 55 },
             { country: "Japan", gold: 70, silver: 60, bronze: 50 },
             { country: "Australia", gold: 60, silver: 56, bronze: 40 },
             { country: "France", gold: 50, silver: 45, bronze: 35 },
             { country: "Germany", gold: 40, silver: 30, bronze: 22 },
             { country: "Italy", gold: 40, silver: 35, bronze: 37 },
             { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];
        this.primaryXAxis = {
            valueType: 'Category',
            title: 'Countries'
        };
        this.primaryYAxis = {
            minimum: 0, maximum: 80,
            interval: 20, title: 'Medals'
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

<!-- markdownlint-disable MD036 -->
**Positioning Axis Labels**
<!-- markdownlint-disable MD036 -->

By default, category labels are placed between the ticks in an axis, this can also be placed on ticks
using [`labelPlacement`](../api/chart/axisDirective/#labelplacement) property.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze'></e-series>
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
             { country: "USA", gold: 50, silver: 70, bronze: 45 },
             { country: "China", gold: 40, silver: 60, bronze: 55 },
             { country: "Japan", gold: 70, silver: 60, bronze: 50 },
             { country: "Australia", gold: 60, silver: 56, bronze: 40 },
             { country: "France", gold: 50, silver: 45, bronze: 35 },
             { country: "Germany", gold: 40, silver: 30, bronze: 22 },
             { country: "Italy", gold: 40, silver: 35, bronze: 37 },
             { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];
        this.primaryXAxis = {
            valueType: 'Category',
            title: 'Countries',
            labelPlacement: 'OnTicks'
        };
        this.primaryYAxis = {
            minimum: 0, maximum: 80,
            interval: 20, title: 'Medals'
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

>Note: To use category axis, we need to inject `CategoryService` into the `@NgModule.providers` and
set the [`valueType`](../api/chart/axisDirective/#valuetype) of axis to `Category`.

<!-- markdownlint-disable MD013 -->

## Numeric Axis

<!-- markdownlint-disable MD013 -->

You can use the numeric axis to represent numeric values of data in chart. By default, the `valueType` of an axis is `Double`.

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
             { x: 1, y: 7 }, { x: 2, y: 1 }, { x: 3, y: 1 },
             { x: 4, y: 14 }, { x: 5, y: 1 }, { x: 6, y: 10 },
             { x: 7, y: 8 }, { x: 8, y: 6 }, { x: 9, y: 10 },
             { x: 10, y: 10 }, { x: 11, y: 16 }, { x: 12, y: 6 },
             { x: 13, y: 14 }, { x: 14, y: 7 }, { x: 15, y: 5 },
             { x: 16, y: 2 }, { x: 17, y: 14 }, { x: 18, y: 7 },
             { x: 19, y: 7 }, { x: 20, y: 10 }
        ];
        this.primaryXAxis = {
            valueType: 'Double',
            title: 'Overs'
        };
        this.primaryYAxis = {
           title: 'Runs'
        };
        this.title = 'England - Run Rate';
    }

}
```

{% endtab %}

**Customize Numeric Range**

Range for an axis, will be calculated automatically based on the provided data, you can also customize the range of the axis using [`minimum`](../api/chart/axisDirective/#minimum), [`maximum`](../api/chart/axisDirective/#maximum) and [`interval`](../api/chart/axisDirective/#interval) property of the axis.

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
             { x: 1, y: 7 }, { x: 2, y: 1 }, { x: 3, y: 1 },
             { x: 4, y: 14 }, { x: 5, y: 1 }, { x: 6, y: 10 },
             { x: 7, y: 8 }, { x: 8, y: 6 }, { x: 9, y: 10 },
             { x: 10, y: 10 }, { x: 11, y: 16 }, { x: 12, y: 6 },
             { x: 13, y: 14 }, { x: 14, y: 7 }, { x: 15, y: 5 },
             { x: 16, y: 2 }, { x: 17, y: 14 }, { x: 18, y: 7 },
             { x: 19, y: 7 }, { x: 20, y: 10 }
        ];
        this.primaryXAxis = {
            valueType: 'Double',
            minimum: 1,
            maximum: 20,
            interval: 5,
            title: 'Overs'
        };
        this.primaryYAxis = {
           title: 'Runs',
           minimum: 0,
           maximum: 20,
           interval: 10
        };
        this.title = 'England - Run Rate';
    }

}
```

{% endtab %}

**Apply Padding to the Range**

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
             { x: 1, y: 7 }, { x: 2, y: 1 }, { x: 3, y: 1 },
             { x: 4, y: 14 }, { x: 5, y: 1 }, { x: 6, y: 10 },
             { x: 7, y: 8 }, { x: 8, y: 6 }, { x: 9, y: 10 },
             { x: 10, y: 10 }, { x: 11, y: 16 }, { x: 12, y: 6 },
             { x: 13, y: 14 }, { x: 14, y: 7 }, { x: 15, y: 5 },
             { x: 16, y: 2 }, { x: 17, y: 14 }, { x: 18, y: 7 },
             { x: 19, y: 7 }, { x: 20, y: 10 }
        ];
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

When the [`rangePadding`](../api/chart/axisDirective/#rangepadding) is set to `Round`, minimum and maximum will be rounded to the nearest possible value divisible by interval. For example, when the minimum is 3.5 and the interval is 1, then the minimum will be rounded to 3.

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
             { x: 1, y: 7 }, { x: 2, y: 1 }, { x: 3, y: 1 },
             { x: 4, y: 14 }, { x: 5, y: 1 }, { x: 6, y: 10 },
             { x: 7, y: 8 }, { x: 8, y: 6 }, { x: 9, y: 10 },
             { x: 10, y: 10 }, { x: 11, y: 16 }, { x: 12, y: 6 },
             { x: 13, y: 14 }, { x: 14, y: 7 }, { x: 15, y: 5 },
             { x: 16, y: 2 }, { x: 17, y: 14 }, { x: 18, y: 7 },
             { x: 19, y: 7 }, { x: 20, y: 10 }
        ];
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

When the [`rangePadding`](../api/chart/axisDirective/#rangepadding) is set to `Additional`, interval of an axis will be padded to the minimum and maximum of the axis.

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
             { x: 1, y: 7 }, { x: 2, y: 1 }, { x: 3, y: 1 },
             { x: 4, y: 14 }, { x: 5, y: 1 }, { x: 6, y: 10 },
             { x: 7, y: 8 }, { x: 8, y: 6 }, { x: 9, y: 10 },
             { x: 10, y: 10 }, { x: 11, y: 16 }, { x: 12, y: 6 },
             { x: 13, y: 14 }, { x: 14, y: 7 }, { x: 15, y: 5 },
             { x: 16, y: 2 }, { x: 17, y: 14 }, { x: 18, y: 7 },
             { x: 19, y: 7 }, { x: 20, y: 10 }
        ];
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

When the [`rangePadding`](../api/chart/axisDirective/#rangepadding) is set to `Normal`, padding is applied to the axis based on default range calculation.

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
             { x: 1, y: 7 }, { x: 2, y: 1 }, { x: 3, y: 1 },
             { x: 4, y: 14 }, { x: 5, y: 1 }, { x: 6, y: 10 },
             { x: 7, y: 8 }, { x: 8, y: 6 }, { x: 9, y: 10 },
             { x: 10, y: 10 }, { x: 11, y: 16 }, { x: 12, y: 6 },
             { x: 13, y: 14 }, { x: 14, y: 7 }, { x: 15, y: 5 },
             { x: 16, y: 2 }, { x: 17, y: 14 }, { x: 18, y: 7 },
             { x: 19, y: 7 }, { x: 20, y: 10 }
        ];
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

When the [`rangePadding`](../api/chart/axisDirective/#rangepadding) is set to `Auto`,horizontal numeric axis takes None as padding calculation, while the vertical numeric axis takes Normal as padding calculation.

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
             { x: 1, y: 7 }, { x: 2, y: 1 }, { x: 3, y: 1 },
             { x: 4, y: 14 }, { x: 5, y: 1 }, { x: 6, y: 10 },
             { x: 7, y: 8 }, { x: 8, y: 6 }, { x: 9, y: 10 },
             { x: 10, y: 10 }, { x: 11, y: 16 }, { x: 12, y: 6 },
             { x: 13, y: 14 }, { x: 14, y: 7 }, { x: 15, y: 5 },
             { x: 16, y: 2 }, { x: 17, y: 14 }, { x: 18, y: 7 },
             { x: 19, y: 7 }, { x: 20, y: 10 }
        ];
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

## DateTime Axis

 Date time axis uses date time scale and displays the date time values as axis labels in the specified format.

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

**Customizing Date Time Range**

Range for an axis, will be calculated automatically based on the provided data, you can also customize the range of the axis using [`minimum`](../api/chart/axisDirective/#minimum), [`maximum`](../api/chart/axisDirective/#maximum) and [`interval`](../api/chart/axisDirective/#interval) property of the axis.

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
            labelFormat: 'yMMM',
            minimum: new Date(2000, 6, 1),
            maximum: new Date(2010, 6, 1)
        };
        this.primaryYAxis = {
           title: 'Sales Amount in millions(USD)'
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}

**Date Time Intervals**

Date time intervals can be customized by using the [`interval`](../api/chart/axisDirective/#interval) and [`intervalType`](../api/chart/axisDirective/#intervaltype) properties of the axis.
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
            labelFormat: 'yMMM',
            minimum: new Date(2000, 6, 1),
            maximum: new Date(2010, 6, 1),
            interval: 2,
            intervalType: 'Years'
        };
        this.primaryYAxis = {
           title: 'Sales Amount in millions(USD)'
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}

**Applying Padding to the Range**

Padding can be applied to the minimum and maximum extremes of the range by using the
[`rangePadding`](../api/chart/axisDirective/#rangepadding) property. Date time axis supports the following types of padding,

* None
* Round
* Additional

**DateTime - None**

When the [`rangePadding`](../api/chart/axisDirective/#rangepadding) is set to `None`, minimum and maximum of the axis is based on the data.

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
            labelFormat: 'yMMM',
            rangePadding: 'None'
        };
        this.primaryYAxis = {
           title: 'Sales Amount in millions(USD)'
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}

**DateTime - Round**

When the [`rangePadding`](../api/chart/axisDirective/#rangepadding) is set to `Round`, minimum and maximum will be rounded to the nearest possible value divisible by interval. For example, when the minimum is 15th Jan, interval is 1 and the interval type is ‘month’, then the axis minimum will be Jan 1st.

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
            labelFormat: 'yMMM',
            rangePadding: 'Round'
        };
        this.primaryYAxis = {
           title: 'Sales Amount in millions(USD)'
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}

**DateTime - Additional**

When the [`rangePadding`](../api/chart/axisDirective/#rangepadding) is set to `Additional`, interval of an axis will be padded to the minimum and maximum of the axis.

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
            labelFormat: 'yMMM',
            rangePadding: 'Additional'
        };
        this.primaryYAxis = {
           title: 'Sales Amount in millions(USD)'
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}

>Note: To use datetime axis, we need to inject `DateTimeService` into the `@NgModule.providers` and set the [`valueType`](../api/chart/axisDirective/#valuetype) of axis to `DateTime`.

<!-- markdownlint-disable MD033 -->

## Logarithmic Axis

<!-- markdownlint-disable MD033 -->
Logarithmic axis uses logarithmic scale and it is very useful in visualizing data, when it has numeric values in both lower order of magnitude (eg: 10<sup>-6</sup>) and higher order of magnitude (eg: 10<sup>6</sup>).

{% tab template="chart/axis/log", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='Product X'></e-series>
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
                { x: new Date(1995, 0, 1), y: 80 }, { x: new Date(1996, 0, 1), y: 200 },
                { x: new Date(1997, 0, 1), y: 400 }, { x: new Date(1998, 0, 1), y: 600 },
                { x: new Date(1999, 0, 1), y: 700 }, { x: new Date(2000, 0, 1), y: 1400 },
                { x: new Date(2001, 0, 1), y: 2000 }, { x: new Date(2002, 0, 1), y: 4000 },
                { x: new Date(2003, 0, 1), y: 6000 }, { x: new Date(2004, 0, 1), y: 8000 },
                { x: new Date(2005, 0, 1), y: 11000 }
        ];
        this.primaryXAxis = {
            valueType: 'DateTime',
            title: 'Years',
            labelFormat: 'y'
        };
        this.primaryYAxis = {
           valueType: 'Logarithmic',
           title: 'Profit'
        };
        this.title = 'Product X Growth [1995-2005]';
    }

}
```

{% endtab %}

**Customize Logarithmic Range**

Range of an axis, will be calculated automatically based on the provided data, you can also customize the range of the axis using [`minimum`](../api/chart/axisDirective/#minimum), [`maximum`](../api/chart/axisDirective/#maximum) and [`interval`](../api/chart/axisDirective/#interval) property of the axis.

{% tab template="chart/axis/log", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='Product X'></e-series>
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
                { x: new Date(1995, 0, 1), y: 80 }, { x: new Date(1996, 0, 1), y: 200 },
                { x: new Date(1997, 0, 1), y: 400 }, { x: new Date(1998, 0, 1), y: 600 },
                { x: new Date(1999, 0, 1), y: 700 }, { x: new Date(2000, 0, 1), y: 1400 },
                { x: new Date(2001, 0, 1), y: 2000 }, { x: new Date(2002, 0, 1), y: 4000 },
                { x: new Date(2003, 0, 1), y: 6000 }, { x: new Date(2004, 0, 1), y: 8000 },
                { x: new Date(2005, 0, 1), y: 11000 }
        ];
        this.primaryXAxis = {
            valueType: 'DateTime',
            title: 'Years',
            labelFormat: 'y'
        };
        this.primaryYAxis = {
           valueType: 'Logarithmic',
           title: 'Profit',
           minimum: 100,
           maximum: 10000
        };
        this.title = 'Product X Growth [1995-2005]';
    }

}
```

{% endtab %}

**Logarithmic Base**

Logarithmic base can be customized by using the [`logBase`](../api/chart/axisDirective/#logbase) property of the axis. For example when the logBase is 5, the axis values follows 5<sup>-2</sup>, 5<sup>-1</sup>, 5<sup>0</sup>, 5<sup>1</sup>, 5<sup>2</sup> etc.

{% tab template="chart/axis/log", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='Product X'></e-series>
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
                { x: new Date(1995, 0, 1), y: 80 }, { x: new Date(1996, 0, 1), y: 200 },
                { x: new Date(1997, 0, 1), y: 400 }, { x: new Date(1998, 0, 1), y: 600 },
                { x: new Date(1999, 0, 1), y: 700 }, { x: new Date(2000, 0, 1), y: 1400 },
                { x: new Date(2001, 0, 1), y: 2000 }, { x: new Date(2002, 0, 1), y: 4000 },
                { x: new Date(2003, 0, 1), y: 6000 }, { x: new Date(2004, 0, 1), y: 8000 },
                { x: new Date(2005, 0, 1), y: 11000 }
        ];
        this.primaryXAxis = {
            valueType: 'DateTime',
            title: 'Years',
            labelFormat: 'y'
        };
        this.primaryYAxis = {
           valueType: 'Logarithmic',
           title: 'Profit',
           logBase: 2
        };
        this.title = 'Product X Growth [1995-2005]';
    }

}
```

{% endtab %}

**Logarithmic Interval**

Logarithmic axis interval can be customized by using the [`interval`](../api/chart/axisDirective/#interval) property of the axis. When the logarithmic base is 10 and logarithmic interval is 2, then the axis labels are placed at an interval of 10<sup>2</sup>. The default value of the interval is 1.

{% tab template="chart/axis/log", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='Product X'></e-series>
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
                { x: new Date(1995, 0, 1), y: 80 }, { x: new Date(1996, 0, 1), y: 200 },
                { x: new Date(1997, 0, 1), y: 400 }, { x: new Date(1998, 0, 1), y: 600 },
                { x: new Date(1999, 0, 1), y: 700 }, { x: new Date(2000, 0, 1), y: 1400 },
                { x: new Date(2001, 0, 1), y: 2000 }, { x: new Date(2002, 0, 1), y: 4000 },
                { x: new Date(2003, 0, 1), y: 6000 }, { x: new Date(2004, 0, 1), y: 8000 },
                { x: new Date(2005, 0, 1), y: 11000 }
        ];
        this.primaryXAxis = {
            valueType: 'DateTime',
            title: 'Years',
            labelFormat: 'y'
        };
        this.primaryYAxis = {
           valueType: 'Logarithmic',
           title: 'Profit',
           interval: 2
        };
        this.title = 'Product X Growth [1995-2005]';
    }

}
```

{% endtab %}

>Note: To use log axis, we need to inject `LogarithmicService` into the `@NgModule.providers` and set the [`valueType`](../api/chart/axisDirective/#valuetype) of axis to `Logarithmic`.

## Inversed Axis

<!-- markdownlint-disable MD033 -->

When an axis is inversed, highest value of the axis comes closer to origin and vice versa. To place an axis in inversed manner set this property
 [`isInversed`](./../api/chart/axisDirective/#isInversed) to true.

 {% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
     `<ejs-chart id="chart-container" [title]='title' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
         [legendSettings]='legend'>
            <e-series-collection>
                <e-series [dataSource]='data' type='Column' xName='x' yName='y' name='Years' [marker]='marker'>
                </e-series>
           </e-series-collection>
       </ejs-chart>`
       })

 export class AppComponent {
    public primaryXAxis: Object;
    public primaryYAxis: Object;
    public data: Object[];
    public marker: Object;
    public legend: Object;
    public title: string

    ngOnInit(): void {
    this.primaryXAxis = {
        valueType: 'Category',
        title: 'Years',
        opposedPosition: true,
        isInversed: true
    };

    this.primaryYAxis = {
        title: 'Exchange rate (INR per USD)',
        edgeLabelPlacement: 'Shift',
        labelIntersectAction: 'Rotate45',
        isInversed: true
    };

    this.data= [
        { x: 2008, y: 15.1 }, { x: 2009, y: 16 }, { x: 2010, y: 21.4 },
        { x: 2011, y: 18 }, { x: 2012, y: 16.2 }, { x: 2013, y: 11 },
        { x: 2014, y: 7.6 }, { x: 2015, y: 1.5 }
        ];

    this.marker = {
        dataLabel: {
            visible: true
        }
    };

    this.legend = {
        visible: true
    };

    this.title= 'Exchange Rate';
    }

}

```

{% endtab %}

## Label Format

**Numeric Label Format**

Numeric labels can be formatted by using the [`labelFormat`](../api/chart/axisDirective/#labelformat) property. Numeric labels supports all globalize format.

{% tab template="chart/axis/double", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' name='Product X' opacity=0.6></e-series>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y1' name='Product Y ' opacity=0.6></e-series>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y2' name='Product Z' opacity=0.6></e-series>
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
                { x: 1900, y: 4, y1: 2.6, y2: 2.8 }, { x: 1920, y: 3.0, y1: 2.8, y2: 2.5 },
                { x: 1940, y: 3.8, y1: 2.6, y2: 2.8 }, { x: 1960, y: 3.4, y1: 3, y2: 3.2 },
                { x: 1980, y: 3.2, y1: 3.6, y2: 2.9 }, { x: 2000, y: 3.9, y1: 3, y2: 2 }
        ];
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

**Datetime Label Format**

You can format and parse the date to all globalize format using [`labelFormat`](../api/chart/axisDirective/#labelformat) property in an axis.

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

**Custom Label Format**

Axis also supports custom label format using placeholder like {value}°C, in which the value represents the axis label. e.g 20°C.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze' ></e-series>
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
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.primaryYAxis = {
           minimum: 0, maximum: 80,
           interval: 20, title: 'Medals',
           labelFormat: '${value}K'
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

## Common Axis Features

**Axis Title**

You can add a title to the axis using [`title`](../api/chart/axisDirective/#title) property to provide quick information to the user about the data plotted in the axis.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze' ></e-series>
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
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.primaryYAxis = {
           minimum: 0, maximum: 80,
           interval: 20, title: 'Medals',
           labelFormat: '${value}K',
           titleStyle: {
            size: '16px', color: 'grey',
            fontFamily : 'Segoe UI', fontWeight : 'bold'
           }
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

**Label Customization**

The [`labelStyle`](../api/chart/axisDirective/#labelstyle) property of an axis provides options to customize the `color`, `font-family`, `font-size` and `font-weight` of the axis labels.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='silver' name='Silver'></e-series>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='bronze' name='Bronze' ></e-series>
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
                { country: "USA", gold: 50, silver: 70, bronze: 45 },
                { country: "China", gold: 40, silver: 60, bronze: 55 },
                { country: "Japan", gold: 70, silver: 60, bronze: 50 },
                { country: "Australia", gold: 60, silver: 56, bronze: 40 },
                { country: "France", gold: 50, silver: 45, bronze: 35 },
                { country: "Germany", gold: 40, silver: 30, bronze: 22 },
                { country: "Italy", gold: 40, silver: 35, bronze: 37 },
                { country: "Sweden", gold: 30, silver: 25, bronze: 27 }
        ];
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.primaryYAxis = {
           minimum: 0, maximum: 80,
           interval: 20, title: 'Medals',
           labelFormat: '${value}K',
           titleStyle: {
            size: '16px', color: 'grey',
            fontFamily : 'Segoe UI', fontWeight : 'bold'
           },
           labelStyle: {
            size: '14px', color: 'blue',
            fontFamily : 'Segoe UI', fontWeight : 'bold'
           }
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

**Edge Label Placement**

Labels with long text at the edges of an axis may appear partially in the chart. To avoid this, use [`edgeLabelPlacement`](../api/chart/axisDirective/#edgelabelplacement) property in axis, which moves the label inside the chart area for better appearance or hides it.

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
            labelFormat: 'yMMM',
            edgeLabelPlacement: 'Shift',
            minimum: new Date(2000, 6, 1),
            maximum: new Date(2010, 6, 1)
        };
        this.primaryYAxis = {
           title: 'Sales Amount in millions(USD)'
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}

**Grid Lines Customization**

You can customize the `width`, `color` and `dashArray` of the minor and major grid lines, using [`majorGridLines`](../api/chart/axisDirective/#majorgridlines) and [`minorGridLines`](../api/chart/axisDirective/#minorgridlines) properties in the axis.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Sales'></e-series>
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
                { x: 'Jan', y: 60 }, { x: 'Feb', y: 50 }, { x: 'Mar', y: 64 },
                { x: 'Apr', y: 63 }, { x: 'May', y: 81 }, { x: 'Jun', y: 64 },
                { x: 'Jul', y: 82 }, { x: 'Aug', y: 96 }, { x: 'Sep', y: 78 },
                { x: 'Oct', y: 60 }, { x: 'Nov', y: 58 }, { x: 'Dec', y: 56 }
        ];
        this.primaryXAxis = {
            valueType: 'Category',
            majorGridLines : {
               color : 'blue',
               width : 1
            },
            minorGridLines : {
               color : 'red',
               width : 0
            }
        };
        this.primaryYAxis = {
           title: 'Temperature (Fahrenheit)',
           majorGridLines : {
              color : 'blue',
              width : 1
           },
           minorGridLines : {
              color : 'red',
              width : 0
           }
        };
        this.title = 'Temperature flow over months';
    }

}
```

{% endtab %}

**Tick Lines Customization**

You can customize the  `width`, `color` and `size` of the minor and major tick lines, using [`majorTickLines`](../api/chart/axisDirective/#majorgridlines) and [`minorTickLines`](../api/chart/axisDirective/#minorgridlines) properties in the axis.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Sales'></e-series>
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
                { x: 'Jan', y: 60 }, { x: 'Feb', y: 50 }, { x: 'Mar', y: 64 },
                { x: 'Apr', y: 63 }, { x: 'May', y: 81 }, { x: 'Jun', y: 64 },
                { x: 'Jul', y: 82 }, { x: 'Aug', y: 96 }, { x: 'Sep', y: 78 },
                { x: 'Oct', y: 60 }, { x: 'Nov', y: 58 }, { x: 'Dec', y: 56 }
        ];
        this.primaryXAxis = {
            valueType: 'Category',
            majorTickLines : {
               color : 'blue',
               width : 5
            },
            minorTickLines : {
               color : 'red',
               width : 0
            }
        };
        this.primaryYAxis = {
           title: 'Temperature (Fahrenheit)',
           majorTickLines : {
              color : 'blue',
              width : 5
           },
           minorTickLines : {
              color : 'red',
              width : 0
           }
        };
        this.title = 'Temperature flow over months';
    }

}
```

{% endtab %}

**Place Axes at the Opposite Side**

<!-- markdownlint-disable MD012 -->
To place an axis opposite from its original position, set [`opposedPosition`](../api/chart/axisDirective/#opposedposition) property of the axis to true.
<!-- markdownlint-disable MD012 -->

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Sales'></e-series>
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
                { x: 'Jan', y: 60 }, { x: 'Feb', y: 50 }, { x: 'Mar', y: 64 },
                { x: 'Apr', y: 63 }, { x: 'May', y: 81 }, { x: 'Jun', y: 64 },
                { x: 'Jul', y: 82 }, { x: 'Aug', y: 96 }, { x: 'Sep', y: 78 },
                { x: 'Oct', y: 60 }, { x: 'Nov', y: 58 }, { x: 'Dec', y: 56 }
        ];
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.primaryYAxis = {
           title: 'Temperature (Fahrenheit)',
           opposedPosition: true
        };
        this.title = 'Temperature flow over months';
    }

}
```

{% endtab %}

## Multiple Axis

In addition to primary X and Y axis, we can add n number of axis to the chart. Series can be associated with
this axis, by mapping with axis's unique name.

{% tab template="chart/axis/multiple-panes", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-axes>
            <e-axis rowIndex=0 name='yAxis1' opposedPosition='true' title='Temperature (Celsius)' [majorGridLines]='majorGridLines' labelFormat='{value}°C'
                   [minimum]='24' [maximum]='36' [interval]='2' [lineStyle]='lineStyle'>
            </e-axis>
        </e-axes>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Germany'></e-series>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y1' yAxisName='yAxis1' name='Japan' [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public majorGridLines: Object;
    public primaryYAxis: Object;
    public lineStyle: Object;
    public marker: Object;
    ngOnInit(): void {
        this.chartData = [
                { x: 'Jan', y: 15, y1: 33 }, { x: 'Feb', y: 20, y1: 31 }, { x: 'Mar', y: 35, y1: 30 },
                { x: 'Apr', y: 40, y1: 28 }, { x: 'May', y: 80, y1: 29 }, { x: 'Jun', y: 70, y1: 30 },
                { x: 'Jul', y: 65, y1: 33 }, { x: 'Aug', y: 55, y1: 32 }, { x: 'Sep', y: 50, y1: 34 },
                { x: 'Oct', y: 30, y1: 32 }, { x: 'Nov', y: 35, y1: 32 }, { x: 'Dec', y: 35, y1: 31 }
        ];
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.primaryYAxis = {
           minimum: 0, maximum: 90, interval: 10,
           lineStyle: { width: 0 },
           title: 'Temperature (Fahrenheit)',
           labelFormat: '{value}°F'
        };
        this.majorGridLines = { width: 0};
        this.lineStyle = { width: 0};
        this.marker = {
            visible: true, width: 10, height: 10, border: { width: 2, color: '#F8AB1D' }
        }
        this.title = 'Weather Condition';
    }

}
```

{% endtab %}

## Smart Axis Labels

When the axis labels overlap with each other, you can use [`labelIntersectAction`](../api/chart/axisDirective/#labelintersectaction) property in the axis, to place them smartly.

When setting `labelIntersectAction` as `Hide`

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Internet'></e-series>>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public majorGridLines: Object;
    public primaryYAxis: Object;
    public lineStyle: Object;
    ngOnInit(): void {
        this.chartData = [
                { x: "South Korea", y: 39.4 }, { x: "India", y: 61.3 }, { x: "Pakistan", y: 20.4 },
                { x: "Germany", y: 65.1 }, { x: "Australia", y: 15.8 }, { x: "Italy", y: 29.2 },
                { x: "France", y: 44.6 }, { x: "Saudi Arabia", y: 9.7 }, { x: "Russia", y: 40.8 },
                { x: "Mexico", y: 31 }, { x: "Brazil", y: 75.9 }, { x: "China", y: 51.4 }
        ];
        this.primaryXAxis = {
           title: 'Countries',
           valueType: 'Category',
           labelIntersectAction: 'Hide'
        };
        this.primaryYAxis = {
           minimum: 0, maximum: 80, interval: 10,
           title: 'People(in millions)'
        };
        this.majorGridLines = { width: 0};
        this.lineStyle = { width: 0};
        this.title = 'Internet Users';
    }

}
```

{% endtab %}

When setting `labelIntersectAction` as `Rotate45`

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Internet'></e-series>>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public majorGridLines: Object;
    public primaryYAxis: Object;
    public lineStyle: Object;
    ngOnInit(): void {
        this.chartData = [
                { x: "South Korea", y: 39.4 }, { x: "India", y: 61.3 }, { x: "Pakistan", y: 20.4 },
                { x: "Germany", y: 65.1 }, { x: "Australia", y: 15.8 }, { x: "Italy", y: 29.2 },
                { x: "France", y: 44.6 }, { x: "Saudi Arabia", y: 9.7 }, { x: "Russia", y: 40.8 },
                { x: "Mexico", y: 31 }, { x: "Brazil", y: 75.9 }, { x: "China", y: 51.4 }
        ];
        this.primaryXAxis = {
           title: 'Countries',
           valueType: 'Category',
           labelIntersectAction: 'Rotate45'
        };
        this.primaryYAxis = {
           minimum: 0, maximum: 80, interval: 10,
           title: 'People(in millions)'
        };
        this.majorGridLines = { width: 0};
        this.lineStyle = { width: 0};
        this.title = 'Internet Users';
    }

}
```

{% endtab %}

When setting `labelIntersectAction` as `Rotate90`

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Internet'></e-series>>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public majorGridLines: Object;
    public primaryYAxis: Object;
    public lineStyle: Object;
    ngOnInit(): void {
        this.chartData = [
                { x: "South Korea", y: 39.4 }, { x: "India", y: 61.3 }, { x: "Pakistan", y: 20.4 },
                { x: "Germany", y: 65.1 }, { x: "Australia", y: 15.8 }, { x: "Italy", y: 29.2 },
                { x: "France", y: 44.6 }, { x: "Saudi Arabia", y: 9.7 }, { x: "Russia", y: 40.8 },
                { x: "Mexico", y: 31 }, { x: "Brazil", y: 75.9 }, { x: "China", y: 51.4 }
        ];
        this.primaryXAxis = {
           title: 'Countries',
           valueType: 'Category',
           labelIntersectAction: 'Rotate90'
        };
        this.primaryYAxis = {
           minimum: 0, maximum: 80, interval: 10,
           title: 'People(in millions)'
        };
        this.majorGridLines = { width: 0};
        this.lineStyle = { width: 0};
        this.title = 'Internet Users';
    }

}
```

{% endtab %}

## Strip Lines

EJ2 chart supports horizontal and vertical strip lines and customization of stripline in both orientation.
To use Stripline in axis, we need to inject `StriplineService` into the `@NgModule.providers`

**Horizontal Strip lines**

You can create horizontal stripline by adding the <code>stripline</code> in the vertical axis and set <code>visible</code> option to true.
Striplines are rendered in the specified start to end range and you can add more than one stripline for an axis.

{% tab template= "chart/axis/strip-line" %}


```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Internet'></e-series>>
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
                 {x: 1, y: 20},{x: 2, y: 22},{x: 3, y: 0},{x: 4, y: 12},{x: 5, y: 5},
                 {x: 6, y: 15},{x: 7, y: 6},{x: 8, y: 12},{x: 9, y: 20},{x: 10, y: 7}];
        this.primaryYAxis = {
           title: 'Runs',
            stripLines:[
           { start: 15, end: 22, text: 'Good', color: '#ff512f', visible: true, zIndex: 'Behind', opacity: 0.5 }
            { start: 8, end: 15, text: 'Medium', color: 'pink', opacity: 0.5, visible: true, zIndex: 'Behind' }
            { start: 0, end: 8, text:'Not enough', color: 'skyblue', opacity: 0.5, visible: true, zIndex: 'Behind' }]
        };
        this.primaryXAxis: {
            title: 'Overs'
        },
        this.title = 'India Vs Australia 1st match';
    }

}
```

{% endtab %}

**Vertical Striplines**

You can create vertical stripline by adding the <code>stripline</code> in the horizontal axis and set <code>visible</code> option to true.
Striplines are rendered in the specified start to end range and you can add more than one stripline for an axis.

{% tab template= "chart/axis/strip-line" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Internet'></e-series>>
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
                 {x: 1, y: 20},{x: 2, y: 22},{x: 3, y: 0},{x: 4, y: 12},{x: 5, y: 5},
                 {x: 6, y: 15},{x: 7, y: 6},{x: 8, y: 12},{x: 9, y: 20},{x: 10, y: 7}];
        this.primaryYAxis = {
           title: 'Runs',
        };
        this.primaryXAxis: {
            stripLines:[
            {start: 0, end: 5, text: 'powerplay 1', color: 'red', visible: true, opacity: 0.5, rotation: 45, testStyle: { size: 20, color: 'black'}},
            {start: 5, end: 10, text: 'powerplay 2', color: 'blue', visible: true, opacity: 0.5, rotation: 45, testStyle: { size: 20, color: 'black'}},
        ],
            title: 'Overs'
        },
        this.title = 'India Vs Australia 1st match';
    }

}
```

{% endtab %}

**Customize the strip line**

Starting value in specific strip line can be customized by <code>start</code> property in strip line. Similarly, ending value is customized by <code>end</code>. It can be also set for starting from the corresponding origin of the axis by
<code>startFromOrigin</code>. Size of the strip line is customized by <code>size</code>. Border for the stripline is customized by <code>border</code>. Order of the strip line such that whether it should be rendered in behind or over the series elements
is customized by <code>zIndex</code>.

{% tab template= "chart/axis/strip-line" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Internet'></e-series>>
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
                 {x: 1, y: 20},{x: 2, y: 22},{x: 3, y: 0},{x: 4, y: 12},{x: 5, y: 5},
                 {x: 6, y: 15},{x: 7, y: 6},{x: 8, y: 12},{x: 9, y: 20},{x: 10, y: 7}];
        this.primaryYAxis = {
           title: 'Runs',
        };
        this.primaryXAxis: {
            stripLines:[
            { startFromOrigin: true, size: 4, zIndex: 'Behind', opacity: 0.5, border: { width: 2, color:'red'}}
        ],
            title: 'Overs'
        },
        this.title = 'India Vs Australia 1st match';
    }

}
```

{% endtab %}

**Customize the stripline text**

You can customize the text rendered in stripline by <code>textStyle</code> property. Rotation of the strip line text can be changed by <code>rotation</code> property.
Horizontal and vertical alignment of stripline text can be changed by `horizontalAlignment`and `verticalAlignment` property.

{% tab template= "chart/axis/strip-line" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Internet'></e-series>>
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
                 {x: 1, y: 20},{x: 2, y: 22},{x: 3, y: 0},{x: 4, y: 12},{x: 5, y: 5},
                 {x: 6, y: 15},{x: 7, y: 6},{x: 8, y: 12},{x: 9, y: 20},{x: 10, y: 7}];
        this.primaryYAxis = {
           title: 'Runs',
        };
        this.primaryXAxis: {
           stripLines:[
            { startFromOrigin: true, size: 4, zIndex: 'Behind', opacity: 0.5,  text: 'Good', verticalAlignment: 'Middle', horizontalAlignment: 'Middle', rotation: 90, textStyle: { size: 15}},
            { start: 5, end: 8, verticalAlignment: 'Start', horizontalAlignment: 'End', rotation: 45, text: 'Poor'}
        ],
            title: 'Overs'
        },
        this.title = 'India Vs Australia 1st match';
    }

}

```

{% endtab %}