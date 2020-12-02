---
title: "Axis"
component: "Heatmap"
description: "This section describes the axis types available in heatmap and other axis customizations available in heatmap like inversed axis, opposed axis and axis label formatting"
---

# Axis

Heat map consists of two axes namely, X-axis and Y-axis that displays the row headers and column headers to plot the data points respectively. You can define the type, format, and other customizing options for both axes in the heat map.

## Types

There are three different axis types available in the heat map, which defines the data type of the axis labels. You can define the axis type by using the [`valueType`](../api/heatmap/axis/#valuetype) property in the heat map.

### Category axis

Category axis type is used to represent the string values in axis labels.

{% tab template= "heatmap/axis/categoryaxis", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

dataSource: Object [] = [
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

    xAxis: Object = {
        valueType:"Category",
        labels: ['Nancy', 'Andrew','Janet', 'Margaret', 'Steven',
        'Michael', 'Robert', 'Laura', 'Anne', 'Paul', 'Karin', 'Mario'],
         };
         yAxis: Object = {
             valueType:"Category",
             labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
             };
}

```

{% endtab %}

### Numeric axis

Numeric axis type is used to represent the numeric values in axis labels.

{% tab template= "heatmap/axis/numericaxis", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

dataSource: Object [] = [
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

    xAxis: Object = {
        valueType:"Numeric",
        minimum: 0,
        maximum: 11,
         };
    yAxis: Object = {
             valueType:"Numeric",
             minimum: 0,
             maximum: 5,
             };
}

```

{% endtab %}

### Date-time axis

Date-time axis type is used to represent the date-time values in axis labels with a specific format. In date-time axis, you can define the start and end date/time using the [`minimum`](../api/heatmap/axis/#minimum) and [`maximum`](../api/heatmap/axis/#maximum) properties.

{% tab template= "heatmap/axis/datetimeaxis", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'
       [titleSettings]='titleSettings' [legendSettings]='legendSettings' [cellSettings]='cellSettings'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

dataSource: Object[] = [
            [36371, 25675, 28292, 33399, 35980, 38585, 39351, 39964, 36543, 30529, 33298, 36985],
            [34702, 27618, 31063, 34525, 36772, 35410, 38750, 39467, 35390, 34196, 35302, 35703],
            [34522, 31324, 32128, 34231, 36817, 34381, 37180, 38255, 32776, 32645, 31539, 32981],
            [32213, 28755, 29517, 31214, 33747, 33507, 35763, 36837, 32910, 33437, 30659, 31965],
            [31282, 28663, 32952, 33941, 34506, 36875, 38836, 35497, 34285, 34094, 32256, 33699],
            [31714, 29405, 33745, 32838, 33461, 35034, 36122, 37943, 34128, 30624, 32398, 33522],
            [32064, 28387, 33751, 32537, 34034, 35977, 37196, 38301, 33627, 34115, 31072, 33939],
            [32417, 27868, 30807, 33386, 35284, 36126, 39753, 40978, 35777, 35277, 31281, 35411],
            [32494, 29848, 34385, 35804, 37943, 38722, 41315, 41335, 37177, 37443, 32457, 37304],
            [34378, 29576, 30547, 35664, 36622, 38145, 40347, 41868, 38252, 36505, 29576, 36450],
            [35219, 31670, 32589, 34927, 36998, 39825, 41126, 42002, 37021, 36583, 32408, 37108]
        ];

        titleSettings: Object = {
            text: 'Monthly Flight Traffic at JFK Airport',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            valueType:"DateTime",
            minimum: new Date(2007,0,1),
            maximum: new Date(2017,0,1),
            intervalType:"Years",
            labelFormat:"yyyy",
            labelRotation: 45,
            labelIntersectAction: 'None'
        };
        yAxis: Object = {
            labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May',
                'Jun', 'July', 'Aug', 'Sept', 'Oct', 'Nov', 'Dec'],
        };
        public legendSettings: Object = {
            visible: false,
        };
        public cellSettings: Object = {
            showLabel: false,
            border: {
                width: 0,
            },
            format: '{value} flights'
        };
}

```

{% endtab %}

## Inversed axis

Heat map supports inversing the axis origin for both axes, where the axis labels are placed in an inversed manner. You can enable axis inversing by enabling the [`isInversed`](../api/heatmap/axis/#isinversed) property.

{% tab template= "heatmap/axis/inversedaxis", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'
       [titleSettings]='titleSettings' [legendSettings]='legendSettings' [cellSettings]='cellSettings'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

dataSource: Object [] = [
            [36371, 25675, 28292, 33399, 35980, 38585, 39351, 39964, 36543, 30529, 33298, 36985],
            [34702, 27618, 31063, 34525, 36772, 35410, 38750, 39467, 35390, 34196, 35302, 35703],
            [34522, 31324, 32128, 34231, 36817, 34381, 37180, 38255, 32776, 32645, 31539, 32981],
            [32213, 28755, 29517, 31214, 33747, 33507, 35763, 36837, 32910, 33437, 30659, 31965],
            [31282, 28663, 32952, 33941, 34506, 36875, 38836, 35497, 34285, 34094, 32256, 33699],
            [31714, 29405, 33745, 32838, 33461, 35034, 36122, 37943, 34128, 30624, 32398, 33522],
            [32064, 28387, 33751, 32537, 34034, 35977, 37196, 38301, 33627, 34115, 31072, 33939],
            [32417, 27868, 30807, 33386, 35284, 36126, 39753, 40978, 35777, 35277, 31281, 35411],
            [32494, 29848, 34385, 35804, 37943, 38722, 41315, 41335, 37177, 37443, 32457, 37304],
            [34378, 29576, 30547, 35664, 36622, 38145, 40347, 41868, 38252, 36505, 29576, 36450],
            [35219, 31670, 32589, 34927, 36998, 39825, 41126, 42002, 37021, 36583, 32408, 37108]
        ];

        titleSettings: Object = {
            text: 'Monthly Flight Traffic at JFK Airport',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            valueType:"DateTime",
            minimum: new Date(2007,0,1),
            maximum: new Date(2017,0,1),
            intervalType:"Years",
            labelFormat:"yyyy",
            labelRotation: 45,
            labelIntersectAction: 'None',
            isInversed:true
        };
        yAxis: Object = {
            labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May',
                'Jun', 'July', 'Aug', 'Sept', 'Oct', 'Nov', 'Dec'],
        };
        public legendSettings: Object = {
            visible: false,
        };
        public cellSettings: Object = {
            showLabel: false,
            border: {
                width: 0,
            },
            format: '{value} flights'
        };
}

```

{% endtab %}

## Opposed axis

In heat map, you can place the axis label in an opposite position of its default axis label position by using the [`opposedPosition`](../api/heatmap/axis/#opposedposition) property.

{% tab template= "heatmap/axis/opposedaxis", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'
       [titleSettings]='titleSettings' [legendSettings]='legendSettings' [cellSettings]='cellSettings'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

dataSource: Object [] = [
            [36371, 25675, 28292, 33399, 35980, 38585, 39351, 39964, 36543, 30529, 33298, 36985],
            [34702, 27618, 31063, 34525, 36772, 35410, 38750, 39467, 35390, 34196, 35302, 35703],
            [34522, 31324, 32128, 34231, 36817, 34381, 37180, 38255, 32776, 32645, 31539, 32981],
            [32213, 28755, 29517, 31214, 33747, 33507, 35763, 36837, 32910, 33437, 30659, 31965],
            [31282, 28663, 32952, 33941, 34506, 36875, 38836, 35497, 34285, 34094, 32256, 33699],
            [31714, 29405, 33745, 32838, 33461, 35034, 36122, 37943, 34128, 30624, 32398, 33522],
            [32064, 28387, 33751, 32537, 34034, 35977, 37196, 38301, 33627, 34115, 31072, 33939],
            [32417, 27868, 30807, 33386, 35284, 36126, 39753, 40978, 35777, 35277, 31281, 35411],
            [32494, 29848, 34385, 35804, 37943, 38722, 41315, 41335, 37177, 37443, 32457, 37304],
            [34378, 29576, 30547, 35664, 36622, 38145, 40347, 41868, 38252, 36505, 29576, 36450],
            [35219, 31670, 32589, 34927, 36998, 39825, 41126, 42002, 37021, 36583, 32408, 37108]
        ];

        titleSettings: Object = {
            text: 'Monthly Flight Traffic at JFK Airport',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            valueType:"DateTime",
            minimum: new Date(2007,0,1),
            maximum: new Date(2017,0,1),
            intervalType:"Years",
            labelFormat:"yyyy",
            labelRotation: 45,
            labelIntersectAction: 'None',
            opposedPosition:true
        };
        yAxis: Object = {
            labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May',
                'Jun', 'July', 'Aug', 'Sept', 'Oct', 'Nov', 'Dec'],
        };
        public legendSettings: Object = {
            visible: false,
        };
        public cellSettings: Object = {
            showLabel: false,
            border: {
                width: 0,
            },
            format: '{value} flights'
        };
}

```

{% endtab %}

## Label formatting

Heat map supports formatting the axis labels by using the [`labelFormat`](../api/heatmap/axis/#labelformat) property. Using this property, you can customize the axis label by global string format ('P', 'C', etc) or customized format like '{value}°C'.

{% tab template= "heatmap/axis/labelformat", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'
       [legendSettings]='legendSettings'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

dataSource: Object [] = [
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
        [74, 33, 88, 23, 86, 59]
    ];

        xAxis: Object = {
            valueType:"DateTime",
            minimum: new Date(2007,0,1),
            intervalType:"Years",
            labelFormat:"yyyy",
        };
        yAxis: Object = {
           valueType:"Numeric",
           labelFormat:"${value}"
        };
        public legendSettings: Object = {
            visible: false,
        };
}

```

{% endtab %}

## Axis intervals

In heat map, you can define an interval between the axis labels using the [`interval`](../api/heatmap/axis/#interval) property. In date-time axis, you can change the interval mode by using the [`intervalType`](../api/heatmap/axis/#intervaltype) property. The date-time axis supports the following interval types:

* Years
* Months
* Days
* Hours
* Minutes

{% tab template= "heatmap/axis/axisinterval", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'
       [legendSettings]='legendSettings' [cellSettings]='cellSettings' [titleSettings]='titleSettings'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

dataSource: Object [] = [
            [36371, 25675, 28292, 33399, 35980, 38585, 39351, 39964, 36543, 30529, 33298, 36985],
            [34702, 27618, 31063, 34525, 36772, 35410, 38750, 39467, 35390, 34196, 35302, 35703],
            [34522, 31324, 32128, 34231, 36817, 34381, 37180, 38255, 32776, 32645, 31539, 32981],
            [32213, 28755, 29517, 31214, 33747, 33507, 35763, 36837, 32910, 33437, 30659, 31965],
            [31282, 28663, 32952, 33941, 34506, 36875, 38836, 35497, 34285, 34094, 32256, 33699],
            [31714, 29405, 33745, 32838, 33461, 35034, 36122, 37943, 34128, 30624, 32398, 33522],
            [32064, 28387, 33751, 32537, 34034, 35977, 37196, 38301, 33627, 34115, 31072, 33939],
            [32417, 27868, 30807, 33386, 35284, 36126, 39753, 40978, 35777, 35277, 31281, 35411],
            [32494, 29848, 34385, 35804, 37943, 38722, 41315, 41335, 37177, 37443, 32457, 37304],
            [34378, 29576, 30547, 35664, 36622, 38145, 40347, 41868, 38252, 36505, 29576, 36450],
            [35219, 31670, 32589, 34927, 36998, 39825, 41126, 42002, 37021, 36583, 32408, 37108]
        ];

        titleSettings: Object = {
            text: 'Monthly Flight Traffic at JFK Airport',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            valueType:"DateTime",
            minimum: new Date(2007,0,1),
            maximum: new Date(2017,0,1),
            intervalType:"Years",
            interval:2,
            labelFormat:"yyyy"
        };
        yAxis: Object = {
            labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May',
                'Jun', 'July', 'Aug', 'Sept', 'Oct', 'Nov', 'Dec'],
        };
        public legendSettings: Object = {
            visible: false,
        };
        public cellSettings: Object = {
            showLabel: false,
            border: {
                width: 0,
            },
            format: '{value} flights'
        };
}

```

{% endtab %}

## Axis label increment

Axis label increment in the heat map is used to display the axis labels with regular interval values in numeric and date-time axes. The labels will be displayed with tick gaps when you set the label interval. But, to achieve the same behavior without tick gaps, use the label increment. You can set the axis label increment using the [`increment`](../api/heatmap/axis/#increment) property and the default value of this property is 1.

{% tab template= "heatmap/axis/increment", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

dataSource: Object [] = [
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

    xAxis: Object = {
        valueType:"Numeric",
        minimum: 0,
        increment:2
    };
    yAxis: Object = {
        valueType:"Numeric",
        minimum: 0,
        increment:3
    };
}

```

{% endtab %}

## Limiting labels in date-time axis

You can display the axis labels at specific time intervals along with the date-time axis using the [`showLabelOn`](../api/heatmap/axis/#showlabelon) property. This property supports the following types:

* None: Displays the axis labels based on the `intervalType` and `interval` property of the axis. This type is default value of the `showLabelOn` property.
* Years: Displays the axis labels on every year between given date-time range.
* Months: Displays the axis labels on every month between given date-time range.
* Days: Displays the axis labels on every day between given date-time range.
* Minutes: Displays the axis labels on every minute between given date-time range.

{% tab template= "heatmap/axis/showlabelon", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';
import { Internationalization } from '@syncfusion/ej2-base';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'
       [legendSettings]='legendSettings' [cellSettings]='cellSettings' [titleSettings]='titleSettings' [height]='height' [paletteSettings]='paletteSettings' (tooltipRender)='tooltipRender($event)'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

    dataSource: Object [] = [
        [null, null, null, null, 16, 48, 0],
        [0, 15, 0, 24, 0, 39, 0],
        [0, 18, 37, 0, 0, 50, 0],
        [0, 10, 0, 0, 44, 5, 0],
        [0, 36, 0, 45, 20, 18, 0],
        [0, 28, 1, 42, 0, 10, 0],
        [0, 16, 32, 0, 1, 25, 0],
        [0, 31, 2, 9, 24, 0, 0],
        [0, 8, 47, 0, 0, 35, 0],
        [0, 31, 0, 0, 0, 40, 0],
        [0, 8, 0, 27, 0, 35, 0],
        [0, 12, 9, 45, 0, 8, 0],
        [0, 0, 13, 0, 22, 10, 0],
        [0, 16, 32, 0, 1, 25, 0],
        [0, 31, 2, 9, 24, 0, 0],
        [0, 8, 47, 27, 0, 35, 0],
        [0, 28, 14, 10, 0, 0, 0],
        [0, 36, 0, 45, 20, 18, 0],
        [0, 28, 1, 42, 0, 10, 0],
        [0, 31, 0, 24, 0, 40, 0],
        [0, 8, 47, 27, 0, 35, 0],
        [0, 36, 0, 45, 20, 18, 0],
        [0, 28, 1, 42, 0, 10, 0],
        [0, 31, 0, 24, 0, 40, 0],
        [0, 16, 32, 0, 1, 25, 0],
        [0, 31, 2, 9, 24, 0, 0],
        [0, 8, 47, 27, 0, 35, 0],
        [0, 10, 0, 36, 23, 19, 0],
        [0, 18, 37, 23, 0, 50, 0],
        [0, 28, 14, 10, 0, 0, 0],
        [0, 18, 37, 23, 0, 50, 0],
        [0, 18, 37, 23, 0, 50, 0],
        [0, 28, 14, 10, 0, 0, 0],
        [0, 31, 2, 9, 24, 0, 0],
        [0, 8, 47, 27, 0, 35, 0],
        [0, 10, 2, 0, 44, 5, 0],
        [0, 36, 0, 45, 20, 18, 0],
        [0, 28, 1, 42, 0, 10, 0],
        [0, 31, 0, 24, 0, 40, 1],
        [0, 16, 32, 0, 1, 25, 0],
        [0, 31, 2, 9, 24, 0, 0],
        [0, 8, 47, 27, 0, 35, 0],
        [0, 10, 2, 0, 44, 5, 0],
        [0, 12, 9, 45, 0, 8, 0],
        [0, 0, 13, 35, 22, 10, 0],
        [0, 28, 14, 10, 0, 0, 0],
        [0, 36, 0, 45, 20, 18, 2],
        [0, 28, 1, 42, 0, 10, 0],
        [0, 31, 0, 24, 0, 40, 1],
        [0, 8, 47, 27, 0, 35, 0],
        [0, 10, 2, 0, 44, 5, 0],
        [0, 31, 2, 9, 24, 0, 1],
        [0, 8, 47, 27, 0, 35, 40],
        [0, 10, 2, 0, 44, 5, null]
        ];
        public height: String = '280px';
        titleSettings: Object = {
            text: 'Annual Summary of User Activities in GitLab',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            opposedPosition: true,
            valueType: 'DateTime',
            minimum: new Date(2017, 6, 23),
            maximum: new Date(2018, 6, 30),
            intervalType: 'Days',
            showLabelOn: 'Months',
            labelFormat: 'MMM',
            increment: 7,
        };
        yAxis: Object = {
            labels: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
            isInversed: true,
        };
        public paletteSettings: Object = {
            palette: [
                { value: 0, color: 'rgb(238,238,238)', label: 'no contributions' },
                { value: 1, color: 'rgb(172, 213, 242)', label: '1-15 contributions' },
                { value: 16, color: 'rgb(127, 168, 201)', label: '16-31 contributions' },
                { value: 32, color: 'rgb(82, 123, 160)', label: '31-49 contributions' },
                { value: 50, color: 'rgb(37, 78, 119)', label: '50+ contributions' },
            ],
            type: 'Fixed',
            emptyPointColor: 'white'
        };
        public legendSettings: Object = {
            position: 'Bottom',
            width: '20%',
            alignment: 'Near',
            showLabel: true,
            labelDisplayType: 'None',
            enableSmartLegend: true
        };
        public tooltipRender(args: ITooltipEventArgs): void {
           let intl: Internationalization = new Internationalization();
            let format: Function = intl.getDateFormat({ format: 'EEE MMM dd, yyyy' });
            let newDate: Date = <Date>args.xValue;
            let date: Date = new Date(newDate.getTime());
            let axisLabel: string[] = args.heatmap.axisCollections[1].axisLabels;
            let index: number = axisLabel.indexOf(args.yLabel);
            (date).setDate((date).getDate() + index);
            let value: string = format(date);
            args.content = [(args.value === 0 ? 'No' : args.value) + ' ' + 'contributions' + '<br>' + value];
        };
        public cellSettings: Object = {
            showLabel: false,
            border: {
                color: 'white'
            }
        };
}

```

{% endtab %}

## Multi Level Labels

You can add many levels of labels using the [`multiLevelLabels`](../api/heatmap/axis/#multilevellabels) property.

 This property can be configured using the following properties:

* Categories
* Overflow
* Alignment
* Text style
* Border

### Categories

Using this property, you can configure [`start`](../api/heatmap/multiLevelCategoriesModel/#start), [`end`](../api/heatmap/multiLevelCategoriesModel/#end), [`text`](../api/heatmap/multiLevelCategoriesModel/#text), [`maximumTextWidth`](../api/heatmap/multiLevelCategoriesModel/#maximumtextwidth) of multiLevelLabels.

{% tab template= "heatmap/axis/multilevelcategory", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'
        [titleSettings]='titleSettings' [paletteSettings]='paletteSettings' (tooltipRender)='tooltipRender($event)'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

    dataSource: Object [] = [
        [52, 65, 67, 45, 37, 52,32, 76, 60, 64, 82, 91],
        [68, 52, 63, 51, 30, 51,51, 81, 70, 60, 88, 80],
        [60, 50, 42, 53, 66, 70,41, 69, 76, 74, 86, 97],
        [66, 64, 46, 40, 47, 41, 45, 76, 83, 69, 92,84],
        [65, 42, 58, 32, 36, 44,49, 79, 83, 69, 83, 93],
        [54, 46, 61, 46, 40, 39,41, 69, 61, 84, 84, 87],
        [48, 46, 61, 47, 49, 41,41, 67, 78, 83, 98, 87],
        [69, 52, 41, 44, 41, 52,46, 71, 63, 84, 83, 91],
        [50, 59, 44, 43, 27, 42,26, 64, 76, 65, 81, 86],
        [47, 49, 66, 53, 50, 34,31, 79, 78, 79, 89, 95],
        [61, 40, 62, 26, 34, 54,56, 74, 83, 78, 95, 98]
        ];
        titleSettings: Object = {
            text: 'Product wise Monthly sales revenue for a e-commerce website',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            labels: ['Laptop', 'Mobile', 'Gaming', 'Cosmetics', 'Fragnance', 'Watches', 'Handbags', 'Apparels', 'Kitchenware', 'Furniture', 'Home Decor'],
            multiLevelLabels: [
                {
                    categories: [
                        { start: 0, end: 2, text: 'Electronics', },
                        { start: 3, end: 4, text: 'Beauty and personal care', maximumTextWidth: 50},
                        { start: 5, end: 7, text: 'Fashion', },
                        { start: 8, end: 10, text: 'Household', },
                    ]
                },
            ]
        };
        yAxis: Object = {
            labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
            multiLevelLabels: [
                {
                    categories: [
                        { start: 0, end: 2, text: 'Q1' },
                        { start: 3, end: 5, text: 'Q2' },
                        { start: 6, end: 8, text: 'Q3' },
                        { start: 9, end: 11, text: 'Q4' }
                    ]
                },
            ]
        };
        public paletteSettings: Object = {
            palette: [
                { color: '#F0C27B' },
                { color: '#4B1248' }
            ],
        };
}

```

{% endtab %}

### Overflow

Using this property, you can trim and wrap the multilevel labels.

>Note: This support works in x-axis only.

{% tab template= "heatmap/axis/multileveloverflow", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'
        [titleSettings]='titleSettings' [paletteSettings]='paletteSettings' (tooltipRender)='tooltipRender($event)'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

    dataSource: Object [] = [
        [52, 65, 67, 45, 37, 52,32, 76, 60, 64, 82, 91],
        [68, 52, 63, 51, 30, 51,51, 81, 70, 60, 88, 80],
        [60, 50, 42, 53, 66, 70,41, 69, 76, 74, 86, 97],
        [66, 64, 46, 40, 47, 41, 45, 76, 83, 69, 92,84],
        [65, 42, 58, 32, 36, 44,49, 79, 83, 69, 83, 93],
        [54, 46, 61, 46, 40, 39,41, 69, 61, 84, 84, 87],
        [48, 46, 61, 47, 49, 41,41, 67, 78, 83, 98, 87],
        [69, 52, 41, 44, 41, 52,46, 71, 63, 84, 83, 91],
        [50, 59, 44, 43, 27, 42,26, 64, 76, 65, 81, 86],
        [47, 49, 66, 53, 50, 34,31, 79, 78, 79, 89, 95],
        [61, 40, 62, 26, 34, 54,56, 74, 83, 78, 95, 98]
        ];
        titleSettings: Object = {
            text: 'Product wise Monthly sales revenue for a e-commerce website',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            labels: ['Laptop', 'Mobile', 'Gaming', 'Cosmetics', 'Fragnance', 'Watches', 'Handbags', 'Apparels', 'Kitchenware', 'Furniture', 'Home Decor'],
            multiLevelLabels: [
                {
                    overflow: 'Trim',
                    categories: [
                        { start: 0, end: 2, text: 'Electronics', },
                        { start: 3, end: 4, text: 'Beauty and personal care', maximumTextWidth: 50},
                        { start: 5, end: 7, text: 'Fashion', },
                        { start: 8, end: 10, text: 'Household', },
                    ]
                },
            ]
        };
        yAxis: Object = {
            labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
            multiLevelLabels: [
                {
                    categories: [
                        { start: 0, end: 2, text: 'Q1' },
                        { start: 3, end: 5, text: 'Q2' },
                        { start: 6, end: 8, text: 'Q3' },
                        { start: 9, end: 11, text: 'Q4' }
                    ]
                },
            ]
        };
        public paletteSettings: Object = {
            palette: [
                { color: '#F0C27B' },
                { color: '#4B1248' }
            ],
        };
}

```

{% endtab %}

### Alignment

This property provides an option to position the multilevel labels at far, center, and near.

{% tab template= "heatmap/axis/multilevelalignment", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'
        [titleSettings]='titleSettings' [paletteSettings]='paletteSettings' (tooltipRender)='tooltipRender($event)'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

    dataSource: Object [] = [
        [52, 65, 67, 45, 37, 52,32, 76, 60, 64, 82, 91],
        [68, 52, 63, 51, 30, 51,51, 81, 70, 60, 88, 80],
        [60, 50, 42, 53, 66, 70,41, 69, 76, 74, 86, 97],
        [66, 64, 46, 40, 47, 41, 45, 76, 83, 69, 92,84],
        [65, 42, 58, 32, 36, 44,49, 79, 83, 69, 83, 93],
        [54, 46, 61, 46, 40, 39,41, 69, 61, 84, 84, 87],
        [48, 46, 61, 47, 49, 41,41, 67, 78, 83, 98, 87],
        [69, 52, 41, 44, 41, 52,46, 71, 63, 84, 83, 91],
        [50, 59, 44, 43, 27, 42,26, 64, 76, 65, 81, 86],
        [47, 49, 66, 53, 50, 34,31, 79, 78, 79, 89, 95],
        [61, 40, 62, 26, 34, 54,56, 74, 83, 78, 95, 98]
        ];
        titleSettings: Object = {
            text: 'Product wise Monthly sales revenue for a e-commerce website',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            labels: ['Laptop', 'Mobile', 'Gaming', 'Cosmetics', 'Fragnance', 'Watches', 'Handbags', 'Apparels', 'Kitchenware', 'Furniture', 'Home Decor'],
            multiLevelLabels: [
                {
                    alignment: 'Center'
                    categories: [
                        { start: 0, end: 2, text: 'Electronics', },
                        { start: 3, end: 4, text: 'Beauty and personal care'},
                        { start: 5, end: 7, text: 'Fashion', },
                        { start: 8, end: 10, text: 'Household', },
                    ]
                },
            ]
        };
        yAxis: Object = {
            labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
            multiLevelLabels: [
                {
                    categories: [
                        { start: 0, end: 2, text: 'Q1' },
                        { start: 3, end: 5, text: 'Q2' },
                        { start: 6, end: 8, text: 'Q3' },
                        { start: 9, end: 11, text: 'Q4' }
                    ]
                },
            ]
        };
        public paletteSettings: Object = {
            palette: [
                { color: '#F0C27B' },
                { color: '#4B1248' }
            ],
        };
}

```

{% endtab %}

### Text Customization

The [`textStyle`](../api/heatmap/multiLevelLabelsModel/#textstyle) property of multilevel labels provides options to customize the size, color, fontFamily, fontWeight, fontStyle, opacity, textAlignment, and textOverflow.

{% tab template= "heatmap/axis/multileveltext", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'
        [titleSettings]='titleSettings' [paletteSettings]='paletteSettings' (tooltipRender)='tooltipRender($event)'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

    dataSource: Object [] = [
        [52, 65, 67, 45, 37, 52,32, 76, 60, 64, 82, 91],
        [68, 52, 63, 51, 30, 51,51, 81, 70, 60, 88, 80],
        [60, 50, 42, 53, 66, 70,41, 69, 76, 74, 86, 97],
        [66, 64, 46, 40, 47, 41, 45, 76, 83, 69, 92,84],
        [65, 42, 58, 32, 36, 44,49, 79, 83, 69, 83, 93],
        [54, 46, 61, 46, 40, 39,41, 69, 61, 84, 84, 87],
        [48, 46, 61, 47, 49, 41,41, 67, 78, 83, 98, 87],
        [69, 52, 41, 44, 41, 52,46, 71, 63, 84, 83, 91],
        [50, 59, 44, 43, 27, 42,26, 64, 76, 65, 81, 86],
        [47, 49, 66, 53, 50, 34,31, 79, 78, 79, 89, 95],
        [61, 40, 62, 26, 34, 54,56, 74, 83, 78, 95, 98]
        ];
        titleSettings: Object = {
            text: 'Product wise Monthly sales revenue for a e-commerce website',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            labels: ['Laptop', 'Mobile', 'Gaming', 'Cosmetics', 'Fragnance', 'Watches', 'Handbags', 'Apparels', 'Kitchenware', 'Furniture', 'Home Decor'],
            multiLevelLabels: [
                {
                    textStyle: {
                        color: 'black',
                        fontWeight: 'Bold'
                    },
                    categories: [
                        { start: 0, end: 2, text: 'Electronics', },
                        { start: 3, end: 4, text: 'Beauty and personal care', maximumTextWidth: 50},
                        { start: 5, end: 7, text: 'Fashion', },
                        { start: 8, end: 10, text: 'Household', },
                    ]
                },
            ]
        };
        yAxis: Object = {
            labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
            multiLevelLabels: [
                {
                    categories: [
                        { start: 0, end: 2, text: 'Q1' },
                        { start: 3, end: 5, text: 'Q2' },
                        { start: 6, end: 8, text: 'Q3' },
                        { start: 9, end: 11, text: 'Q4' }
                    ]
                },
            ]
        };
        public paletteSettings: Object = {
            palette: [
                { color: '#F0C27B' },
                { color: '#4B1248' }
            ],
        };
}

```

{% endtab %}

### Border Customization

Using the [`border`](../api/heatmap/multiLevelLabelsModel/#border) property, you can customize the width, color, and type. The types of border are `Rectangle`, `WithoutTopBorder`, `WithoutBottomBorder`, `WithoutTopAndBottomBorder`, `Brace`, and `WithoutBorder`.

{% tab template= "heatmap/axis/multilevelborder", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'
        [titleSettings]='titleSettings' [paletteSettings]='paletteSettings' (tooltipRender)='tooltipRender($event)'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{

    dataSource: Object [] = [
        [52, 65, 67, 45, 37, 52,32, 76, 60, 64, 82, 91],
        [68, 52, 63, 51, 30, 51,51, 81, 70, 60, 88, 80],
        [60, 50, 42, 53, 66, 70,41, 69, 76, 74, 86, 97],
        [66, 64, 46, 40, 47, 41, 45, 76, 83, 69, 92,84],
        [65, 42, 58, 32, 36, 44,49, 79, 83, 69, 83, 93],
        [54, 46, 61, 46, 40, 39,41, 69, 61, 84, 84, 87],
        [48, 46, 61, 47, 49, 41,41, 67, 78, 83, 98, 87],
        [69, 52, 41, 44, 41, 52,46, 71, 63, 84, 83, 91],
        [50, 59, 44, 43, 27, 42,26, 64, 76, 65, 81, 86],
        [47, 49, 66, 53, 50, 34,31, 79, 78, 79, 89, 95],
        [61, 40, 62, 26, 34, 54,56, 74, 83, 78, 95, 98]
        ];
        titleSettings: Object = {
            text: 'Product wise Monthly sales revenue for a e-commerce website',
            textStyle: {
                size: '15px',
                fontWeight: '500',
                fontStyle: 'Normal',
                fontFamily: 'Segoe UI'
            }
        };
        xAxis: Object = {
            labels: ['Laptop', 'Mobile', 'Gaming', 'Cosmetics', 'Fragnance', 'Watches', 'Handbags', 'Apparels', 'Kitchenware', 'Furniture', 'Home Decor'],
            multiLevelLabels: [
                {
                    border: { type: 'Rectangle', color: '#a19d9d' },
                    categories: [
                        { start: 0, end: 2, text: 'Electronics', },
                        { start: 3, end: 4, text: 'Beauty and personal care', maximumTextWidth: 50},
                        { start: 5, end: 7, text: 'Fashion', },
                        { start: 8, end: 10, text: 'Household', },
                    ]
                },
            ]
        };
        yAxis: Object = {
            labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
            multiLevelLabels: [
                {
                    border: { type: 'Brace', color: '#a19d9d' },
                    categories: [
                        { start: 0, end: 2, text: 'Q1' },
                        { start: 3, end: 5, text: 'Q2' },
                        { start: 6, end: 8, text: 'Q3' },
                        { start: 9, end: 11, text: 'Q4' }
                    ]
                },
            ]
        };
        public paletteSettings: Object = {
            palette: [
                { color: '#F0C27B' },
                { color: '#4B1248' }
            ],
        };
}

```

{% endtab %}