---
title: " Chart DataLabel | Angular "

component: "Chart"

description: "Data labels are names of the data points that are displayed on the x-axis of a chart and also used to highlight important data points"
---

# Data Labels

Data label can be added to a chart series by enabling the [`visible`](../api/chart/dataLabelSettings/#visible)
option in the dataLabel. By default, the labels will arrange smartly without overlapping.

{% tab template="chart/data-marker/datalabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { columnData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Warmest' width=2 [marker]='marker'></e-series>
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
        this.chartData = columnData;
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.marker = { dataLabel: { visible: true }
        };
        this.title = 'Alaska Weather Statistics - 2016';
    }

}
```

{% endtab %}

>Note: To use datalabel feature, we need to inject `DataLabelService` into the `@NgModule.providers`.

## Position

Using [`position`](../api/chart/dataLabelSettings/#position) property, you can place the label either on
`Top`, `Middle`,`Bottom` or `Outer` (outer is applicable for column and bar type series).

{% tab template="chart/data-marker/datalabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { columnData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Warmest' width=2 [marker]='marker'></e-series>
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
        this.chartData = columnData;
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.marker = { dataLabel: { visible: true, position: 'Middle' }
        };
        this.title = 'Alaska Weather Statistics - 2016';
    }

}
```

{% endtab %}

>Note: The position `Outer` is applicable for column and bar type series.

## Datalabel template

Label content can be formatted by using the template option. Inside the template, you can add the placeholder text
`${point.x}` and `${point.y}` to display corresponding data points x & y value.
Using [`template`](../api/chart/dataLabelSettingsModel/#template) property, you can set data label template
in chart.

{% tab template="chart/data-marker/datalabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { columnData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Warmest' width=2 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    ngOnInit(): void {
        this.chartData = columnData;
        this.primaryXAxis = {
            title: 'Months',
            valueType: 'Category', labelFormat: 'yMMM',
            edgeLabelPlacement: 'Shift'
        };
        this.marker = { dataLabel: { visible: true, position: 'Middle',
                        template: '<div>${point.x}</div><div>${point.y}</div>' }
        };
        this.title = 'Alaska Weather Statistics - 2016';
    }

}
```

{% endtab %}

## Text Mapping

Text from the data source can be mapped using `name` property.

{% tab template="chart/data-marker/datalabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { mapData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Warmest' width=2 [marker]='marker'></e-series>
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
        this.chartData = mapData;
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.marker = { dataLabel: { visible: true, name: 'text'}
        };
        this.title = 'Alaska Weather Statistics - 2016';
    }

}
```

{% endtab %}

## Margin

`margin` for data label can be applied to using `left`, `right`, `bottom` and `top` properties.

{% tab template="chart/data-marker/datalabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { columnData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Warmest' width=2 [marker]='marker'></e-series>
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
        this.chartData = columnData;
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.marker = { dataLabel: { visible: true,border:{width: 1, color : 'red'},
                        margin:{
                            left:5,
                            right:5,
                            top:5,
                            bottom:5
                        } }
        };
        this.title = 'Alaska Weather Statistics - 2016';
    }

}
```

{% endtab %}

## DataLabel Rotation

Using `angle` property, you can rotate the data label by its given angle.

{% tab template="chart/data-marker/datalabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { columnData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Warmest' width=2 [marker]='marker'></e-series>
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
        this.chartData = columnData;
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.marker = { dataLabel: { visible: true, border:{width: 1, color : 'red'},
                        margin:{
                            left:5,
                            right:5,
                            top:5,
                            bottom:5
                        }, angle : 45, enableRotation: true }
        };
        this.title = 'Alaska Weather Statistics - 2016';
    }
}
```

{% endtab %}

## Customization

`stroke` and `border` of data label can be customized using `fill` and `border` properties. Rounded corners
can be customized using `rx` and `ry` properties.

{% tab template="chart/data-marker/datalabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { columnData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Warmest' width=2 [marker]='marker'></e-series>
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
        this.chartData = columnData;
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.marker = { dataLabel: { visible: true,
                        border:{width: 2, color : 'red'},
                        rx:10, ry: 10
                    }
        };
        this.title = 'Alaska Weather Statistics - 2016';
    }

}
```

{% endtab %}

>Note: `rx` and `ry` properties requires `border` values not to be null.

## Customizing Specific Point

You can also customize the specific marker and label using
[`pointRender`](../api/chart/iPointRenderEventArgs/) and
[`textRender`](../api/chart/iTextRenderEventArgs/) event.
 `pointRender` event allows you to change the shape, color and border for a point, whereas the `textRender` event
allows you to change the text for the point.

{% tab template="chart/data-marker/datalabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IPointRenderEventArgs, ITextRenderEventArgs } from '@syncfusion/ej2-angular-charts';
import { columnData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' (pointRender)='pointRender($event)' (textRender)='textRender($event)'[title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Warmest' width=2 [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    public pointRender(args: IPointRenderEventArgs): void {
        if(args.point.index === 6) {
                args.fill = 'red'
        }
    };
    public textRender(args: ITextRenderEventArgs): void {
            if(args.point.index === 6){
                args.text = 'Maximum Temperature';
                args.color = 'red';
            }
    };
    ngOnInit(): void {
        this.chartData = columnData;
        this.primaryXAxis = {
            title: 'Months',
            valueType: 'Category', labelFormat: 'yMMM',
            edgeLabelPlacement: 'Shift'
        };
        this.marker = { dataLabel: { visible: true }
        };
        this.title = 'Alaska Weather Statistics - 2016';
    }

}
```

{% endtab %}

## See Also

* [Show total stacking values in data label](./how-to/stacking-total/#show-the-total-value-for-stacking-series-in-data-label)
* [Prevent the data label when the data value is 0](./how-to/prevent-data-label/#prevent-the-data-label-when-the-data-value-is-0)