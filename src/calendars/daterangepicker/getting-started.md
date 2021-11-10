---
title: "Getting Started"
component: "DateRangePicker"
description: "This getting started section briefly explains how to create a date range picker component in an application."
---

# Getting Started

The following section explains the steps required to create a
simple DateRangePicker component and also it demonstrates the basic usage of the DateRangePicker.

## Dependencies

Install the below required dependency packages in order to use the `DateRangePicker` component in your application.

```javascript
|-- @syncfusion/ej2-angular-calendars
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-calendars
        |-- @syncfusion/ej2-lists
        |-- @syncfusion/ej2-inputs
          |-- @syncfusion/ej2-splitbuttons
        |-- @syncfusion/ej2-popups
            |-- @syncfusion/ej2-buttons
```

## Setup Angular environment

Angular provides the easiest way to set angular CLI projects using [`Angular CLI`](https://github.com/angular/angular-cli) tool.

Install the CLI application globally to your machine.

```bash
npm install -g @angular/cli
```

## Create a new application

```bash
ng new syncfusion-angular-daterangepicker
```

By default, it install the CSS style base application. To setup with SCSS, pass --style=scss argument on create project.

Example code snippet.

```bash
ng new syncfusion-angular-daterangepicker --style=scss
```

Navigate to the created project folder.

```bash
cd syncfusion-angular-daterangepicker
```

## Adding DateRangePicker package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install DateRangePicker component, use the following command.

```bash
npm install @syncfusion/ej2-angular-calendars --save
(or)
npm I @syncfusion/ej2-angular-calendars --save
```

> The **--save** will instruct NPM to include the DateRangePicker package inside of the `dependencies` section of the `package.json`.

## Registering DateRangePicker module

Import DateRangePicker module into Angular application(src/app/app.module.ts) from the package `@syncfusion/ej2-angular-calendars`.

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the DateRangePickerModule for the DateRangPicker component
import { DateRangePickerModule } from '@syncfusion/ej2-angular-calendars';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of DateRangePickerModule into NgModule
  imports:      [ BrowserModule, DateRangePickerModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding CSS reference

The following CSS files are available in `../node_modules/@syncfusion` package folder.
This can be referenced in [src/styles.css] using following code.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-lists/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-calendars/styles/material.css';
@import '../node_modules/@syncfusion/ej2-angular-calendars/styles/material.css';
```

>If you want to refer the combined component styles, please make use of our [`CRG`](https://crg.syncfusion.com/) (Custom Resource Generator) in your application.

## Adding DateRangePicker component

Modify the template in [src/app/app.component.ts] file to render the DateRangePicker component. by using `<ejs-daterangepicker>` selector.

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<!-- To Render DateRangePicker -->
             <ejs-daterangepicker></ejs-daterangepicker>`
})
export class AppComponent  { }
```

## Running the application

After completing the configuration required to render a basic DateRangePicker, run the following command to
display the output in your default browser.

```cmd
ng serve
```

The following example illustrates the output in your browser

{% tab template="daterangepicker/getting-started", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-daterangepicker></ejs-daterangepicker>`
})
export class AppComponent {
    constructor() {
    }
}

```

{% endtab %}

## Setting the start and end date

The start and end date in a range can be set by using `startDate` and `endDate` properties. To know more about range restriction in DateRangePicker, please refer this [page](./range-selection).

The below example demonstrates the DateRangePicker with startDate and endDate.

{% tab template="daterangepicker/getting-started", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-daterangepicker placeholder='Select a range' [startDate]='start' [endDate]='end'></ejs-daterangepicker>`
})
export class AppComponent {
    public month: number = new Date().getMonth();
    public fullYear: number = new Date().getFullYear();
    public start: Date = new Date(this.fullYear, this.month - 1 , 7);
    public end: Date = new Date(this.fullYear, this.month, 25);
    constructor() {
    }
}

```

{% endtab %}

> You can refer to our [Angular Date Range Picker](https://www.syncfusion.com/angular-ui-components/angular-daterangepicker) feature tour page for its groundbreaking feature representations. You can also explore our [Angular Date Range Picker example](https://ej2.syncfusion.com/angular/demos/#/material/daterangepicker/default) that shows how to render the Date Range Picker in Angular.

## See Also

* [Render DateRangePicker with pre-defined ranges](./customization#preset-ranges)
* [Render DateRangePicker with specific culture](./globalization)
* [How to achieve validation with DateRangePicker](./how-to/custom-validation-using-form-validator)
* [How to achieve two-way binding with DateRangePicker](./how-to/two-way-binding)
* [Reactive forms with DateRangePicker](./how-to/reactive-form)