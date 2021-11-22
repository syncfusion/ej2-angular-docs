# Getting Started with Angular CLI

Refer to the following steps to use for Syncfusion Angular UI Components (Essential JS 2).

## Prerequisites

To get started with Syncfusion Angular UI Components, ensure the compatible versions of Angular and Typescript.

* `Angular` : 6+
* `Typescript` : 2.6+

## Getting started with Angular CLI

### Setting up an angular project

Angular provides the easiest way to set angular CLI projects using [`Angular CLI`](https://github.com/angular/angular-cli) tool.

Install the CLI application globally to your machine.

```bash
npm install -g @angular/cli
```

## Create a new application

```bash
ng new syncfusion-angular-app
```

By default, it installs the CSS style base application. To setup with SCSS, pass --style=SCSS argument on create project.

Example code snippet.

```bash
ng new syncfusion-angular-app --style=scss
```

Navigate to the created project folder.

```bash
cd syncfusion-angular-app
```

## Installing Syncfusion button package

Syncfusion packages are distributed in npm as `@syncfusion` scoped packages. You can get all the angular syncfusion package from npm [link]( https://www.npmjs.com/search?q=%40syncfusion%2Fej2-angular- ).

Add `@syncfusion/ej2-angular-buttons` package to the application.

```bash
npm install @syncfusion/ej2-angular-buttons --save
(or)
npm i @syncfusion/ej2-angular-buttons --save
```

## Installing Syncfusion button package with Custom Tagname

You can also change the tag name of Syncfusion Angular UI Controls. 

Run the below command to add `@syncfusion/ej2-angular-buttons` package to the application with the desired tag name `custom`.

```bash
SET tagName=custom && npm install @syncfusion/ej2-angular-buttons
```
After executing the above command, the Syncfusion Angular UI component selector will be changed. For example, the tag name of `<ejs-buttons>` will be changed into `<custom-buttons>`.

## Adding button module

After installing the package, the component modules are available to configure into your application from the installed syncfusion package. Syncfusion Angular package provides two different types of `ngModules`.

Refer to [`Ng-Module`](https://ej2.syncfusion.com/angular/documentation/common/ng-module.html) to learn about `ngModules`.

Refer to the following snippet to import the button module in `app.module.ts` from the `@syncfusion/ej2-angular-buttons`.

```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';

import { AppComponent } from './app.component';

// Imported syncfusion button module from buttons package
import { ButtonModule } from '@syncfusion/ej2-angular-buttons';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule,

    // Registering EJ2 Button Module
    ButtonModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

## Adding Syncfusion component

Add the button component snippet in `app.component.ts` as follows.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
<h1>
    Hello Angular, Syncfusion Angular UI Button!
 </h1>

 <button ejs-button cssClass=”e-primary”>Button</button>
 `
 })
export class AppComponent {
}
```

## Adding CSS reference

Add button component styles in the `src/style.css` file as below.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
```
## Adding SCSS reference

To avoid SCSS compilation issues and to map the SCSS file path, add the stylePreprocessorOptions to the .angular-cli.json file.

Add the `stylePreprocessorOptions` option under apps in the `angular.json` file.

The following paths can be used globally in Angular app.

```typescript
"stylePreprocessorOptions": {
         "includePaths": [
         "node_modules/@syncfusion"
        ]
  },
```
Add button component styles in the `src/style.scss` file as below.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.scss";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.scss";
```

## Running the application

Run the `ng serve` command in the console, it will serve your application and you can open the browser window. The Output will appear as follows.

![output](images/angular-cli-output.png)

Refer the below sample for more information.

{% tab template="common/quickstart", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { enableRipple } from '@syncfusion/ej2-base';
import { Component } from '@angular/core';

// enable ripple effects
enableRipple(true);

@Component({
  selector: 'app-root',
  template: `
  <h1>
    Syncfusion Angular UI Button!
  </h1>

  <button ejs-button>Button</button>
  `
})
export class AppComponent {

}

```

{% endtab %}