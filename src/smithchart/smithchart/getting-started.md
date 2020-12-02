# Getting Started

This section explains you the steps required to create a Smith Chart and demonstrate the basic usage of the Smith Chart control.

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

## Adding Syncfusion TreeMap package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install treemap component, use the following command.

```bash
npm install @syncfusion/ej2-angular-charts --save
```

> The **--save** will instruct NPM to include the treemap package inside of the `dependencies` section of the `package.json`.

## Registering TreeMap Module

Import TreeMap module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-charts` [src/app/app.module.ts].

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the SmithchartModule for the Smithchart component
import { SmithchartModule } from '@syncfusion/ej2-angular-charts';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-smithchart module into NgModule
  imports:      [ BrowserModule, SmithchartModule ],
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
  // specifies the template string for the Smithchart component
  template: `<ejs-smithchart style='display: block;' id='container'></ejs-smithchart>`,
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

The below example shows a basic Smithchart.

{% tab template="smithchart/getting-started/smithchart", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    // specifies the template string for the Smithchart component
    template: `<ejs-smithchart id="smithchart-container"  height='350px'></ejs-smithchart>`
})
export class AppComponent {

}
```

{% endtab %}

## Module Injection

Smithchart component are segregated into individual feature-wise modules. In order to use a particular feature,
you need to inject its feature service in the AppModule. In the current application, we are
going to modify the above basic smithchart to visualize transmission lines.
For this application we are going to use  tooltip and legend feature of the smithchart. Please find relevant
feature service name and description as follows.

* SmithchartLegendService - Inject this provider to use legend feature.
* TooltipRenderService - Inject this provider to use tooltip feature.

These modules should be injected to the provider section as follows,

 ```javascript
    import { NgModule } from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';
    import { AppComponent } from './app.component';
    import { SmithchartComponent } from '@syncfusion/ej2-angular-charts';
    import { SmithchartLegendService, TooltipRenderService } from '@syncfusion/ej2-angular-charts';

    @NgModule({
        imports: [
            BrowserModule,
        ],
        declarations: [AppComponent, SmithchartComponent],
        bootstrap: [AppComponent],
        providers: [ SmithchartLegendService, TooltipRenderService ]
    })

 ```

## Add Series to Smithchart

Smithchart had two type of specification for adding series.
* dataSource - Using this, Data object can bind directly by specifying the resistance and reactance values, series add to smithchart.
* points - Using this, collection of resistance and reactance values can bind directly to render series.

Below sample demonstrate adding two series to smithchart both ways.
* First series Transmission1 shows dataSource bound series.
* Second series Transmission2 shows points bound series.

