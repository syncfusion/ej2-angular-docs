---
title: "Drop-down list Getting started"
component: "DropDownList"
description: "This section explains how to create a simple Syncfusion angular drop-down list component and configure it's functionalities in angular."
---

# Getting Started

This section briefly explains how to create a simple **DropDownList** component and configure its available
functionalities in Angular.

## Dependencies

The following list of dependencies are required to use the DropDownList component in your application.

```javascript
|-- @syncfusion/ej2-angular-dropdowns
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-dropdowns
        |-- @syncfusion/ej2-lists
        |-- @syncfusion/ej2-inputs
        |-- @syncfusion/ej2-navigations
        |-- @syncfusion/ej2-popups
            |-- @syncfusion/ej2-buttons

```

## Setup angular environment

Angular provides the easiest way to set angular CLI projects using [`Angular CLI`](https://github.com/angular/angular-cli) tool.

Install the CLI application globally to your machine.

```bash
npm install -g @angular/cli
```

## Create a new application

```bash
ng new syncfusion-angular-dropdownlist
```

By default, it install the CSS style base application. To setup with SCSS, pass --style=scss argument on create project.

Example code snippet.

```bash
ng new syncfusion-angular-dropdownlist --style=scss
```

Navigate to the created project folder.

```bash
cd syncfusion-angular-dropdownlist
```

## Adding DropDownList package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install DropDownList component, use the following command.

```bash
npm install @syncfusion/ej2-angular-dropdowns --save
(or)
npm i @syncfusion/ej2-angular-dropdowns --save
```

> The **--save** will instruct NPM to include the DropDownList package inside of the [dependencies](./getting-started#dependencies) section of the `package.json`.

## Registering DropDownList module

Import DropDownList module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-dropdowns`.

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the DropDownListModule for the DropDownList component
import { DropDownListModule } from '@syncfusion/ej2-angular-dropdowns';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-dropdowns module into NgModule
  imports:      [ BrowserModule, DropDownListModule ],
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
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-lists/styles/material.css';
@import '../node_modules/@syncfusion/ej2-angular-dropdowns/styles/material.css';
```

## Adding DropDownList component

Modify the template in [src/app/app.component.ts] file to render the DropDownList component.
Add the Angular DropDownList by using `<ejs-dropdownlist>` selector in `template` section of the app.component.ts file.

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  // specifies the template string for the DropDownList component
  template: `<ejs-dropdownlist id='ddlelement'></ejs-dropdownlist>`
})
export class AppComponent  { }
```

## Binding data source

After initialization, populate the DropDownList with data using the `dataSource` property.
Here, an array of string values passed to DropDownList component.

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component
    template: `<ejs-dropdownlist id='ddlelement' [dataSource]='data'></ejs-dropdownlist>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: string[] = ['Snooker', 'Tennis', 'Cricket', 'Football', 'Rugby'];
}
```

## Running the application

After completing the configuration required to render a basic DropDownList, run the following command to
display the output in your default browser.

```cmd
ng serve
```

The following example illustrates the output in your browser.

{% tab template="dropdownlist/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component with dataSource
    template: `<ejs-dropdownlist id='ddlelement' [dataSource]='data' placeholder = 'Select a game'></ejs-dropdownlist>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: string[] = ['Snooker', 'Tennis', 'Cricket', 'Football', 'Rugby'];
}
```

{% endtab %}

## Configure the popup list

By default, the width of the popup list automatically adjusts according to the DropDownList input
element's width, and the height of the popup list has '300px'.

The height and width of the popup list can also be customized using the
[popupHeight](../api/drop-down-list/#popupheight)
 &nbsp;and [popupWidth](../api/drop-down-list/#popupwidth) property
respectively.

In the following sample, popup list's width and height are configured.

{% tab template="dropdownlist/getting-started", sourceFiles="app/**/*.ts"%}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template url path
    template: `<ejs-dropdownlist id='ddlelement' [dataSource]='data' placeholder='Select a game' popupHeight='200px' popupWidth='250px' ></ejs-dropdownlist>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: string[] = ['Badminton', 'Basketball', 'Cricket', 'Football', 'Golf', 'Hockey', 'Rugby', 'Snooker','Tennis'];
}
```

{% endtab %}

## Two-way binding

In DropDownList, the `value` property supports two-way binding functionality.
The following example demonstrates how to work the two-way binding functionality in DropDownList.

{% tab template="dropdownlist/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component and
    // input element for checking the two-way binding support using value property
    template: `
    <ejs-dropdownlist id='ddlelement' [dataSource]='data' [(value)]='value' placeholder='Select a game'></ejs-dropdownlist>
    <div style='margin-top: 50px'>
        <input type="text" [(ngModel)]="value" style="width:245px;height:25px" />
     </div>
    `
})
export class AppComponent {
    constructor() {
    }
    // defined the array of complex data
    public data: string[] = [ 'Badminton', 'Basketball', 'Cricket', 'Football' ];
    // set a value to pre-select
    public value: string = 'Badminton';
}

```

{% endtab %}

## See Also

* [How to bind the data](./data-binding/)