---
title: " Chart Appearance | Angular "

component: "Chart"

description: "We can customize chart appearance by using color palette, point level customization, chart area cutomization, title and margin customizations."
---

# Appearance

## Custom Color Palette

You can customize the default color of series or points by providing a custom color palette of your choice by
using the [`palettes`](../api/chart/#palettes) property.

{% tab template="chart/axis/category", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'[palettes]='palette'>
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
    public palette: string[];
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
        this.palette = ["#E94649", "#F6B53F", "#6FAAB0", "#C4C24A"];
        this.title = 'Olympic Medals';
    }

}
```

{% endtab %}

## Point Level Customization

Marker, datalabel and fill color of each data point can be customized with
[`pointRender`](../api/chart/iPointRenderEventArgs/) and
[`textRender`](../api/chart/iTextRenderEventArgs/) event.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IPointRenderEventArgs } from '@syncfusion/ej2-angular-charts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' (pointRender)='pointRender($event)' [title]='title'>
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
    public pointRender(args: IPointRenderEventArgs): void {
        let seriesColor: string[] = ['#00bdae', '#404041', '#357cd2', '#e56590', '#f8b883',
                '#70ad47', '#dd8abd', '#7f84e8', '#7bb4eb', '#ea7a57'];
        args.fill = seriesColor[args.point.index];
    };
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

<!-- markdownlint-disable MD036 -->

## Chart Area Customization

<!-- markdownlint-disable MD036 -->

**Customize the Chart Background**

<!-- markdownlint-disable MD013 -->
Using [`background`](../api/chart/#background) and [`border`](../api/chart/#border) properties, you can change the background color and border of the chart.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' background='skyblue' [border]='border'>
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
        this.border = { width: 2, color: '#FF0000'};
    }

}
```

{% endtab %}

**Chart Margin**

You can set margin for chart from its container through [`margin`](../api/chart/#margin) property.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' background='skyblue' [border]='border' [margin]='margin'>
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
        this.border = { width: 2, color: '#FF0000'};
        this.margin = { left: 40, right: 40, top: 40, bottom: 40 };
    }

}
```

{% endtab %}

**Chart Area Background**

The chart area background can be customized by using the [`background`](../api/chart/chartAreaModel/#background)
property in the [`chartArea`](../api/chart/chartAreaModel/).

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IPointRenderEventArgs } from '@syncfusion/ej2-angular-charts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'[chartArea]='chartArea'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' [border]='border'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public border: Object;
    public chartArea: Object;
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
        this.border = { width: 2, color: 'grey'};
        this.chartArea = { background: 'skyblue'};
    }

}
```

{% endtab %}

## Animation