{% tab template= "smithchart/getting-started/smithchart", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-smithchart style='display: block;' id='container' height='350px'>
    <e-seriesCollection>
        <e-series [dataSource]='seriesdata1' name='Transmission1' reactance='reactance' resistance='resistance'> </e-series>
        <e-series [points]='seriespoints' name='Transmission2'> </e-series>
    </e-seriesCollection>
    </ejs-smithchart>`
})
export class AppComponent {
    public seriesdata1: object[] = [
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0.3, reactance: 0.1 }, { resistance: 0.5, reactance: 0.2 },
        { resistance: 1.5, reactance: 0.5 }, { resistance: 2.0, reactance: 0.5 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 4.5, reactance: -0.5 }, { resistance: 5.0, reactance: -1.0 }
    ];
    public seriespoints: object[] = [
        { resistance: 0, reactance: 0.15 }, { resistance: 0, reactance: 0.15 },
        { resistance: 0, reactance: 0.15 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.3, reactance: 0.2 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.3, reactance: 0.2 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.5, reactance: 0.4 }, { resistance: 1.0, reactance: 0.8 },
        { resistance: 2.5, reactance: 1.3 }, { resistance: 3.5, reactance: 1.6 },
        { resistance: 3.5, reactance: 1.6 }, { resistance: 3.5, reactance: 1.6 },
        { resistance: 4.5, reactance: 2.0 }, { resistance: 6.0, reactance: 4.5 },
        { resistance: 8, reactance: 6 }, { resistance: 10, reactance: 25 }
    ];
}

```

{% endtab %}

## Add title to SmithChart

smithchart `title` API used to add title for smithchart. In that `text` API used to set text of the title.
API `visible` used to toggle the title.

{% tab template= "smithchart/getting-started/smithchart", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { TitleModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-smithchart style='display: block;' id='container' [title]='title' height='350px'>
    <e-seriesCollection>
        <e-series [dataSource]='seriesdata1' name='Transmission1' reactance='reactance' resistance='resistance'> </e-series>
        <e-series [points]='seriespoints' name='Transmission2'> </e-series>
    </e-seriesCollection>
    </ejs-smithchart>`
})
export class AppComponent {
    public title: TitleModel = { text: 'Transmission lines applied for both impedance and admittance' };
    public seriesdata1: object[] = [
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0.3, reactance: 0.1 }, { resistance: 0.5, reactance: 0.2 },
        { resistance: 1.5, reactance: 0.5 }, { resistance: 2.0, reactance: 0.5 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 4.5, reactance: -0.5 }, { resistance: 5.0, reactance: -1.0 }
    ];
    public seriespoints: object[] = [
        { resistance: 0, reactance: 0.15 }, { resistance: 0, reactance: 0.15 },
        { resistance: 0, reactance: 0.15 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.3, reactance: 0.2 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.3, reactance: 0.2 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.5, reactance: 0.4 }, { resistance: 1.0, reactance: 0.8 },
        { resistance: 2.5, reactance: 1.3 }, { resistance: 3.5, reactance: 1.6 },
        { resistance: 3.5, reactance: 1.6 }, { resistance: 3.5, reactance: 1.6 },
        { resistance: 4.5, reactance: 2.0 }, { resistance: 6.0, reactance: 4.5 },
        { resistance: 8, reactance: 6 }, { resistance: 10, reactance: 25 }
    ];
}
```

{% endtab %}

## Enable Marker to Smithchart

To use series marker and it's customization in smithchart, use series `marker`. To display marker for particular series, need to specify  `marker visible` as true. Below sample marker enabled for first series only.

{% tab template= "smithchart/getting-started/smithchart", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-smithchart style='display: block;' id='container' [title]='title' height='350px'>
    <e-seriesCollection>
        <e-series [marker]='marker' [dataSource]='seriesdata1' name='Transmission1' reactance='reactance' resistance='resistance'></e-series>
        <e-series [points]='seriespoints' name='Transmission2'> </e-series>
    </e-seriesCollection>
    </ejs-smithchart>`
})
export class AppComponent {
    public title: object = { text: 'Transmission lines applied for both impedance and admittance' };
    public marker: object = {
        visible: true
    };
    public seriesdata1: object[] = [
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0.3, reactance: 0.1 }, { resistance: 0.5, reactance: 0.2 },
        { resistance: 1.5, reactance: 0.5 }, { resistance: 2.0, reactance: 0.5 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 4.5, reactance: -0.5 }, { resistance: 5.0, reactance: -1.0 }
    ];
    public seriespoints: object[] = [
        { resistance: 0, reactance: 0.15 }, { resistance: 0, reactance: 0.15 },
        { resistance: 0, reactance: 0.15 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.3, reactance: 0.2 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.3, reactance: 0.2 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.5, reactance: 0.4 }, { resistance: 1.0, reactance: 0.8 },
        { resistance: 2.5, reactance: 1.3 }, { resistance: 3.5, reactance: 1.6 },
        { resistance: 3.5, reactance: 1.6 }, { resistance: 3.5, reactance: 1.6 },
        { resistance: 4.5, reactance: 2.0 }, { resistance: 6.0, reactance: 4.5 },
        { resistance: 8, reactance: 6 }, { resistance: 10, reactance: 25 }
    ];
}

```

{% endtab %}

## Enable DataLabel to Smithchart Marker

To use marker dataLabel and it's customization in smithchart, use marker `dataLabel`. To display dataLabel for particular series marker, need to specify  `dataLabel visible` as true in that series `marker`. Below sample dataLabel enabled for first series.

{% tab template= "smithchart/getting-started/smithchart", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-smithchart style='display: block;' id='container' [title]='title' height='350px'>
    <e-seriesCollection>
        <e-series [marker]='marker' [dataSource]='seriesdata1' name='Transmission1' reactance='reactance' resistance='resistance'></e-series>
        <e-series [points]='seriespoints' name='Transmission2'> </e-series>
    </e-seriesCollection>
    </ejs-smithchart>`
})
export class AppComponent {
    public title: object = { text: 'Transmission lines applied for both impedance and admittance' };
    public marker: object = {
        visible: true,
        dataLabel: {
            visible: true
        }
    };
    public seriesdata1: object[] = [
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0.3, reactance: 0.1 }, { resistance: 0.5, reactance: 0.2 },
        { resistance: 1.5, reactance: 0.5 }, { resistance: 2.0, reactance: 0.5 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 4.5, reactance: -0.5 }, { resistance: 5.0, reactance: -1.0 }
    ];
    public seriespoints: object[] = [
        { resistance: 0, reactance: 0.15 }, { resistance: 0, reactance: 0.15 },
        { resistance: 0, reactance: 0.15 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.3, reactance: 0.2 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.3, reactance: 0.2 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.5, reactance: 0.4 }, { resistance: 1.0, reactance: 0.8 },
        { resistance: 2.5, reactance: 1.3 }, { resistance: 3.5, reactance: 1.6 },
        { resistance: 3.5, reactance: 1.6 }, { resistance: 3.5, reactance: 1.6 },
        { resistance: 4.5, reactance: 2.0 }, { resistance: 6.0, reactance: 4.5 },
        { resistance: 8, reactance: 6 }, { resistance: 10, reactance: 25 }
    ];
}

```

{% endtab %}

## Enable Legend for Smithchart

Smithchart had a legend feature, which is used to denote the correspond series. To enable the legend, need to inject `SmithchartLegendService` module in the AppModule and smithchart `legendSettings` `visible` as true. Following example sample shows enabling legend for smithchart. Series name can customize using series `name`.

{% tab template= "smithchart/getting-started/smithchart", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-smithchart style='display: block;' id='container' [title]='title' [legendSettings]='legendSettings' height='350px'>
    <e-seriesCollection>
        <e-series [marker]='marker' [dataSource]='seriesdata1' name='Transmission1' reactance='reactance' resistance='resistance'></e-series>
        <e-series [points]='seriespoints' name='Transmission2'> </e-series>
    </e-seriesCollection>
    </ejs-smithchart>`
})
export class AppComponent {
    public title: object = { text: 'Transmission lines applied for both impedance and admittance' };
    public marker: object = {
        visible: true,
        dataLabel: {
            visible: true
        }
    };
    public legendSettings: object = {
        visible: true
    };
    public seriesdata1: object[] = [
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0.3, reactance: 0.1 }, { resistance: 0.5, reactance: 0.2 },
        { resistance: 1.5, reactance: 0.5 }, { resistance: 2.0, reactance: 0.5 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 4.5, reactance: -0.5 }, { resistance: 5.0, reactance: -1.0 }
    ];
    public seriespoints: object[] = [
        { resistance: 0, reactance: 0.15 }, { resistance: 0, reactance: 0.15 },
        { resistance: 0, reactance: 0.15 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.3, reactance: 0.2 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.3, reactance: 0.2 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.5, reactance: 0.4 }, { resistance: 1.0, reactance: 0.8 },
        { resistance: 2.5, reactance: 1.3 }, { resistance: 3.5, reactance: 1.6 },
        { resistance: 3.5, reactance: 1.6 }, { resistance: 3.5, reactance: 1.6 },
        { resistance: 4.5, reactance: 2.0 }, { resistance: 6.0, reactance: 4.5 },
        { resistance: 8, reactance: 6 }, { resistance: 10, reactance: 25 }
    ];
}

```

{% endtab %}

## Enable Tooltip for Smithchart Series

Smithchart had a tooltip feature, which is used to show the current point's values. To enable the tooltip, need to inject `TooltipRenderService` module in the AppModule and smithchart series `tooltip` `visible` as true. Following example sample shows enabling tooltip for smithchart series collection.

{% tab template= "smithchart/getting-started/smithchart", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-smithchart style='display: block;' id='container' [title]='title' [legendSettings]='legendSettings' height='350px'>
    <e-seriesCollection>
        <e-series [marker]='marker' [tooltip]='tooltip' [dataSource]='seriesdata1' name='Transmission1' reactance='reactance' resistance='resistance'></e-series>
        <e-series [points]='seriespoints' [tooltip]='tooltip' name='Transmission2'> </e-series>
    </e-seriesCollection>
    </ejs-smithchart>`
})
export class AppComponent {
    public title: object = { text: 'Transmission lines applied for both impedance and admittance' };
    public marker: object = {
        visible: true,
        dataLabel: {
            visible: true
        }
    };
    public tooltip: object = {
        visible: true
    };
    public legendSettings: object = {
        visible: true
    };
    public seriesdata1: object[] = [
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0, reactance: 0.05 }, { resistance: 0, reactance: 0.05 },
        { resistance: 0.3, reactance: 0.1 }, { resistance: 0.5, reactance: 0.2 },
        { resistance: 1.5, reactance: 0.5 }, { resistance: 2.0, reactance: 0.5 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 2.5, reactance: 0.4 }, { resistance: 3.5, reactance: 0.0 },
        { resistance: 4.5, reactance: -0.5 }, { resistance: 5.0, reactance: -1.0 }
    ];
    public seriespoints: object[] = [
        { resistance: 0, reactance: 0.15 }, { resistance: 0, reactance: 0.15 },
        { resistance: 0, reactance: 0.15 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.3, reactance: 0.2 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.3, reactance: 0.2 }, { resistance: 0.3, reactance: 0.2 },
        { resistance: 0.5, reactance: 0.4 }, { resistance: 1.0, reactance: 0.8 },
        { resistance: 2.5, reactance: 1.3 }, { resistance: 3.5, reactance: 1.6 },
        { resistance: 3.5, reactance: 1.6 }, { resistance: 3.5, reactance: 1.6 },
        { resistance: 4.5, reactance: 2.0 }, { resistance: 6.0, reactance: 4.5 },
        { resistance: 8, reactance: 6 }, { resistance: 10, reactance: 25 }
    ];
}

```

{% endtab %}