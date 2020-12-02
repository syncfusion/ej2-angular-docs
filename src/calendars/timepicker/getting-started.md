---
title: "Getting Started"
component: "TimePicker"
description: "This getting started section briefly explains how to create a time picker component in an application."
---

# Getting Started

This section briefly explains how to create a simple **TimePicker** component, and configure its available functionalities in Angular by
using [quickstart](https://github.com/angular/quickstart.git) seed repository.

## Dependencies

Install the below required dependency package in order to use the `TimePicker` component in your application.

```javascript
|-- @syncfusion/ej2-angular-calendars
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-calendars
        |-- @syncfusion/ej2-inputs
          |-- @syncfusion/ej2-splitbuttons
        |-- @syncfusion/ej2-lists
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
ng new syncfusion-angular-timepicker
```

By default, it install the CSS style base application. To setup with SCSS, pass --style=scss argument on create project.

Example code snippet.

```bash
ng new syncfusion-angular-timepicker --style=scss
```

Navigate to the created project folder.

```bash
cd syncfusion-angular-timepicker
```

## Adding TimePicker package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install TimePicker component, use the following command.

```bash
npm install @syncfusion/ej2-angular-calendars --save
(or)
npm I @syncfusion/ej2-angular-calendars --save
```

> The **--save** will instruct NPM to include the TimePicker package inside of the `dependencies` section of the `package.json`.

## Registering TimePicker module

Import TimePicker module into Angular application(src/app/app.module.ts) from the package `@syncfusion/ej2-angular-calendars`.

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the TimePickerModule for the TimePicker component
import { TimePickerModule } from '@syncfusion/ej2-angular-calendars';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of TimePickerModule into NgModule
  imports:      [ BrowserModule, TimePickerModule ],
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

## Adding TimePicker component

Modify the template in [src/app/app.component.ts] file to render the TimePicker component.
Add the Angular TimePicker by using `<ejs-timepicker>` selector in `template` section of the app.component.ts file.

```javascript
import { Component } from '@angular/core';
import { enableRipple } from '@syncfusion/ej2-base';

//enable ripple style
enableRipple(true);

@Component({
  selector: 'app-root',
  template: `<!-- To Render TimePicker -->
             <ejs-timepicker></ejs-timepicker>`
})
export class AppComponent  { }
```

## Running the application

After completing the configuration required to render a basic TimePicker, run the following command to
display the output in your default browser.

```cmd
ng serve
```

The following example illustrates the output in your browser

{% tab template="timepicker/getting-started", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { enableRipple } from '@syncfusion/ej2-base';

//enable ripple style
enableRipple(true);

@Component({
    selector: 'app-root',
    template: `<ejs-timepicker placeholder='Select a time' ></ejs-timepicker>`
})
export class AppComponent {
    constructor() {
    }
}

```

{% endtab %}

## Setting the selected, min, and max time

The following example demonstrates how to set the value, min and max time on initializing
the TimePicker. The TimePicker allows you to select the time value within a range from `7:00 AM` to `4:00 PM`.

{% tab template="timepicker/getting-started", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { enableRipple } from '@syncfusion/ej2-base';

//enable ripple style
enableRipple(true);

@Component({
    selector: 'app-root',
    template: `
        <ejs-timepicker [value]='dateValue' [min]='minValue' [max]='maxValue'></ejs-timepicker>
        `
})

export class AppComponent {
    public month: number = new Date().getMonth();
    public fullYear: number = new Date().getFullYear();
    public date: number = new Date().getDate();
    public dateValue: Date = new Date(this.fullYear, this.month , this.date, 10, 0, 0);
    public minValue: Date = new Date(this.fullYear, this.month , this.date, 7, 0, 0);
    public maxValue: Date = new Date(this.fullYear, this.month, this.date, 16, 0 ,0);
    constructor() {
    }

}
```

{% endtab %}

## Setting the time format

Time formats is a way of representing the time value in different string format in textbox and popup
list. By default, the TimePicker's format is based on the culture. You can also customize the format by using the
[`format`](../api/timepicker#format)
property. To know more about the time format standards, refer to the
[`Date and Time Format](../base/internationalization#custom-formats) section.

The following example demonstrates the TimePicker component in 24 hours format with 60 minutes
interval. The time interval is set to
60 minutes by using the [`step`](../api/timepicker#step-number) property.

{% tab template="timepicker/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { enableRipple } from '@syncfusion/ej2-base';

//enable ripple style
enableRipple(true);

@Component({
    selector: 'app-root',
    template: `
        <ejs-timepicker [placeholder]='watermark' [format]='formatString' [step]='interval' ></ejs-timepicker>
        `
})

export class AppComponent {
    public watermark: string = 'Select a time';
    // sets the format property to display the time value in 24 hours format.
    public formatString: string = 'HH:mm';
    public interval: number = 60;
    constructor() {
    }
}

```

{% endtab %}

> Once the format property is defined, it will be applicable to all the cultures.

## See Also

* [Render TimePicker with min and max time](./time-range)
* [How to achieve validation with TimePicker](./how-to/custom-validation-using-form-validator)
* [Render TimePicker with specific culture](./globalization)
* [How to achieve two-way binding with TimePicker](./how-to/two-way-binding)
* [Reactive forms with TimePicker](./how-to/reactive-form)
