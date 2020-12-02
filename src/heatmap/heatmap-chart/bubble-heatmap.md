---
title: "Bubble HeatMap"
component: "Heatmap"
description: "This section describes about the bubble heatmap, its types and its key features"
---

# Bubble heat map

Data points represent the data source values with `gradient` or `fixed` colors in the heat map.
You can customize the appearance of these data points by changing the `color` and `shape` attributes.

The data points can be represented in color fill or bubble shape by defining the [`tileType`](../api/heatmap/cellSettings/#tiletype) property.
By default, the data points are color filled with `gradient` or `fixed` and this depiction of data points is defined as `rect` in the [`tileType`](../api/heatmap/cellSettings/#tiletype) property.

The cell customizations and color mapping for `rect` tile type is defined in [`appearance`](./appearance/) and [`palette`](./palette/) sections in detail.

## Bubble attributes

The data points can be represented in the bubble along with its attributes by setting the [`tileType`](../api/heatmap/cellSettings/#tiletype) property to `bubble`.

In bubble heat map, you can display the data points with bubble size, bubble colors, and sector attributes of the bubble.

### Bubble size

In this bubble heat map type, the size factor of the bubble is used to denote the data variations. The radius of the bubble varies according to data values.

By default, the bubble with small size denotes the data value with small magnitude and the larger bubble size denotes the data value with larger magnitude. This behavior can be inversed by using the [`isinversedbubblesize`](../api/heatmap/cellSettings/#isinversedbubblesize) property.

To render a bubble heat map with size series, set the [`bubbleType`](../api/heatmap/cellSettings/#bubbletype) property to `Size`.

{% tab template= "heatmap/bubble-heatmap/sizeBubble", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'
       [titleSettings]='titleSettings' [paletteSettings]='paletteSettings' [cellSettings]='cellSettings' [legendSettings]='legendSettings'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

dataSource: Object[] = [
    [73, 39, 26, 39, 94, 0],
    [93, 58, 53, 38, 26, 68],
    [99, 28, 22, 4, 66, 90],
    [14, 26, 97, 69, 69, 3],
    [7, 46, 47, 47, 88, 6],
    [41, 55, 73, 23, 3, 79],
    [56, 69, 21, 86, 3, 33],
    [45, 7, 53, 81, 95, 79],
    [60, 77, 74, 68, 88, 51],
    [25, 25, 10, 12, 78, 14],
    [25, 56, 55, 58, 12, 82],
    [74, 33, 88, 23, 86, 59]];

    titleSettings: Object = {
            text: 'Sales Revenue per Employee (in 1000 US$)',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven',
            'Michael', 'Robert', 'Laura', 'Anne', 'Paul', 'Karin',   'Mario'],
        };
        yAxis: Object = {
            labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
        };
        public paletteSettings: Object = {
                palette: [
                { color: '#C06C84'},
                { color: '#6C5B7B'},
                { color: '#355C7D'}
            ],
            type: "Gradient"
        };
        public cellSettings: Object = {
            border: {
                width: 1
            },
            tileType: 'Bubble',
            bubbleType: 'Size',
            showLabel: false
        };
        public legendSettings: Object = {
            visible: true,
        };
 }

```

{% endtab %}

### Bubble color

In heat map, defined with this tile type, the data points will be represented with same sized bubbles and the data value variations are represented with the bubble colors.

To represent the data points with variations in bubble colors, set the [`bubbleType`](../api/heatmap/cellSettings/#bubbletype) property to `Color`.

{% tab template= "heatmap/bubble-heatmap/colorBubble", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'
       [titleSettings]='titleSettings' [paletteSettings]='paletteSettings' [cellSettings]='cellSettings' [legendSettings]='legendSettings'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

dataSource: Object[] = [
    [73, 39, 26, 39, 94, 0],
    [93, 58, 53, 38, 26, 68],
    [99, 28, 22, 4, 66, 90],
    [14, 26, 97, 69, 69, 3],
    [7, 46, 47, 47, 88, 6],
    [41, 55, 73, 23, 3, 79],
    [56, 69, 21, 86, 3, 33],
    [45, 7, 53, 81, 95, 79],
    [60, 77, 74, 68, 88, 51],
    [25, 25, 10, 12, 78, 14],
    [25, 56, 55, 58, 12, 82],
    [74, 33, 88, 23, 86, 59]];

    titleSettings: Object = {
            text: 'Sales Revenue per Employee (in 1000 US$)',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven',
            'Michael', 'Robert', 'Laura', 'Anne', 'Paul', 'Karin',   'Mario'],
            labelRotation: 45,
            labelIntersectAction: 'None'
        };
        yAxis: Object = {
            labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
        };
        public paletteSettings: Object = {
                palette: [
                { color: '#C06C84'},
                { color: '#6C5B7B'},
                { color: '#355C7D'}
            ],
            type: "Gradient"
        };
        public cellSettings: Object = {
            border: {
                width: 1
            },
            tileType: 'Bubble',
            bubbleType: 'Color'
        };
        public legendSettings: Object = {
            visible: true,
        };
 }

```

{% endtab %}

### Bubble sector

In this bubble heat map type, the sector of the bubble decides the magnitude of data point. If the sector is large, then the data point value will be high.

To render the data points with bubble sector, set the [`bubbleType`](../api/heatmap/cellSettings/#bubbletype) property to `Sector`.

{% tab template= "heatmap/bubble-heatmap/sectorBubble", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'
       [titleSettings]='titleSettings' [paletteSettings]='paletteSettings' [cellSettings]='cellSettings' [legendSettings]='legendSettings'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

dataSource: Object[] = [
    [73, 39, 26, 39, 94, 0],
    [93, 58, 53, 38, 26, 68],
    [99, 28, 22, 4, 66, 90],
    [14, 26, 97, 69, 69, 3],
    [7, 46, 47, 47, 88, 6],
    [41, 55, 73, 23, 3, 79],
    [56, 69, 21, 86, 3, 33],
    [45, 7, 53, 81, 95, 79],
    [60, 77, 74, 68, 88, 51],
    [25, 25, 10, 12, 78, 14],
    [25, 56, 55, 58, 12, 82],
    [74, 33, 88, 23, 86, 59]];

    titleSettings: Object = {
            text: 'Sales Revenue per Employee (in 1000 US$)',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven',
            'Michael', 'Robert', 'Laura', 'Anne', 'Paul', 'Karin',   'Mario'],
        };
        yAxis: Object = {
            labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
        };
        public paletteSettings: Object = {
                palette: [
                { color: '#C06C84'},
                { color: '#6C5B7B'},
                { color: '#355C7D'}
            ],
            type: "Gradient"
        };
        public cellSettings: Object = {
            border: {
                width: 1
            },
            tileType: 'Bubble',
            bubbleType: 'Sector'
        };
        public legendSettings: Object = {
            visible: true,
        };
 }

```

{% endtab %}

### Combining size and color bubble attributes

In this bubble heat map type, you can bind the two data source fields to a single data point. Thereby, each data point represents the two data values with bubble size and bubble color attributes, where the bubble size denotes the magnitude of one data source field and the bubble color denotes the magnitude of another data source field.

To render a bubble heat map with size and color series, set the [`bubbleType`](../api/heatmap/cellSettings/#bubbletype) property to `SizeAndColor`.

#### Binding data for bubble heat map with size and color attributes

##### Array binding - Table

{% tab template= "heatmap/bubble-heatmap/sizeAndColorTable", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'
       [titleSettings]='titleSettings' [paletteSettings]='paletteSettings' [cellSettings]='cellSettings' [legendSettings]='legendSettings' (tooltipRender)='tooltipRender($event)'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

dataSource: Object[] = [
    [[4,39], [3,8], [1,3], [1,10], [4,4], [2,15]],
    [[4,28], [5,92], [5,73], [3,1], [3,4], [4,126]],
    [[4,45], [5,152], [0,44], [4,54], [5,243], [2,45]]
    ];

    titleSettings: Object = {
            text: 'Commercial Aviation Accidents and Fatalities by year 2012 - 2017',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            labels: ['2017', '2016', '2015'],
        };
        yAxis: Object = {
            labels: ['Jan-Feb', 'Mar-Apr', 'May-Jun', 'Jul-Aug', 'Sep-Oct', 'Nov-Dec'],
        };
        public paletteSettings: Object = {
                palette: [
                { color: '#C06C84'},
                { color: '#6C5B7B'},
                { color: '#355C7D'}
            ],
            type: "Gradient"
        };
        public cellSettings: Object = {
            border: {
                width: 1
            },
            tileType: 'Bubble',
            bubbleType: 'SizeAndColor'
        };
        public legendSettings: Object = {
            visible: true,
        };
        public tooltipRender(args: ITooltipEventArgs): void {
        args.content = ['Year ' + ' : ' + args.xLabel + '<br/>' + 'Months ' + ' : ' + args.yLabel + '<br/>'
                + 'Accidents ' + ' : ' + (args.value as BubbleTooltipData[])[0].bubbleData + '<br/>' + 'Fatalities ' + ' : '
                + (args.value as BubbleTooltipData[])[1].bubbleData];
    };
 }

```

{% endtab %}

##### Array binding - Cell

{% tab template= "heatmap/bubble-heatmap/sizeAndColorCell", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [dataSourceSettings]='dataSourceSettings' [xAxis]='xAxis' [yAxis]='yAxis'
       [titleSettings]='titleSettings' [paletteSettings]='paletteSettings' [cellSettings]='cellSettings' [legendSettings]='legendSettings' (tooltipRender)='tooltipRender($event)'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

dataSource:Object[] =  [
    [0,0,[4,39]], [0,1,[3,8]], [0,2,[1,3]], [0,3,[1,10]], [0,4,[4,4]], [0,5,[2,15]],
    [1,0,[4,28]], [1,1,[5,92]], [1,2,[5,73]], [1,3,[3,1]], [1,4,[3,4]], [1,5,[4,126]],
    [2,0,[4,45]], [2,1,[5,152]], [2,2,[0,44]], [2,3,[4,54]], [2,4,[5,243]], [2,5,[2,45]]
    ];
dataSourceSettings: Object = {
            isJsonData: false,
            adaptorType: 'Cell'
        };

    titleSettings: Object = {
            text: 'Commercial Aviation Accidents and Fatalities by year 2012 - 2017',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            labels: ['2017', '2016', '2015'],
        };
        yAxis: Object = {
            labels: ['Jan-Feb', 'Mar-Apr', 'May-Jun', 'Jul-Aug', 'Sep-Oct', 'Nov-Dec'],
        };
        public paletteSettings: Object = {
                palette: [
                { color: '#C06C84'},
                { color: '#6C5B7B'},
                { color: '#355C7D'}
            ],
            type: "Gradient"
        };
        public cellSettings: Object = {
            border: {
                width: 1
            },
            tileType: 'Bubble',
            bubbleType: 'SizeAndColor'
        };
        public legendSettings: Object = {
            visible: true,
        };
        public tooltipRender(args: ITooltipEventArgs): void {
        args.content = ['Year ' + ' : ' + args.xLabel + '<br/>' + 'Months ' + ' : ' + args.yLabel + '<br/>'
                + 'Accidents ' + ' : ' + (args.value as BubbleTooltipData[])[0].bubbleData + '<br/>' + 'Fatalities ' + ' : '
                + (args.value as BubbleTooltipData[])[1].bubbleData];
    };
 }

```

{% endtab %}

##### JSON binding - Table

{% tab template= "heatmap/bubble-heatmap/sizeAndColorJsonTable", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [dataSourceSettings]='dataSourceSettings' [xAxis]='xAxis' [yAxis]='yAxis'
       [titleSettings]='titleSettings' [paletteSettings]='paletteSettings' [cellSettings]='cellSettings' [legendSettings]='legendSettings' (tooltipRender)='tooltipRender($event)'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

dataSource:Object[] =             [
        { 'Year': '2017', 'Jan-Feb': [4,39], 'Mar-Apr': [3,8], 'May-Jun': [1,3], 'Jul-Aug': [1,10], 'Sep-Oct': [4,4], 'Nov-Dec': [2,15]},
        { 'Year': '2016', 'Jan-Feb': [4,28], 'Mar-Apr': [5,92], 'May-Jun': [5,73], 'Jul-Aug': [3,1], 'Sep-Oct': [3,4], 'Nov-Dec': [4,126]},
        { 'Year': '2015', 'Jan-Feb': [4,45], 'Mar-Apr': [5,152], 'May-Jun': [0,44], 'Jul-Aug':[4,54], 'Sep-Oct': [5,243], 'Nov-Dec': [2,45]}
        ];
dataSourceSettings: Object = {
            isJsonData: true,
            adaptorType: 'Table',
            xDataMapping: 'Year',
        };

    titleSettings: Object = {
            text: 'Commercial Aviation Accidents and Fatalities by year 2012 - 2017',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            labels: ['2017', '2016', '2015'],
        };
        yAxis: Object = {
            labels: ['Jan-Feb', 'Mar-Apr', 'May-Jun', 'Jul-Aug', 'Sep-Oct', 'Nov-Dec'],
        };
        public paletteSettings: Object = {
                palette: [
                { color: '#C06C84'},
                { color: '#6C5B7B'},
                { color: '#355C7D'}
            ],
            type: "Gradient"
        };
        public cellSettings: Object = {
            border: {
                width: 1
            },
            tileType: 'Bubble',
            bubbleType: 'SizeAndColor'
        };
        public legendSettings: Object = {
            visible: true,
        };
        public tooltipRender(args: ITooltipEventArgs): void {
        args.content = ['Year ' + ' : ' + args.xLabel + '<br/>' + 'Months ' + ' : ' + args.yLabel + '<br/>'
                + 'Accidents ' + ' : ' + (args.value as BubbleTooltipData[])[0].bubbleData + '<br/>' + 'Fatalities ' + ' : '
                + (args.value as BubbleTooltipData[])[1].bubbleData];
    };
 }

```

{% endtab %}

##### JSON binding - Cell

{% tab template= "heatmap/bubble-heatmap/sizeAndColorJsonCell", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [dataSourceSettings]='dataSourceSettings' [xAxis]='xAxis' [yAxis]='yAxis'
       [titleSettings]='titleSettings' [paletteSettings]='paletteSettings' [cellSettings]='cellSettings' [legendSettings]='legendSettings' (tooltipRender)='tooltipRender($event)'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
dataSource:Object[] = [
            { Year: '2017', Months: 'Jan-Feb', Accidents: 4, Fatalities: 39 },
            { Year: '2017', Months: 'Mar-Apr', Accidents: 3, Fatalities: 8 },
            { Year: '2017', Months: 'May-Jun', Accidents: 1, Fatalities: 3 },
            { Year: '2017', Months: 'Jul-Aug', Accidents: 1, Fatalities: 10 },
            { Year: '2017', Months: 'Sep-Oct', Accidents: 4, Fatalities: 4 },
            { Year: '2017', Months: 'Nov-Dec', Accidents: 2, Fatalities: 15 },
            { Year: '2016', Months: 'Jan-Feb', Accidents: 4, Fatalities: 28 },
            { Year: '2016', Months: 'Mar-Apr', Accidents: 5, Fatalities: 92 },
            { Year: '2016', Months: 'May-Jun', Accidents: 5, Fatalities: 73 },
            { Year: '2016', Months: 'Jul-Aug', Accidents: 3, Fatalities: 1 },
            { Year: '2016', Months: 'Sep-Oct', Accidents: 3, Fatalities: 4 },
            { Year: '2016', Months: 'Nov-Dec', Accidents: 4, Fatalities: 126 },
            { Year: '2015', Months: 'Jan-Feb', Accidents: 4, Fatalities: 45 },
            { Year: '2015', Months: 'Mar-Apr', Accidents: 5, Fatalities: 152 },
            { Year: '2015', Months: 'May-Jun', Accidents: 0, Fatalities: 0 },
            { Year: '2015', Months: 'Jul-Aug', Accidents: 4, Fatalities: 54 },
            { Year: '2015', Months: 'Sep-Oct', Accidents: 5, Fatalities: 243 },
            { Year: '2015', Months: 'Nov-Dec', Accidents: 2, Fatalities: 45 },
        ];
dataSourceSettings: Object = {
            isJsonData: true,
            adaptorType: 'Cell',
            xDataMapping: 'Year',
            yDataMapping: 'Months',
            bubbleDataMapping: { size: 'Accidents', color: 'Fatalities' }
        };

    titleSettings: Object = {
            text: 'Commercial Aviation Accidents and Fatalities by year 2012 - 2017',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            labels: ['2017', '2016', '2015'],
        };
        yAxis: Object = {
            labels: ['Jan-Feb', 'Mar-Apr', 'May-Jun', 'Jul-Aug', 'Sep-Oct', 'Nov-Dec'],
        };
        public paletteSettings: Object = {
                palette: [
                { color: '#C06C84'},
                { color: '#6C5B7B'},
                { color: '#355C7D'}
            ],
            type: "Gradient"
        };
        public cellSettings: Object = {
            border: {
                width: 1
            },
            tileType: 'Bubble',
            bubbleType: 'SizeAndColor'
        };
        public legendSettings: Object = {
            visible: true,
        };
        public tooltipRender(args: ITooltipEventArgs): void {
        args.content = ['Year ' + ' : ' + args.xLabel + '<br/>' + 'Months ' + ' : ' + args.yLabel + '<br/>'
                + 'Accidents ' + ' : ' + (args.value as BubbleTooltipData[])[0].bubbleData + '<br/>' + 'Fatalities ' + ' : '
                + (args.value as BubbleTooltipData[])[1].bubbleData];
    };
 }

```

{% endtab %}