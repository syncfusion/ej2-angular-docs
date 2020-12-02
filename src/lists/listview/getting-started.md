---
title: "ListView Getting Started"
component: "ListView"
description: "Getting started with ListView component."
---

# Getting Started

The ListView component is available in `@syncfusion/ej2-angular-lists` package. Utilize this package to render the
ListView Component.

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

## Adding Syncfusion Listview package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Listview component, use the following command.

```bash
npm install @syncfusion/ej2-angular-lists --save
```

> The **--save** will instruct NPM to include the listview package inside of the `dependencies` section of the `package.json`.

## Registering Listview Module

Import Listview module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-lists` [src/app/app.module.ts].

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import Listview component Module
import { ListviewModule } from '@syncfusion/ej2-angular-lists';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of listview module into NgModule
  imports:      [ BrowserModule, ListviewModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding CSS Reference

* Add ListView component's styles as given below in `styles.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-angular-lists/styles/material.css";
```

* If you are using `CheckList` behaviour in ListView, we need to add `Button` component's styles as given below in `styles.css` file

```css
@import "../node_modules/@syncfusion/ej2-angular-buttons/styles/material.css";
```

> We can also use [CRG](https://crg.syncfusion.com/) to generate combined component styles.

## Add Listview component

Modify the template in [src/app/app.component.ts] file to render the listview component.
Add the Angular Listview by using `<ejs-listview>` selector in `template` section of the app.component.ts file.

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-container',
  // specifies the template string for the Listview component
    template: `<ejs-listview id='sample-list' [dataSource]='data'></ejs-listview>`
})

export class AppComponent {
    public data: Object = [
    { text: 'Artwork', id: '01' },
    { text: 'Abstract', id: '02' },
    { text: 'Modern Painting', id: '03' },
    { text: 'Ceramics', id: '04' },
    { text: 'Animation Art', id: '05' },
    { text: 'Oil Painting', id: '06' }];
}

```

## Run the application

Use the following command to run the application in browser.

```javascript
ng serve --open
```

The output will appear as follows.

{% tab template="listview/getting-started", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `<ejs-listview id='sample-list' [dataSource]='data'></ejs-listview>`
})

export class AppComponent {
    public data: Object = [
    { text: 'Artwork', id: '01' },
    { text: 'Abstract', id: '02' },
    { text: 'Modern Painting', id: '03' },
    { text: 'Ceramics', id: '04' },
    { text: 'Animation Art', id: '05' },
    { text: 'Oil Painting', id: '06' }];
}

```

{% endtab %}

## See Also

[Data Binding Types](./data-binding)

[ListView customization](./customizing-templates)

[Virtualization](./virtualization)