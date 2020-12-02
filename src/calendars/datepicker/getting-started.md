---
title: "Getting Started"
component: "DatePicker"
description: "This getting started section briefly explains how to create a date picker component in an application."
---

# Getting Started

The following section explains the steps required to create a
simple DatePicker component and also it demonstrates the basic usage of the DatePicker.

## Dependencies

Install the below required dependency package in order to use the `DatePicker` component in your application.

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
ng new syncfusion-angular-datepicker
```

By default, it install the CSS style base application. To setup with SCSS, pass --style=scss argument on create project.

Example code snippet.

```bash
ng new syncfusion-angular-datepicker --style=scss
```

Navigate to the created project folder.

```bash
cd syncfusion-angular-datepicker
```

## Adding DatePicker package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install DatePicker component, use the following command.

```bash
npm install @syncfusion/ej2-angular-calendars --save
(or)
npm I @syncfusion/ej2-angular-calendars --save
```

> The **--save** will instruct NPM to include the DatePicker package inside of the `dependencies` section of the `package.json`.

## Registering DatePicker module

Import DatePicker module into Angular application(src/app/app.module.ts) from the package `@syncfusion/ej2-angular-calendars`.

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the DatePickerModule for the DatePicker component
import { DatePickerModule } from '@syncfusion/ej2-angular-calendars';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of DatePickerModule into NgModule
  imports:      [ BrowserModule, DatePickerModule ],
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

## Adding DatePicker component

Modify the template in [src/app/app.component.ts] file to render the DatePicker component. by using `<ejs-datepicker>` selector.

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<!-- To Render DatePicker -->
             <ejs-datepicker></ejs-datepicker>`
})
export class AppComponent  { }
```

## Running the application

After completing the configuration required to render a basic DatePicker, run the following command to
display the output in your default browser.

```cmd
ng serve
```

The following example illustrates the output in your browser

{% tab template="datepicker/getting-started", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-datepicker></ejs-datepicker>`
})
export class AppComponent {
    constructor() {
    }
}

```

{% endtab %}

## Setting the selected date

To set the selected date, use the [`value`](../api/datepicker#value)
property.

The below example demonstrates the DatePicker with current date as selected one.

{% tab template="datepicker/getting-started", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-datepicker [value]='dateValue' placeholder='Enter date'></ejs-datepicker>`
})
export class AppComponent {
    public dateValue: Date = new Date();
    constructor() {
    }
}

```

{% endtab %}

## Setting the date range to restrict selection

To restrict the selection of date within a specified range, use the [`min`](../api/datepicker#min)
and [`max`](../api/datepicker#max) properties. To know more about range restriction in DatePicker, please refer this [page](./date-range).

The below example demonstrates the DatePicker to select a date within a range from 7 to 27.

{% tab template="datepicker/getting-started", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <ejs-datepicker id="datepicker" [min]='minDate' [max]='maxDate'></ejs-datepicker>
        `
})
export class AppComponent {
    public month: number = new Date().getMonth();
    public fullYear: number = new Date().getFullYear();
    public minDate: Date = new Date(this.fullYear, this.month , 7);
    public maxDate: Date = new Date(this.fullYear, this.month, 27);
    constructor() {
    }
}
```

{% endtab %}

## See Also

* [Change the format of selected date](./date-format)
* [Render DatePicker with specific culture](./globalization)
* [How to change the initial view of the DatePicker](./date-views)
* [How to achieve validation with DatePicker](./how-to/custom-validation-using-form-validator)
* [How to achieve two-way binding with DatePicker](./how-to/two-way-binding)
