---
title: " Chart Getting Started | Angular "

component: "Chart"

description: "Getting started file explains how to configure and install chart packages and also how to create basic chart, module injections."
---

# Getting started

This section explains you the steps required to create a simple Chart and demonstrate the basic usage of the Chart component in an Angular environment.

To get start quickly with Angular Chart using CLI and Schematics, you can check on this video:

`youtube:uAubTKfbBy8`

## Setup Angular Environment

You can use [`Angular CLI`](https://github.com/angular/angular-cli) to setup your Angular applications.
To install Angular CLI use the following command.

```bash
npm install -g @angular/cli
```

## Create an Angular Application

Start a new Angular application using below Angular CLI command.

```bash
ng new my-app
cd my-app
```

## Adding Syncfusion Chart package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Chart component, use the following command.

```bash
npm install @syncfusion/ej2-angular-charts --save
```

> The **--save** will instruct NPM to include the chart package inside of the `dependencies` section of the `package.json`.

## Registering Chart Module

Import Chart module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-charts` [src/app/app.module.ts].

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the ChartModule for the Chart component
import { ChartModule } from '@syncfusion/ej2-angular-charts';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ChartModule into NgModule
  imports:      [ BrowserModule, ChartModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

* Modify the template in `app.component.ts` file to render the `ej2-angular-charts` component
`[src/app/app.component.ts]`.

```javascript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'app-container',
  // specifies the template string for the Charts component
  template: `<ejs-chart id='chart-container'></ejs-chart>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent  { }
```

<!-- markdownlint-disable MD033 -->

Now use the <code>app-container</code> in the index.html instead of default one.

```html
<app-container></app-container>
```

* Now run the application in the browser using the below command.

```cmd
npm start
```

The below example shows a basic Charts.

{% tab template="chart/getting-started/initialize", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    // specifies the template string for the Chart component
    template: `<ejs-chart id="chart-container"></ejs-chart>`
})
export class AppComponent {

}
```

{% endtab %}

## Module Injection

Chart component are segregated into individual feature-wise modules. In order to use a particular feature,
you need to inject its feature service in the AppModule. In the current application, we are
going to modify the above basic chart to visualize sales data for a particular year.
For this application we are going to use  line series, tooltip, data label, category axis and legend
feature of the chart. Please find relevant
feature service name and description as follows.

* `LineSeriesService` - Inject this provider to use line series.
* `LegendService` - Inject this provider to use legend feature.
* `TooltipService` - Inject this provider to use tooltip feature.
* `DataLabelService` - Inject this provider to use datalabel feature.
* `CategoryService`  - Inject this provider to use category feature.

These modules should be injected to the provider section as follows,

 ```javascript
    import { NgModule } from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';
    import { AppComponent } from './app.component';
    import { ChartComponent } from '@syncfusion/ej2-angular-charts';
    import { CategoryService, LegendService, TooltipService } from '@syncfusion/ej2-angular-charts';
    import { DataLabelService, LineSeriesService} from '@syncfusion/ej2-angular-charts';

    @NgModule({
        imports: [
            BrowserModule,
        ],
        declarations: [AppComponent, ChartComponent],
        bootstrap: [AppComponent],
        providers: [ CategoryService, LegendService, TooltipService, DataLabelService, LineSeriesService ]
    })

 ```

## Populate Chart with Data

This section explains how to plot below JSON data to the chart.

```javascript
    export class AppComponent implements OnInit {
    public chartData: Object[];
    ngOnInit(): void {
        // Data for chart series
        this.chartData = [
            { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
            { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
            { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
            { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
            { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
            { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
        ];
    }

}

 ```

 Add a series object to the chart by using [`series`](../api/chart/seriesDirective/) property. Now map the field names `month` and `sales` in the JSON data to the [`xName`](../api/chart/seriesDirective/#xname) and
[`yName`](../api/chart/seriesDirective/#yname) properties of the series, then set the JSON data to [`dataSource`](../api/chart/seriesDirective#datasource) property.

Since the JSON contains category data, set the [`valueType`](../api/chart/axisDirective/#valuetype)for horizontal axis to `Category`. By default, the axis valueType is `Numeric`.

{% tab template="chart/getting-started/datasource", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='month' yName='sales' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    ngOnInit(): void {
        // Data for chart series
        this.chartData = [
            { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
            { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
            { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
            { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
            { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
            { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
        ];
        this.primaryXAxis = {
            valueType: 'Category'
        };
    }

}

```

{% endtab %}

The sales data are in thousands, so format the vertical axis label by adding
`$` as a prefix and `K` as a suffix to each label. This can be achieved by setting the
`${value}K` to the [`labelFormat`](../api/chart/axisDirective#labelformat) property of axis. Here, `{value}` act as a placeholder
for each axis label.

{% tab template="chart/getting-started/datasource", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='month' yName='sales' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public primaryYAxis: Object;
    public chartData: Object[];
    ngOnInit(): void {
        this.chartData = [
            { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
            { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
            { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
            { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
            { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
            { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
        ];
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.primaryYAxis = {
            labelFormat: '${value}K'
        };
    }

}

```

{% endtab %}

## Add Chart Title

You can add a title using [`title`](../api/chart/chartModel/#title) property to the chart to provide
quick information to the user about the data plotted in the chart.

{% tab template="chart/getting-started/tooltip", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
    [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='month' yName='sales' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public primaryYAxis: Object;
    public title: string;
    ngOnInit(): void {
        // Title for chart
        this.title = 'Sales Analysis';
        this.chartData = [
            { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
            { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
            { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
            { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
            { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
            { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
        ];
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.primaryYAxis = {
            labelFormat: '${value}K'
        };
    }

}

```

{% endtab %}

## Enable Legend

You can use legend for the chart by setting the `visible` property to true in [`legendSettings`](../api/chart/chartModel/#legendsettings) object and by injecting the `LegendService` into the `@NgModule.providers`.

{% tab template="chart/getting-started/legend", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis' [legendSettings]='legendSettings' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='month' yName='sales' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public primaryYAxis: Object;
    public legendSettings: Object;
    public title: string;
    ngOnInit(): void {
        // Legend for chart
        this.legendSettings = {
            visible: true
        }
        this.chartData = [
            { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
            { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
            { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
            { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
            { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
            { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
        ];
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.primaryYAxis = {
            labelFormat: '${value}K'
        };
        this.title = 'Sales Analysis';
    }

}

```

{% endtab %}

## Add Data Label

You can add data labels to improve the readability of the chart.
This can be achieved by setting the visible property to true in the `dataLabel` object  and by injecting `DataLabelService` into the `@NgModule.providers`.

{% tab template="chart/getting-started/datalabel", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis' [legendSettings]='legendSettings' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='month' yName='sales' name='Sales' [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public primaryYAxis: Object;
    public legendSettings: Object;
    public marker: Object;
    public title: string;
    ngOnInit(): void {
        // Data label for chart series
        this.marker = {
            dataLabel:{
                visible: true
            }
        };
        this.chartData = [
            { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
            { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
            { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
            { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
            { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
            { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
        ];
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.primaryYAxis = {
            labelFormat: '${value}K'
        };
        this.legendSettings = {
            visible: true
        };
        this.title = 'Sales Analysis';
    }

}

```

{% endtab %}

## Enable Tooltip

The tooltip is useful when you cannot display information by using the data labels
due to space constraints. You can enable tooltip by setting the enable property as true in [`tooltip`](../api/chart/chartModel/#tooltip) object and by injecting `TooltipService` into the `@NgModule.providers`.

{% tab template="chart/getting-started/tooltip", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis' [primaryYAxis]='primaryYAxis'
    [legendSettings]='legendSettings' [tooltip]='tooltip' [title]='title'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='month' yName='sales' name='Sales' [marker]='marker'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public primaryYAxis: Object;
    public legendSettings: Object;
    public tooltip: Object;
    public title: string;
    public marker: Object;
    ngOnInit(): void {
        // Tooltip for chart
        this.tooltip = {
            enable: true
        }
        this.chartData = [
            { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
            { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
            { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
            { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
            { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
            { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
        ];
        this.primaryXAxis = {
            valueType: 'Category'
        };
        this.primaryYAxis = {
            labelFormat: '${value}K'
        };
        this.marker = {
            dataLabel:{
                visible: true
            }
        };
        this.legendSettings = {
            visible: true
        };
        this.title = 'Sales Analysis';
    }

}

```

{% endtab %}