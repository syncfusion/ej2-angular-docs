---
title: "Getting Started"
component: "Sidebar"
description: "This getting started section briefly explains how to create a sidebar component in application."
---

# Getting Started

This section briefly explains how to create a simple **Sidebar** component, and configure its available functionalities.

## Prerequisites

To get started with **Sidebar** component, ensure the compatible versions of Angular and Typescript.

* Angular : `4+`
* Typescript : `2.6+`

## Setting up angular project

Angular provides the easiest way to set angular CLI projects using Angular CLI tool.

Install the CLI application globally to your machine by using following command.

```sh
npm install -g @angular/cli
Create a new application
ng new syncfusion-angular-app
```

Navigate to the created project folder by using following command.

```sh
cd syncfusion-angular-app
```

>Refer [Syncfusion Angular Getting Started](../../getting-started/angular-cli/#getting-started-with-angular-cli) section to know more about setting up `angular-cli` project.

## Adding Dependencies

Below dependency packages are required in order to use the `Sidebar` component in your application.

```javascript
|-- @syncfusion/ej2-angular-navigations
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-navigations
        |-- @syncfusion/ej2-inputs
        |-- @syncfusion/ej2-lists
            |-- @syncfusion/ej2-splitbuttons
        |-- @syncfusion/ej2-popups
            |-- @syncfusion/ej2-buttons
```

Add @syncfusion/ej2-angular-navigations package to the application by using following command.

```sh
npm install @syncfusion/ej2-angular-navigations --save
(or)
npm i @syncfusion/ej2-angular-navigations --save
```

>Installing @syncfusion/ej2-angular-navigations package from npm, also installs all the dependency packages.

## Adding Styles

To render the Sidebar component, need to import Sidebar and its dependent component's styles as given below in `app.component.css`.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-angular-navigations/styles/material.css';
```

>Note: If you want to refer the combined component styles,
please make use of our [`CRG`](https://crg.syncfusion.com/) (Custom Resource Generator) in your application.

## Adding Sidebar module

After installing the package, the sidebar component module is available to configure into your application from installed syncfusion package.

Refer to the following snippet to import the sidebar module in `app.module.ts` from the `@syncfusion/ej2-angular-navigations`.

```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppComponent } from './app.component';

// Imported syncfusion sidebar module from navigations package
import { SidebarModule } from '@syncfusion/ej2-angular-navigations';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    // Registering EJ2 Sidebar Module
    SidebarModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

## Adding Syncfusion component

Add the sidebar component snippet in `app.component.html` as follows.

```html
<ejs-sidebar id="default-sidebar" >
    <div class="title"> Sidebar content</div>
</ejs-sidebar>
<div>
    <div class="title">Main content</div>
    <div class="sub-title">
        Content goes here.
    </div>
</div>
```

Refer the sidebar component snippet in app.component.ts as follows.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: 'app/app.component.html',
  styleUrls: ['app/app.component.css']
 })
export class AppComponent {
}

```

## Run the application

Use the npm run start command to run the application in the browser.

```sh
npm start
```

The following samples shows the sidebar component in browser.

{% tab template="sidebar/getting-started", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('sidebar') sidebar: SidebarComponent;
    public onCreated(args: any) {
         this.sidebar.element.style.visibility = '';
    }
}

```

{% endtab %}

>Note: The ViewChild property need two parameters in **Angular 7+**, use this @ViewChild(ChildDirective,{static: false}) syntax in **Angular 7+**.

## Enable backdrop

