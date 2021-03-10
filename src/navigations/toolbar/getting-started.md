---
title: "Toolbar Getting Started"
component: "Toolbar"
description: "This section explains how to create the Toolbar control in an Angular application with its basic features."
---

# Getting Started

This section explains briefly about how to create a simple **Toolbar** using Angular and
configuring the Toolbar items like button, separator and input components.

## Dependencies

Install the below required dependency package in order to use the `Toolbar` component in your application.

```javascript
|-- @syncfusion/ej2-angular-navigations
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-navigations
        |-- @syncfusion/ej2-buttons
        |-- @syncfusion/ej2-popups
```

## Setup Angular Environment

You can use [`Angular CLI`](https://github.com/angular/angular-cli) to setup your Angular applications.
To install Angular CLI use the following command.

```bash
npm install -g @angular/cli
```

## Create an Angular Application

Start a new Angular application using below Angular CLI command.

```bash
ng new my-app
cd my-app
```

## Adding Syncfusion Toolbar package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Toolbar component, use the following command.

```bash
npm install @syncfusion/ej2-angular-navigations --save
```

> The **--save** will instruct NPM to include the Toolbar package inside of the **dependencies** section of the **package.json**.

## Registering Toolbar Module

Import Toolbar module into Angular application(app.module.ts) from the package **@syncfusion/ej2-angular-navigations** [src/app/app.module.ts].

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the ToolbarModule for the Toolbar component
import { ToolbarModule } from '@syncfusion/ej2-angular-navigations';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-navigations module into NgModule
  imports:      [ BrowserModule, ToolbarModule ],
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
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';

```

## Add Toolbar component

Modify the template in [src/app/app.component.ts] file to render the toolbar component.
Add the Angular Toolbar by using `<ejs-toolbar>` selector in **template** section of the app.component.ts file.

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-root',
  // specifies the template string for the Toolbar component
  template: `<ejs-toolbar>
          <e-items>
             <e-item text='Cut'></e-item>
             <e-item text='Copy'></e-item>
             <e-item text='Paste'></e-item>
             <e-item type='Separator'></e-item>
             <e-item text='Bold'></e-item>
             <e-item text='Italic'></e-item>
             <e-item text='Underline'></e-item>
          </e-items>
        </ejs-toolbar>`
})
export class AppComponent {

}

```

* Now, run the application in the browser using the following command.

```shell
npm start
```

The following code example depicts the way to initialize The Toolbar on a single element.

{% tab template="toolbar/toolbar", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { ToolbarComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-container',
    template: `
        <ejs-toolbar>
          <e-items>
             <e-item text='Cut'></e-item>
             <e-item text='Copy'></e-item>
             <e-item text='Paste'></e-item>
             <e-item type='Separator'></e-item>
             <e-item text='Bold'></e-item>
             <e-item text='Italic'></e-item>
             <e-item text='Underline'></e-item>
          </e-items>
        </ejs-toolbar>
        `
})

export class AppComponent {

}
```

{% endtab %}

## Initialize the Toolbar using HTML elements

The Toolbar component can be rendered based on the given HTML element using `<ejs-toolbar>`.
You need to follow the below structure of HTML elements to render the Toolbar inside the `<ejs-toolbar>` tag.

```html
   <ejs-toolbar>   --> Root Toolbar Element
    <div>      --> Toolbar Items Container
       <div>   --> Toolbar Item Element
       </div>
    </div>
  </ejs-toolbar>
```

{% tab template="toolbar/toolbar-container", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ToolbarComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-container',
    template: `
        <ejs-toolbar>
          <div>
                <div><button class='e-btn e-tbar-btn'>Cut</button> </div>
                <div><button class='e-btn e-tbar-btn'>Copy</button> </div>
                <div><button class='e-btn e-tbar-btn'>Paste</button> </div>
                <div class='e-separator'> </div>
                <div><button class='e-btn e-tbar-btn'>Bold</button> </div>
                <div><button class='e-btn e-tbar-btn'>Italic</button> </div>
          </div>
        </ejs-toolbar>
        `
})

export class AppComponent {

}
```

{% endtab %}

## See Also

* [How to add Toggle Button](./how-to/add-toggle-button/)