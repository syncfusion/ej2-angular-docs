---
title: "Chart Types | Angular "
component: "Chart"
description: "Essential JS 2 Chart  chart supports 32 types of series and also supports different tpes customizations for each type of chart."
---

# Chart Types

Essential JS 2 Chart supports 32 types of series.

<!-- markdownlint-disable MD036 -->
To know about Angular Chart types, you can check on this video:

`youtube:TvA2mFAFDgY`

## Line Charts

<!-- markdownlint-disable MD036 -->

**Line**

To render a line series, use series [`type`](../api/chart/seriesDirective/#type) as `Line` and
inject `LineSeriesService` into the `@NgModule.providers`.

{% tab template="chart/series/line", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { lineData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis'
    [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public chartData: Object[];
    public title: string;
     public primaryXAxis: Object;
      public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = lineData;
        this.primaryXAxis = {
            interval: 1
        };
        this.primaryYAxis =
        {
            title: 'Expense',
        },
        this.title = 'Efficiency of oil-fired power production';
    }

}
```

{% endtab %}

**Step Line**

To render a step line series, use series [`type`](../api/chart/seriesDirective/#type) as `StepLine` and inject `StepLineSeriesService` into
the `@NgModule.providers`.

{% tab template="chart/series/line", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' name='USA' width=2 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = data;
        this.title = 'CO2 - Intensity Analysis';
    }

}
```

{% endtab %}

**Stacked Line**

To render a stacked line series, use series [`type`](../api/chart/seriesModel/#type-string) as
`StackingLine` and inject `StackingLineSeriesService`  into the `@NgModule.providers`.

{% tab template="chart/series/line", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data0, data1, data2, data3} from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis'>
        <e-series-collection>
            <e-series [dataSource]='chartData1' type='StackingLine' xName='x' yName='y' name='John' width='2' [marker]='marker' dashArray='5,1'> </e-series>
            <e-series [dataSource]='chartData2' type='StackingLine' xName='x' yName='y' name='Peter' width='2' [marker]='marker' dashArray='5,1'> </e-series>
            <e-series [dataSource]='chartData3' type='StackingLine' xName='x' yName='y' name='Steve' width='2' [marker]='marker' dashArray='5,1'> </e-series>
            <e-series [dataSource]='chartData4' type='StackingLine' xName='x' yName='y' name='Charle' width='2' [marker]='marker' dashArray='5,1'> </e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public marker: Object;
    public series: Object;
    public chartData1: Object[]; public chartData2: Object[]; public chartData3: Object[];
    public chartData4: Object[];
    ngOnInit(): void {
        this.primaryXAxis = {
            interval: 1, valueType: 'Category'
        };
        this.primaryYAxis =
        {
            title: 'Expense',
            interval: 100,
            labelFormat: '${value}',
        },
        this.chartData1 = data0;
        this.chartData2 = data1;
        this.chartData3 = data2;
        this.chartData4 = data3;
        this.marker = { visible: true };
    }

}
```

{% endtab %}

**100% Stacked Line**

To render a 100% stacked line series, use series [`type`](../api/chart/seriesModel/#type-string) as
`StackingLine100` and inject `StackingLineSeriesService`  into the `@NgModule.providers`.

{% tab template="chart/series/line", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data0, data1, data2, data3} from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis'>
        <e-series-collection>
            <e-series [dataSource]='chartData1' type='StackingLine100' xName='x' yName='y' name='John' width='2' [marker]='marker' dashArray='5,1'> </e-series>
            <e-series [dataSource]='chartData2' type='StackingLine100' xName='x' yName='y' name='Peter' width='2' [marker]='marker' dashArray='5,1'> </e-series>
            <e-series [dataSource]='chartData3' type='StackingLine100' xName='x' yName='y' name='Steve' width='2' [marker]='marker' dashArray='5,1'> </e-series>
            <e-series [dataSource]='chartData4' type='StackingLine100' xName='x' yName='y' name='Charle' width='2' [marker]='marker' dashArray='5,1'> </e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public marker: Object;
    public series: Object;
    public chartData1: Object[]; public chartData2: Object[]; public chartData3: Object[];
    public chartData4: Object[];
    ngOnInit(): void {
        this.primaryXAxis = {
            interval: 1, valueType: 'Category'
        };
        this.primaryYAxis =
        {
            title: 'Expense',
            interval: 100,
            labelFormat: '${value}',
        },
        this.chartData1 = data0;
        this.chartData2 = data1;
        this.chartData3 = data2;
        this.chartData4 = data3;
        this.marker = { visible: true };
    }

}
```

{% endtab %}

**Spline**

To render a spline series, use series [`type`](../api/chart/seriesDirective/#type) as `Spline` and inject `SplineSeriesService` into the `@NgModule.providers`.

{% tab template="chart/series/line", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { splineData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Spline' xName='x' yName='y' name='London' width=2 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public marker: Object;
    ngOnInit(): void {
        this.chartData = splineData;
        this.primaryXAxis = {
           title: 'Month',
           valueType: 'Category'
        };
        this.marker = { visible: true, width: 10, height: 10 };
        this.title = 'Climate Graph-2012';
    }

}
```

{% endtab %}

**Spline Area**

To render a spline series, use series [`type`](../api/chart/seriesDirective/#type) as `Spline` and
inject `SplineAreaSeriesService` into the `@NgModule.providers`.

{% tab template="chart/series/line", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { splineData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='SplineArea' xName='x' yName='y' name='London' width=2 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public marker: Object;
    ngOnInit(): void {
        this.chartData = splineData;
        this.primaryXAxis = {
           title: 'Month',
           valueType: 'Category'
        };
        this.marker = { visible: true, width: 10, height: 10 };
        this.title = 'Climate Graph-2012';
    }

}
```

{% endtab %}

**Multicolored Line**

To render a multicolored line series, use the series type as `MultiColoredLine`, and inject the
`MultiColoredLineSeriesService` into the `@NgModule.providers`.
Here, the individual colors to the data can be mapped by using `pointColorMapping`.

{% tab template="chart/series/line", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { splineData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='MultiColoredLine' xName='x' yName='y' name='London' width=2 [marker]='marker'
            pointColorMapping= 'color'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public chartData: Object[];
    public title: string;
    public marker: Object;
    ngOnInit(): void {
        this.chartData = [{ x: 2005, y: 28 , color: 'red'}, { x: 2006, y: 25, color:'green'},
        { x: 2007, y: 26, color: '#ff0097' }, { x: 2008, y: 27, color: 'crimson' },
        { x: 2009, y: 32, color: 'blue' }, { x: 2010, y: 35 ,color: 'darkorange'}];
        this.marker = { visible: true, width: 10, height: 10 };
        this.title = 'Climate Graph-2012';
    }

}
```

{% endtab %}

**Customization of Line Charts**

`stroke`, `stroke-width` and `dashArray` of all line type series can be customized by using [`fill`](../api/chart/seriesDirective/#fill),
[`width`](../api/chart/seriesDirective/#width) and [`dashArray`](../api/chart/seriesDirective/#dasharray) properties.

{% tab template="chart/series/line", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { lineData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='x' yName='y' name='India' fill='green' width=3 dashArray='5,5' [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = lineData;
        this.marker = { visible: true };
        this.title = 'Efficiency of oil-fired power production';
    }

}
```

{% endtab %}

## Area Charts

**Area**

To render a area series, use series [`type`](../api/chart/seriesDirective/#type) as `Area` and inject `AreaSeriesService` into the `@NgModule.providers`.

{% tab template="chart/series/area", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { areaData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' name='Product A' fill='#69D2E7' opacity=0.6></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = areaData;
        this.primaryXAxis = {
           title: 'Year',
           minimum: 1900, maximum: 2000, interval: 10,
           edgeLabelPlacement: 'Shift'
        };
        this.primaryYAxis = {
           minimum: 2, maximum: 5, interval: 0.5,
           title: 'Sales Amount in Millions'
        };
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}

**Range Area**

To render a range area series, use series [`type`](../api/chart/seriesDirective/#type)
as `RangeArea` and inject `RangeAreaSeriesService`  into the `@NgModule.providers`.

{% tab template="chart/series/area", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { rangeData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='RangeArea' xName='x' high='high' low='low' name='India' fill='#69D2E7' opacity=0.6></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = rangeData;
        this.primaryXAxis = {
           title: 'Month',valueType: 'Category',
           edgeLabelPlacement: 'Shift'
        };
        this.primaryYAxis = {
            title: 'Temperature(Celsius)',
            minimum: 0, maximum: 20
        };
        this.title = 'Maximum and Minimum Temperature'
    }
}

```

{% endtab %}

**Stacked Area**

To render a stacked area series, use series [`type`](../api/chart/seriesDirective/#type) as `StackingArea` and inject `StackingAreaSeriesService`
into the `@NgModule.providers`.

{% tab template="chart/series/area", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { stackedData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StackingArea' xName='x' yName='y' name='Organic'></e-series>
            <e-series [dataSource]='chartData' type='StackingArea' xName='x' yName='y1' name='Fair-trade'></e-series>
            <e-series [dataSource]='chartData' type='StackingArea' xName='x' yName='y2' name='Veg Alternatives'></e-series>
            <e-series [dataSource]='chartData' type='StackingArea' xName='x' yName='y3' name='Others'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = stackedData;
        this.primaryXAxis = {
            valueType: 'DateTime'
        };
        this.title = 'Trend in Sales of Ethical Produce';
    }

}
```

{% endtab %}

**100% Stacked Area**

To render a 100% stacked area series, use series [`type`](../api/chart/seriesDirective/#type) as `StackingArea100` and inject
`StackingAreaSeriesService` into the `@NgModule.providers`.

{% tab template="chart/series/area", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { percentData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StackingArea100' xName='x' yName='y' name='USA'></e-series>
            <e-series [dataSource]='chartData' type='StackingArea100' xName='x' yName='y1' name='UK'></e-series>
            <e-series [dataSource]='chartData' type='StackingArea100' xName='x' yName='y2' name='Canada'></e-series>
            <e-series [dataSource]='chartData' type='StackingArea100' xName='x' yName='y3' name='China'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = percentData;
        this.primaryXAxis = {
            valueType: 'DateTime'
        };
        this.title = 'Annual Temperature Comparison';
    }

}
```

{% endtab %}

**Step Area**

To render a step area series, use series [`type`](../api/chart/seriesDirective/#type) as `StepArea` and inject
`StepAreaSeriesService` into the `@NgModule.providers`.

{% tab template="chart/series/area", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { stepData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StepArea' xName='x' yName='y' name='England'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = stepData;
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

**Stacked Step Area**

To render a stacked step area series, use series `type` as `StackingStepArea` and inject
`StackingStepAreaSeriesService` into the `@NgModule.providers`.

{% tab template="chart/series/area", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { stackedStepData1, stackedStepData2 } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container">
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StackingStepArea' xName='x' yName='y'></e-series>
            <e-series [dataSource]='chartData2' type='StackingStepArea' xName='x' yName='y'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public chartData: Object[];
    public chartData2: Object[];
    ngOnInit(): void {
        this.chartData = stackedStepData1;
        this.chartData2 = stackedStepData2;
    }
}
```

{% endtab %}

**Multicolored area**

To render a multicolored area series, use the series type as `MultiColoredArea`, and
inject the `MultiColoredAreaSeriesService` into the `@NgModule.providers`.
The required `segments` of the series can be customized using the `value`, `color`, and `dashArray`.

{% tab template="chart/series/area", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { stepData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='MultiColoredArea' xName='x' yName='y' name='England'
            segmentAxis='X' [segments]='segments'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public segments: Object[];
    ngOnInit(): void {
        this.chartData = [{ x: 2005, y: 28 }, { x: 2006, y: 25}, { x: 2007, y: 26 }, { x: 2008, y: 27 },
        { x: 2009, y: 32}, { x: 2010, y: 35 }, { x: 2011, y: 25 }];
        this.title = 'England - Run Rate';
        this.segments =[{
                    value: 2007,
                    color: 'blue'
                }, {
                    value: 2009,
                    color: 'lightgreen'
                }, {
                    color: 'orange'
        }];
    }

}
```

{% endtab %}

**Customization of Area Charts**

`fill`, `border` and `dashArray` of all area type series can be customized
using [`fill`](../api/chart/seriesDirective/#fill),
[`border`](../api/chart/seriesDirective/#border)
and [`dashArray`](../api/chart/seriesDirective/#dasharray) properties.

{% tab template="chart/series/area", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { areaData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' name='Product A' fill='green' width=2 dashArray='5,5' [border]='border' opacity=0.6></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public chartData: Object[];
    public title: string;
    public border: Object;
    ngOnInit(): void {
        this.border = {
          color: 'red',
          width: 2
        };
        this.chartData = areaData;
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}

## Column Charts

**Column**

To render a column series, use series [`type`](../api/chart/seriesDirective/#type) as `Column` and inject `ColumnSeriesService` into the `@NgModule.providers`.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { columnData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = columnData;
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

**Range Column**

To render a range column series, use series [`type`](../api/chart/seriesDirective/#type) as `RangeColumn` and inject `RangeColumnSeriesService`
into the `@NgModule.providers`.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data1 } from 'datasource.ts';
import { data2 } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='data1' type='RangeColumn' xName='x' low='low' high='high'></e-series>
            <e-series [dataSource]='data2' type='RangeColumn' xName='x' low='low' high='high'></e-series>
        </e-series-collection>
    </ejs-chart>`
})

export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public data1: Object[];
    public data2: Object[];
    ngOnInit(): void {
        this.data1 = data1;
        this.data2 = data2;
        this.primaryXAxis = {
            title: 'month',
            valueType: 'Category'
        };
        this.title = 'Maximum and minimum Temperature';
    }
}
```

{% endtab %}

**Stacked Column**

To render a stacked column series, use series [`type`](../api/chart/seriesDirective/#type) as `StackingColumn` and inject
`StackingColumnSeriesService` into the `@NgModule.providers`.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { stackedData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StackingColumn' xName='x' yName='y' name='UK'></e-series>
            <e-series [dataSource]='chartData' type='StackingColumn' xName='x' yName='y1' name='Germany'></e-series>
            <e-series [dataSource]='chartData' type='StackingColumn' xName='x' yName='y2' name='France'></e-series>
            <e-series [dataSource]='chartData' type='StackingColumn' xName='x' yName='y3' name='Italy'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = stackedData;
        this.primaryXAxis = {
            title: 'Years',
            interval: 1,
            valueType: 'Category'
        };
        this.title = 'Mobile Game Market by Country';
    }

}
```

{% endtab %}

**100% Stacked Column**

To render a 100% stacked column series, use series [`type`](../api/chart/seriesDirective/#type) as `StackingColumn100` and
inject `StackingColumnSeriesService` into the `@NgModule.providers`.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { percentData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StackingColumn100' xName='x' yName='y' name='UK'></e-series>
            <e-series [dataSource]='chartData' type='StackingColumn100' xName='x' yName='y1' name='Germany'></e-series>
            <e-series [dataSource]='chartData' type='StackingColumn100' xName='x' yName='y2' name='France'></e-series>
            <e-series [dataSource]='chartData' type='StackingColumn100' xName='x' yName='y3' name='Italy'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = percentData;
        this.primaryXAxis = {
            title: 'Years',
            interval: 1,
            valueType: 'Category'
        };
        this.title = 'Gross Domestic Product Growth';
    }

}
```

{% endtab %}

**Stacking Group**

<!-- markdownlint-disable MD010 -->

You can use the [`stackingGroup`](../api/chart/seriesDirective/#stackinggroup) property to group the stacked columns and 100% stacked columns.
Columns with same group name are stacked on top of each other.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart style='display:block;' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'>
	    <e-series-collection>
	        <e-series stackingGroup="A" [dataSource]='data' type='StackingColumn' xName='x' yName='y' name='UK' width='2'> </e-series>
		    <e-series stackingGroup="B" [dataSource]='data1' type='StackingColumn' xName='x' yName='y' name='Germany' width='2'> </e-series>
		    <e-series stackingGroup="A" [dataSource]='data2' type='StackingColumn' xName='x' yName='y' name='France' width='2'> </e-series>
		    <e-series stackingGroup="B" [dataSource]='data3' type='StackingColumn' xName='x' yName='y' name='Italy' width='2'> </e-series>
	    </e-series-collection>
	</ejs-chart>`
})
export class AppComponent implements OnInit {
  public data: Object[];
  public data1: Object[];
  public data2: Object[];
  public data3: Object[];
  public primaryXAxis: Object;
  public primaryYAxis: Object;
    ngOnInit(): void {
        this.primaryXAxis = {
            majorGridLines: { width: 0 },
            minorGridLines: { width: 0 },
            majorTickLines: { width: 0 },
            minorTickLines: { width: 0 },
            interval: 1,
            lineStyle: { width: 0 },
            valueType: "Category"
        };
        this.primaryYAxis = {
            title: "Sales",
            lineStyle: { width: 0 },
            majorTickLines: { width: 0 },
            majorGridLines: { width: 1 },
            minorGridLines: { width: 1 },
            minorTickLines: { width: 0 },
            labelFormat: "{value}B"
        };
    this.data = [
    { x: "2014", y: 111.1 },
    { x: "2015", y: 127.3 },
    { x: "2016", y: 143.4 },
    { x: "2017", y: 159.9 }
  ];
  this.data1 = [
    { x: "2014", y: 76.9 },
    { x: "2015", y: 99.5 },
    { x: "2016", y: 121.7 },
    { x: "2017", y: 142.5 }
  ];
  this.data2 = [
    { x: "2014", y: 66.1 },
    { x: "2015", y: 79.3 },
    { x: "2016", y: 91.3 },
    { x: "2017", y: 102.4 }
  ];
  this.data3 = [
    { x: "2014", y: 34.1 },
    { x: "2015", y: 38.2 },
    { x: "2016", y: 44.0 },
    { x: "2017", y: 51.6 }
  ];
}

}
```

{% endtab %}

**Customization of Column Charts**

<!-- markdownlint-disable MD013 -->
`fill` and `border` of all column type series can be
customized using [`fill`](../api/chart/seriesDirective/#fill) and [`border`](../api/chart/seriesDirective/#border) properties.
For customizing a specify point, please refer the
[`pointRender`](./chart-appearance/#point-level-customization).

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { columnData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' fill='red' [border]='border'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public border: Object;
    ngOnInit(): void {
        this.border = {
            color: 'green',
            width: 2
        };
        this.chartData = columnData;
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

## Bar Charts

**Bar**

To render a bar series, use series [`type`](../api/chart/seriesDirective/#type) as `Bar` and inject `BarSeriesService` into the `@NgModule.providers`.

{% tab template="chart/series/bar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { barData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Bar' xName='x' yName='y' name='India'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = barData;
        this.title = 'Unemployment rate (%)';
    }

}
```

{% endtab %}

**Stacked bar**

To render a stacked bar series, use series [`type`](../api/chart/seriesDirective/#type) as `StackingBar` and
inject `StackingBarSeriesService` into the `@NgModule.providers`.

{% tab template="chart/series/bar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { stackData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StackingBar' xName='x' yName='y' name='Apple'></e-series>
            <e-series [dataSource]='chartData' type='StackingBar' xName='x' yName='y1' name='Orange'></e-series>
            <e-series [dataSource]='chartData' type='StackingBar' xName='x' yName='y2' name='Wastage'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = stackData;
        this.primaryXAxis = {
            valueType: 'Category',
            title: 'Months'
        };
        this.title = 'Sales Comparison';
    }

}
```

{% endtab %}

**100% Stacked Bar**

To render a 100% stacked bar series, use series [`type`](../api/chart/seriesDirective/#type) as `StackingBar100` and
inject `StackingBarSeriesService` into the `@NgModule.providers`.

{% tab template="chart/series/bar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { stackData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StackingBar100' xName='x' yName='y' name='Apple'></e-series>
            <e-series [dataSource]='chartData' type='StackingBar100' xName='x' yName='y1' name='Orange'></e-series>
            <e-series [dataSource]='chartData' type='StackingBar100' xName='x' yName='y2' name='Wastage'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = stackData;
        this.primaryXAxis = {
            valueType: 'Category',
            title: 'Months'
        };
        this.title = 'Sales Comparison';
    }

}
```

{% endtab %}

**Stacking Group**

You can use the [`stackingGroup`](../api/chart/seriesDirective/#stackinggroup) property to group the stacked
bar and 100% stacked bar. Columns with same group name are stacked on top of each other.

{% tab template="chart/series/bar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { groupData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StackingBar' xName='x' yName='y' name='John' stackingGroup='JohnandAndrew'></e-series>
            <e-series [dataSource]='chartData' type='StackingBar' xName='x' yName='y1' name='Andrew' stackingGroup='JohnandAndrew'></e-series>
            <e-series [dataSource]='chartData' type='StackingBar' xName='x' yName='y2' name='Thomas' stackingGroup='ThomasandMichael'></e-series>
            <e-series [dataSource]='chartData' type='StackingBar' xName='x' yName='y3' name='Michael' stackingGroup='ThomasandMichael'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = groupData;
        this.title = 'Sales by year';
    }

}
```

{% endtab %}

**Customization of Bar Charts**

`fill` and `border` of all bar type series can be
customized using [`fill`](../api/chart/seriesDirective/#fill) and [`border`](../api/chart/seriesDirective/#border).
For customizing a specify point, please refer the [`pointRender`](./appearance/#point-level-customization).

{% tab template="chart/series/bar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { barData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Bar' xName='x' yName='y' name='India' fill='red' [border]='border'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public chartData: Object[];
    public title: string;
    public border: Object;
    ngOnInit(): void {
        this.border = {
            color: 'green',
            width: 2
        };
        this.chartData = barData;
        this.title = 'Unemployment rate (%)';
    }

}
```

{% endtab %}

## Scatter Charts

To render a scatter series, use series [`type`](../api/chart/seriesDirective/#type) as `Scatter` and inject `ScatterSeriesService` into the `@NgModule.providers`.

{% tab template="chart/series/scatter", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { ChartData } from './chartdata.service';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='series1' type='Scatter' xName='x' yName='y' name='Male' opacity=0.7 [marker]='marker'></e-series>
            <e-series [dataSource]='series2' type='Scatter' xName='x' yName='y' name='Female' opacity=0.7 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public series1: Object;
    public series2: Object;
    public marker: Object;
    ngOnInit(): void {
        this.primaryXAxis = {
            title: 'Height (cm)',
            minimum: 120, maximum: 180,
            edgeLabelPlacement: 'Shift',
            labelFormat: '{value}cm'
        };
        this.primaryYAxis = {
            title: 'Weight (kg)',
            minimum: 60, maximum: 90,
            labelFormat: '{value}kg',
            rangePadding: 'None'
        };
        this.title = 'Height Vs Weight';
        this.marker = {  width: 10, height: 10 };
        this.series1 = ChartData.prototype.getScatterData().series1;
        this.series2 = ChartData.prototype.getScatterData().series2;
    }

}
```

{% endtab %}

<!-- markdownlint-disable MD018 -->

##Bubble Chart

To render a bubble series, use series [`type`](../api/chart/seriesDirective/#type) as `Bubble` and inject `BubbleSeriesService` into the `@NgModule.providers`.

{% tab template="chart/series/bubble", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { bubbleData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart style='display:block;' id='chart-container' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [title]='title' >
                <e-series-collection>
                    <e-series [dataSource]='data' type='Bubble' xName='x' yName='y' size='size' name='pound'> </e-series>
                </e-series-collection>
     </ejs-chart>`
})
export class AppComponent implements OnInit {
    public title: string;
    public data: Object[];
    ngOnInit(): void {
    this.data = bubbleData;
    this.title = 'GDP vs Literacy Rate';
    }
}

```

{% endtab %}

**Bubble Size Mapping**

`size` property can be used to map the size value specified in data source.

{% tab template="chart/series/bubble", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { bubbleData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart style='display:block;' id='chart-container' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
                [title]='title' >
                <e-series-collection>
                    <e-series [dataSource]='data' type='Bubble' xName='x' yName='y' size='size' name='pound'> </e-series>
                </e-series-collection>
     </ejs-chart>`
})
export class AppComponent implements OnInit {
    public title: string;
    public data: Object[];
    ngOnInit(): void {
    this.data = bubbleData;
    this.title = 'GDP vs Literacy Rate';
    }
}

```

{% endtab %}