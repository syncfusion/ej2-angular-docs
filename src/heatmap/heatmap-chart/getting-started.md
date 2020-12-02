---
title: "Getting started"
component: "Heatmap"
description: "This section describes on how to visualize a two-dimensional data by enabling the basic features in heatmap"
---

# Getting Started

This section explains  the steps required to create a heat map and demonstrates the basic usage of the heat map control.

## Setup Angular Environment

You can use `Angular CLI` to setup your Angular applications. To install Angular CLI use the following command.

```javascript
npm install -g @angular/cli
```

## Create an Angular Application

Start a new `Angular` application using below Angular CLI command.

```javascript
ng new my-app
cd my-app
```

## Adding Syncfusion Heatmap package

* All the available Essential JS 2 packages are published in npmjs.com registry.

* Install heatmap packages using below command.

```javascript
npm install @syncfusion/ej2-angular-heatmap --save
```

```javascript
The —save will instruct NPM to include the heatmap package inside of the dependencies section of the package.json.
```

## Registering Heatmap Module

* Import Heatmap module into Angular application(app.module.ts) from the package `@syncfusion/ej2-ng-heatmap` `[src/app/app.module.ts]`.

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the HeatMapModule for the heatmap component
import { HeatMapModule } from '@syncfusion/ej2-angular-heatmap';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-ng-heatmap module into NgModule
  imports:      [ BrowserModule, HeatMapModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Add Heatmap component

* Modify the template in `app.component.ts` file to render the `ej2-ng-heatmap` component
`[src/app/app.component.ts]`.

```javascript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'my-app',
  // specifies the template string for the Heatmap component
  template: `<ejs-heatmap id='heatmap-container'></ejs-heatmap>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent  { }
```

<!-- markdownlint-disable MD033 -->

Now use the <code>my-app</code> in the index.html instead of default one.

```html
<my-app></my-app>
```

* Use the `npm run start` command to run the application in the browser.

```cmd
npm start
```

The below example shows a basic Heatmap.

{% tab template="heatmap/getting-started/initialize", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    // specifies the template string for the HeatMap component
    template: `<ejs-heatmap id="heatmap-container"></ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {

}
```

{% endtab %}

## Module injection

The heat map components are segregated into individual feature-wise modules. To use its feature, you need to inject its feature module using the `HeatMap.Inject()` method. In the current application,the basic heat map is modified to visualize sales revenue data for week, and  the tooltip and legend features of the heat map are used. Find the relevant feature modules and descriptions as follows.

* `LegendService` - Provides the legend feature by injecting it.
* `TooltipService` - Provides the tooltip feature by injecting it.

Now, import the above-mentioned modules from the heat map package and inject them into the heat map component as follows.

 ```javascript
    import { NgModule } from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';
    import { AppComponent } from './app.component';
    import { HeatmapComponent, Legend, Tooltip } from '@syncfusion/ej2-ng-heatmap';

    @NgModule({
        imports: [
            BrowserModule,
        ],
        declarations: [AppComponent, HeatMapComponent],
        bootstrap: [AppComponent],
        providers: [ HeatmapComponent, LegendService, TooltipService ]
    })

 ```

## Populate heat map with data

This section explains how to populate the following two-dimensional array data to the heat map.

{% tab template="heatmap/getting-started/datasource", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';
import { HeatMap } from '@syncfusion/ej2-heatmap';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
        // Data for heatmap
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
           [74, 33, 88, 23, 86, 59]
        ];
    }

```

{% endtab %}

## Enable axis labels

You can add axis labels to the heat map and format those labels using the [`xAxis`](../api/heatmap/#xaxis) and [`yAxis`](../api/heatmap/#yaxis) properties. Axis labels provide additional information about the data points populated in the heat map.

{% tab template="heatmap/getting-started/axis", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';
import { HeatMap } from '@syncfusion/ej2-heatmap';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
        // Data for heatmap
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
           [74, 33, 88, 23, 86, 59]
        ];
        xAxis: Object = {
        labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven', 'Michael', 'Robert',
            'Laura', 'Anne', 'Paul', 'Karin', 'Mario'],
    };
    yAxis: Object = {
        labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
    };
}

```

{% endtab %}

## Add heat map title

Add a title using the [`titleSettings`](../api/heatmap/#titlesettings) property to the heat map to provide quick information to the user about the data populated in the heat map.

{% tab template="heatmap/getting-started/title", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';
import { HeatMap } from '@syncfusion/ej2-heatmap';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;"  [titleSettings]='titleSettings' [dataSource]='dataSource' [xAxis]='xAxis' [yAxis]='yAxis'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
     titleSettings: Object = {
        text: 'Sales Revenue per Employee (in 1000 US$)',
        textStyle: {
            size: '15px',
            fontWeight: '500',
            fontStyle: 'Normal'
        }
    };
        // Data for heatmap
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
           [74, 33, 88, 23, 86, 59]
        ];
        xAxis: Object = {
        labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven', 'Michael', 'Robert',
            'Laura', 'Anne', 'Paul', 'Karin', 'Mario'],
    };
    yAxis: Object = {
        labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
    };
}

```

{% endtab %}

## Enable legend

