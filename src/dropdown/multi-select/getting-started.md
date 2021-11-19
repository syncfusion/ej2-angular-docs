---
title: "Multiselect Getting started"
component: "MultiSelect"
description: "This section explains how to create a simple Syncfusion angular multiselect component and configure it's functionalities in Angular."
---

# Getting Started

This section explains how to create a simple **MultiSelect** component and configure its available
functionalities in Angular.

## Dependencies

The following list of dependencies are required to use the Angular MultiSelect component in your application.

```javascript
|-- @syncfusion/ej2-angular-dropdowns
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-dropdowns
        |-- @syncfusion/ej2-inputs
        |-- @syncfusion/ej2-lists
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
ng new syncfusion-angular-multiselect
```

By default, it install the CSS style base application. To setup with SCSS, pass --style=scss argument on create project.

Example code snippet.

```bash
ng new syncfusion-angular-multiselect --style=scss
```

Navigate to the created project folder.

```bash
cd syncfusion-angular-multiselect
```

## Adding MultiSelect package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install MultiSelect component, use the following command.

```bash
npm install @syncfusion/ej2-angular-dropdowns --save
(or)
npm i @syncfusion/ej2-angular-dropdowns --save
```

> The **--save** will instruct NPM to include the MultiSelect package inside of the [dependencies](./getting-started#dependencies) section of the `package.json`.

## Registering MultiSelect module

Import MultiSelect module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-dropdowns`.

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MultiSelectModule for the MultiSelect component
import { MultiSelectModule } from '@syncfusion/ej2-angular-dropdowns';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-dropdowns module into NgModule
  imports:      [ BrowserModule, MultiSelectModule ],
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

## Adding MultiSelect component

Modify the template in [src/app/app.component.ts] file to render the Angular MultiSelect component.
Add the Angular MultiSelect by using `<ejs-multiselect>` selector in `template` section of the app.component.ts file.

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  // specifies the template string for the MultiSelect component
  template: `<ejs-multiselect id='multiselectelement'></ejs-multiselect>`
})
export class AppComponent  { }
```

## Binding data source

After initialization, populate the MultiSelect with data using the `dataSource` property.
Here, an array of string values passed to MultiSelect component.

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='data'></ejs-multiselect>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: string[] = ['Badminton', 'Basketball', 'Cricket', 'Football', 'Golf', 'Gymnastics', 'Hockey', 'Rugby', 'Snooker', 'Tennis'];
}
```

## Running the application

After completing the configuration required to render a basic MultiSelect, run the following command to
display the output in your default browser.

```cmd
ng serve
```

The following example illustrates the output in your browser.

{% tab template="multiselect/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component with dataSource
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='data' [placeholder]='placeholder'></ejs-multiselect>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: string[] = ['Badminton', 'Cricket', 'Football', 'Golf', 'Tennis'];
    // set placeholder to MultiSelect input element
    public placeholder: string = 'Select games';
}
```

{% endtab %}

## Configure the popup list

By default, the width of the popup list automatically adjusts according to the
MultiSelect input element's width, and the height auto adjust's according to
the height of the popup list items.

The height and width of the popup list can also be customized using the
[popupHeight](../api/multi-select/#popupheight)
&nbsp;and [popupWidth](../api/multi-select/#popupwidth) properties
respectively.

In the following sample, popup list's width and height are configured.

{% tab template="multiselect/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component with dataSource
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='data' [placeholder]='placeholder' [popupHeight]='popupHeight' [popupWidth]='popupWidth'></ejs-multiselect>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: string[] = ['Badminton', 'Cricket', 'Football', 'Golf', 'Hockey', 'Rugby'];
    // set placeholder to MultiSelect input element
    public placeholder: string = 'Select games';
    //set height to popup list
    public popupHeight:string = '200px';
    //set width to popup list
    public popupWidth:string = '250px';
}

```

{% endtab %}

> You can refer to our [Angular MultiSelect](https://www.syncfusion.com/angular-ui-components/angular-multiselect-dropdown) feature tour page for its groundbreaking feature representations. You can also explore our [Angular MultiSelect example](https://ej2.syncfusion.com/angular/demos/#/material/multi-select/default) that shows how to render the MultiSelect Dropdown in Angular.