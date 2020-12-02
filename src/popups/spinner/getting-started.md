---
title: "Getting Started"
component: "Spinner"
description: "This example demonstrates how to create the Essential JS 2 Spinner control with its basic features in Angular application."
---

# Getting Started

This section explains the steps to create a simple **Spinner** and configure its functionalities in Angular.

## Getting Started with Angular CLI

The following section explains the steps required to create a simple angular-cli application and how to configure the `Spinner'.

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

By default, it install the CSS style base application. To setup with SCSS, pass --style=SCSS argument on create project.

Example code snippet.

```javascript

  ng new syncfusion-angular-app --style=SCSS

```

Use below command to Navigate into the created project folder.

```javascript

  cd syncfusion-angular-app

```

## Install Syncfusion Popups package

Add Syncfusion Angular popups package in your application by using following Command,

```javascript

npm install @syncfusion/ej2-angular-popups --save
(or)
npm i @syncfusion/ej2-angular-popups --save

```

## Adding CSS reference

The following CSS files can be referenced in [src/styles.css] file.

```css

       @import '../node_modules/@syncfusion/ej2-angular-popups/styles/material.css';

```

> The [Custom Resource Generator (CRG)](https://crg.syncfusion.com/) is an online web tool, which can be used to generate the custom script and styles for a set of specific components.
> This web tool is useful to combine the required component scripts and styles in a single file.

## Adding Spinner

Initialize the Spinner using "createSpinner" method and show/hide the spinner using "showSpinner" and "hideSpinner" methods accordingly. Set the target to the spinner to render it based on specific target.

The following steps explains you on how to create and how to show/hide your Spinner.

* Import the "createSpinner" method from "ej2-popups" library into your file as shown in below.

```typescript
import { createSpinner } from '@syncfusion/ej2-angular-popups';
```

* Show and hide this spinner by using "showSpinner" and "hideSpinner" methods for loading in your page and import them in your file as shown in below.

```typescript
import { showSpinner, hideSpinner } from '@syncfusion/ej2-popups';
```

## Create the Spinner globally

The Spinner can be render globally in a page using public exported functions of the "ej2-popups" package.

```typescript
import { showSpinner, hideSpinner } from '@syncfusion/ej2-angular-popups';
```

{% tab template="spinner/intro", isDefaultActive = "true", sourceFiles="app/**/*.ts,index.css"  %}

```typescript

import { Component } from '@angular/core';
import { createSpinner, showSpinner, hideSpinner } from '@syncfusion/ej2-angular-popups';

@Component({
  selector: 'app-container',
  template: `<div id="container"></div>`
})
export class AppComponent {
  constructor() {}

  ngAfterViewInit() {
    //createSpinner() method is used to create spinner
    createSpinner({
      // Specify the target for the spinner to show
      target: document.getElementById('container')
    });

    // showSpinner() will make the spinner visible
    showSpinner(document.getElementById('container'));

    setInterval(function(){
      // hideSpinner() method used hide spinner
      hideSpinner(document.getElementById('container'));
    }, 100000);
  }
}

```

{% endtab %}