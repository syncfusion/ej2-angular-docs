---
title: "Getting started"
component: "Pager"
description: "Learn how to add and customize the pager in the Essential JS 2."
---

# Getting started

This section explains you the steps required to create a simple Pager
and demonstrate the basic usage of the Pager component in Angular environment.

## Dependencies

Below is the list of minimum dependencies required to use the Pager.

```javascript
|-- @syncfusion/ej2-angular-grids
    |-- @syncfusion/ej2-grids
```

## Setup for Local Development

* To setup basic `Angular` sample use following commands.

```javascript
git clone https://github.com/angular/quickstart.git quickstart
cd quickstart
npm install
```

For more information, refer to [Angular sample setup](https://angular.io/guide/setup)

* To install `Pager` packages use below command.

```javascript
npm install @syncfusion/ej2-angular-grids --save
```

The above package installs `Pager dependencies` which are required to render the component in Angular environment.

## Configuring System JS

`Syncfusion Pager packages` need to be mapped in system.config.js configuration file.

* Syncfusion `ej2-angular-grids` packages needs to be mapped in `systemjs.config.js` configuration file.

```javascript
/**
 * System configuration for Angular samples
 * Adjust as necessary for your application needs.
 */
(function (global) {
  System.config({
    paths: {
      // paths serve as alias
      'npm:': 'node_modules/'
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
      "@syncfusion/ej2-data": "node_modules/@syncfusion/ej2-data/dist/ej2-data.umd.min.js",
      "@syncfusion/ej2-grids": "node_modules/@syncfusion/ej2-grids/dist/ej2-grids.umd.min.js",
      "@syncfusion/ej2-angular-base": "node_modules/@syncfusion/ej2-angular-base/dist/ej2-angular-base.umd.min.js",
      "@syncfusion/ej2-angular-grids": "node_modules/@syncfusion/ej2-angular-grids/dist/ej2-angular-grids.umd.min.js",

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

## Adding CSS reference

Combined CSS files are available in the Essential JS 2 package root folder.
This can be referenced in your [src/styles/styles.css] using following code.

```css
@import '../../node_modules/@syncfusion/ej2/material.css';
```

> To refer individual component CSS, please refer to
[Individual Component theme files](../appearance/theme/#referring-individual-component-theme) section.

## Adding Pager component

Import Pager module into Angular application(app.module.ts) from the package @syncfusion/ej2-angular-grids [src/app/app.module.ts].

Now place the below Pager code in the `app.ts`.
Here the Pager is rendered with `totalRecordsCount` which is used to render numeric container.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the PagerModule for the Pager component
import { PagerModule } from '@syncfusion/ej2-angular-grids';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-grids module into NgModule
  imports:      [ BrowserModule, PagerModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

Modify the template in [src/app/app.component.ts] file to render the `ej2-angular-grids` component.

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'my-app',
  // specifies the template string for the Pager component
  template: `<ejs-pager' [totalRecordsCount]='20'>
               </ejs-pager>`
})
export class AppComponent implements OnInit {
     ngOnInit(): void {
    }

}
```

## Page Size

`pageSize` value defines the number of records to be displayed per page. The default value for the `pageSize` is 12.

{% tab template="pager/pager", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-pager [pageSize]= '1' [totalRecordsCount]='20'>
                </ejs-pager>`
})
export class AppComponent implements OnInit{

    ngOnInit(): void {
    }
}

```

{% endtab %}

## Page Count

`pageCount` value defines the number of pages to be displayed in the pager component for navigation.
The default value for `pageCount` is 10 and value will be updated based on [`totalRecordsCount`](../api/pager#totalrecordscount)
and [`pageSize`](#page-size) values.

{% tab template="pager/pager", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-pager [pageSize]='1' [pageCount]='3' [totalRecordsCount]='20'>
                </ejs-pager>`
})
export class AppComponent implements OnInit{

    ngOnInit(): void {
    }
}

```

{% endtab %}

## Run the application

The quickstart project is configured to compile and run the application in browser. Use the following command to run the application.

```javascript
npm start
```

Output will be appears as follows.

{% tab template="pager/pager", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-pager [pageSize]='8' [pageCount]='3' [totalRecordsCount]='20'>
                </ejs-pager>`
})
export class AppComponent implements OnInit{

    ngOnInit(): void {
    }
}

```

{% endtab %}