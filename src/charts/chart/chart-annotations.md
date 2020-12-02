---
title: " Chart Annotations | Angular "

component: "Chart"

description: "Chart annotations are used to mark the specific area of interest in the chart area with texts, shapes or images."
---

# Annotation

Annotations are used to mark the specific area of interest in the chart area with texts, shapes or images.

<!-- markdownlint-disable MD033 -->

You can add annotations to the chart by using the <code>annotations</code> option. By using the
[`content`](../api/chart/annotationDirective/#content) option of annotation object, you can specify
the id of the element that needs to be displayed in the chart area.

To known more about annotations, you can check on this video:

`youtube:8JSZW9mZVpY`

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-annotations>
            <e-annotation  content='70 Gold Medals' region='Series' coordinateUnits='Point' x='Japan' y=75>
            </e-annotation>
        </e-annotations>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold'></e-series>
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
             { country: "USA", gold: 50 },
             { country: "China", gold: 40 },
             { country: "Japan", gold: 70 },
             { country: "Australia", gold: 60 },
             { country: "France", gold: 50 },
             { country: "Germany", gold: 40 },
             { country: "Italy", gold: 40 },
             { country: "Sweden", gold: 30 }
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

>Note: To use annotation feature in chart, we need to inject `ChartAnnotationService` into the `@NgModule.providers`.

## Region

Annotations can be placed either with respect to `Series` or `Chart`. by default, it will placed with respect
to `Chart`.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { columnData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-annotations>
            <e-annotation  content='<div>Highest Medal Count</div>' region='Series' coordinateUnits='Point' x='Japan' y=75>
            </e-annotation>
        </e-annotations>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = columnData;
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

## Co-ordinate Units

Specified the coordinates units of the annotation either `Pixel` or `Point`.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { columnData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-annotations>
            <e-annotation  content='<div style="border: 1px solid black; padidng: 5px 5px 5px 5px, backgrund:#f5f5f5">Annotation in Pixel</div>'
             coordinateUnits='Pixel' x=150 y=75>
            </e-annotation>
        </e-annotations>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    ngOnInit(): void {
        this.chartData = columnData;
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

## Alignment

Annotation provides `verticalAlignment` and `horizontalAlignment`. The `verticalAlignment` can be customized
via `Top`, `Bottom` or `Middle` and the `horizontalAlignment` can be customized via `Near`, `Far` or `Center`.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { columnData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-annotations>
            <e-annotation  content='<div style="border: 1px solid black; padidng: 5px 5px 5px 5px, backgrund:#f5f5f5">Highest Medal Count</div>'
           verticalAlignment='Top' horizontalAlignment='Near' x='France' y=50>
            </e-annotation>
        </e-annotations>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public border: Object;
    public margin: Object;
    ngOnInit(): void {
        this.chartData = columnData;
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

## Adding y-axis sub title through on annotation

By setting text div in the `content` option of annotation object you can add sub title to chart y-axis. Specified the
`coordinate` value as `pixel` and customize x and y location of the text.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { columnData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-annotations>
            <e-annotation content='<div id="text" style="transform: rotate(-90deg);">Speed</div>'
           verticalAlignment='Top' horizontalAlignment='Near' x=18 y=180 coordinateUnits='Pixel'>
            </e-annotation>
        </e-annotations>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold'></e-series>
        </e-series-collection>
    </ejs-chart>
    <style></style>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public border: Object;
    public margin: Object;
    ngOnInit(): void {
        this.chartData = columnData;
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.primaryYAxis = {
            minimum: 0, maximum: 80,
            interval: 20, title: 'm3/min'
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

## See Also

* [Show total stacking values in data label](./how-to/stacking-total/#show-the-total-value-for-stacking-series-in-data-label)
* [Create footer and watermark for chart](./how-to/footer/#create-footer-and-watermark-for-chart)