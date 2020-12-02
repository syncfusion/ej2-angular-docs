---
title: " Chart Polar and Radar | Angular "

component: "Chart"

description: "Polar and Radar chart supports different draw types and customization to display the data."
---

<!-- markdownlint-disable MD036 -->

# Polar Chart and Radar Chart

## Polar Chart

To render a polar series, use series[`type`](../api/chart/seriesModel#type) as `Polar` and
inject `PolarSeriesService`  into the `@NgModule.providers`.

### Draw Types

Polar drawType property is used to change the series plotting type to line, column, area, range column, spline,
scatter, stacking area and stacking column. The default value of drawType is `Line`.

**Line**

To render a line draw type, use series [`drawType`](../api/chart/seriesModel#drawtype) as `Line` and inject
`LineSeriesService` inject `LineSeriesService`  into the `@NgModule.providers`.
[`isClosed`](../api/chart/seriesModel#isclosed) property specifies whether to join start and end point of
 a line series used in polar chart to form a closed path. Default value of isClosed is true.

{% tab template= "chart/series/polar" , sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='Polar' xName='x' yName='y' drawType='Line'> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];


    ngOnInit(): void {
        this.data = [{ x: 2005, y: 28 }, { x: 2006, y: 25 },{ x: 2007, y: 26 }, { x: 2008, y: 27 },
                     { x: 2009, y: 32 }, { x: 2010, y: 35 }, { x: 2011, y: 30 }];
        this.primaryXAxis = {
            title: 'Year',
            minimum: 2004, maximum: 2012, interval: 1
            };
        this.primaryYAxis = {
            minimum: 20, maximum: 40, interval: 5,
            title: 'Efficiency',
            labelFormat: '{value}%'
            };

        this.title = 'Efficiency of oil-fired power production';

    }
}

```

{% endtab %}

**Spline**

To render a spline line draw type, use series [`drawType`](../api/chart/seriesModel#drawtype) as `Spline`
and inject `SplineSeriesService` inject `SplineSeriesService`  into the `@NgModule.providers`.

{% tab template= "chart/series/polar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { polarCategory } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='Polar' xName='x' yName='y' drawType='Spline' name='London'> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];
    ngOnInit(): void {
        this.data = polarCategory;
        this.primaryXAxis = {
            title: 'Month',
            valueType: 'Category'
        };
        this.primaryYAxis = {
            minimum: -5, maximum: 35, interval: 10,
            title: 'Temperature in Celsius',
            labelFormat: '{value}C'
        };

        this.title = 'Climate Graph-2012';

    }
}

```

{% endtab %}

**Area**

To render a area line draw type, use series [`drawType`](../api/chart/seriesModel#drawtype) as `Area` and
inject `AreaSeriesService`  into the `@NgModule.providers`.

{% tab template= "chart/series/polar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { polarCategory } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='Polar' xName='x' yName='y' drawType='Area' name='London'> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];
    ngOnInit(): void {
        this.data = polarCategory;
        this.primaryXAxis = {
            title: 'Month',
            valueType: 'Category'
        };
        this.primaryYAxis = {
            minimum: -5, maximum: 35, interval: 10,
            title: 'Temperature in Celsius',
            labelFormat: '{value}C'
        };

        this.title = 'Climate Graph-2012';

    }
}

```

{% endtab %}

**Stacked Area**

To render a stacked area draw type, use series [`drawType`](../api/chart/seriesModel#drawtype) as `StackingArea` and inject `StackingAreaSeriesService`
into the `@NgModule.providers`.

{% tab template= "chart/series/polar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { stackedData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='Polar' xName='x' yName='y' drawType='StackingArea' name='Organic'> </e-series>
                <e-series [dataSource]='data' type='Polar' xName='x' yName='y1' drawType='StackingArea' name='Fair-trade'> </e-series>
                <e-series [dataSource]='data' type='Polar' xName='x' yName='y2' drawType='StackingArea' name='veg-Alternatives'> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public data: Object[];


    ngOnInit(): void {
        this.data = stackedData;
        this.primaryXAxis = {
            valueType: 'Category',
        };
        this.title = 'Trend in Sales of Ethical Produce';

    }
}

```

{% endtab %}

**Column**

To render a column draw type, use series [`drawType`](../api/chart/seriesModel#drawtype) as `Column` and inject `ColumnSeriesService`
into the `@NgModule.providers`.

{% tab template= "chart/series/polar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { columnData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='Polar' xName='country' yName='gold' drawType='Column' name='Gold'> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public data: Object[];
    ngOnInit(): void {
        this.data = columnData;
        this.primaryXAxis = {
            valueType: 'Category',
            title: 'Countries'
        };
        this.title = 'Olympic Medals';

    }
}

```

{% endtab %}

**Stacked Column**

To render a stacked column draw type, use series [`drawType`](../api/chart/seriesModel#drawtype) as `StackingColumn` and inject `StackingColumnSeriesService`
into the `@NgModule.providers`.

{% tab template= "chart/series/polar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='Polar' xName='x' yName='y' drawType='StackingColumn' name='UK'> </e-series>
                <e-series [dataSource]='data' type='Polar' xName='x' yName='y1' drawType='StackingColumn' name='Germany'> </e-series>
                <e-series [dataSource]='data' type='Polar' xName='x' yName='y2' drawType='StackingColumn' name='France'> </e-series>
                <e-series [dataSource]='data' type='Polar' xName='x' yName='y2' drawType='StackingColumn' name='Italy'> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public data: Object[];
    ngOnInit(): void {
        this.data = data;
        this.primaryXAxis = {
            title: 'Years',
            valueType: 'Category'
        };
        this.title = 'Mobile Game Market by Country';

    }
}

```

{% endtab %}

**Range Column**

To render a range column draw type, use series [`drawType`](../api/chart/seriesModel#drawtype) as `RangeColumn` and inject `RangeColumnSeriesService`
into the `@NgModule.providers`.

{% tab template= "chart/series/polar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { rangeData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='Polar' xName='x' high='high' low='low' drawType='RangeColumn' name='Gold'> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];
    ngOnInit(): void {
        this.data = rangeData;
        this.primaryXAxis = {
            valueType: 'Category',
            title: 'Months'
        };
        this.primaryYAxis = {
            title: 'Temperature(Celsius)',
        };

        this.title = 'Maximum and Minimum Temperature';

    }
}

```

{% endtab %}

**Scatter**

To render a scatter draw type, use series [`drawType`](../api/chart/seriesModel#drawtype) as `Scatter` and
inject `ScatterSeriesService`  into the `@NgModule.providers`.

{% tab template= "chart/series/polar" , sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { polarCategory } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='Polar' xName='x' yName='y' drawType='Scatter' name='London'> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];


    ngOnInit(): void {
        this.data = polarCategory;
        this.primaryXAxis = {
            title: 'Month',
            valueType: 'Category'
        };
        this.primaryYAxis = {
            minimum: -5, maximum: 35, interval: 10,
            title: 'Temperature in Celsius',
            labelFormat: '{value}C'
        };

        this.title = 'Climate Graph-2012';

    }
}

```

{% endtab %}

## Radar Chart

To render a radar series, use series [`type`](../api/chart/seriesModel#type) as `Radar` and
inject `RadarSeriesService` into the `@NgModule.providers`.

### Draw Type

**Line**

To render a line draw type, use series [`drawType`](../api/chart/seriesModel#drawtype) as `Line` and inject
`LineSeriesService` inject `LineSeriesService`  into the `@NgModule.providers`.
[`isClosed`](../api/chart/seriesModel#isclosed) property specifies whether to join start and end point of
a line series used in polar chart to form a closed path. Default value of isClosed is true.

{% tab template= "chart/series/polar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { radarData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='Radar' xName='x' yName='y' drawType='Line'> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public title: string;
    public data: Object[];
    ngOnInit(): void {
        this.data = radarData;
        this.title = 'Efficiency of oil-fired power production';

    }
}

```

{% endtab %}

### Customization

**Start Angle**

You can customize the start angle of the polar series using
[`startAngle`](../api/chart/axis#startangle) property. By default, `startAngle` is 0 degree.

{% tab template= "chart/series/polar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { radarData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='Radar' xName='x' yName='y' drawType='Line'> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public primaryYAxis: Object;
    public data: Object[];


    ngOnInit(): void {
        this.data = radarData;
        this.primaryXAxis = {
            title: 'Year', startAngle: 90,
            minimum: 2004, maximum: 2012, interval: 1
            };
        this.title = 'Efficiency of oil-fired power production';

    }
}

```

{% endtab %}

**Coefficient in axis**

You can customize the radius of the polar series and radar series using
[`coefficient`](../api/chart/axis#coefficient) property. By default, `coefficient` is 100.

{% tab template= "chart/series/polar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { radarData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='Radar' xName='x' yName='y' drawType='Line'> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public data: Object[];
    ngOnInit(): void {
        this.data = radarData;
        this.primaryXAxis = {
            title: 'Year', coefficient: 90,
            minimum: 2004, maximum: 2012, interval: 1
            };
        this.title = 'Efficiency of oil-fired power production';

    }
}

```

{% endtab %}

**DashArray**

You can customize the DashArray of the polar series and radar series using
[`dashArray`](../api/chart) property. By default, `dashArray` is 0.

{% tab template= "chart/series/polar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { radarData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
            <e-series [dataSource]='data' type='Radar' xName='x' yName='y' dashArray='2'
            drawType='Line' width=2> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public data: Object[];
    ngOnInit(): void {
        this.data = radarData;
        this.primaryXAxis = {
            title: 'Year',
            minimum: 2004, maximum: 2012, interval: 1
            };
        this.title = 'Efficiency of oil-fired power production';

    }
}

```

{% endtab %}

**Marker and Customization**

Markers can be added to the points by enabling the visible option of the
[`marker`](../api/chart) property. Markers can be assigned with different shapes such as Rectangle, Circle, Diamond, Pentagon etc using the `shape` property.

{% tab template= "chart/series/polar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { radarData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
            <e-series [dataSource]='data' type='Radar' xName='x' yName='y' [marker]='marker'
            drawType='Line' width=2> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public data: Object[];
    public marker: Object[];
    ngOnInit(): void {
        this.data = radarData;
        this.primaryXAxis = {
            title: 'Year',
            minimum: 2004, maximum: 2012, interval: 1
            };
        this.title = 'Efficiency of oil-fired power production';
        this.marker = {
            visible: true,
            height: 10, width: 10,
            shape: 'Pentagon'
        };
    }
}

```

{% endtab %}

**Datalabel and customization**

You can customize the dataLabel of the polar series and radar series using
[`dataLabel`](../api/chart) property. By setting `dataLabel` visible true.

{% tab template= "chart/series/polar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { radarData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
            <e-series [dataSource]='data' type='Radar' xName='x' yName='y' [marker]='marker'
            drawType='Line'> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public data: Object[];
    public marker: Object;
    ngOnInit(): void {
        this.data = radarData;
        this.primaryXAxis = {
            title: 'Year',
            minimum: 2004, maximum: 2012, interval: 1
            };
        this.title = 'Efficiency of oil-fired power production';
        this.marker = {
            dataLabel:
            {
                visible: true,
                labelStyle: {
                    color: 'red'
                }
            }
        };
    }
}

```

{% endtab %}

**Axis label and customization**

You can customize the Axis label of the polar series and radar series using `labelStyle`,
`labelPlacement`, `labelRotation`, `labelIntersectAction` properties in the `primaryXAxis` and
`primaryYAxis`.
In the below sample `labelPlacement` and `labelStyle` properties is used in `primaryXAxis`.

{% tab template= "chart/series/polar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { radarData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
            <e-series [dataSource]='data' type='Radar' xName='x' yName='y' drawType='Line'>
            </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public data: Object[];
    ngOnInit(): void {
        this.data = radarData;
        this.primaryXAxis = {
            title: 'Year',
            minimum: 2004, maximum: 2012, interval: 1,
            labelPlacement: 'OnTicks'
            labelStyle: {
                  color: 'blue'
                }
            };
        this.title = 'Efficiency of oil-fired power production';
    }
}

```

{% endtab %}

**Annotation**

Annotations are used to mark the specific area of interest in the chart area with texts, shapes or images.
You can add annotations to the chart by using the annotations option.
By using the `content` option of annotation object, you can specify either the id of the element or directly specify the element in the content that needs to be displayed in the chart area.
Specified the `coordinateUnits` of the annotation either `Pixel` or `Point`.

{% tab template= "chart/series/polar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { columnData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-annotations>
            <e-annotation  content='<div>Highest Medal Count</div>' coordinateUnits='Pixel' x=250 y=160>
            </e-annotation>
            </e-annotations>
            <e-series-collection>
                <e-series [dataSource]='data' type='Polar' xName='country' yName='gold' drawType='Column' name='Gold'> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public data: Object[];
    ngOnInit(): void {
        this.data = columnData;
        this.primaryXAxis = {
            valueType: 'Category',
            title: 'Countries'
        };
        this.title = 'Olympic Medals';

    }
}

```

{% endtab %}

**Point customization**

You can customize the series points with patterns by using the `pointColorMapping` property.
To customize the series point colors, define the patterns and map the pattern URL to the series point using `pointColorMapping` property in series.

{% tab template= "chart/series/polar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { columnData } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    ` <ejs-chart id='chartcontainer' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [title]='title' >
            <e-series-collection>
                <e-series [dataSource]='data' type='Polar' xName='country' yName='gold' drawType='Column' pointColorMapping='color' name='Gold'> </e-series>
            </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public title: string;
    public data: Object[];
    ngOnInit(): void {
        this.data = [{ country: "USA", gold: 60, color: 'url(#chess)'},
      { country: "China", gold: 50, color:  'url(#cross)'},
      { country: "Japan", gold: 80, color: 'url(#circle)'},
      { country: "Australia", gold: 70, color:  'url(#rectangle)'},
      { country: "France", gold: 60,  color: 'url(#line)'},
      { country: "Germany", gold: 50, color: 'url(#circle)' },
      { country: "Sweden", gold: 40, color: 'url(#rectangle)'}];
        this.primaryXAxis = {
            valueType: 'Category',
            title: 'Countries'
        };
        this.title = 'Olympic Medals';
    }
}

```

{% endtab %}

To known about polar and radar charts, you can check on this video:

`youtube:i-fo4QnEQZI`

## See Also

* [Data label](./data-labels/)
* [Tooltip](./tool-tip/)
