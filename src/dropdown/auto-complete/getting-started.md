---
title: "Autocomplete Getting started"
component: "AutoComplete"
description: "This section explains how to create a simple Syncfusion angular autocomplete component and configure it's functionalities in angular."
---

# Getting started

This section explains how to create a simple **AutoComplete** component and configure its
available functionalities in Angular.

## Dependencies

The following list of dependencies are required to use the AutoComplete component in your application.

```javascript
|-- @syncfusion/ej2-angular-dropdowns
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-lists
    |-- @syncfusion/ej2-inputs
    |-- @syncfusion/ej2-navigations
    |-- @syncfusion/ej2-popups
        |-- @syncfusion/ej2-buttons
    |-- @syncfusion/ej2-angular-base
```

## Setup angular environment

Angular provides the easiest way to set angular CLI projects using [`Angular CLI`](https://github.com/angular/angular-cli) tool.

Install the CLI application globally to your machine.

```bash
npm install -g @angular/cli
```

## Create a new application

```bash
ng new syncfusion-angular-autocomplete
```

By default, it install the CSS style base application. To setup with SCSS, pass --style=scss argument on create project.

Example code snippet.

```bash
ng new syncfusion-angular-autocomplete --style=scss
```

Navigate to the created project folder.

```bash
cd syncfusion-angular-autocomplete
```

## Adding AutoComplete package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install AutoComplete component, use the following command.

```bash
npm install @syncfusion/ej2-angular-dropdowns --save
(or)
npm i @syncfusion/ej2-angular-dropdowns --save
```

> The **--save** will instruct NPM to include the AutoComplete package inside of the [dependencies](./getting-started#dependencies) section of the `package.json`.

## Registering AutoComplete module

Import AutoComplete module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-dropdowns` [src/app/app.module.ts].

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the AutoCompleteModule for the AutoComplete component
import { AutoCompleteModule } from '@syncfusion/ej2-angular-dropdowns';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-dropdowns module into NgModule
  imports:      [ BrowserModule, AutoCompleteModule ],
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

## Adding AutoComplete component

Modify the template in [src/app/app.component.ts] file to render the AutoComplete component.
Add the Angular Autocomplete by using `<ejs-autocomplete>` selector in `template` section of the app.component.ts file.

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  // specifies the template string for the AutoComplete component
  template: `<ejs-autocomplete id='atcelement'></ejs-autocomplete>`
})
export class AppComponent  { }
```

## Binding data source

After initializing, populate the data in AutoComplete using [`dataSource`](../api/auto-complete/#datasource) property.
Here, an array of string values is passed to the AutoComplete component.

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component
    template: `<ejs-autocomplete id='atcelement' [dataSource]='sportsData'></ejs-autocomplete>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public sportsData: string[] = ['Badminton', 'Basketball', 'Cricket', 'Football', 'Golf', 'Gymnastics', 'Hockey', 'Rugby', 'Snooker', 'Tennis'];
}

```

## Running the application

After completing the configuration required to render a basic AutoComplete, run the following command to
display the output in your default browser.

```cmd
ng serve
```

The following example illustrates the output in your browser.

{% tab template="autocomplete/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component with dataSource
    template: `<ejs-autocomplete id='atcelement' [dataSource]='sportsData'></ejs-autocomplete>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public sportsData: string[] = ['Badminton', 'Basketball', 'Cricket', 'Football', 'Golf', 'Gymnastics'];
}
```

{% endtab %}

## Configure the popup list

By default, the width of the popup list automatically adjusts according to the DropDownList input element's
width, and the height of the popup list has '300px'.

The height and width of the popup list can also be customized using the
[popupHeight](../api/auto-complete/#popupheight)
&nbsp;and [popupWidth](../api/auto-complete/#popupwidth) properties
respectively.

In the following sample, popup list's width and height are configured.

{% tab template="autocomplete/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component with dataSource
    template: `<ejs-autocomplete id='atcelement' [dataSource]='sportsData' [popupHeight]='height' [popupWidth]='width' [placeholder]='text'></ejs-autocomplete>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public sportsData: string[] = ['Badminton', 'Cricket', 'Football', 'Golf', 'Hockey', 'Rugby', 'Snooker', 'Tennis'];
    // set width of the popup list
    public width: string = '250px';
    // set height of the popup list
    public height: string = '200px';
    // set placeholder to autocomplete element
    public text: string = "Find a game"
}
```

{% endtab %}

## Two-way binding

In AutoComplete, the `value` property supports two-way binding functionality.
The following example demonstrates how to work with the two-way binding functionality in AutoComplete.

{% tab template="autocomplete/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component and
    // input element for checking the two-way binding support using value property
    template: `<ejs-autocomplete id='atcelement' [dataSource]='sportsData' [(value)]='value'></ejs-autocomplete>
    <div style='margin-top: 50px'>
        <input type="text" [(ngModel)]="value" style="width:245px;height:25px" />
     </div>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of complex data
    public sportsData: string[] = ['Badminton', 'Basketball', 'Cricket', 'Football', 'Golf', 'Gymnastics'];
    // set a value to pre-select
    public value: string = 'Badminton';
}
```

{% endtab %}

## See Also

* [How to bind the data](./data-binding/)
