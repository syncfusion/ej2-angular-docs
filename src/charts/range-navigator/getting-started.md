---
title: " RangeNavigator Getting Started | Angular "

component: "RangeNavigator"

description: "Getting started file explains how to configure and install rangenavigator packages and also how to create basic rangenavigator, module injections."
---

# Getting started

This section explains you the steps required to create a simple RangeNavigator and demonstrate the basic usage of the RangeNavigator component in an Angular environment.

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

To install RangeNavigator component, use the following command.

```bash
npm install @syncfusion/ej2-angular-charts --save
```

> The **--save** will instruct NPM to include the chart package inside of the `dependencies` section of the `package.json`.

## Registering RangeNavigator Module

Import Chart module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-charts` [src/app/app.module.ts].

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the RangeNavigatorModule for the RangeNavigator component
import { RangeNavigatorModule } from '@syncfusion/ej2-angular-charts';
import { AppComponent }  from './app.component';

@NgModule({
    //declaration of RangeNavigatorModule into NgModule
  imports:  [ BrowserModule, RangeNavigatorModule ],
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
  // specifies the template string for the RangeNavigator component
  template: `<ejs-rangenavigator id="rn-container"></ejs-rangenavigator>`
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

## Module Injection

To create range navigator with additional features, inject the required modules. The following modules are used to extend rangenavigator’s basic functionality.

* `AreaSeriesService` - Inject this module to use area series.
* `DateTimeService` - Inject this module to use date time axis.
* `RangeTooltipService` - Inject this module to show the tooltip.

These modules should be injected to the provider section as follows,

 ```javascript
    import { NgModule } from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';
    import { AppComponent } from './app.component';
    import { RangeNavigatorComponent } from '@syncfusion/ej2-angular-charts';
    import { AreaSeriesService, DateTimeService, RangeTooltipService } from '@syncfusion/ej2-angular-charts';

    @NgModule({
        imports: [
            BrowserModule,
        ],
        declarations: [AppComponent, RangeNavigatorComponent],
        bootstrap: [AppComponent],
        providers: [ AreaSeriesService, DateTimeService, RangeTooltipService ]
    })

 ```

## Populate Range Navigator with Data

Now, we are going to provide data to the range navigator. Add a series object to the range navigator  by using `series` property. Now map the field names x and y in the JSON data to the `xName` and `yName` properties of the series, then set the JSON data to dataSource property.
Since the JSON contains Datetime data, set the `valueType` as `DateTime`. By default, the axis valueType is Numeric.

{% tab template="rangenavigator/getting-started/default", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'datasource.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    ngOnInit(): void {
        this.value = [new Date('2017-09-01'), new Date('2018-02-01')];
        this.chartData = datasrc;
    }
}

```

{% endtab %}

>Note: Get data from [here](https://ej2.syncfusion.com/demos/src/range-navigator/data-source/default-data.json).

The sample should look like our [default](https://ej2.syncfusion.com/angular/demos/#/material/range-navigator/default), don’t worry about the gradient color, let it takes the default color.

## Enable Tooltip

The tooltip is useful to show the selected data. You can enable tooltip by setting the enable property as true in `tooltip` object and by injecting `RangeTooltipService` module into the `@NgModule.providers`.

{% tab template="rangenavigator/getting-started/tooltip", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { datasrc } from 'data.ts'

@Component({
    selector: 'app-container',
    template:
    `<ejs-rangenavigator id="rn-container" valueType='DateTime' [value]='value' [tooltip]='tooltip'>
            <e-rangenavigator-series-collection>
                <e-rangenavigator-series [dataSource]='chartData' type='Area' xName='x' yName='y' width=2>
                </e-rangenavigator-series>
            </e-rangenavigator-series-collection>
        </ejs-rangenavigator>`
})
export class AppComponent implements OnInit {
    public value: Object[];
    public chartData: Object[];
    public tooltip: Object[];
    ngOnInit(): void {
        this.value = [new Date('2017-09-01'), new Date('2018-02-01')];
        this.chartData = datasrc;
        this.tooltip = { enable: true, displayMode: 'Always' };
    }
}

```

{% endtab %}