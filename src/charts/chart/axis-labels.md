---
title: "Chart Axis Labels | Angular "
component: "Chart"
description: "Chart contains smart axis labels, label positioning, multilevelabels, text customization and sorting properties "
---

# Axis Labels

## Smart Axis Labels

When the axis labels overlap with each other, you can use [`labelIntersectAction`](../api/chart/axisDirective/#labelintersectaction)
property in the axis, to place them smartly.

When setting `labelIntersectAction` as `Hide`

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" width='450px' [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
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
        this.title = 'Internet Users';
    }

}
```

{% endtab %}

When setting `labelIntersectAction` as `Rotate45`

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { labelData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" width='450px' [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
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
        this.chartData = labelData;
        this.primaryXAxis = {
           title: 'Countries',
           valueType: 'Category',
           labelIntersectAction: 'Rotate45'
        };
        this.primaryYAxis = {
           minimum: 0, maximum: 80, interval: 10,
           title: 'People(in millions)'
        };
        this.title = 'Internet Users';
    }

}
```

{% endtab %}

When setting `labelIntersectAction` as `Rotate90`

{% tab template="chart/axis/multiple", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { labelData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" width='450px' [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
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
        this.chartData = labelData;
        this.primaryXAxis = {
           title: 'Countries',
           valueType: 'Category',
           labelIntersectAction: 'Rotate90'
        };
        this.primaryYAxis = {
           minimum: 0, maximum: 80, interval: 10,
           title: 'People(in millions)'
        };
        this.title = 'Internet Users';
    }

}
```

{% endtab %}

## Axis Labels Positioning

By default, the axis labels can be placed at `outside` the axis line and this also can be placed at `inside`
the axis line using the `labelPosition` property.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { categoryData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container"  [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = categoryData;
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries',
           labelPosition: 'Inside'
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

## Multilevel Labels

Any number of levels of labels can be added to an axis using the `multiLevelLabels` property. This property can be
configured using the following properties:

• Categories
• Overflow
• Alignment
• Text style
• Border

>Note: To use multilevel label feature, we need to inject `MultiLevelLabel` into the `@NgModule.providers`.

### Categories

Using the categories property, you can configure the `start`, `end`, `text`, and `maximumTextWidth` of multilevel labels.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { categoryData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [legendSettings]='legendSettings'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public legendSettings: Object = { visible: false};
    ngOnInit(): void {
        this.chartData = categoryData;
        this.primaryXAxis = {
           valueType: 'Category',
           multiLevelLabels:[{ categories: [
                        {
                            //Start and end values of the multi-level labels accepts number, date and sring values
                            start: -0.5,
                            end: 3.5,
                            //Multi-level label's text.
                            text: 'Half Yearly 1',

                        },
                        { start: 3.5, end: 7.5, text: 'Half Yearly 2' },
                    ]}]
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

### Overflow

Using the `overflow` property, you can `trim` or `wrap` the multilevel labels.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { categoryData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [legendSettings]='legendSettings'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public legendSettings: Object = { visible: false};
    ngOnInit(): void {
        this.chartData = categoryData;
        this.primaryXAxis = {
           valueType: 'Category',
           multiLevelLabels:[{
               categories: [{start: -0.5, end: 3.5, text: 'Half Yearly 1', maximumTextWidth:50},
                        { start: 3.5, end: 7.5, text: 'Half Yearly 2', maximumTextWidth:50 }],
               overflow:'Trim'
           }]
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

### Alignment

The `alignment` property provides option to position the multilevel labels at `far`, `center`, or `near`.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { categoryData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'
    [legendSettings]='legendSettings'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public legendSettings: Object = { visible: false};
    ngOnInit(): void {
        this.chartData = categoryData;
        this.primaryXAxis = {
           valueType: 'Category',
           multiLevelLabels:[{
               categories: [{start: -0.5, end: 3.5, text: 'Half Yearly 1' },
                        { start: 3.5, end: 7.5, text: 'Half Yearly 2' }],
                alignment :'Far'
           }]
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

### Text customization

The `textStyle` property of multilevel labels provides options to customize the `size`, `color`, `fontFamily`,
`fontWeight`, `fontStyle`, `opacity`, `textAlignment` and `textOverflow`.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { categoryData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'
    [legendSettings]='legendSettings'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public legendSettings: Object = { visible: false};
    ngOnInit(): void {
        this.chartData = categoryData;
        this.primaryXAxis = {
           valueType: 'Category',
           multiLevelLabels:[{
               categories: [{start: -0.5, end: 3.5, text: 'Half Yearly 1' },
                        { start: 3.5, end: 7.5, text: 'Half Yearly 2' }],
               textStyle:{size:'18px', color:'Red'}
           }]
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

### Border customization

Using the `border` property, you can customize the `width`, `color`, and `type`. The `type` of border
are `Rectangle`, `Brace`, `WithoutBorder`, `WithoutTopBorder`, `WithoutTopandBottomBorder` and `CurlyBrace`.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { categoryData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'
    [legendSettings]='legendSettings'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public legendSettings: Object = { visible: false};
    ngOnInit(): void {
        this.chartData = categoryData;
        this.primaryXAxis = {
           valueType: 'Category',
           multiLevelLabels:[{
               categories: [{start: -0.5, end: 3.5, text: 'Half Yearly 1' },
                        { start: 3.5, end: 7.5, text: 'Half Yearly 2' }],
               border:{type:'Brace', color:'Blue', width: 2},
           }]
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

## Edge Label Placement

Labels with long text at the edges of an axis may appear partially in the chart. To avoid this,
use [`edgeLabelPlacement`](../api/chart/axisDirective/#edgelabelplacement) property in axis, which moves
the label inside the chart area for better appearance or hides it.

{% tab template="chart/axis/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { dateData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'
    [legendSettings]='legendSettings'>
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
    public legendSettings: Object = { visible: false};
    ngOnInit(): void {
        this.chartData = dateData;
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

## Trim using maximum label width

You can trim the label using [`enableTrim`](../api/chart/axisModel/#enabletrim) property and width of the labels can also be
customized using [`maximumLabelWidth`](../api/chart/axisModel/#maximumlabelwidth) property in the axis, the value maximum label width is `34` by default.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { categoryData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis' [legendSettings]='legendSettings'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' ></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public legendSettings: Object = { visible: false };
    ngOnInit(): void {
    this.chartData = [
    { x: "South Korea", y: 39.4 }, { x: "India", y: 61.3 }, { x: "Pakistan", y: 20.4 },
    { x: "Germany", y: 65.1 }, { x: "Australia", y: 15.8 }, { x: "Italy", y: 29.2 },
    { x: "United Kingdom", y: 44.6 }, { x: "Saudi Arabia", y: 9.7 }, { x: "Russia", y: 40.8 },
    { x: "Mexico", y: 31 }, { x: "Brazil", y: 75.9 }, { x: "China", y: 51.4 }];
        this.primaryXAxis = {
        valueType: 'Category',
        enableTrim: true,
        maximumLabelWidth: '34',

        };
    }

}
```

