---
title: "Menu Getting Started"
component: "Menu"
description: "This section helps to learn how to create the menu in Angular application with its basic features (rendering with data items and divider in menu items) in step-by-step procedure."
---

# Getting Started

This section explains how to create a simple Menu, and demonstrate the basic usage of the Menu module in an Angular environment.

## Dependencies

The list of dependencies required to use the Menu module in your application is given below:

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

## Installing Syncfusion Menu package

To install Menu package, use the following command.

```cmd
npm install @syncfusion/ej2-angular-navigations --save
```

The above package installs [Menu dependencies](./getting-started#dependencies)
which are required to render the component in the Angular environment.

## Adding Menu module

Import Menu module into Angular application(app.module.ts) from the package
`@syncfusion/ej2-angular-navigations`.

```javascript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

// Imported Syncfusion menu module from navigations package.
import { MenuModule } from '@syncfusion/ej2-angular-navigations';

import { AppComponent } from './app.component';

@NgModule({
    imports: [BrowserModule, MenuModule], // Registering EJ2 Menu Module.
    declarations: [AppComponent],
    bootstrap: [AppComponent]
})
export class AppModule { }
```

## Adding Syncfusion Menu component

Modify the template in `app.component.ts` file with `ejs-menu` to render the Menu
component.

```javascript
import { Component } from '@angular/core';
import { enableRipple } from '@syncfusion/ej2-base';
import { MenuItemModel } from '@syncfusion/ej2-angular-navigations';

enableRipple(true);

@Component({
    selector: 'app-root',
    template: `<!-- To Render Menu. -->
            <ejs-menu [items]='menuItems'></ejs-menu>`
})

export class AppComponent {
    public menuItems: MenuItemModel[] = [
        {
            text: 'File',
            items: [
                { text: 'Open' },
                { text: 'Save' },
                { text: 'Exit' }
            ]
        },
        {
            text: 'Edit',
            items: [
                { text: 'Cut' },
                { text: 'Copy' },
                { text: 'Paste' }
            ]
        },
        {
            text: 'View',
            items: [
                { text: 'Toolbar' },
                { text: 'Sidebar' }
            ]
        },
        {
            text: 'Tools',
            items: [
                { text: 'Spelling & Grammar' },
                { text: 'Customize' },
                { text: 'Options' }
            ]
        },
        { text: 'Go' },
        { text: 'Help' }
    ];
}
```

## Adding CSS reference

Add Menu component's styles as given below in `style.css`.

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-navigations/styles/material.css";
```

## Running the application

Run the application in the browser using the following command:

```cmd
ng serve
```

The following example shows a basic `Menu` component.

{% tab template="menu/getting-started", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { enableRipple } from '@syncfusion/ej2-base';
import { MenuItemModel } from '@syncfusion/ej2-angular-navigations';

enableRipple(true);

@Component({
    selector: 'app-root',
    template: `<!-- To Render Menu. -->
            <ejs-menu [items]='menuItems'></ejs-menu>`
})

export class AppComponent {
    public menuItems: MenuItemModel[] = [
        {
            text: 'File',
            items: [
                { text: 'Open' },
                { text: 'Save' },
                { text: 'Exit' }
            ]
        },
        {
            text: 'Edit',
            items: [
                { text: 'Cut' },
                { text: 'Copy' },
                { text: 'Paste' }
            ]
        },
        {
            text: 'View',
            items: [
                { text: 'Toolbar' },
                { text: 'Sidebar' }
            ]
        },
        {
            text: 'Tools',
            items: [
                { text: 'Spelling & Grammar' },
                { text: 'Customize' },
                { text: 'Options' }
            ]
        },
        { text: 'Go' },
        { text: 'Help' }
    ];
}
```

{% endtab %}

> This example demonstrates the basic rendering of Menu with items support.
For more information about data source support,
refer to the [`Data Source Binding`](./data-source-binding-and-custom-menu-items#data-binding) section.

## Group Menu items with separator

The separators are both horizontal and vertical lines used to separate the menu items.
You cannot select the separators, but you can enable separators to group the menu items
using the [`separator`](../api/menu/menuItemModel#separator) property.
The `Open` and `Save` sub menu items are grouped using the `separator` property in the following sample.

{% tab template="menu/getting-started", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { enableRipple } from '@syncfusion/ej2-base';
import { MenuItemModel } from '@syncfusion/ej2-angular-navigations';

enableRipple(true);

@Component({
    selector: 'app-root',
    template: `<!-- To Render Menu. -->
            <ejs-menu [items]='menuItems'></ejs-menu>`
})

export class AppComponent {
    public menuItems: MenuItemModel[] = [
        {
            text: 'File',
            items: [
                { text: 'Open' },
                { text: 'Save' },
                { separator: true },
                { text: 'Exit' }
            ]
        },
        {
            text: 'Edit',
            items: [
                { text: 'Cut' },
                { text: 'Copy' },
                { text: 'Paste' }
            ]
        },
        {
            text: 'View',
            items: [
                { text: 'Toolbar' },
                { text: 'Sidebar' },
                { text: 'Full Screen' }
            ]
        },
        {
            text: 'Tools',
            items: [
                { text: 'Spelling & Grammar' },
                { text: 'Customize' },
                { text: 'Options' }
            ]
        },
        { text: 'Go' },
        { text: 'Help' }
    ];
}
```

{% endtab %}

> The [`separator`](../api/menu/menuItemModel#separator) property should not be given
along with the other fields in the [`MenuItemModel`](../api/menu/menuItemModel).
You can also enable the separator to group **horizontal** menu items.