You can customize animation for a particular series using [`animation`](../api/chart/animationModel/) property. You can enable or disable animation of the series using `enable` property, `duration` specifies the duration of an animation and `delay` allows us to start the animation at desire time.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IPointRenderEventArgs } from '@syncfusion/ej2-angular-charts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='country' yName='gold' name='Gold' [border]='border' [animation]='animation'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public border: Object;
    public animation: Object;
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
        this.border = { width: 2, color: 'grey'};
        this.animation = { enable: true};
    }

}
```

{% endtab %}

## Fluid Animation

Fluid animation used to animate series with updated dataSource continues animation rather than animation whole series. You can customize animation for a particular series using [`animate`] method.

{% tab template="chart/series/column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { ILoadedEventArgs } from '@syncfusion/ej2-angular-charts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-chart #roundcol id="column-container" [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis' [title]='title' (loaded)='loaded($event)'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Column' xName='x' yName='y' name='Tiger' width='2' [cornerRadius]='radius'> </e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public border: Object;
    public radius: Object;
    public execute: boolean = false;
    public count: number = 0;
    @ViewChild('roundcol')
    public chart: ChartComponent;
    public loaded(args: ILoadedEventArgs): void {
        if (this.execute) {
            return;
        }
        let columninterval: number = setInterval(
            () => {
                if (document.getElementById('column-container')) {
                    if (this.count === 0) {
                        this.chart.series[0].dataSource = [
                            { x: 'Egg', y: 206, text: 'Bangaladesh' },
                            { x: 'Fish', y: 123, text: 'Bhutn' },
                            { x: 'Misc', y: 48, text: 'Nepal' },
                            { x: 'Tea', y: 240, text: 'Thiland' },
                            { x: 'Fruits', y: 170, text: 'Malaysia' }
                        ];
                        this.execute = true;
                        this.chart.animate();
                        this.count++;
                    } else if (this.count === 1) {
                        this.chart.series[0].dataSource = [
                            { x: 'Egg', y: 86, text: 'Bangaladesh' },
                            { x: 'Fish', y: 173, text: 'Bhutn' },
                            { x: 'Misc', y: 188, text: 'Nepal' },
                            { x: 'Tea', y: 109, text: 'Thiland' },
                            { x: 'Fruits', y: 100, text: 'Malaysia' }
                        ];
                        this.execute = true;
                        this.chart.animate();
                        this.count++;
                    } else if (this.count === 2) {
                        this.chart.series[0].dataSource = [
                            { x: 'Egg', y: 156, text: 'Bangaladesh' },
                            { x: 'Fish', y: 33, text: 'Bhutn' },
                            { x: 'Misc', y: 260, text: 'Nepal' },
                            { x: 'Tea', y: 200, text: 'Thiland' },
                            { x: 'Fruits', y: 30, text: 'Malaysia' }
                        ];
                        this.execute = true;
                        this.chart.animate();
                        this.count = 0;
                    }
                } else {
                    clearInterval(columninterval);
                }
            },
            2000
        );
    }
    ngOnInit(): void {
        this.chartData = [
        { x: 'Egg', y: 106, text: 'Bangaladesh' },
        { x: 'Fish', y: 103, text: 'Bhutn' },
        { x: 'Misc', y: 198, text: 'Nepal' },
        { x: 'Tea', y: 189, text: 'Thiland' },
        { x: 'Fruits', y: 250, text: 'Malaysia' }

        ];
        this.primaryXAxis = {
        valueType: 'Category', interval: 1, majorGridLines: { width: 0 }, tickPosition: 'Inside',
        labelPosition: 'Inside', labelStyle: { color: '#ffffff' }
        };
        this.primaryYAxis = {
        minimum: 0, maximum: 300, interval: 50, majorGridLines: { width: 0 },
        majorTickLines: { width: 0 }, lineStyle: { width: 0 }, labelStyle: { color: 'transparent' }

        };
        this.title = 'Trade in Food Groups';
        this.radius = { bottomLeft: 10, bottomRight: 10, topLeft: 10, topRight: 10 };
        }
        }
```

{% endtab %}

## Chart Title

