# Getting Started

This section explains you the steps required to create a simple circular gauge and demonstrate the basic usage of circular gauge control.

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

## Adding Syncfusion Circular Gauge package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Circular Gauge component, use the following command.

```bash
npm install @syncfusion/ej2-angular-circulargauge --save
```

> The **--save** will instruct NPM to include the circular gauge package inside of the `dependencies` section of the `package.json`.

## Registering Circular Gauge Module

Import Circular Gauge module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-circulargauge` [src/app/app.module.ts].

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the CircularGaugeModule for the Circular Gauge component
import { CircularGaugeModule } from '@syncfusion/ej2-angular-circulargauge';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ChartModule into NgModule
  imports:      [ BrowserModule, CircularGaugeModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

* Modify the template in `app.component.ts` file to render the `ej2-angular-circulargauge` component
`[src/app/app.component.ts]`.

```javascript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'app-container',
  // specifies the template string for the Charts component
  template: `<ejs-circulargauge id='circular-container'></ejs-circulargauge>`,
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

The below example shows a basic Circular Gauge.

{% tab template="circulargauge/getting-started", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    // specifies the template string for the CircularGauge component
    template: `<ejs-circulargauge id="circular-container"></ejs-circulargauge>`
})
export class AppComponent {

}
```

{% endtab %}

## Set Pointer Value

Pointer value is used to indicate the gauge value using [`value`](../api/circular-gauge/pointer#value-number) property in [`pointers`](../api/circular-gauge/pointer).

{% tab template="circulargauge/getting-started", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container">
        <e-axes>
            <e-axis>
                <e-pointers>
                    <e-pointer value=35></e-pointer>
                </e-pointers>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
        // Initialize objects.
    }

}

```

{% endtab %}