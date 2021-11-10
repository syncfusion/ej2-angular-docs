---
title: "Getting Started"
component: "DateTimePicker"
description: "This getting started section briefly explains how to create a date time picker component in an application."
---

# Getting Started

The following section explains the steps required to create a
simple DateTimePicker component and also it demonstrates the basic usage of the DateTimePicker.

## Dependencies

Install the below required dependency package in order to use the `DateTimePicker` component in your application.

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
ng new syncfusion-angular-datetimepicker
```

By default, it install the CSS style base application. To setup with SCSS, pass --style=scss argument on create project.

Example code snippet.

```bash
ng new syncfusion-angular-datetimepicker --style=scss
```

Navigate to the created project folder.

```bash
cd syncfusion-angular-datetimepicker
```

## Adding DateTimePicker package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install DateTimePicker component, use the following command.

```bash
npm install @syncfusion/ej2-angular-calendars --save
(or)
npm I @syncfusion/ej2-angular-calendars --save
```

> The **--save** will instruct NPM to include the DateTimePicker package inside of the `dependencies` section of the `package.json`.

## Registering DateTimePicker module

Import DateTimePicker module into Angular application(src/app/app.module.ts) from the package `@syncfusion/ej2-angular-calendars`.

```javascript
import { NgModule } from "@angular/core";
import { BrowserModule } from "@angular/platform-browser";
// import the DateTimePickerModule for the DateTimePicker component
import { DateTimePickerModule } from "@syncfusion/ej2-angular-calendars";
import { AppComponent } from "./app.component";

@NgModule({
  //declaration of DateTimePickerModule into NgModule
  imports: [BrowserModule, DateTimePickerModule],
  declarations: [AppComponent],
  bootstrap: [AppComponent]
})
export class AppModule {}
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

## Adding DateTimePicker component

Modify the template in [src/app/app.component.ts] file to render the Angular DateTime Picker component.
Add the Angular DateTimePicker by using `<ejs-datetimepicker>` selector in `template` section of the app.component.ts file.

```javascript

import { Component } from "@angular/core";

@Component({
  selector: 'app-root',
  template: `<!-- To Render DateTimePicker -->
             <ejs-datetimepicker></ejs-datetimepicker>`
})
export class AppComponent {}

```

## Running the application

After completing the configuration required to render a basic DateTimePicker, run the following command to
display the output in your default browser.

```cmd
ng serve
```

The following example illustrates the output in your browser

{% tab template="datetimepicker/accessibility", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from "@angular/core";

@Component({
  selector: 'app-root',
  template: `<ejs-datetimepicker></ejs-datetimepicker>`
})
export class AppComponent {
  constructor() {}
}
```

{% endtab %}

## Setting the min and max

The minimum and maximum date time can be defined with the help of `min` and `max` property. The following example demonstrates to set the `min` and `max` on initializing the DateTimePicker. To know more about range restriction in Angular DateTime Picker, please refer this [page](./date-time-range).

{% tab template="datetimepicker/accessibility", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from "@angular/core";

@Component({
  selector: 'app-root',
  template: `<ejs-datetimepicker [min]='minDate' [max]='maxDate'></ejs-datetimepicker>`
})
export class AppComponent {
  public month: number = new Date().getMonth();
  public fullYear: number = new Date().getFullYear();
  public minDate: Date = new Date(this.fullYear, this.month , 22, 12);
  public maxDate: Date = new Date(this.fullYear, this.month, 25, 17);
  constructor() {}
}

```

{% endtab %}

> If the value of `min` or `max` properties
changed through code behind, then you have to
update the `value` property to set within the
range.

N> You can refer to our [Angular DateTime Picker]( https://www.syncfusion.com/angular-ui-components/angular-datetime-picker) feature tour page for its groundbreaking feature representations. You can also explore our [Angular DateTime Picker example](https://ej2.syncfusion.com/angular/demos/#/material/datetimepicker/default) that shows how to render the DateTime Picker in Angular.

## See Also

* [Render DateTimePicker with specific culture](./globalization)
* [How to achieve validation with DateTimePicker](./how-to/custom-validation-using-form-validator)
* [How to achieve two-way binding with DateTimePicker](./how-to/two-way-binding)
* [Reactive forms with DateTimePicker](./how-to/reactive-form)
* [Template-driven forms with DateTimePicker](./how-to/template-driven-forms)
