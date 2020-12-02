---
title: "Title and SubTitle | Angular "

component: "Accumulation Chart"

description: "Accumulation Chart title and sub title shows information about plotted data"
---

# Title

Accumulation Chart can be given a title using [`title`](../api/accumulation-chart/#title) property, to show the information
about the data plotted.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings' [title]='title'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' type='Pie'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    public title: string;
    public titleStyle: Object;
    ngOnInit(): void {
        this.piedata = [{ x: 'Saudi Arabia', y: 58, text: '58%' },
                        { x: 'Persian Gulf', y: 15, text: '15%' },
                        { x: 'Canada', y: 13, text: '13%' },
                        { x: 'Venezuela', y: 8, text: '8%' },
                        { x: 'Mexico', y: 3, text: '3%' },
                        { x: 'Russia', y: 2, text: '2%' },
                        { x: 'Miscellaneous', y: 1, text: '1%' }];
        this.legendSettings = {
            visible: false
        };
        this.title = 'Oil and other liquid imports in USA';
    }

}
```

{% endtab %}

## Title Customization

Accumulation Chart can be customizing a title using [`titleStyle`](../api/accumulation-chart/accumulationChartModel/#titlestyle) property.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings' [title]='title' [titleStyle]='titleStyle'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' type='Pie'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    public title: string;
    public titleStyle: Object;
    ngOnInit(): void {
        this.piedata = [{ x: 'Saudi Arabia', y: 58, text: '58%' },
                        { x: 'Persian Gulf', y: 15, text: '15%' },
                        { x: 'Canada', y: 13, text: '13%' },
                        { x: 'Venezuela', y: 8, text: '8%' },
                        { x: 'Mexico', y: 3, text: '3%' },
                        { x: 'Russia', y: 2, text: '2%' },
                        { x: 'Miscellaneous', y: 1, text: '1%' }];
        this.legendSettings = {
            visible: false
        };
        this.title = 'Oil and other liquid imports in USA';
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

## SubTitle

Accumulation Chart can be given a subtitle using [`subTitle`](../api/accumulation-chart/accumulationChartModel/#subtitle) property, to show the information
about the data plotted.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings' [title]='title' [subTitle]='subTitle'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' type='Pie'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    public title: string;
    public SubTitle: string;
    public subTitleStyle: Object;
    ngOnInit(): void {
        this.piedata = [{ x: 'Saudi Arabia', y: 58, text: '58%' },
                        { x: 'Persian Gulf', y: 15, text: '15%' },
                        { x: 'Canada', y: 13, text: '13%' },
                        { x: 'Venezuela', y: 8, text: '8%' },
                        { x: 'Mexico', y: 3, text: '3%' },
                        { x: 'Russia', y: 2, text: '2%' },
                        { x: 'Miscellaneous', y: 1, text: '1%' }];
        this.legendSettings = {
            visible: false
        };
        this.title = 'Oil and other liquid imports in USA';
        this.subTitle = 'In the year 2014 - 2015';
    }

}
```

{% endtab %}

## SubTitle Customization

Accumulation Chart can be customizing a subtitle using [`subTitleStyle`](../api/accumulation-chart/accumulationChartModel/#subtitlestyle) property.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings' [title]='title' [subTitle]='subTitle' [subTitleStyle]='subTitleStyle'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y' type='Pie'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    public title: string;
    public SubTitle: string;
    public subTitleStyle: Object;
    ngOnInit(): void {
        this.piedata = [{ x: 'Saudi Arabia', y: 58, text: '58%' },
                        { x: 'Persian Gulf', y: 15, text: '15%' },
                        { x: 'Canada', y: 13, text: '13%' },
                        { x: 'Venezuela', y: 8, text: '8%' },
                        { x: 'Mexico', y: 3, text: '3%' },
                        { x: 'Russia', y: 2, text: '2%' },
                        { x: 'Miscellaneous', y: 1, text: '1%' }];
        this.legendSettings = {
            visible: false
        };
        this.title = 'Oil and other liquid imports in USA';
        this.subTitle = 'In the year 2014 - 2015';
        this.subTitleStyle = {
            fontFamily: "Arial",
            fontStyle: 'italic',
            fontWeight: 'regular',
            color: "#E27F2D"
     }
    }

}
```

{% endtab %}