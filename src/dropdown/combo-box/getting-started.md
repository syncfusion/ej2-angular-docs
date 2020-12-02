---
title: "Combo box Getting started"
component: "ComboBox"
description: "This section explains how to create a simple Syncfusion angular combo box component and configure its functionalities."
---

# Getting Started

This section explains how to create a simple **ComboBox** component and configure its available
functionalities in Angular.

## Dependencies

The following list of dependencies are required to use the ComboBox component in your application.

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
ng new syncfusion-angular-combobox
```

By default, it install the CSS style base application. To setup with SCSS, pass --style=scss argument on create project.

Example code snippet.

```bash
ng new syncfusion-angular-combobox --style=scss
```

Navigate to the created project folder.

```bash
cd syncfusion-angular-combobox
```

## Adding ComboBox package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install ComboBox component, use the following command.

```bash
npm install @syncfusion/ej2-angular-dropdowns --save
(or)
npm i @syncfusion/ej2-angular-dropdowns --save
```

> The **--save** will instruct NPM to include the ComboBox package inside of the [dependencies](./getting-started#dependencies) section of the `package.json`.

## Registering ComboBox module

Import ComboBox module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-dropdowns`.

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the ComboBoxModule for the ComboBox component
import { ComboBoxModule } from '@syncfusion/ej2-angular-dropdowns';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-dropdowns module into NgModule
  imports:      [ BrowserModule, ComboBoxModule ],
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

## Adding ComboBox component

Modify the template in [src/app/app.component.ts] file to render the ComboBox component.
Add the Angular ComboBox by using `<ejs-combobox>` selector in `template` section of the app.component.ts file.

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  // specifies the template string for the ComboBox component
  template: `<ejs-combobox id='comboelement'></ejs-combobox>`
})
export class AppComponent  { }
```

## Binding data source

After initializing, populate the ComboBox with data using the [`dataSource`](../api/combo-box/#datasource) property.
Here, an array of string values passed to ComboBox component.

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the ComboBox component
    template: `<ejs-combobox id='comboelement' [dataSource]='data'></ejs-combobox>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: string[] = ['Cricket', 'Football', 'Rugby', 'Snooker', 'Tennis'];
}
```

## Running the application

After completing the configuration required to render a basic ComboBox, run the following command to
display the output in your default browser.

```cmd
ng serve
```

The following example illustrates the output in your browser.

{% tab template="combobox/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the ComboBox component with dataSource
    template: `<ejs-combobox id='comboelement' [dataSource]='data' placeholder = 'Select a game'></ejs-combobox>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: string[] = ['Cricket', 'Football', 'Rugby', 'Snooker', 'Tennis'];
}
```

{% endtab %}

## Custom values

The ComboBox allows the user to give input as custom value which is not required to present in predefined
set of values. By default, this support is enabled by [allowCustom](../api/combo-box/#allowcustom)
 property. In this case, both text field and value field considered as same.
The custom value will be sent to post back handler when a form is about to be submitted.

{% tab template="combobox/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the ComboBox component with dataSource
    template: `<ejs-combobox id='comboelement' [dataSource]='sportsData' [fields]=fields allowCustom=true placeholder = 'Select a game'></ejs-combobox>`
})
export class AppComponent {
    constructor() {
    }
    public fields: Object = {text: 'Game', value: 'Id'};
    // defined the array of data
    public sportsData: { [key: string]: Object }[] = [
        { Id: 'game1', Game: 'Badminton' },
        { Id: 'game2', Game: 'Football' },
        { Id: 'game3', Game: 'Tennis' }
    ];
}
```

{% endtab %}

## Configure the popup list

By default, the width of the popup list automatically adjusts according to the ComboBox input
element's width, and the height of the popup list has '300px'.

The height and width of the popup list can also be customized using the
[popupHeight](../api/combo-box/#popupheight)
 &nbsp;and [popupWidth](../api/combo-box/#popupwidth) property
respectively.

In the following sample, popup list's width and height are configured.

{% tab template="combobox/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the ComboBox component with value property
    template: `<ejs-combobox id='comboelement' #samples [dataSource]='data' placeholder='Select a game' popupHeight='200px' popupWidth='250px'></ejs-combobox>`
})
export class AppComponent {
    constructor() {
    }
    // define the array of data
    public data: string[] = ['Cricket', 'Football', 'Golf', 'Rugby', 'Snooker', 'Tennis'];
}
```

{% endtab %}

## Two-way binding

In ComboBox, the `value` property supports two-way binding functionality.
The following example demonstrates how to work the two-way binding functionality in ComboBox.

{% tab template="combobox/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the ComboBox component and
    // input element for checking the two-way binding support using value property
    template: `
    <ejs-combobox id='comboelement' [dataSource]='data' [(value)]='value' placeholder="Select a game"></ejs-combobox>
    <div style='margin-top: 50px'>
        <input type="text" [(ngModel)]="value" style='width:245px;height:25px' />
     </div>
    `
})
export class AppComponent {
    constructor() {
    }
    // defined the array of complex data
    public data: string[] = [ 'Badminton', 'Football', 'Rugby', 'Snooker', 'Tennis' ];
    // set a value to pre-select
    public value: string = 'Badminton';
}

```

{% endtab %}

## See Also

* [How to bind the data](./data-binding/)