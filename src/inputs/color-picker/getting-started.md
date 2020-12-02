# Getting Started

This section explains how to create a default ColorPicker and demonstrate the basic usage of the ColorPicker module.

## Dependencies

The list of dependencies required to use the ColorPicker module in your application is given below:

```javascript
|-- @syncfusion/ej2-angular-inputs
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-inputs
    |-- @syncfusion/ej2-buttons
    |-- @syncfusion/ej2-popups
    |-- @syncfusion/ej2-splitbuttons
```

## Setup Angular environment

You can use [Angular CLI](https://github.com/angular/angular-cli) to setup your Angular applications. To install Angular CLI use the following command.

```cmd
npm install -g @angular/cli
```

## Create an Angular application

Start a new Angular application using below Angular CLI command.

```cmd
ng new my-app
cd my-app
```

## Installing Syncfusion ColorPicker package

To install ColorPicker package, use the following command.

```cmd
npm install @syncfusion/ej2-angular-inputs --save
```

## Adding ColorPicker module

Import ColorPicker module into Angular application(app.module.ts) from the package
`@syncfusion/ej2-angular-inputs`.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

// Importing Colorpicker module from Syncfusion ej2-angular-inputs package.
import { ColorPickerModule } from '@syncfusion/ej2-angular-inputs';

import { AppComponent }  from './app.component';

@NgModule({
  imports:      [ BrowserModule, ColorPickerModule ], // Declaration of ColorPickerModule into NgModule.
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding Syncfusion ColorPicker component

Modify the template in `app.component.ts` file to render the ColorPicker component.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<!-- To render ColorPicker. -->
             <input ejs-colorpicker type="color" id="colorpicker" />`
})
export class AppComponent  { }
```

## Adding CSS reference

Add ColorPicker component's styles as given below in `style.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
@import "../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
```

## Running the application

Run the application in the browser using the following command:

```cmd
ng serve
```

The following example shows a default ColorPicker component.

{% tab template="colorpicker/getting-started/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<h4>Choose Color</h4>
               <!-- To render ColorPicker. -->
               <input ejs-colorpicker type="color" id="colorpicker" />`
})

export class AppComponent { }
```

{% endtab %}

## Inline type

By default, the ColorPicker will be rendered using SplitButton and open the pop-up to access the ColorPicker. To
render the ColorPicker container alone and to access it directly, render it as inline. It can be achieved by setting the [`inline`](../api/color-picker#inline) property to `true`.

The following sample shows the inline type rendering of ColorPicker.

{% tab template="colorpicker/getting-started/inline", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<h4>Choose Color</h4>
               <!-- To render inline ColorPicker. -->
               <input ejs-colorpicker type="color" id="colorpicker" [inline]="true" [showButtons]="false" />`
})

export class AppComponent { }
```

{% endtab %}

>> The `showButtons` property is disabled in this sample because the control buttons are not needed for inline type. To know about the control buttons functionality, refer to the [`showButtons`](./how-to/hide-control-buttons) sample.
