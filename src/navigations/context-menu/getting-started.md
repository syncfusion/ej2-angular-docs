---
title: "ContextMenu Getting Started"
component: "ContextMenu"
description: "This section helps to learn how to create the contextmenu in Angular application with its basic features in step-by-step procedure."
---

# Getting Started

This section explains how to create a simple ContextMenu, and demonstrate the basic usage of the ContextMenu component in an Angular environment.

## Dependencies

The list of dependencies required to use the ContextMenu component in your application is given below:

```javascript
|-- @syncfusion/ej2-angular-navigations
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-navigations
        |-- @syncfusion/ej2-base
        |-- @syncfusion/ej2-data
        |-- @syncfusion/ej2-lists
        |-- @syncfusion/ej2-inputs
        |-- @syncfusion/ej2-splitbuttons
        |-- @syncfusion/ej2-popups
            |-- @syncfusion/ej2-buttons
```

## Setup Angular environment

You can use [Angular CLI](https://github.com/angular/angular-cli) to setup your Angular applications. To install Angular CLI use the following command.

```cmd
npm install -g @angular/cli
```

## Create an Angular application

Start a new Angular application using below Angular CLI command.

```cmd
ng new my-app
cd my-app
```

## Installing Syncfusion ContextMenu package

To install ContextMenu package, use the following command.

```cmd
npm install @syncfusion/ej2-angular-navigations --save
```

The above package installs [ContextMenu dependencies](./getting-started#dependencies)
which are required to render the component in the Angular environment.

## Adding ContextMenu module

Import ContextMenu module into Angular application(app.module.ts) from the package
`@syncfusion/ej2-angular-navigations`.

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

// Imported Syncfusion contextmenu module from navigations package
import { ContextMenuModule } from '@syncfusion/ej2-angular-navigations';
import { AppComponent }  from './app.component';

@NgModule({
  imports:      [ BrowserModule, ContextMenuModule ], // Registering EJ2 ContextMenu Module
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding Syncfusion ContextMenu component

Modify the template in `app.component.ts` file with `ejs-contextmenu` to render the ContextMenu
component and the option contains `menuItems` and `target` in which ContextMenu will be opened.

```javascript
import { Component } from '@angular/core';
import { MenuItemModel } from '@syncfusion/ej2-navigations';

@Component({
  selector: 'app-root',
  template: `<!--target element-->
            <div id="target">Right click / Touch hold to open the ContextMenu</div>

            <!-- To Render ContextMenu. -->
            <ejs-contextmenu id='contextmenu' target='#target' [items]= 'menuItems'></ejs-contextmenu>`
})

export class AppComponent {
    public menuItems: MenuItemModel[] = [
    {
        text: 'Cut'
    },
    {
        text: 'Copy'
    },
    {
        text: 'Paste'
    }];
}
```

## Adding CSS reference

Add ContextMenu component's styles as given below in `style.css`.

```css
@import "../node_modules/@syncfusion/ej2-navigations/styles/material.css";

/* Context Menu target */
#target {
    border: 1px dashed;
    height: 150px;
    padding: 10px;
    position: relative;
    text-align: justify;
    color: gray;
    user-select: none;
}
```

## Running the application

Run the application in the browser using the following command:

```cmd
ng serve
```

The following example shows a basic `ContextMenu` component.

{% tab template="context-menu/getting-started", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { MenuItemModel } from '@syncfusion/ej2-navigations';

@Component({
  selector: 'app-root',
  template: `<!--target element-->
            <div id="target">Right click / Touch hold to open the ContextMenu</div>

            <!-- To Render ContextMenu. -->
            <ejs-contextmenu id='contextmenu' target='#target' [items]= 'menuItems'></ejs-contextmenu>`
})

export class AppComponent {
    public menuItems: MenuItemModel[] = [
    {
        text: 'Cut'
    },
    {
        text: 'Copy'
    },
    {
        text: 'Paste'
    }];
}
```

{% endtab %}

## Rendering items with Separator

The Separators are the horizontal lines used to separate the menu items. You `cannot` select the separators. You
can enable separators to group the menu items using the [`separator`](../api/context-menu/menuItemModel#separator)
property. Cut, Copy, and Paste menu items are grouped using `separator` property in the following sample.

{% tab template="context-menu/separators", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { MenuItemModel } from '@syncfusion/ej2-navigations';

@Component({
  selector: 'app-root',
  template: `<div id="target">Right click / Touch hold to open the ContextMenu</div>
            <ejs-contextmenu id='contextmenu' target='#target' [items]= 'menuItems'></ejs-contextmenu>`
})

export class AppComponent {
    public menuItems: MenuItemModel[] = [
        {
            text: 'Cut'
        },
        {
            text: 'Copy'
        },
        {
            text: 'Paste'
        },
        {
            separator: true
        },
        {
            text: 'Font'
        },
        {
            text: 'Paragraph'
        }
        ];
}
```

{% endtab %}

> The [`separator`](../api/context-menu/menuItemModel#separator) property should not be given along with
the other fields in the [`MenuItem`](../api/context-menu/menuItemModel).
