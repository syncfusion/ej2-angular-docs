---
title: "Bullet Chart Getting Started | Angular "

component: "Bullet Chart"

description: "Getting started file explains how to configure and install chart packages and also how to create basic bullet chart, module injections."
---

# Getting started

This section explains you the steps required to create a simple [Bullet Chart](https://www.syncfusion.com/angular-ui-components/angular-bullet-chart) and demonstrate the basic usage of the Bullet Chart component in an Angular environment.

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

## Adding Syncfusion Bullet Chart package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Bullet Chart component, use the following command.

```bash
npm install @syncfusion/ej2-angular-charts --save
```

The **--save** will instruct NPM to include the bullet chart package inside of the `dependencies` section of the `package.json`.

## Registering Bullet Chart Module

Import Bullet Chart module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-charts` [src/app/app.module.ts].

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the BulletChartModule for the Chart component
import { BulletChartModule } from '@syncfusion/ej2-angular-charts';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ChartModule into NgModule
  imports:      [ BrowserModule, BulletChartModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

* Modify the template in `app.component.ts` file to render the `ej2-angular-charts` component
`[src/app/app.component.ts]`.

```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'app-container',
  // specifies the template string for the Bullet Charts component
  template: `<ejs-bulletchart id='container'></ejs-bulletchart>`,
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

{% tab template="bullet-chart/getting-started/initialize", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

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

Bullet Chart component are segregated into individual feature-wise modules. In order to use a particular feature, you need to inject its feature service in the AppModule. Please find relevant feature service name and description as follows.

* `BulletTooltipService` - Inject this provider to use tooltip feature.

These modules should be injected to the provider section as follows,

```typescript
    import { NgModule } from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';
    import { AppComponent } from './app.component';
    import { BulletChartComponent } from '@syncfusion/ej2-angular-charts';
    import { BulletTooltipService } from '@syncfusion/ej2-angular-charts';
    @NgModule({
        imports: [
            BrowserModule,
        ],
        declarations: [AppComponent, BulletChartComponent],
        bootstrap: [AppComponent],
        providers: [ BulletTooltipService ]
    })
```

## Bullet Chart with Data

This section explains how to plot local data to the bullet chart.

```typescript
    export class AppComponent implements OnInit {
    public data: Object[];
    ngOnInit(): void {
        // Data for bullet chart
        this.data = [
       { value: 100, target: 80 },
       { value: 200, target: 180 },
       { value: 300, target: 280 },
       { value: 400, target: 380 },
       { value: 500, target: 480 },
        ];
    }
}
```

Now assign the local data to `dataSource` property. `value` and `target` values should be mapped with `valueName` and `targetName` respectively.

{% tab template="bullet-chart/getting-started/datasource", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueName='value' targetName='target'
                [minimum]='minimum' [maximum]='maximum' [interval]='interval' [dataSource]='data'>
                </ejs-bulletchart>`
})
export class AppComponent {
  public minimum: number = 0;
  public maximum: number = 300;
  public interval: number = 50;
  public data: Object[] = [
       { value: 100, target: 80 },
       { value: 200, target: 180 },
       { value: 300, target: 280 },
       { value: 400, target: 380 },
       { value: 500, target: 480 },
    ];
}
```

{% endtab %}

## Add Bullet Chart Title

You can add a title using `title` property to the bullet chart to provide quick
information to the user about the data plotted in the bullet chart.

{% tab template="bullet-chart/getting-started/title", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueName='value' targetName='target' title='Revenue'
                [minimum]='minimum' [maximum]='maximum' [interval]='interval' [dataSource]='data'>
                </ejs-bulletchart>`
})
export class AppComponent {
  public minimum: number = 0;
  public maximum: number = 300;
  public interval: number = 50;
  public data: Object[] = [
       { value: 270, target: 250 }
    ];
}
```

{% endtab %}

## Ranges

You can add a range using `ranges` property to the bullet chart.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueName='value' targetName='target' title='Revenue'
                [minimum]='minimum' [maximum]='maximum' [interval]='interval' [dataSource]='data'>
                <e-bullet-range-collection>
                <e-bullet-range end='100' color='#ebebeb'></e-bullet-range>
                <e-bullet-range end='200' color='#d8d8d8'></e-bullet-range>
                <e-bullet-range end='300' color='#7f7f7f'></e-bullet-range>
                </e-bullet-range-collection>
                </ejs-bulletchart>`
})
export class AppComponent {
  public minimum: number = 0;
  public maximum: number = 300;
  public interval: number = 50;
  public data: Object[] = [
      { value: 270, target: 250 }
    ];
}
```

{% endtab %}

## Enable Tooltip

The tooltip is useful when you cannot display information by using the data labels
due to space constraints. You can enable tooltip by setting the enable property as true in [`tooltip`]object and by injecting `BulletTooltipService` into the `@NgModule.providers`.

{% tab template="bullet-chart/getting-started/tooltip", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueName='value' targetName='target' title='Revenue'
                [minimum]='minimum' [maximum]='maximum' [interval]='interval' [dataSource]='data'
                [tooltip]='tooltip'>
                <e-bullet-range-collection>
                <e-bullet-range end='100' color='#ebebeb'></e-bullet-range>
                <e-bullet-range end='200' color='#d8d8d8'></e-bullet-range>
                <e-bullet-range end='300' color='#7f7f7f'></e-bullet-range>
                </e-bullet-range-collection>
                </ejs-bulletchart>`
})
export class AppComponent {
  public minimum: number = 0;
  public maximum: number = 300;
  public interval: number = 50;
  public tooltip: Object = {enable: true};
  public data: Object[] = [
      { value: 270, target: 250 }
    ];
}
```

{% endtab %}