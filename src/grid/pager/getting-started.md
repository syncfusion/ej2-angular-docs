---
title: "Getting started"
component: "Pager"
description: "Learn how to add and customize the pager in the Essential JS 2."
---

# Getting started

This section explains you the steps required to create a simple Pager
and demonstrate the basic usage of the Pager component in Angular environment.

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

## Adding Syncfusion Pager package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Pager component, use the following command.

```bash
npm install @syncfusion/ej2-angular-grids --save
```

> The **--save** will instruct NPM to include the pager package inside of the **dependencies** section of the **package.json**.

## Registering Pager Module

Import Pager module into Angular application(app.module.ts) from the package **@syncfusion/ej2-angular-grids** [src/app/app.module.ts].

```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { PagerModule} from '@syncfusion/ej2-angular-grids';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    PagerModule
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

## Adding CSS reference

The CSS files are available in ../node_modules/@syncfusion package folder. This can be referenced in [src/styles.css] using following code..

```css
@import '../node_modules/@syncfusion/ej2-angular-grids/styles/material.css';
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
```

## Adding Pager component

Modify the template in [src/app/app.component.ts] file to render the pager component. Add the Angular pager by using `<ejs-pager>` selector in template section of the app.component.ts file.

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-root',
  // specifies the template string for the Pager component
  template: `<ejs-pager [totalRecordsCount]='20'>
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
    selector: 'app-root',
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
    selector: 'app-root',
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
ng serve --open
```

Output will be appears as follows.

{% tab template="pager/pager", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-pager [pageSize]='8' [pageCount]='3' [totalRecordsCount]='20'>
                </ejs-pager>`
})
export class AppComponent implements OnInit{

    ngOnInit(): void {
    }
}

```

{% endtab %}