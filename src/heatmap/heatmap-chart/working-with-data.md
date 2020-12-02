---
title: "Working with data"
component: "Heatmap"
description: "This section describes the data binding options available in heatmap. User can bind either two-dimensional array or JSON data to the heatmap."
---

# Working with data

Heat map visualizes the JSON data and two-dimensional array data. Using the data adaptor support, data can be bound to the heat map.

## Data adaptor

Heat map supports the following types of data binding with the adaptor support.

* Array
    * Table Binding
    * Cell Binding
* JSON data
    * Table Binding
    * Cell Binding

### Array - table binding

This data type is a collection of one dimensional array objects, at which each inner array contains data points for an X-axis data label. This is the default data binding type for heat map. You can also directly bind the array object to the [`dataSource`](../api/heatmap/#datasource) property.

{% tab template= "heatmap/working-with-data/arraytable", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'
       (tooltipRender)='tooltipRender($event)' [titleSettings]='titleSettings' [paletteSettings]='paletteSettings' [legendSettings]='legendSettings' [showTooltip]='showTooltip'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
dataSource: Object[] = [
        [9.5, 2.2, 4.2, 8.2, -0.5, 3.2, 5.4, 7.4, 6.2, 1.4],
        [4.3, 8.9, 10.8, 6.5, 5.1, 6.2, 7.6, 7.5, 6.1, 7.6],
        [3.9, 2.7, 2.5, 3.7, 2.6, 5.1, 5.8, 2.9, 4.5, 5.1],
        [2.4, -3.7, 4.1, 6.0, 5.0, 2.4, 3.3, 4.6, 4.3, 2.7],
        [2.0, 7.0, -4.1, 8.9, 2.7, 5.9, 5.6, 1.9, -1.7, 2.9],
        [5.4, 1.1, 6.9, 4.5, 2.9, 3.4, 1.5, -2.8, -4.6, 1.2],
        [-1.3, 3.9, 3.5, 6.6, 5.2, 7.7, 1.4, -3.6, 6.6, 4.3],
        [-1.6, 2.3, 2.9, -2.5, 1.3, 4.9, 10.1, 3.2, 4.8, 2.0],
        [10.8, -1.6, 4.0, 6.0, 7.7, 2.6, 5.6, -2.5, 3.8, -1.9],
        [6.2, 9.8, -1.5, 2.0, -1.5, 4.3, 6.7, 3.8, -1.2, 2.4],
        [1.2, 10.9, 4.0, -1.4, 2.2, 1.6, -2.6, 2.3, 1.7, 2.4],
        [5.1, -2.4, 8.2, -1.1, 3.5, 6.0, -1.3, 7.2, 9.0, 4.2]
    ];

        titleSettings: Object = {
            text: 'GDP Growth Rate for Major Economies (in Percentage)',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            labels: ['China', 'India', 'Australia', 'Mexico', 'Canada', 'Brazil',
                'USA', 'UK', 'Germany', 'Russia', 'France', 'Japan'],
            labelRotation: 45,
            labelIntersectAction: 'None',
        };
        yAxis: Object = {
            labels: ['2008', '2009', '2010', '2011', '2012', '2013', '2014', '2015', '2016', '2017']
        };
         public paletteSettings: Object = {
            palette: [
                { value: -1, color: '#F0D6AD' },
                { value: 0, color: '#9da49a' },
                { value: 3.5, color: '#d7c7a7' },
                { value: 6.0, color: '#6e888f' },
                { value: 7.5, color: '#466f86' },
                { value: 10, color: '#19547B' },
            ],
        };
        public legendSettings: Object = {
            visible: false
        };
        public tooltipRender(args: ITooltipEventArgs): void {
            args.content = [args.yLabel + ' | ' + args.xLabel + ' : ' + args.value + ' %'];
        };
        public showTooltip: Boolean = true;
}

```

{% endtab %}

### Array - cell binding

This data type is a collection of array objects that contain information about the row index, column index, and data value for each cell. You can bind the data to heat map by using the [`data`](../api/heatmap/data/#data) property in the [`dataSource`](../api/heatmap/#datasource) and setting the [`adaptorType`](../api/heatmap/data/#adaptortype) property to `Cell`.

{% tab template= "heatmap/working-with-data/arraycell", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [dataSourceSettings]='dataSourceSettings' [xAxis]='xAxis' [yAxis]='yAxis'
       (tooltipRender)='tooltipRender($event)' [titleSettings]='titleSettings' [cellSettings]='cellSettings' [paletteSettings]='paletteSettings' [legendSettings]='legendSettings'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

        titleSettings: Object = {
            text: 'Percentage of Individuals Using Internet by Country',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            labels: ['China', 'Australia', 'Mexico', 'Canada', 'Brazil', 'USA',
                'UK', 'Germany', 'Russia', 'France', 'Japan'],
        };
        yAxis: Object = {
            labels: ['2000', '2005', '2010', '2011', '2012', '2013', '2014'],
        };
        dataSource: Object[] = [
        [0, 0, 10.75], [0, 1, 14.5], [0, 2, 25.5], [0, 3, 39.5], [0, 4, 59.75], [0, 5, 35.50], [0, 6, 75.5],
        [1, 0, 20.75], [1, 1, 35.5], [1, 2, 29.5], [1, 3, 75.5], [1, 4, 80], [1, 5, 65], [1, 6, 85],
        [2, 0, 6], [2, 1, 18.5], [2, 2, 30.05], [2, 3, 35.5], [2, 4, 40.75], [2, 5, 50.75], [2, 6, 65],
        [3, 0, 30.5], [3, 1, 20.5], [3, 2, 45.30], [3, 3, 50], [3, 4, 55], [3, 5, 85.80], [3, 6, 87.5],
        [4, 0, 10.5], [4, 1, 20.75], [4, 2, 35.5], [4, 3, 35.5], [4, 4, 45.5], [4, 5, 65.], [4, 6, 75.5],
        [5, 0, 45.5], [5, 1, 20.75], [5, 2, 45.5], [5, 3, 50.75], [5, 4, 79.30], [5, 5, 84.20], [5, 6, 87.36],
        [6, 0, 26.82], [6, 1, 70], [6, 2, 75], [6, 3, 79.5], [6, 4, 88.5], [6, 5, 89.5], [6, 6, 91.75],
        [7, 0, 15.75], [7, 1, 20.75], [7, 2, 25.5], [7, 3, 42.35], [7, 4, 45.15], [7, 5, 76.5], [7, 6, 80.5],
        [8, 0, 1.98], [8, 1, 15.23], [8, 2, 43], [8, 3, 49], [8, 4, 63.80], [8, 5, 67.97], [8, 6, 70.52],
        [9, 0, 14.31], [9, 1, 42.87], [9, 2, 77.28], [9, 3, 77.82], [9, 4, 81.44], [9, 5, 81.92], [9, 6, 83.75],
        [10, 0, 25.5], [10, 1, 35.5], [10, 2, 40.5], [10, 3, 45.05], [10, 4, 50.5], [10, 5, 75.5], [10, 6, 90.58]
        ];
        dataSourceSettings: Object = {
            isJsonData: false,
            adaptorType: 'Cell'
        };
        public paletteSettings: Object = {
            palette: [{ color: '#3498DB' },
            { color: '#2C3E50' }
            ]
        };
        public cellSettings: Object = {
            border: {
                width: '0'
            },
            textStyle: {
                color: 'white'
            },
            format: '{value} %'
        };
        public legendSettings: Object = {
            visible: false,
        };
        public tooltipRender(args: ITooltipEventArgs): void {
            args.content = [args.yLabel + ' | ' + args.xLabel + ' : ' + args.value + ' %'];
        };
}

```

{% endtab %}

### JSON data - table binding

In JSON table data binding, each JSON object contains an X-axis data point as row header and all the corresponding Y-axis data values. You can bind the JSON table data to the heat map using the [`data`](../api/heatmap/data/#data) property in [`dataSource`](../api/heatmap/#datasource). To achieve this, you should enable the [`isJsonData`](../api/heatmap/data/#isjsondata) property and  define the [`adaptorType`](../api/heatmap/data/#adaptortype) property as `Table`. The [`xDataMapping`](../api/heatmap/data/#xdatamapping) property is used to map the row header in JSON data.

{% tab template= "heatmap/working-with-data/jsontable", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [dataSourceSettings]='dataSourceSettings' [xAxis]='xAxis' [yAxis]='yAxis'
       [cellSettings]='cellSettings' [titleSettings]='titleSettings' [paletteSettings]='paletteSettings'>
        </ejs-heatmap>`
})
export class AppComponent{

        titleSettings: Object = {
            text: 'Olympic Medal Achievements of most Successful Countries',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            labels: ['China', 'France', 'GBR', 'Germany', 'Italy', 'Japan', 'KOR', 'Russia', 'USA'],
            labelRotation: 45,
            labelIntersectAction: 'None',
        };
        yAxis: Object = {
            title : {text: 'Olympic Year'},
            labels: ['2000', '2004', '2008', '2012', '2016'],
        };
        dataSource: Object[] = [
        { 'Region': 'USA', '2000': 93, '2004': 101, '2008': 112, '2012': 103, '2016': 121 },
        { 'Region': 'GBR', '2000': 28, '2004': 30, '2008': 49, '2012': 65, '2016': 67 },
        { 'Region': 'China', '2000': 58, '2004': 63, '2008': 100, '2012': 91, '2016': 70 },
        { 'Region': 'Russia', '2000': 89, '2004': 90, '2008': 60, '2012': 69, '2016': 55 },
        { 'Region': 'Germany', '2000': 56, '2004': 49, '2008': 41, '2012': 44, '2016': 42 },
        { 'Region': 'Japan', '2000': 18, '2004': 37, '2008': 25, '2012': 38, '2016': 41 },
        { 'Region': 'France', '2000': 38, '2004': 33, '2008': 43, '2012': 35, '2016': 42 },
        { 'Region': 'KOR', '2000': 28, '2004': 30, '2008': 32, '2012': 30, '2016': 21 },
        { 'Region': 'Italy', '2000': 34, '2004': 32, '2008': 27, '2012': 28, '2016': 28 }
        ];
        dataSourceSettings: Object = {
            isJsonData: true,
            adaptorType: 'Table',
            xDataMapping: 'Region',
        };
        paletteSettings: Object = {
            palette: [{ color: '#F0C27B' },
            { color: '#4B1248' }
            ],
        };
        cellSettings: Object = {
            border: {
                width: 1,
                radius: 4,
                color: 'white'
            }
        };
}

```

{% endtab %}

### JSON data - Cell binding

In JSON cell data binding, each JSON object consists a value for each cell along with a mapping value for row and column. You can bind the JSON cell data having information for each cell to the heat map using the [`data`](../api/heatmap/data/#data) property in [`dataSource`](../api/heatmap/#datasource). To achieve this, you should define the [`adaptorType`](../api/heatmap/data/#adaptortype) property as `Cell` and enable the [`isJsonData`](../api/heatmap/data/#isjsondata) property. Now, map the fields of data by using the [`valueMapping`](../api/heatmap/data/#valuemapping),
[`xDataMapping`](../api/heatmap/data/#xdatamapping) and [`yDataMapping`](../api/heatmap/data/#ydatamapping) properties.

{% tab template= "heatmap/working-with-data/jsoncell", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [dataSourceSettings]='dataSourceSettings' [xAxis]='xAxis' [yAxis]='yAxis'
       [cellSettings]='cellSettings' [titleSettings]='titleSettings' [paletteSettings]='paletteSettings'>
        </ejs-heatmap>`
})
export class AppComponent{

        titleSettings: Object = {
            text: 'Most Visited Destinations by International Tourist Arrivals',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            labels: ['Austria', 'China', 'France', 'Germany', 'Italy', 'Mexico', 'Spain', 'Thailand', 'UK', 'USA'],
        };
        yAxis: Object = {
            labels: ['2010', '2011', '2012', '2013', '2014', '2015', '2016'],
        };
        dataSource: Object[] = [
        { 'rowid': 'France', 'columnid': '2010', 'value': '77.6' },
        { 'rowid': 'France', 'columnid': '2011', 'value': '79.4' },
        { 'rowid': 'France', 'columnid': '2012', 'value': '80.8' },
        { 'rowid': 'France', 'columnid': '2013', 'value': '86.6' },
        { 'rowid': 'France', 'columnid': '2014', 'value': '83.7' },
        { 'rowid': 'France', 'columnid': '2015', 'value': '84.5' },
        { 'rowid': 'France', 'columnid': '2016', 'value': '82.6' },
        { 'rowid': 'USA', 'columnid': '2010', 'value': '60.6' },
        { 'rowid': 'USA', 'columnid': '2011', 'value': '65.4' },
        { 'rowid': 'USA', 'columnid': '2012', 'value': '70.8' },
        { 'rowid': 'USA', 'columnid': '2013', 'value': '73.8' },
        { 'rowid': 'USA', 'columnid': '2014', 'value': '75.3' },
        { 'rowid': 'USA', 'columnid': '2015', 'value': '77.5' },
        { 'rowid': 'USA', 'columnid': '2016', 'value': '77.6' },
        { 'rowid': 'Spain', 'columnid': '2010', 'value': '64.9' },
        { 'rowid': 'Spain', 'columnid': '2011', 'value': '52.6' },
        { 'rowid': 'Spain', 'columnid': '2012', 'value': '60.8' },
        { 'rowid': 'Spain', 'columnid': '2013', 'value': '65.6' },
        { 'rowid': 'Spain', 'columnid': '2014', 'value': '52.6' },
        { 'rowid': 'Spain', 'columnid': '2015', 'value': '68.5' },
        { 'rowid': 'Spain', 'columnid': '2016', 'value': '75.6' },
        { 'rowid': 'China', 'columnid': '2010', 'value': '55.6' },
        { 'rowid': 'China', 'columnid': '2011', 'value': '52.3' },
        { 'rowid': 'China', 'columnid': '2012', 'value': '54.8' },
        { 'rowid': 'China', 'columnid': '2013', 'value': '51.1' },
        { 'rowid': 'China', 'columnid': '2014', 'value': '55.6' },
        { 'rowid': 'China', 'columnid': '2015', 'value': '56.9' },
        { 'rowid': 'China', 'columnid': '2016', 'value': '59.3' },
        { 'rowid': 'Italy', 'columnid': '2010', 'value': '43.6' },
        { 'rowid': 'Italy', 'columnid': '2011', 'value': '43.2' },
        { 'rowid': 'Italy', 'columnid': '2012', 'value': '55.8' },
        { 'rowid': 'Italy', 'columnid': '2013', 'value': '50.1' },
        { 'rowid': 'Italy', 'columnid': '2014', 'value': '48.5' },
        { 'rowid': 'Italy', 'columnid': '2015', 'value': '50.7' },
        { 'rowid': 'Italy', 'columnid': '2016', 'value': '52.4' },
        { 'rowid': 'UK', 'columnid': '2010', 'value': '28.2' },
        { 'rowid': 'UK', 'columnid': '2011', 'value': '31.6' },
        { 'rowid': 'UK', 'columnid': '2012', 'value': '29.8' },
        { 'rowid': 'UK', 'columnid': '2013', 'value': '33.1' },
        { 'rowid': 'UK', 'columnid': '2014', 'value': '32.6' },
        { 'rowid': 'UK', 'columnid': '2015', 'value': '34.4' },
        { 'rowid': 'UK', 'columnid': '2016', 'value': '35.8' },
        { 'rowid': 'Germany', 'columnid': '2010', 'value': '26.8' },
        { 'rowid': 'Germany', 'columnid': '2011', 'value': '29' },
        { 'rowid': 'Germany', 'columnid': '2012', 'value': '26.8' },
        { 'rowid': 'Germany', 'columnid': '2013', 'value': '27.6' },
        { 'rowid': 'Germany', 'columnid': '2014', 'value': '33' },
        { 'rowid': 'Germany', 'columnid': '2015', 'value': '35' },
        { 'rowid': 'Germany', 'columnid': '2016', 'value': '35.6' },
        { 'rowid': 'Mexico', 'columnid': '2010', 'value': '23.2' },
        { 'rowid': 'Mexico', 'columnid': '2011', 'value': '24.9' },
        { 'rowid': 'Mexico', 'columnid': '2012', 'value': '30.1' },
        { 'rowid': 'Mexico', 'columnid': '2013', 'value': '22.2' },
        { 'rowid': 'Mexico', 'columnid': '2014', 'value': '29.3' },
        { 'rowid': 'Mexico', 'columnid': '2015', 'value': '32.1' },
        { 'rowid': 'Mexico', 'columnid': '2016', 'value': '35' },
        { 'rowid': 'Thailand', 'columnid': '2010', 'value': '15.9' },
        { 'rowid': 'Thailand', 'columnid': '2011', 'value': '19.8' },
        { 'rowid': 'Thailand', 'columnid': '2012', 'value': '21.8' },
        { 'rowid': 'Thailand', 'columnid': '2013', 'value': '23.5' },
        { 'rowid': 'Thailand', 'columnid': '2014', 'value': '24.8' },
        { 'rowid': 'Thailand', 'columnid': '2015', 'value': '29.9' },
        { 'rowid': 'Thailand', 'columnid': '2016', 'value': '32.6' },
        { 'rowid': 'Austria', 'columnid': '2010', 'value': '22' },
        { 'rowid': 'Austria', 'columnid': '2011', 'value': '21.3' },
        { 'rowid': 'Austria', 'columnid': '2012', 'value': '24.2' },
        { 'rowid': 'Austria', 'columnid': '2013', 'value': '23.2' },
        { 'rowid': 'Austria', 'columnid': '2014', 'value': '25' },
        { 'rowid': 'Austria', 'columnid': '2015', 'value': '26.7' },
        { 'rowid': 'Austria', 'columnid': '2016', 'value': '28.1' },
    ];
        dataSourceSettings: Object = {
            isJsonData: true,
            adaptorType: 'Cell',
            xDataMapping: 'rowid',
            yDataMapping: 'columnid',
            valueMapping: 'value'
        };
         cellSettings: Object = {
            border: {
                radius: 4,
                width: 1,
                color: 'white'
            },
            showLabel: true,
            format: '{value} M',
        };
         paletteSettings: Object = {
            palette: [{ color: '#DCD57E' },
            { color: '#A6DC7E' },
            { color: '#7EDCA2' },
            { color: '#6EB5D0' }
            ],
        };
}

```

{% endtab %}

## Empty points

The data points that use the `null` or `""` or `undefined` as value are considered as empty points. Empty data points are ignored and not displayed in the heat map, and these points are rendered with default palette. You can customize the empty data point color value using the [`emptyPointColor`](../api/heatmap/paletteSettings/#emptypointcolor) property.

{% tab template= "heatmap/working-with-data/emptypoint", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';
@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'
        [legendSettings]='legendSettings'>
        </ejs-heatmap>`
})
export class AppComponent{

        xAxis: Object = {
            valueType:"DateTime",
            minimum: new Date(2007,0,1),
            intervalType:"Years",
            labelFormat:"yyyy",
        };
        yAxis: Object = {
           valueType:"Numeric"
        };
        legendSettings: Object = {
            visible: false,
        };
        dataSource: Object[] = [
        [73, 39, 26, 39, 94, 0],
        [93, 58, 53, 38, 26, 68],
        [99, 28, null, 4, 66, 90],
        [14, 26, 97, 69, 69, 3],
        [7, 46, 47, 47, 88, 6],
        [41, 55, 73, 23, "", 79],
        [56, 69, 21, 86, 3, 33],
        [45, 7, undefined, 81, 95, 79],
        [60, 77, 74, 68, 88, 51],
        [25, 25, 10, 12, 78, 14],
        [25, 56, 55, 58, 12, 82],
        [74, 33, 88, 23, 86, 59]
    ];
}

```

{% endtab %}

## Binding nested JSON data

In complex data binding, you can bind the nested JSON data to the data points in the heat map.
The nested data can be mapped using the [`xDataMapping`](../api/heatmap/data/#xdatamapping), [`yDataMapping`](../api/heatmap/data/#ydatamapping), [`valueMapping`](../api/heatmap/data/#valuemapping)
and [`bubbleDataMapping`](../api/heatmap/data/#bubbledatamapping) properties as string value concatenated by a dot.

{% tab template= "heatmap/working-with-data/nestedJsonCell", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';
import { HeatMap, ITooltipEventArgs } from '@syncfusion/ej2-heatmap';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [dataSourceSettings]='dataSourceSettings' [xAxis]='xAxis' [yAxis]='yAxis'
       [cellSettings]='cellSettings' [titleSettings]='titleSettings' [paletteSettings]='paletteSettings'>
        </ejs-heatmap>`
})
export class AppComponent{

        titleSettings: Object = {
            text: 'Most Visited Destinations by International Tourist Arrivals',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            labels: ['Austria', 'China', 'France', 'Germany', 'Italy', 'Mexico', 'Spain', 'Thailand', 'UK', 'USA'],
        };
        yAxis: Object = {
            labels: ['2010', '2011', '2012', '2013', '2014', '2015', '2016'],
        };
        dataSource: Object[] = [
        { 'Labels':{'Xlabel': 'France','Ylabel': '2010' },'data':{'value': '77.6' }},
{ 'Labels':{'Xlabel': 'France','Ylabel': '2011'},'data':{'value': '79.4'}},
{ 'Labels':{'Xlabel': 'France','Ylabel': '2012'},'data':{'value': '80.8'}},
{ 'Labels':{'Xlabel': 'France','Ylabel': '2013'},'data':{'value': '86.6'}},
{ 'Labels':{'Xlabel': 'France','Ylabel': '2014'},'data':{'value': '83.7'}},
{ 'Labels':{'Xlabel': 'France','Ylabel': '2015'},'data':{'value': '84.5'}},
{ 'Labels':{'Xlabel': 'France','Ylabel': '2016'},'data':{'value': '82.6'}},
{ 'Labels':{'Xlabel': 'USA','Ylabel': '2010'},'data':{'value': '60.6'}},
{ 'Labels':{'Xlabel': 'USA','Ylabel': '2011'},'data':{'value': '65.4'}},
{ 'Labels':{'Xlabel': 'USA','Ylabel': '2012'},'data':{'value': '70.8'}},
{ 'Labels':{'Xlabel': 'USA','Ylabel': '2013'},'data':{'value': '73.8'}},
{ 'Labels':{'Xlabel': 'USA','Ylabel': '2014'},'data':{'value': '75.3'}},
{ 'Labels':{'Xlabel': 'USA','Ylabel': '2015'},'data':{'value': '77.5'}},
{ 'Labels':{'Xlabel': 'USA','Ylabel': '2016'},'data':{'value': '77.6'}},
{ 'Labels':{'Xlabel': 'Spain','Ylabel': '2010'},'data':{'value': '64.9'}},
{ 'Labels':{'Xlabel': 'Spain','Ylabel': '2011'},'data':{'value': '52.6'}},
{ 'Labels':{'Xlabel': 'Spain','Ylabel': '2012'},'data':{'value': '60.8'}},
{ 'Labels':{'Xlabel': 'Spain','Ylabel': '2013'},'data':{'value': '65.6'}},
{ 'Labels':{'Xlabel': 'Spain','Ylabel': '2014'},'data':{'value': '52.6'}},
{ 'Labels':{'Xlabel': 'Spain','Ylabel': '2015'},'data':{'value': '68.5'}},
{ 'Labels':{'Xlabel': 'Spain','Ylabel': '2016'},'data':{'value': '75.6'}},
{ 'Labels':{'Xlabel': 'China','Ylabel': '2010'},'data':{'value': '55.6'}},
{ 'Labels':{'Xlabel': 'China','Ylabel': '2011'},'data':{'value': '52.3'}},
{ 'Labels':{'Xlabel': 'China','Ylabel': '2012'},'data':{'value': '54.8'}},
{ 'Labels':{'Xlabel': 'China','Ylabel': '2013'},'data':{'value': '51.1'}},
{ 'Labels':{'Xlabel': 'China','Ylabel': '2014'},'data':{'value': '55.6'}},
{ 'Labels':{'Xlabel': 'China','Ylabel': '2015'},'data':{'value': '56.9'}},
{ 'Labels':{'Xlabel': 'China','Ylabel': '2016'},'data':{'value': '59.3'}},
{ 'Labels':{'Xlabel': 'Italy','Ylabel': '2010'},'data':{'value': '43.6'}},
{ 'Labels':{'Xlabel': 'Italy','Ylabel': '2011'},'data':{'value': '43.2'}},
{ 'Labels':{'Xlabel': 'Italy','Ylabel': '2012'},'data':{'value': '55.8'}},
{ 'Labels':{'Xlabel': 'Italy','Ylabel': '2013'},'data':{'value': '50.1'}},
{ 'Labels':{'Xlabel': 'Italy','Ylabel': '2014'},'data':{'value': '48.5'}},
{ 'Labels':{'Xlabel': 'Italy','Ylabel': '2015'},'data':{'value': '50.7'}},
{ 'Labels':{'Xlabel': 'Italy','Ylabel': '2016'},'data':{'value': '52.4'}},
{ 'Labels':{'Xlabel': 'UK','Ylabel': '2010'},'data':{'value': '28.2'}},
{ 'Labels':{'Xlabel': 'UK','Ylabel': '2011'},'data':{'value': '31.6'}},
{ 'Labels':{'Xlabel': 'UK','Ylabel': '2012'},'data':{'value': '29.8'}},
{ 'Labels':{'Xlabel': 'UK','Ylabel': '2013'},'data':{'value': '33.1'}},
{ 'Labels':{'Xlabel': 'UK','Ylabel': '2014'},'data':{'value': '32.6'}},
{ 'Labels':{'Xlabel': 'UK','Ylabel': '2015'},'data':{'value': '34.4'}},
{ 'Labels':{'Xlabel': 'UK','Ylabel': '2016'},'data':{'value': '35.8'}},
{ 'Labels':{'Xlabel': 'Germany','Ylabel': '2010'},'data':{'value': '26.8'}},
{ 'Labels':{'Xlabel': 'Germany','Ylabel': '2011'},'data':{'value': '29' }},
{ 'Labels':{'Xlabel': 'Germany','Ylabel': '2012'},'data':{'value': '26.8'}},
{ 'Labels':{'Xlabel': 'Germany','Ylabel': '2013'},'data':{'value': '27.6'}},
{ 'Labels':{'Xlabel': 'Germany','Ylabel': '2014'},'data':{'value': '33' }},
{ 'Labels':{'Xlabel': 'Germany','Ylabel': '2015'},'data':{'value': '35' }},
{ 'Labels':{'Xlabel': 'Germany','Ylabel': '2016'},'data':{'value': '35.6'}},
{ 'Labels':{'Xlabel': 'Mexico','Ylabel': '2010'},'data':{'value': '23.2'}},
{ 'Labels':{'Xlabel': 'Mexico','Ylabel': '2011'},'data':{'value': '24.9'}},
{ 'Labels':{'Xlabel': 'Mexico','Ylabel': '2012'},'data':{'value': '30.1'}},
{ 'Labels':{'Xlabel': 'Mexico','Ylabel': '2013'},'data':{'value': '22.2'}},
{ 'Labels':{'Xlabel': 'Mexico','Ylabel': '2014'},'data':{'value': '29.3'}},
{ 'Labels':{'Xlabel': 'Mexico','Ylabel': '2015'},'data':{'value': '32.1'}},
{ 'Labels':{'Xlabel': 'Mexico','Ylabel': '2016'}, 'data':{'value': '35' }},
{ 'Labels':{'Xlabel': 'Thailand','Ylabel': '2010'},'data':{'value': '15.9'}},
{ 'Labels':{'Xlabel': 'Thailand','Ylabel': '2011'},'data':{'value': '19.8'}},
{ 'Labels':{'Xlabel': 'Thailand','Ylabel': '2012'},'data':{'value': '21.8'}},
{ 'Labels':{'Xlabel': 'Thailand','Ylabel': '2013'},'data':{'value': '23.5'}},
{ 'Labels':{'Xlabel': 'Thailand','Ylabel': '2014'},'data':{'value': '24.8'}},
{ 'Labels':{'Xlabel': 'Thailand','Ylabel': '2015'},'data':{'value': '29.9'}},
{ 'Labels':{'Xlabel': 'Thailand','Ylabel': '2016'},'data':{'value': '32.6'}},
{ 'Labels':{'Xlabel': 'Austria','Ylabel': '2010'},'data':{'value': '22' }},
{ 'Labels':{'Xlabel': 'Austria','Ylabel': '2011'},'data':{'value': '21.3'}},
{ 'Labels':{'Xlabel': 'Austria','Ylabel': '2012'},'data':{'value': '24.2'}},
{ 'Labels':{'Xlabel': 'Austria','Ylabel': '2013'},'data':{'value': '23.2'}},
{ 'Labels':{'Xlabel': 'Austria','Ylabel': '2014'},'data':{'value': '25' }},
{ 'Labels':{'Xlabel': 'Austria','Ylabel': '2015'},'data':{'value': '26.7' }},
{ 'Labels':{'Xlabel': 'Austria','Ylabel': '2016'},'data':{'value': '28.1' }}
    ];
        dataSourceSettings: Object = {
            isJsonData: true,
            adaptorType: 'Cell',
            xDataMapping: 'Labels.Xlabel',
            yDataMapping: 'Labels.Ylabel',
            valueMapping: 'data.value'
        };
         cellSettings: Object = {
            border: {
                radius: 4,
                width: 1,
                color: 'white'
            },
            showLabel: true,
            format: '{value} M',
        };
         paletteSettings: Object = {
            palette: [{ color: '#DCD57E' },
            { color: '#A6DC7E' },
            { color: '#7EDCA2' },
            { color: '#6EB5D0' }
            ],
        };
}

```

{% endtab %}

## See Also

* [To bind data for bubble heat map with size and color attributes](./bubble-heatmap/#binding-data-for-bubble-heat-map-with-size-and-color-attributes)