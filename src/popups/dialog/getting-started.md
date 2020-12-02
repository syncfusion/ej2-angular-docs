---
title: "Angular Dialog Getting Started"
component: "Dialog"
description: "Helps to get started with the dialog component along with its key features such as modal dialog, positioning and draggable."
---

# Getting started

This section explains the steps to create a simple **Dialog** component and configure its available functionalities in Angular.

## Getting Started with Angular CLI

The following section explains the steps required to create a simple angular-cli application and how to configure `Dialog` component.

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

Syncfusion packages are distributed in npm as `@syncfusion` scoped packages. You can get all the angular Syncfusion package from npm [link](https://www.npmjs.com/search?q=%40syncfusion%2Fej2-angular-).

Add Syncfusion Angular popups package in your application by using following Command,

```javascript

npm install @syncfusion/ej2-angular-popups --save
(or)
npm i @syncfusion/ej2-angular-popups --save

```

## Adding Dialog module

Once you have successfully installed the popups package, the component modules are ready to configure in your application from the installed location. Syncfusion Angular package provides two different types of ngModules.

Refer to [Ng-Module](https://ej2.syncfusion.com/angular/documentation/common/ng-module/) to learn about `ngModules`.

Refer to the following snippet to import the `DialogModule` in `app.module.ts` from the `@syncfusion/ej2-angular-popups`.

```javascript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
// Imported syncfusion DialogModule from popups package
import { DialogModule } from '@syncfusion/ej2-angular-popups';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    // Registering EJ2 Dialog Module
    DialogModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

```

## Adding Dialog component

Add the Dialog component snippet in `app.component.ts` as follows.

```javascript

import { Component, ViewChild, OnInit, ElementRef  } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
  selector: 'app-root',
  template: `
  <button class="e-control e-btn" style="position: absolute;" id="targetButton" (click)="onOpenDialog($event)">Open Dialog</button>
  <div #container class='root-container'></div>
  <ejs-dialog id='dialog' #ejDialog content='This is a Dialog with content' [target]='targetElement' width='250px'>
  </ejs-dialog>`
})
export class AppComponent implements OnInit {
  @ViewChild('ejDialog') ejDialog: DialogComponent;
  // Create element reference for dialog target element.
  @ViewChild('container', { read: ElementRef }) container: ElementRef;
  // The Dialog shows within the target element.
  public targetElement: HTMLElement;

  // To get all element of the dialog component after component get initialized.
  ngOnInit() {
    this.initilaizeTarget();
  }

  // Initialize the Dialog component target element.
  public initilaizeTarget: EmitType<object> = () => {
    this.targetElement = this.container.nativeElement.parentElement;
  }
  // Sample level code to handle the button click action
  public onOpenDialog = function(event: any): void {
      // Call the show method to open the Dialog
      this.ejDialog.show();
  };
}

```

Add following styles in corresponding css file. The below mentioned styles are used in styles.css file,

```css

html,
body,
#dialog-container {
    display: block;
    height: 100%;
    margin: 0;
    overflow: hidden;
    width: 100%;
}

```

> Note: Please do the necessary change in `index.html` file. In this demo we used id selector in `<app-root id='dialog-container'></app-root>`

## Adding CSS reference

The following CSS files are available in `../node_modules/@syncfusion` package folder. This can be referenced in [src/styles.css] using following code.

```css

       @import '../node_modules/@syncfusion/ej2-base/styles/material.css';
       @import '../node_modules/@syncfusion/ej2-icons/styles/material.css';
       @import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
       @import '../node_modules/@syncfusion/ej2-angular-popups/styles/material.css';

```

> The [Custom Resource Generator (CRG)](https://crg.syncfusion.com/) is an online web tool, which can be used to generate the custom script and styles for a set of specific components.
> This web tool is useful to combine the required component scripts and styles in a single file.

## Running the application

Run the `ng serve` command in command window, it will serve your application and you can open the browser window. Output will appear as follows.

{% tab template="dialog/getting-started",isDefaultActive = "true",sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript
import { Component, ViewChild, OnInit, ElementRef } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `
    <button class="e-control e-btn" style="position: absolute;" id="targetButton" (click)="onOpenDialog($event)">Open Dialog</button>
    <div #container class='root-container'></div>
      <ejs-dialog id='dialog' #ejDialog content='This is a Dialog with content' [target]='targetElement' width='250px'>
      </ejs-dialog>
        `
})

export class AppComponent implements OnInit {
  @ViewChild('ejDialog') ejDialog: DialogComponent;
  // Create element reference for dialog target element.
  @ViewChild('container', { read: ElementRef }) container: ElementRef;
  // The Dialog shows within the target element.
  public targetElement: HTMLElement;

  // To get all element of the dialog component after component get initialized.
  ngOnInit() {
    this.initilaizeTarget();
  }

  // Initialize the Dialog component target element.
  public initilaizeTarget: EmitType<object> = () => {
    this.targetElement = this.container.nativeElement.parentElement;
  }
  // Sample level code to handle the button click action
  public onOpenDialog = function(event: any): void {
      // Call the show method to open the Dialog
      this.ejDialog.show();
  };
}
```

{% endtab %}

> In the dialog control, max-height is calculated based on the dialog target element height. If the target property is not configured, the document.body is considered as a target. Therefore, to show a dialog in proper height, you need to add min-height to the target element.
If the dialog is rendered based on the body, then the dialog will get the height based on its body element height. If the height of the dialog is larger than the body height, then the dialog's height will not be set. For this scenario, we can set the CSS style for the html and body to get the dialog height.

```css

html, body {
   height: 100%;
}

```

## Modal Dialog

A [modal](../api/dialog/#ismodal) shows an overlay behind the Dialog. So, the user
should interact the Dialog compulsory before interacting with the remaining content in an
application.

While the user clicks the overlay, the action can be handled through the
[`overlayClick`](../api/dialog/#overlayclick) event. In the below sample the
Dialog close action is performed while clicking on the overlay.

> When the modal Dialog is opened, the Dialog's target scrolling will be disabled. The scrolling
will be enabled again once close the Dialog.

{% tab template="dialog/getting-started", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild, OnInit, ElementRef } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `
    <button class="e-control e-btn" style="position: absolute;" id="targetButton" (click)="onOpenDialog($event)">Open Modal Dialog</button>
    <div #container class='root-container'></div>
    <ejs-dialog id='dialog' #ejDialog isModal='true' (overlayClick)="onOverlayClick()"
    content='This is a modal dialog' [target]='targetElement' width='250px'> </ejs-dialog>`
})

export class AppComponent implements OnInit {
  @ViewChild('ejDialog') ejDialog: DialogComponent;
  // The Dialog shows within the target element.
  @ViewChild('container', { read: ElementRef }) container: ElementRef;
  // The Dialog shows within the target element.
  public targetElement: HTMLElement;

  // To get all element of the dialog component after component get initialized.
  ngOnInit() {
    this.initilaizeTarget();
  }

  // Initialize the Dialog component target element.
  public initilaizeTarget: EmitType<object> = () => {
    this.targetElement = this.container.nativeElement.parentElement;
  }
  // Sample level code to handle the button click action
  public onOpenDialog = function(event: any): void {
      // Call the show method to open the Dialog
      this.ejDialog.show();
  };
  // Sample level code to hide the Dialog when click the Dialog overlay
  public onOverlayClick: EmitType<object> = () => {
      this.ejDialog.hide();
  }
}
```

{% endtab %}

## Enable header

The Dialog header can be enabled by adding the header content as text or HTML content through the
[`header`](../api/dialog/#header) property.

{% tab template="dialog/getting-started", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript
import { Component, ViewChild, OnInit, ElementRef } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `
    <button class="e-control e-btn" style="position: absolute;" id="targetButton" (click)="onOpenDialog($event)">Open Dialog</button>
    <div #container class='root-container'></div>
    <ejs-dialog id='dialog' #ejDialog  header='Dialog' showCloseIcon='true' content='This is a dialog with header'
    [target]='targetElement' width='250px'> </ejs-dialog>`
})

export class AppComponent implements OnInit {
  @ViewChild('ejDialog') ejDialog: DialogComponent;
  // Create element reference for dialog target element.
  @ViewChild('container', { read: ElementRef }) container: ElementRef;
  // The Dialog shows within the target element.
  public targetElement: HTMLElement;

  // To get all element of the dialog component after component get initialized.
  ngOnInit() {
    this.initilaizeTarget();
  }

  // Initialize the Dialog component target element.
  public initilaizeTarget: EmitType<object> = () => {
    this.targetElement = this.container.nativeElement.parentElement;
  }
  // Sample level code to handle the button click action
  public onOpenDialog = function(event: any): void {
    // Call the show method to open the Dialog
    this.ejDialog.show();
  };
}

```

{% endtab %}

## Enable footer

The Dialog provides built-in support to render the `buttons` on the footer (for ex: ‘OK’ or
‘Cancel’ buttons). Each Dialog button allows the user to perform any action while clicking on it.

The primary button will be focused automatically when open the Dialog and add the [`click`](../api/dialog/buttonProps/#click)
event to handle the actions

> When the Dialog initialize with more than one primary buttons, the first primary button gets focus on open the Dialog.

The below sample render with button and its click event.

{% tab template="dialog/getting-started", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild, OnInit, ElementRef } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `
    <button class="e-control e-btn" style="position: absolute;" id="targetButton" (click)="onOpenDialog($event)">Open Dialog</button>
    <div #container class='root-container'></div>
      <ejs-dialog id='dialog' #ejDialog header='Dialog' content='This is a Dialog with button and primary button' [target]='targetElement'
      width='250px' [buttons]='buttons'>
      </ejs-dialog>
        `
})

export class AppComponent implements OnInit {
     @ViewChild('ejDialog') ejDialog: DialogComponent;
  // Create element reference for dialog target element.
  @ViewChild('container', { read: ElementRef }) container: ElementRef;
  // The Dialog shows within the target element.
  public targetElement: HTMLElement;

  // To get all element of the dialog component after component get initialized.
  ngOnInit() {
    this.initilaizeTarget();
  }

  // Initialize the Dialog component's target element.
  public initilaizeTarget: EmitType<object> = () => {
    this.targetElement = this.container.nativeElement.parentElement;
  }

  // Hide the Dialog when click the footer button.
  public hideDialog: EmitType<object> = () => {
      this.ejDialog.hide();
  }

  // Enables the footer buttons
  public buttons: Object = [
    {
      'click': this.hideDialog.bind(this),
      // Accessing button component properties by buttonModel property
        buttonModel:{
        content: 'OK',
        // Enables the primary button
        isPrimary: true
      }
    },
    {
      'click': this.hideDialog.bind(this),
      buttonModel: {
        content: 'Cancel'
      }
    }
  ];

  // Sample level code to handle the button click action
  public onOpenDialog = function(event: any): void {
      // Call the show method to open the Dialog
      this.ejDialog.show();
  };
}


```

{% endtab %}

## Draggable

The Dialog supports to [drag](../api/dialog/#allowdragging) within its target
container by grabbing the Dialog header, which allows the user to reposition the
Dialog dynamically.

> The Dialog can be draggable only when the Dialog header is enabled.
From `16.2.x` version, enabled draggable support for modal Dialog also.

{% tab template="dialog/getting-started", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript
import { Component, ViewChild, OnInit, ElementRef } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
  selector: 'app-root',
  template: `
    <button class="e-control e-btn" style="position: absolute;" id="targetButton" (click)="onOpenDialog($event)">Open Dialog</button>
    <div #container class='root-container'></div>
    <ejs-dialog id='dialog' #ejDialog allowDragging='true' header='Dialog' content='This is a Dialog with drag enabled'
    [target]='targetElement' width='250px' [buttons]='buttons'> </ejs-dialog>`
})

export class AppComponent implements OnInit {
  @ViewChild('ejDialog') ejDialog: DialogComponent;
  // Create element reference for dialog target element.
  @ViewChild('container', { read: ElementRef }) container: ElementRef;
  // The Dialog shows within the target element.
  public targetElement: HTMLElement;

  // To get all element of the dialog component after component get initialized.
  ngOnInit() {
    this.initilaizeTarget();
  }

  // Initialize the Dialog component's target element.
  public initilaizeTarget: EmitType<object> = () => {
    this.targetElement = this.container.nativeElement.parentElement;
  }
  // Hide the Dialog when click the footer button.
  public hideDialog: EmitType<object> = () => {
    this.ejDialog.hide();
  }
  // Enables the footer buttons
  public buttons: Object = [
      {
          'click': this.hideDialog.bind(this),
          // Accessing button component properties by buttonModel property
            buttonModel: {
            content: 'OK',
            isPrimary: true
          }
      },
      {
          'click': this.hideDialog.bind(this),
          buttonModel: {
            content: 'Cancel'
          }
      }
  ];
  // Sample level code to handle the button click action
  public onOpenDialog = function(event: any): void {
    // Call the show method to open the Dialog
    this.ejDialog.show();
  };
}

```

{% endtab %}

## Positioning

The Dialog can be positioned using the [position](../api/dialog/#position) property by providing the X and Y co-ordinates. It can be positioned inside the target of the container or `<body>` of the element based on the given X and Y values.

* for X is: left, center, right (or) any offset value
* for Y is: top, center, bottom (or) any offset value

The below example demonstrates the different Dialog positions.

{% tab template="dialog/position", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild, OnInit, ElementRef } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `
      <div #container class='root-container'></div>
      <ejs-dialog id='dialog' #ejDialog [position]='position' [target]='targetElement' width='363px'
      [closeOnEscape]='closeOnEscape'>
       <ng-template #header>
            <span>Choose a Dialog Position</span>
        </ng-template>
        <ng-template #content>
          <table style="width:320px;padding:18px; padding-top:0px;">
            <tr>
              <td><input type="radio" name="xy" (click)="changePosition($event)" value="left top"
              checked="true">left top</td>
              <td><input type="radio" name="xy" (click)="changePosition($event)"
              value="center top">center top</td>
              <td><input type="radio" name="xy" (click)="changePosition($event)" value="right top">right top</td> </tr>
              <tr>
              <td><input type="radio" name="xy" (click)="changePosition($event)" value="left center">left center</td>
              <td><input type="radio" name="xy" (click)="changePosition($event)" value="center center">center center</td>
              <td><input type="radio" name="xy" (click)="changePosition($event)" value="right center">right center</td> </tr>
              <tr>
              <td><input type="radio" name="xy" (click)="changePosition($event)" value="left bottom">left bottom</td>
              <td><input type="radio" name="xy" (click)="changePosition($event)" value="center bottom">center bottom</td>
              <td><input type="radio" name="xy" (click)="changePosition($event)" value="right bottom">right bottom</td>
              </tr>
          </table>
        </ng-template>
        <ng-template #footerTemplate>
            <span id="posvalue" style="float:left; padding-left:10px;">Position: "Left", "Top"</span>
        </ng-template>
      </ejs-dialog>
        `
})

export class AppComponent implements OnInit {
    @ViewChild('ejDialog') ejDialog: DialogComponent;
   // Create element reference for dialog target element.
    @ViewChild('container', { read: ElementRef }) container: ElementRef;
    // The Dialog shows within the target element.
    public targetElement: HTMLElement;

    //To get all element of the dialog component after component get initialized.
    ngOnInit() {
      this.initilaizeTarget();
    }

    // Initialize the Dialog component's target element.
    public initilaizeTarget: EmitType<object> = () => {
      this.targetElement = this.container.nativeElement.parentElement;
    }
    // Set Dialog position
    public position: object={ X: 'left', Y: 'top' };
    // Disable the Esc key option to hide the Dialog
    public closeOnEscape: boolean =false;

    // Sample level code to handle the button click action
    public onOpenDialog = function(event: any): void {
        // Call the show method to open the Dialog
        this.ejDialog.show();
    }
    public changePosition = function(event: any): void{
      this.ejDialog.position = { X: event.currentTarget.value.split(" ")[0], Y: event.currentTarget.value.split(" ")[1] };
      document.getElementById("posvalue").innerHTML = 'Position: {X: "' + event.currentTarget.value.split(" ")[0] + '", Y: "' + event.currentTarget.value.split(" ")[1] + '"}';
    }
}

```

{% endtab %}

## See Also

* [Load dialog content using AJAX](./how-to/load-dialog-content-using-ajax)
* [How to position the dialog on center of the page on scrolling](./how-to/position-the-dialog-on-center-of-the-page-on-scrolling)
* [Prevent closing of modal dialog](./how-to/prevent-closing-of-modal-dialog)
* [Close dialog while click on outside of dialog](./how-to/close-dialog-while-click-on-outside-of-dialog)
* [How to make a reusable alert and confirm dialog](./how-to/render-a-dialog-using-utility-functions)
