# Getting started

This section explains you the steps required to create a simple `Chip` and demonstrate the basic usage of the Chip component in an Angular environment.

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

## Adding Syncfusion Button package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install `Chip` component, use the following command.

```bash
npm install @syncfusion/ej2-angular-buttons --save
```

> The **--save** will instruct NPM to include the button package inside of the `dependencies` section of the `package.json`.

## Registering ChipList Module

Import `ChipList` module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-buttons` [src/app/app.module.ts].

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the ChipListModule for the Chip component
import { ChipListModule } from '@syncfusion/ej2-angular-buttons';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-buttons module into NgModule
  imports:      [ BrowserModule, ChipListModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding CSS reference

Add `Chip` component CSS using the following code in [`src/styles.css`].

```css
@import "../node_modules/@syncfusion/ej2-angular-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-angular-buttons/styles/material.css";
```

## Add Chip

Modify the template in [src/app/app.component.ts] file to render the `Chip` component. Add the Angular `Chip` by using `<e-chip>` child selector with text attribute inside of `ChipList` component selector `<ejs-chiplist>` in `template` section of the `app.component.ts` file.

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'my-app',
  // specifies the template string for the Chip component
  template: `<ejs-chiplist text="Janet Leverling"></ejs-chiplist>`
})
export class AppComponent {

}

```

Now, the basic `chip` is included in Angular CLI application.

## Run the application

Use the following command to run the application in browser.

```javascript
ng serve --open
```

The output will appear as follows.

{% tab template="chips/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `<ejs-chiplist text="Janet Leverling"></ejs-chiplist>`
})
export class AppComponent {

}

```

{% endtab %}
