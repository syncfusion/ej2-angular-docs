---
title: "Angular Toast Getting Started"
component: "Toast"
description: "This section explains how to create the Essential JS2 Toast component in Angular application with its basic features."
---

# Getting started

This section briefly explains about how to create a simple **Toast** and configure its available functionalities in Angular
using Angular quickstart.

## Getting Started with Angular CLI

The following section explains the steps required to create a simple `angular-cli` application and how to configure `Toast` component.

### Prerequisites

To get started with Syncfusion Angular UI Components, make sure that you have compatible versions of Angular and TypeScript.

* Angular : 4+
* TypeScript : 2.6+

### Setting up an Angular project

Angular provides an easiest way to setup project using Angular CLI [Angular CLI](https://github.com/angular/angular-cli) tool.

Install the CLI application globally in your machine.

```javascript

  npm install -g @angular/cli

```

### Create a new application

```javascript

  ng new syncfusion-angular-app

```

Once you have executed the above command you may ask for following options,
* Would you like to add Angular routing?
* Which stylesheet format would you like to use?

By default it install the CSS style base application. To setup with SCSS, pass --style=SCSS argument on create project.

Example code snippet.

```javascript

  ng new syncfusion-angular-app --style=SCSS

```

Navigate to the created project folder.

```javascript

  cd syncfusion-angular-app

```

## Install Syncfusion notifications package

Syncfusion packages are distributed in npm as `@syncfusion` scoped packages. You can get all the angular syncfusion package from npm [link](https://www.npmjs.com/search?q=%40syncfusion%2Fej2-angular-).

Add Syncfusion Angular notifications package in your application by using following Command,

```javascript

npm install @syncfusion/ej2-angular-notifications --save
(or)
npm i @syncfusion/ej2-angular-notifications --save

```

## Adding Toast module

After installing the package, the component modules are ready to configure in your application from installed syncfusion package. Syncfusion Angular package provides two different types of ngModules.

Refer to [Ng-Module](https://ej2.syncfusion.com/angular/documentation/common/ng-module/) to learn about `ngModules`.

Refer the following snippet to import the `ToastModule` in `app.module.ts` from the `@syncfusion/ej2-angular-notifications`.

```javascript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
// Imported syncfusion ToastModule from ej2-angular-notifications package
import { ToastModule } from '@syncfusion/ej2-angular-notifications';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    // Registering EJ2 Toast Module
    ToastModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

```

## Adding Toast component

Add the Toast component snippet in `app.component.ts` as follows.

```typescript

import { Component, ViewChild } from '@angular/core';
import { ToastComponent } from '@syncfusion/ej2-angular-notifications';

@Component({
  selector: 'app-root',
  template: `<ejs-toast #element (created)="onCreate($event)">
    <ng-template #title>
      <div>Sample Toast Title</div>
    </ng-template>
    <ng-template #content>
      <div>Sample Toast Content</div>
    </ng-template>
    </ejs-toast>`
})

export class AppComponent {
  @ViewChild('element') element: ToastComponent;

    onCreate() {
    this.element.show();
  }

  constructor() {
  }
}

```

## Adding CSS reference

The following CSS files are available in `../node_modules/@syncfusion` package folder. This can be referenced in [src/styles.css] using following code.

```css

      @import '../node_modules/@syncfusion/ej2-base/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-angular-notifications/styles/material.css';


```

> The [Custom Resource Generator (CRG)](https://crg.syncfusion.com/) is an online web tool, which can be used to generate the custom script and styles for a set of specific components.
> This web tool is useful to combine the required component scripts and styles in a single file.

## Initialize the Toast with message

The Toast message can be rendered by defining an `title` or `content`.

## Running the application

Run the `ng serve` command in command window, it will serve your application and you can open the browser window. Output will appear as follows.

{% tab template="toast/toast", isDefaultActive=true, sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
       <button ejs-button [isPrimary]="true" (click)="btnClick($event)">Show Toast</button>
        <ejs-toast #element (created)="onCreate($event)" [position]='position'>
              <ng-template #title>
                  <div>Matt sent you a friend request</div>
              </ng-template>
              <ng-template #content>
                  <div>Hey, wanna dress up as wizards and ride our hoverboards?</div>
              </ng-template>
    </ejs-toast>`
})

export class AppComponent {
  @ViewChild('element') element;
  public position = { X: 'Right' };

  onCreate() {
    this.element.show();
  }

  btnClick() {
    this.element.show();
  }
}

```

{% endtab %}

## See Also

* [Render different types of toast](./how-to/show-different-types-of-toast/)