Chart can be given a title using [`title`](../api/chart/#title) property, to show the information about the data plotted.

{% tab template="chart/chart-title", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [titleStyle]='titleStyle'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' width=2 name='China' [marker]='marker'></e-series>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y1' width=2 name='Australia' [marker]='marker'></e-series>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y2' width=2 name='Japan' [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public primaryYAxis: Object;
    public marker: Object;
    public titleStyle: Object;
    ngOnInit(): void {
        this.chartData = [
                { x: new Date(1975, 0, 1), y: 16, y1: 10, y2: 4.5 },
                { x: new Date(1980, 0, 1), y: 12.5, y1: 7.5, y2: 5 },
                { x: new Date(1985, 0, 1), y: 19, y1: 11, y2: 6.5 },
                { x: new Date(1990, 0, 1), y: 14.4, y1: 7, y2: 4.4 },
                { x: new Date(1995, 0, 1), y: 11.5, y1: 8, y2: 5 },
                { x: new Date(2000, 0, 1), y: 14, y1: 6, y2: 1.5 },
                { x: new Date(2005, 0, 1), y: 10, y1: 3.5, y2: 2.5 },
                { x: new Date(2010, 0, 1), y: 16, y1: 7, y2: 3.7 }
        ];
        this.primaryXAxis = {
            title: 'Years',
            lineStyle: { width: 0 },
            labelFormat: 'y',
            intervalType: 'Years',
            valueType: 'DateTime',
            edgeLabelPlacement: 'Shift'
        };
        this.primaryYAxis = {
            title: 'Percentage (%)',
            minimum: 0, maximum: 20, interval: 2,
            labelFormat: '{value}%'
        };
        this.marker = { visible: true, width: 10, height: 10 };
        this.title = 'Unemployment Rates 1975-2010';
        this.titleStyle = {
            fontFamily: "Arial",
            fontStyle: 'italic',
            fontWeight: 'regular',
            color: "#E27F2D",
            size: '23px'
        }
    }

}
```

{% endtab %}

**Title wrap**

Chart can be given a title using [`title`](../api/chart/#title) property, to show the information about the data plotted.

{% tab template="chart/chart-title", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [titleStyle]='titleStyle'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='month' yName='sales' width=2 name='China' [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    public titleStyle: Object;
    ngOnInit(): void {
        this.chartData =  [
      { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
      { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
      { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
      { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
      { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
      { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
];
        this.primaryXAxis = {
            valueType: 'Category',
        };
        this.marker = { visible: true, width: 10, height: 10 };
        this.title = 'Unemployment Rates 1975-2010';
        this.titleStyle = {
           size:'18px', color:'Red', textAlignment: 'Far', textOverflow: 'Wrap'
        }
    }

}
```

{% endtab %}

## Chart SubTitle

Chart can be given a subtitle using [`subTitle`](../api/chart/#subtitle) property, to show the information
about the data plotted.

{% tab template="chart/chart-title", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' [subTitle]='subTitle' [subTitleStyle]='subTitleStyle'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y' width=2 name='China' [marker]='marker'></e-series>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y1' width=2 name='Australia' [marker]='marker'></e-series>
            <e-series [dataSource]='chartData' type='StepLine' xName='x' yName='y2' width=2 name='Japan' [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public subTitle: string;
    public primaryYAxis: Object;
    public marker: Object;
    public subTitleStyle: Object;
    ngOnInit(): void {
        this.chartData = [
                { x: new Date(1975, 0, 1), y: 16, y1: 10, y2: 4.5 },
                { x: new Date(1980, 0, 1), y: 12.5, y1: 7.5, y2: 5 },
                { x: new Date(1985, 0, 1), y: 19, y1: 11, y2: 6.5 },
                { x: new Date(1990, 0, 1), y: 14.4, y1: 7, y2: 4.4 },
                { x: new Date(1995, 0, 1), y: 11.5, y1: 8, y2: 5 },
                { x: new Date(2000, 0, 1), y: 14, y1: 6, y2: 1.5 },
                { x: new Date(2005, 0, 1), y: 10, y1: 3.5, y2: 2.5 },
                { x: new Date(2010, 0, 1), y: 16, y1: 7, y2: 3.7 }
        ];
        this.primaryXAxis = {
            title: 'Years',
            lineStyle: { width: 0 },
            labelFormat: 'y',
            intervalType: 'Years',
            valueType: 'DateTime',
            edgeLabelPlacement: 'Shift'
        };
        this.primaryYAxis = {
            title: 'Percentage (%)',
            minimum: 0, maximum: 20, interval: 2,
            labelFormat: '{value}%'
        };
        this.marker = { visible: true, width: 10, height: 10 };
        this.title = 'Unemployment Rates 1975-2010';
        this.subTitle = '(1975-2010)';
        this.subTitleStyle = {
            fontFamily: "Arial",
            fontStyle: 'italic',
            fontWeight: 'regular',
            color: "#E27F2D",
            size: '20px'
        }
    }

}
```

{% endtab %}

## See Also

* [Customize the series points using patterns](./how-to/points-customization/#customize-the-series-points-by-using-patterns)