---
title: "Getting Started"
component: "Calendar"
description: "This getting started section briefly explains how to create a calendar component in an application."
---

# Getting Started

The following section explains the steps required to create a
simple Calendar component and also it demonstrates the basic usage of the Calendar.

## Dependencies

Install the below required dependency package in order to use the `Calendar` component in your application.

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
ng new syncfusion-angular-calendar
```

By default, it install the CSS style base application. To setup with SCSS, pass --style=scss argument on create project.

Example code snippet.

```bash
ng new syncfusion-angular-calendar --style=scss
```

Navigate to the created project folder.

```bash
cd syncfusion-angular-calendar
```

## Adding Calendar package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Calendar component, use the following command.

```bash
npm install @syncfusion/ej2-angular-calendars --save
(or)
npm I @syncfusion/ej2-angular-calendars --save
```

> The **--save** will instruct NPM to include the Calendar package inside of the `dependencies` section of the `package.json`.

## Registering Calendar module

Import Calendar module into Angular application(src/app/app.module.ts) from the package`@syncfusion/ej2-angular-calendars`.

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the CalendarModule for the Calendar component
import { CalendarModule } from '@syncfusion/ej2-angular-calendars';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of CalendarModule into NgModule
  imports:      [ BrowserModule, CalendarModule ],
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

## Adding Calendar component

Modify the template in [src/app/app.component.ts] file to render the Calendar component. by using `<ejs-calendar>` selector.

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<!-- To Render Calendar -->
             <ejs-calendar></ejs-calendar>`
})
export class AppComponent  { }
```

## Running the application

After completing the configuration required to render a basic Calendar, run the following command to
display the output in your default browser.

```cmd
ng serve
```

The following example illustrates the output in your browser

{% tab template="calendar/getting-started",sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
    <!-- To Render Calendar -->
    <ejs-calendar></ejs-calendar>`
})
export class AppComponent {
    constructor() {
    }
}
```

{% endtab %}

## Setting the value, min and max dates

The following example demonstrates how to set the value,  min and max dates on initializing the Calendar. Here the Calendar allows you to select a date within a range from 9th to 15th. To know more about range restriction in Calendar, please refer this [page](./date-range).

{% tab template="calendar/getting-started", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
              <!-- Sets the value, min and max -->
              <ejs-calendar [value]='dateValue' [min]='minDate' [max]='maxDate'></ejs-calendar>
        `
})
export class AppComponent {
    public month: number = new Date().getMonth();
    public fullYear: number = new Date().getFullYear();
    public dateValue: Date = new Date(this.fullYear, this.month , 11);
    public minDate: Date = new Date(this.fullYear, this.month , 9);
    public maxDate: Date = new Date(this.fullYear, this.month, 15);
    constructor() {
    }
}
```

{% endtab %}

## See Also

* [Select multiple dates in the Calendar](./multi-select)
* [Render Calendar with specific culture](./globalization)
* [How to change the initial view of the Calendar](./calendar-views)
* [Render Calendar with week numbers](./how-to/render-the-calendar-with-week-numbers)
* [Show other month dates](./how-to/show-dates-of-other-months)