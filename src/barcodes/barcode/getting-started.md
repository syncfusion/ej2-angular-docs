---
title: "getting-started"
component: "BarcodeGenerator"
description: "BarcodeGenerator component is a pure JavaScript library which will convert a string to Barcode and show it to the user. This supports major 1D and 2D barcodes including coda bar, code 128, QR Code."
---

# Getting Started

This section explains you the steps required to create a simple barcode and demonstrate the basic usage of the barcode control.

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

## Adding Syncfusion Barcode Generator package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Barcode Generator component, use the following command.

```bash
npm install @syncfusion/ej2-angular-barcode-generator --save
```

> The **--save** will instruct NPM to include the barcode generator package inside of the `dependencies` section of the `package.json`.

## Registering Barcode Generator Module

Import Barcode Generator module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-barcode-generator` [src/app/app.module.ts].

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { BarcodeGeneratorAllModule,QRCodeGeneratorAllModule,DataMatrixGeneratorAllModule } from '@syncfusion/ej2-angular-barcode-generator';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-Barcode Generator module into NgModule
  imports:      [ BrowserModule, BarcodeGeneratorAllModule, QRCodeGeneratorAllModule ,DataMatrixGeneratorAllModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding Barcode Generator control

You can start adding Essential JS 2 barcode-generator component to the application. To get started, add the barcode component in `app.ts` and `index.html` files using the following code.

{% tab template="barcode/getting-started/initialize", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "app-container",
  // specifies the template string for the barcode generator component
  template: `<ejs-barcodegenerator style="display: block;"  #barcode id="barcode" width="200px" height="150px" mode="SVG" type="Codabar" value="123456789">`
})
export class AppComponent {}
```

{% endtab %}

## Adding QR Generator control

You can add the QR code in our barcode generator component.

{% tab template="barcode/getting-started/qrcode", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "app-container",
  // specifies the template string for the barcode generator component
  template: `<ejs-qrcodegenerator style="display: block;"  #barcode id="barcode" width="200px" height="150px" mode="SVG"value="Syncfusion"></ejs-qrcodegenerator>`
})
export class AppComponent {}
```

{% endtab %}

## Adding Datamatrix Generator control

You can add the datamatrix code in our barcode generator component.

{% tab template="barcode/getting-started/datamatrix", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "app-container",
  // specifies the template string for the barcode generator component
  template: `<ejs-datamatrixgenerator style="display: block;"  #barcode id="barcode" width="200px" height="200px" mode="SVG"
                        type="DataMatrix" value="Syncfusion">
                    </ejs-datamatrixgenerator>`
})
export class AppComponent {}
```

{% endtab %}