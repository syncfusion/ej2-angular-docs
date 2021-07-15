---
title: "Getting Started"
component: "Uploader"
description: "Explains to get started with HTML5 file upload control with its key features such as asynchronous mode, handle success, fail action, etc."
---

# Getting Started

This section explains how to create and configure the **uploader** component in Angular. The uploader component is available in @syncfusion/ej2-angular-inputs package. Utilize this package to render the uploader Component.

## Dependencies

The following packages are required to render the uploader component in your Angular application.

```js
|-- @syncfusion/ej2-angular-inputs
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-angular-popups
    |-- @syncfusion/ej2-angular-buttons
    |-- @syncfusion/ej2-inputs
        |-- @syncfusion/ej2-base
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
ng new syncfusion-angular-uploader
```

By default, it install the CSS style base application. To setup with SCSS, pass --style=scss argument on create project.

Example code snippet.

```bash
ng new syncfusion-angular-uploader --style=scss
```

Navigate to the created project folder.

```bash
cd syncfusion-angular-uploader
```

## Adding Uploader package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install uploader component, use the following command.

```bash
npm install @syncfusion/ej2-angular-inputs --save
(or)
npm i @syncfusion/ej2-angular-inputs --save
```

> The **--save** will instruct NPM to include the uploader package inside of the [dependencies](./getting-started#dependencies) section of the `package.json`.

## Initialize Uploader

The below couple of steps describes to initialize the uploader component in Angular application.

* Import `UploaderModule` from `@syncfusion/ej2-angular-inputs` package, inject into `imports` section of `NgModule` in the module file `src/app/app.module.ts` to use the `Uploader` component across the application.

```typescript

import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent }  from './app.component';
import { UploaderModule  } from '@syncfusion/ej2-angular-inputs';
@NgModule({
  imports:      [ BrowserModule , UploaderModule],
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
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-angular-inputs/styles/material.css';
```

> The [Custom Resource Generator (CRG)](https://crg.syncfusion.com/) is an online web tool, which can be used to generate the custom script and styles for a set of specific components.
> This web tool is useful to combine the required component scripts and styles in a single file.

## Adding Uploader component

Modify the template in [src/app/app.component.ts] file to render the Uploader component.
Add the Angular Uploader by using `<ejs-uploader>` selector in `template` section of the app.component.ts file.

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
               <ejs-uploader #defaultupload  [autoUpload]='false'></ejs-uploader>
              `
})
export class AppComponent {
    constructor() {
    }
}

```

## Running the application

After completing the configuration required to render the uploader, run the application using the following command to display the output in your default browser.

```cmd
ng serve
```

> From v16.2.41 version, the `Essential JS2 AJAX` library has been integrated for uploader server requests.
Hence, use the third party `promise` library like blue-bird to use the uploader in Internet Explorer.

The below example shows a uploader component.

{% tab template="uploader/uploader", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
               <ejs-uploader #defaultupload  [autoUpload]='false'></ejs-uploader>
              `
})
export class AppComponent {
    constructor() {
    }
}

```

{% endtab %}

## Adding drop area

By default, the uploader component allows to upload files by drag the files from file explorer, and drop into the drop area.
You can configure any other external element as drop target using `dropArea` property.

In the following sample, external element is configured as drop target to uploader component.

{% tab template="uploader/draganddrop", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
               <div id='droparea'>
            Drop files here to upload
        </div>
        <div id='uploadfile' >
               <ejs-uploader #defaultupload  [autoUpload]='false' [dropArea]='dropEle'></ejs-uploader>
               </div>
              `
})
export class AppComponent {
    public dropEle: HTMLElement ;
    ngOnInit() {
          this.dropEle = document.getElementById('droparea');
    }
    constructor() {
    }
}

```

{% endtab %}

## Configure asynchronous settings

By default, the uploader component process the files in Asynchronous mode.
Define the properties `saveUrl` and `removeUrl` to handle the save and remove action as follows.

{% tab template="uploader/uploader", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
               <div id='droparea'>
            Drop files here to upload
        </div>
        <div id='uploadfile' >
               <ejs-uploader #defaultupload  [autoUpload]='false' [dropArea]='dropEle' [asyncSettings]='path'></ejs-uploader>
               </div>
              `
})
export class AppComponent {
     public path: Object = {
      saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
      removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove' };
    constructor() {
    }
}

```

{% endtab %}

## Handle success and failed upload

You can handle the success and failure actions using the `success` and `failure` events.
To handle these events, define the function and assign it to corresponding event as follows.

{% tab template="uploader/uploader", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
               <ejs-uploader #defaultupload [autoUpload]='false' [dropArea]='dropEle' [asyncSettings]='path' (success)="onUploadSuccess($event)" (failure)="onUploadFailure($event)"></ejs-uploader>
              `
})
export class AppComponent {
public path: Object = {
      saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
      removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove' };
      public onUploadSuccess(args: any): void  {
        if (args.operation === 'upload') {
            console.log('File uploaded successfully');
        }
    }

    public onUploadFailure(args: any): void  {
    console.log('File failed to upload');
    }

    public dropEle: HTMLElement ;
    ngOnInit() {
          this.dropEle = document.getElementById('droparea');
    }

    constructor() {
    }
}

```

{% endtab %}

> You can also explore [Angular File Upload](https://www.syncfusion.com/angular-ui-components/angular-file-upload) feature tour page for its groundbreaking features. You can also explore our [Angular File Upload example](https://ej2.syncfusion.com/angular/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.

## See Also

* [How to add additional data on upload](./how-to/add-additional-data-on-upload)
* [Achieve file upload programmatically](./how-to/achieve-file-upload-programmatically)
* [Achieve invisible upload](./how-to/achieve-invisible-upload)
