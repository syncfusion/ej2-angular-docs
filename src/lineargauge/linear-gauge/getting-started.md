---
title: "Getting Started with Angular Linear Gauge component | Syncfusion "

component: "Linear Gauge"

description: "Learn here about getting started with Syncfusion Angular Linear Gauge component, its element and more."
---

# Getting Started with Angular Linear Gauge

<!-- markdownlint-disable MD013 -->

This section explains you the steps required to create a simple Linear Gauge and demonstrate the basic usage of the Linear Gauge component.

## Dependencies

Below is the list of minimum dependencies required to use the Linear Gauge component.

```javascript
|-- @syncfusion/ej2-angular-lineargauge
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-angular-buttons
    |-- @syncfusion/ej2-angular-popups
    |-- @syncfusion/ej2-lineargauge
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-buttons
    |-- @syncfusion/ej2-popups
```

## Setting up an angular project

Angular provides the easiest way to set angular CLI projects using Angular CLI tool.

Install the CLI application globally to your machine using the below command.

```javascript
npm install -g @angular/cli
```

## Installation and Configuration

* To get started with the basic `Angular` sample, use the following commands.

```javascript
git clone https://github.com/angular/quickstart.git quickstart
cd quickstart
npm install
```

For more information, refer to [Angular sample setup](https://angular.io/guide/setup)

* Install the Linear Gauge packages using below command. The Syncfusion packages can be be get from the npm [`link`](https://www.npmjs.com/search?q=%40syncfusion%2Fej2-angular-).

Add `@syncfusion/ej2-angular-lineargauge` package to the application.

```javascript
npm install @syncfusion/ej2-angular-lineargauge --save
```

The above package installs `Linear Gauge dependencies` which are required to render the Linear Gauge component in Angular environment

* Syncfusion `ej2-angular-lineargauge` packages needs to be mapped in `systemjs.config.js` configuration file.

```javascript
/**
 * System configuration for Angular samples
 * Adjust as necessary for your application needs.
 */
(function (global) {
  System.config({
    paths: {
      // paths serve as alias
      'npm:': 'node_modules/',
      "syncfusion:": "node_modules/@syncfusion/", // syncfusion alias

    },
    // map tells the System loader where to look for things
    map: {
      // our app is within the app folder
      'app': 'app',

      // angular bundles
      '@angular/core': 'npm:@angular/core/bundles/core.umd.js',
      '@angular/common': 'npm:@angular/common/bundles/common.umd.js',
      '@angular/compiler': 'npm:@angular/compiler/bundles/compiler.umd.js',
      '@angular/platform-browser': 'npm:@angular/platform-browser/bundles/platform-browser.umd.js',
      '@angular/platform-browser-dynamic': 'npm:@angular/platform-browser-dynamic/bundles/platform-browser-dynamic.umd.js',
      '@angular/http': 'npm:@angular/http/bundles/http.umd.js',
      '@angular/router': 'npm:@angular/router/bundles/router.umd.js',
      '@angular/forms': 'npm:@angular/forms/bundles/forms.umd.js',

      // syncfusion bundles
      "@syncfusion/ej2-base": "node_modules/@syncfusion/ej2-base/dist/ej2-base.umd.min.js",
      "@syncfusion/ej2-lineargauge": "node_modules/@syncfusion/ej2-lineargauge/dist/ej2-lineargauge.umd.min.js",
      "@syncfusion/ej2-angular-base": "node_modules/@syncfusion/ej2-angular-base/dist/ej2-angular-base.umd.min.js",
      "@syncfusion/ej2-angular-lineargauge": "node_modules/@syncfusion/ej2-angular-lineargauge/dist/ej2-angular-lineargauge.umd.min.js",
      "@syncfusion/ej2-buttons": "syncfusion:ej2-buttons/dist/ej2-buttons.umd.min.js",
      "@syncfusion/ej2-popups": "syncfusion:ej2-popups/dist/ej2-popups.umd.min.js",
      "@syncfusion/ej2-angular-buttons": "syncfusion:ej2-angular-buttons/dist/ej2-angular-buttons.umd.min.js",
      "@syncfusion/ej2-angular-popups": "syncfusion:ej2-angular-popups/dist/ej2-angular-popups.umd.min.js",

      // other libraries
      'rxjs':                      'npm:rxjs',
      'angular-in-memory-web-api': 'npm:angular-in-memory-web-api/bundles/in-memory-web-api.umd.js'
    },
    // packages tells the System loader how to load when no filename and/or no extension
    packages: {
      app: {
        defaultExtension: 'js',
        meta: {
          './*.js': {
            loader: 'systemjs-angular-loader.js'
          }
        }
      },
      rxjs: {
        defaultExtension: 'js'
      }
    }
  });
})(this);
```

* Import LinearGauge module in the **app.module.ts** file into Angular application from the package `@syncfusion/ej2-angular-lineargauge`.

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the LinearGaugeModule for the LinearGauge component
import { LinearGaugeModule } from '@syncfusion/ej2-angular-lineargauge';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-lineargauge module into NgModule
  imports:      [ BrowserModule, LinearGaugeModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

* Change the template in `app.component.ts` file to render the `ej2-angular-lineargauge` component.

```javascript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'my-app',
  // specifies the template string for the linear gauge component
  template: `<ejs-lineargauge id='container'></ejs-lineargauge>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent  { }
```

* Now run the application in the browser using the below command.

```cmd
ng serve
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
