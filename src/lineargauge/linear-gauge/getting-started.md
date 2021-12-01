---
title: "Getting Started with Angular Linear Gauge component | Syncfusion "

component: "Linear Gauge"

description: "Learn here about getting started with Syncfusion Angular Linear Gauge component, its element and more."
---

# Getting Started with Angular Linear Gauge

<!-- markdownlint-disable MD013 -->

This section explains the steps required to create a simple Linear Gauge and demonstrate the basic usage of the Linear Gauge component.

## Dependencies

Below is the list of minimum dependencies required to use the Linear Gauge component.

```javascript
|-- @syncfusion/ej2-angular-lineargauge
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-angular-lineargauge
    |-- @syncfusion/ej2-lineargauge
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-svg-base
```

## Setup Angular Environment

[`Angular CLI`](https://github.com/angular/angular-cli) can be used to setup the Angular applications. To install Angular CLI use the following command.

```bash
npm install -g @angular/cli
```

## Create an Angular Application

Start a new Angular application using below Angular CLI command.

```bash
ng new my-app
cd my-app
```

## Adding Syncfusion Linear Gauge package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry. To install linear gauge component, use the following command.

```bash
npm install @syncfusion/ej2-angular-lineargauge --save
```

> The **--save** will instruct NPM to include the linear gauge package inside of the `dependencies` section of the `package.json`.

## Registering LinearGauge Module

Import **LinearGaugeModule** into Angular application in the **src/app/app.module.ts** file from the package `@syncfusion/ej2-angular-lineargauge`.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the LinearGaugeModule for the LinearGauge component
import { LinearGaugeModule } from '@syncfusion/ej2-angular-lineargauge';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of Linear Gauge module in NgModule
  imports:      [ BrowserModule, LinearGaugeModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

* Modify the template in **app.component.ts** file to render the Linear Gauge component.
`[src/app/app.component.ts]`.

```javascript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'app-container',
  // specifies the template string for the LinearGauge component
  template: `<ejs-lineargauge id='linear-container'></ejs-lineargauge>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent  { }
```

<!-- markdownlint-disable MD033 -->

Now use the `<code>app-container</code>` in the index.html instead of default one.

```html
<app-container></app-container>
```

* Now run the application in the browser using the below command.

```cmd
npm start
```

The below example shows a basic Linear Gauge.

{% tab template= "linear-gauge/getting-started", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    // specifies the template string for the linear gauge component
    template: `<ejs-lineargauge id="gauge-container"></ejs-lineargauge>`
})
export class AppComponent {

}
```

{% endtab %}

## Module Injection

LinearGauge component is segregated into the individual feature-wise modules. In order to use a particular feature, inject its feature module using the `providers: {}`. Please find the feature module name and description as follows.

* `AnnotationsService` - Inject this provider to use Annotation feature.
* `GaugeTooltipService` - Inject this provider to use Tooltip feature.

These modules should be injected in the providers section of the **app.module.ts** file as follows,

 ```javascript
    import { NgModule } from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';
    import { AppComponent } from './app.component';
    import { LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
    import { AnnotationsService, GaugeTooltipService} from '@syncfusion/ej2-angular-lineargauge';

    @NgModule({
        imports: [
            BrowserModule,
        ],
        declarations: [AppComponent, LinearGaugeComponent],
        bootstrap: [AppComponent],
        providers: [ AnnotationsService, GaugeTooltipService ]
    })

```

## Add Gauge Title

The title can be added to the Linear Gauge component using the [`title`](../api/linear-gauge/linearGaugeModel#title-string) property in the Linear Gauge.

{% tab template= "linear-gauge/getting-started", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-lineargauge id="gauge-container" [title]='Title'>
    </ejs-lineargauge>`
})
export class AppComponent implements OnInit {
    public Title: string;
    ngOnInit(): void {
        // Title for linear gauge
        this.Title = 'linear gauge';
    }
}

```

{% endtab %}

## Axis Range

The range of the axis can be set using the [`minimum`](../api/linear-gauge/axis#minimum-number) and [`maximum`](../api/linear-gauge/axis#maximum-number) properties in the Linear Gauge.

{% tab template= "linear-gauge/getting-started", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-lineargauge id="gauge-container">
      <e-axes>
         <e-axis [minimum]='Minimum' [maximum]='Maximum'>
         </e-axis>
      </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent implements OnInit {
    public Minimum: number;
    public Maximum: number;
    ngOnInit(): void {
       this.Minimum = 0,
       this.Maximum = 200
    }
}

```

{% endtab %}

To denote the axis labels with temperature units, add the °C as suffix to each label. This can be achieved by setting the **{value}°C** to the [`format`](../api/linear-gauge/labelModel/#format-string) property in the [`labelStyle`](../api/linear-gauge/axis#labelstyle-labelmodel) object of the axis. Here, **{value}** acts as a placeholder for each axis label.

To change the pointer value from the default value of the gauge, set the [`value`](../api/linear-gauge/pointer/#value-number) property in [`pointers`](../api/linear-gauge/pointerModel/) object of the axis.

{% tab template= "linear-gauge/getting-started", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-lineargauge id="gauge-container">
      <e-axes>
         <e-axis minimum=0 maximum=200>
           <e-pointers>
             <e-pointer value=140></e-pointer>
           </e-pointers>
           <e-ranges>
             <e-range start=0 end=80 startWidth=15 endWidth=15></e-range>
             <e-range start=80 end=120 startWidth=15 endWidth=15></e-range>
             <e-range start=120 end=140 startWidth=15 endWidth=15></e-range>
             <e-range start=140 end=200 startWidth=15 endWidth=15></e-range>
           </e-ranges>
         </e-axis>
      </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent implements OnInit {
    public Label: Object;
    ngOnInit(): void {
      this.Label = {
           format: '{value}°C'
      };
    }
}

```

{% endtab %}

## Setting the value of pointer

The pointer value is changed in the below sample using the [`value`](../api/linear-gauge/pointer/#value-number) property in [`pointers`](../api/linear-gauge/pointer) object of the axis.

{% tab template= "linear-gauge/getting-started", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-lineargauge id="gauge-container">
      <e-axes>
         <e-axis minimum=0 maximum=200>
           <e-pointers>
             <e-pointer value=40 color='green'></e-pointer>
           </e-pointers>
         </e-axis>
      </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
    }
}

```

{% endtab %}