Use a legend for the heat map in the [`legendSettings`](../api/heatmap/#legendsettings) object by setting the [`visible`](../api/heatmap/legendSettings/#visible) property to `true` and injecting the `Legend` module using the `HeatMap.Inject(Legend)` method.

{% tab template="heatmap/getting-started/legend", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';
import { HeatMap } from '@syncfusion/ej2-heatmap';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;"  [titleSettings]='titleSettings' [dataSource]='dataSource'
       [xAxis]='xAxis' [yAxis]='yAxis' [legendSettings]='legendSettings'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
     titleSettings: Object = {
        text: 'Sales Revenue per Employee (in 1000 US$)',
        textStyle: {
            size: '15px',
            fontWeight: '500',
            fontStyle: 'Normal'
        }
    };
        // Data for heatmap
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
           [74, 33, 88, 23, 86, 59]
        ];
        xAxis: Object = {
        labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven', 'Michael', 'Robert',
            'Laura', 'Anne', 'Paul', 'Karin', 'Mario'],
    };
    yAxis: Object = {
        labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
    };
    public legendSettings: Object = {
        visible:true,
        position: 'Right',
        showLabel:true,
        height:'150px'
    };
}

```

{% endtab %}

## Add data label

Add data labels to improve the readability of the heat map. This can be achieved by setting the [`showLabel`](../api/heatmap/cellSettings/#showlabel) property to `true` in the [`cellSettings`](../api/heatmap/#cellsettings) object.

{% tab template="heatmap/getting-started/datalabel", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { HeatMap } from '@syncfusion/ej2-heatmap';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [cellSettings]='cellSettings' [titleSettings]='titleSettings' [dataSource]='dataSource'
       [xAxis]='xAxis' [yAxis]='yAxis' [legendSettings]='legendSettings'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
     titleSettings: Object = {
        text: 'Sales Revenue per Employee (in 1000 US$)',
        textStyle: {
            size: '15px',
            fontWeight: '500',
            fontStyle: 'Normal'
        }
    };
        // Data for heatmap
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
           [74, 33, 88, 23, 86, 59]
        ];
        xAxis: Object = {
        labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven', 'Michael', 'Robert',
            'Laura', 'Anne', 'Paul', 'Karin', 'Mario'],
    };
    yAxis: Object = {
        labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
    };
    public legendSettings: Object = {
        visible:true,
        position: 'Right',
        showLabel:true,
        height:'150px'
    };
    public cellSettings: Object = {
        showLabel: true,
        format: '{value} $'
    };
}

```

{% endtab %}

## Add custom cell palette

The default palette settings of the heat map cells can be customized by using the [`paletteSettings`](../api/heatmap/#palettesettings) property. Using the [`palette`](../api/heatmap/paletteSettings/#palette) property in `paletteSettings` object, you can change the color set for the cells.   You can change the color mode of the cells to `fixed` or `gradient` mode using the [`type`](../api/heatmap/paletteSettings/#type) property.

{% tab template="heatmap/getting-started/palette", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { HeatMap } from '@syncfusion/ej2-heatmap';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" [paletteSettings]='paletteSettings'
       [cellSettings]='cellSettings' [titleSettings]='titleSettings' [dataSource]='dataSource'
       [xAxis]='xAxis' [yAxis]='yAxis' [legendSettings]='legendSettings'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
     titleSettings: Object = {
        text: 'Sales Revenue per Employee (in 1000 US$)',
        textStyle: {
            size: '15px',
            fontWeight: '500',
            fontStyle: 'Normal'
        }
    };
        // Data for heatmap
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
           [74, 33, 88, 23, 86, 59]
        ];
        xAxis: Object = {
        labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven', 'Michael', 'Robert',
            'Laura', 'Anne', 'Paul', 'Karin', 'Mario'],
    };
    yAxis: Object = {
        labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
    };
    public legendSettings: Object = {
        visible:true,
        position: 'Right',
        showLabel:true,
        height:'150px'
    };
    public cellSettings: Object = {
        showLabel: true,
        format: '{value} $'
    };
     public paletteSettings: Object = {
        palette: [{ value: 0, color: '#C06C84' },
        { value: 50, color: '#6C5B7B' },
        { value: 100, color: '#355C7D' },
        ]
    };
}

```

{% endtab %}

## Enable tooltip

The tooltip is used when you cannot display information by using the data labels due to space constraints. You can enable the tooltip by setting the [`showTooltip`](../api/heatmap/#showtooltip) property to true and injecting the Tooltip module using the `HeatMap.Inject(Tooltip)` method.

{% tab template="heatmap/getting-started/tooltip", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { HeatMap } from '@syncfusion/ej2-heatmap';

@Component({
    selector: 'my-app',
    template:
       `<ejs-heatmap id='container' style="display:block;" showTooltip='true' [paletteSettings]='paletteSettings'
       [cellSettings]='cellSettings' [titleSettings]='titleSettings' [dataSource]='dataSource'
       [xAxis]='xAxis' [yAxis]='yAxis' [legendSettings]='legendSettings'>
        </ejs-heatmap>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
     titleSettings: Object = {
        text: 'Sales Revenue per Employee (in 1000 US$)',
        textStyle: {
            size: '15px',
            fontWeight: '500',
            fontStyle: 'Normal'
        }
    };
        // Data for heatmap
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
           [74, 33, 88, 23, 86, 59]
        ];
        xAxis: Object = {
        labels: ['Nancy', 'Andrew', 'Janet', 'Margaret', 'Steven', 'Michael', 'Robert',
            'Laura', 'Anne', 'Paul', 'Karin', 'Mario'],
    };
    yAxis: Object = {
        labels: ['Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
    };
    public legendSettings: Object = {
        visible:true,
        position: 'Right',
        showLabel:true,
        height:'150px'
    };
    public cellSettings: Object = {
        showLabel: true,
        format: '{value} $'
    };
     public paletteSettings: Object = {
        palette: [{ value: 0, color: '#C06C84' },
        { value: 50, color: '#6C5B7B' },
        { value: 100, color: '#355C7D' },
        ]
    };
}

```

{% endtab %}