Enabling the [`showBackdrop`](../api/sidebar#showbackdrop) in the Sidebar component will prevent the main content from user interactions, when it is in expanded state.
Here, DOM elements will not get changed. It only close the main content by covering with black backdrop overlay and focus only the Sidebar in screen. Sidebar can be rendered with specific width by setting [`width`](../api/sidebar/#width) property

{% tab template="sidebar/showBackDrop", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript
import { Component, ViewChild} from '@angular/core';
import { SidebarComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('sidebar') sidebar: SidebarComponent;
    public showBackdrop: boolean = true;
    public type: string = 'Push';
    public width: string ='280px';
    public closeOnDocumentClick: boolean = true;
    public onCreated(args: any) {
         this.sidebar.element.style.visibility = '';
    }
    closeClick(): void {
        this.sidebar.hide();
    };

    toggleClick():void{
      this.sidebar.show();
    }
}
```

{% endtab %}

## Position

Positioning the Sidebar to the right or left of the main content can be achieved by using the
[`position`](../api/sidebar/#position) property. If the position is not set,the Sidebar will expand from the left to the body element. [`enablePersistence`](../api/sidebar/#enablepersistence) will persist the component's state between page reloads. [`change`](../api/sidebar/#change) event will be triggered when the state(expand/collapse) of the component is changed.

>Note: Add the required Button and Radio Button component style dependency to **app.component.css**.

{% tab template="sidebar/position", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript
import { SidebarComponent } from '@syncfusion/ej2-angular-navigations';
import { ButtonComponent, RadioButtonComponent } from "@syncfusion/ej2-angular-buttons";
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('sidebar') sidebar: SidebarComponent;
    public type: string = 'Push';
    public target: string = 'content';
    public enablePersistence: boolean = true;
    @ViewChild('togglebtn')
    public togglebtn: ButtonComponent;
    public onCreated(args: any) {
         this.sidebar.element.style.visibility = '';
    }
    btnClick() {
        if (this.togglebtn.element.classList.contains('e-active')) {
            this.togglebtn.content = 'Open';
            this.sidebar.hide();
        } else {
            this.togglebtn.content = 'Close';
            this.sidebar.show();
        }
    }
    closeClick() {
        this.sidebar.hide();
        this.togglebtn.element.classList.remove('e-active');
        this.togglebtn.content = 'Open'
    }
    @ViewChild('radio')
    public radiobutton: RadioButtonComponent;
    public changeHandler(args: any): void {
        this.sidebar.position = (args.event.target.ej2_instances[0].label == "Left") ? "Left" : "Right";
    }
}
```

{% endtab %}

## Animate

Animation transitions can be set while expanding or collapsing the Sidebar using the [`animate`](../api/sidebar/#animate) property. By default , [`animate`](../api/sidebar/#animate) property is set to true. [`enableRTL`](../api/sidebar/#enablertl) will display the sidebar in the right-to-left direction.

{% tab template="sidebar/animate", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript
import { Component, ViewChild} from '@angular/core';
import { SidebarComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('sidebar') sidebar: SidebarComponent;
    public animate: boolean = false;
    public enableRtl: boolean = true;
    public type: string = 'Push';
    public onCreated(args: any) {
         this.sidebar.element.style.visibility = '';
    }
    closeClick(): void {
        this.sidebar.hide();
    };

    toggleClick():void{
      this.sidebar.toggle();
    }
}
```

{% endtab %}

## Close on document click

Sidebar can be closed on document click by setting [`closeOnDocumentClick`](../api/sidebar/#closeondocumentclick) to true. If this property is not set, the Sidebar will not close on document click since its default value is false. Sidebar can be kept opened during rendering using [`isOpen`](../api/sidebar/#isopen) property.

{% tab template="sidebar/document-click", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript
import { Component, ViewChild} from '@angular/core';
import { SidebarComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('sidebar') sidebar: SidebarComponent;
    public isOpen: boolean = true;
    public closeOnDocumentClick: boolean = true;
    public type: string = 'Push';
    public onCreated(args: any) {
         this.sidebar.element.style.visibility = '';
    }

    toggleClick():void{
      this.sidebar.show();
    }
}
```

{% endtab %}

## Enable gestures

Expand or collapse the Sidebar while swiping in touch devices using [`enableGestures`](../api/sidebar/#enablegestures) property. By default, [`enableGestures`](../api/sidebar/#enablegestures) is set to true.

{% tab template="sidebar/gestures", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript
import { Component, ViewChild} from '@angular/core';
import { SidebarComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('sidebar') sidebar: SidebarComponent;
    public enableGestures: boolean = false;
    public type: string = 'Push';
    public onCreated(args: any) {
         this.sidebar.element.style.visibility = '';
    }
    closeClick(): void {
        this.sidebar.hide();
    };

    toggleClick():void{
      this.sidebar.toggle();
    }
}
```

{% endtab %}

## See Also

* [Sidebar with navigation menu](https://ej2.syncfusion.com/angular/demos/#/material/sidebar/sidebar-menu)
* [Sidebar responsive panel](https://ej2.syncfusion.com/angular/demos/#/material/sidebar/responsive-panel)
* [Sidebar with listView](./how-to/initialize-the-sidebar-listview)
* [Initialize sidebar using systemjs](./how-to/initialize-sidebar-using-systemjs)
* [Usecase sample](https://ej2.syncfusion.com/showcase/angular/webmail/)