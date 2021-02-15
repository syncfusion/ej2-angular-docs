---
title: "Getting Started"
component: "Spreadsheet"
description: "This section helps to learn how to create the Spreadsheet control in Angular application with its basic features like selection, editing, formatting, importing and exporting to Excel."
---

# Getting Started

This section explains the steps to create a simple Spreadsheet control with basic features in an Angular environment.

To get start quickly with Angular Spreadsheet using CLI, you can check on this video:

`youtube:2Ozwe37X-7Q`

## Dependencies

The following list of dependencies are required to use the Spreadsheet control in your application.

```js
  |-- @syncfusion/ej2-angular-spreadsheet
      |-- @syncfusion/ej2-angular-base
      |-- @syncfusion/ej2-spreadsheet
          |-- @syncfusion/ej2-base
          |-- @syncfusion/ej2-dropdowns
          |-- @syncfusion/ej2-navigations
          |-- @syncfusion/ej2-grids
```

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

## Adding Syncfusion Spreadsheet package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Spreadsheet control, use the following command.

```bash
npm install @syncfusion/ej2-angular-spreadsheet --save
```

> The **--save** will instruct NPM to include the spreadsheet package inside of the `dependencies` section of the `package.json`.

## Registering Spreadsheet Module

Import Spreadsheet module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-spreadsheet` [src/app/app.module.ts].

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { SpreadsheetAllModule } from '@syncfusion/ej2-angular-spreadsheet';
import { AppComponent } from './app.component';

@NgModule({
  imports:      [ BrowserModule, SpreadsheetAllModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding CSS reference

The following CSS files are available in `../node_modules/@syncfusion` package folder.
This can be referenced in `[src/styles.css]` using following code.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-lists/styles/material.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../node_modules/@syncfusion/ej2-spreadsheet/styles/material.css';
@import '../node_modules/@syncfusion/ej2-grids/styles/material.css';
```

## Add Spreadsheet control

Modify the template in [src/app/app.component.ts] file to render the spreadsheet component. Add the Angular Spreadsheet by using `<ejs-spreadsheet>` selector in template section of the `app.component.ts` file.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-container',
  // specifies the template string for the Spreadsheet control
  template: `<ejs-spreadsheet> </ejs-spreadsheet>`
})
export class AppComponent { }

```

## Run the application

Use the following command to run the application in the web browser

```cmd
ng serve
```

The following example shows a basic Spreadsheet component

{% tab template="spreadsheet/spreadsheet", sourceFiles="app/**/*.ts", isDefaultActive=true , iframeHeight="450px" %}

```javascript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: '<ejs-spreadsheet > </ejs-spreadsheet>'
})
export class AppComponent { }
```

{% endtab %}

## See Also

* [Data Binding](./data-binding)
* [Open and Save](./open-save)