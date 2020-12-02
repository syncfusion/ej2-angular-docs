---
title: " Accumulation Chart Getting Started | Angular "

component: "Accumulation Chart"

description: "Getting started file explains how configure and install chart packages and also how to create basic accumulation chart."
---

<!-- markdownlint-disable MD036 -->

# Getting started

This section explains you the steps required to create a simple Chart and demonstrate the basic usage of the AccumulationChart component in an Angular environment.

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

To install AccumulationChart component, use the following command.

```bash
npm install @syncfusion/ej2-angular-charts --save
```

> The **--save** will instruct NPM to include the chart package inside of the `dependencies` section of the `package.json`.

## Registering AccumulationChart Module

Import AccumulationChart module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-charts` [src/app/app.module.ts].

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the AccumulationChartModule for the AccumulationChart component
import { AccumulationChartModule } from '@syncfusion/ej2-angular-charts';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of AccumulationChartModule into NgModule
  imports:      [ BrowserModule, AccumulationChartModule ],
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
  // specifies the template string for the Accumulation Charts component
  template: `<ejs-accumulationchart id="pie-container">
    </ejs-accumulationchart>`,
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

**Pie Series**

By default pie series will be rendered on assigning JSON data to the series by using
[`dataSource`](../api/accumulation-chart/accumulationSeries/#datasource) property. Map the field names
in the JSON data to the [`xName`](../api/accumulation-chart/accumulationSeries/#xname) and
[`yName`](../api/accumulation-chart/accumulationSeries/#yname) properties of the series.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container" [legendSettings]='legendSettings'>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    public legendSettings: Object;
    ngOnInit(): void {
        this.piedata = [
                { x: 'Jan', y: 3, text: 'Jan: 3' }, { x: 'Feb', y: 3.5, text: 'Feb: 3.5' },
                { x: 'Mar', y: 7, text: 'Mar: 7' }, { x: 'Apr', y: 13.5, text: 'Apr: 13.5' },
                { x: 'May', y: 19, text: 'May: 19' }, { x: 'Jun', y: 23.5, text: 'Jun: 23.5' },
                { x: 'Jul', y: 26, text: 'Jul: 26' }, { x: 'Aug', y: 25, text: 'Aug: 25' },
                { x: 'Sep', y: 21, text: 'Sep: 21' }, { x: 'Oct', y: 15, text: 'Oct: 15' },
                { x: 'Nov', y: 9, text: 'Nov: 9' }, { x: 'Dec', y: 3.5, text: 'Dec: 3.5' }];

        this.legendSettings = {
            visible: false
        };
    }

}
```

{% endtab %}