{% endtab %}

## Labels Customization

The [`labelStyle`](../api/chart/axisDirective/#labelstyle) property of an axis provides options to customize the
`color`, `font-family`, `font-size` and `font-weight` of the axis labels.

To known more about labels customization, you can check on this video:

`youtube:gjO67nmQIwY`

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { categoryData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'
    [legendSettings]='legendSettings'>
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
    public legendSettings: Object = { visible: false};
    ngOnInit(): void {
        this.chartData = categoryData;
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

## Customizing Specific Point

You can customize the specific text in the axis labels using `axisLabelRender` event.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { categoryData } from 'datasource.ts';
import { IAxisLabelRenderEventArgs } from '@syncfusion/ej2-angular-charts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' (axisLabelRender) = 'axisLabelRender($event)'
    [legendSettings]='legendSettings'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' ></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public legendSettings: Object = { visible: false};
    public axisLabelRender(args : IAxisLabelRenderEventArgs ): void {
        if(args.text === 'France') {
            args.labelStyle.color = 'Red';
        }
    };
    ngOnInit(): void {
        this.chartData = categoryData;
        this.primaryXAxis = {
           valueType: 'Category',
           title: 'Countries'
        };
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

## Line break support

Line break feature used to customize the long axis label text into multiple lines by using tag. Refer the below example in that dataSource x value contains long text, it breaks into two lines by using  `<br>` tag.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { data } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Bar' xName='x' yName='y' width=2 ></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public primaryYAxis: Object;
    public chartData: Object[];
    public title: string;
    ngOnInit(): void {
        this.chartData = data;
        this.primaryXAxis = {
        title: 'Country',
        valueType: 'Category',
        majorGridLines: { width: 0 },
        enableTrim: false,
        };
        this.primaryYAis = {
        minimum: 0,
        maximum: 800,
        labelFormat: Browser.isDevice ? '{value}' : '{value}M',
        edgeLabelPlacement: 'Shift',
        majorGridLines: { width: 0 },
        majorTickLines: { width: 0 },
        lineStyle: { width: 0 },
        labelStyle: {
            color: 'transparent'
        }
        };
        this.title = 'Internet Users – 2016';
    }

}
```

{% endtab %}

## Maximum Labels

`MaximumLabels` property is set, then the labels will be rendered based on the count in the property per 100 pixel. If you have set range (minimum, maximum, interval) and maximumLabels, then the priority goes to range only. If you haven’t set the range, then we have considered priority to maximumLabels property.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { series1 } from 'datasource.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart style='display:block' align='center' id='chartcontainer' [title]='title' [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
            [tooltip]='tooltip'  [chartArea]='chartArea' [width]='width'>
            <e-series-collection>
                <e-series [dataSource]='series1' type='Line' xName='x' yName='y' name='Germany' width=2 > </e-series>
            </e-series-collection>
        </ejs-chart>`
})
export class AppComponent implements OnInit {
    public series1: Object[] = series1;
    //Initializing Primary X Axis
    public primaryXAxis: Object = {
        title: 'Years',
           edgeLabelPlacement: 'Shift',
            majorGridLines : { width : 0 },
           maximumLabels:1,
    };
    //Initializing Primary Y Axis
    public primaryYAxis: Object = {
     title: 'Profit ($)',
            rangePadding: 'None',
            lineStyle : { width: 0 },
            majorTickLines : {width : 0}
    };
    public chartArea: Object = {
        border: {
            width: 0
        }
    };
    public width: string ='60%';
    public tooltip: Object = {
        enable: true
    };
    // custom code end
    public title: string = 'Inflation - Consumer Price';
    constructor() {
       //code
    };

}
```

{% endtab %}