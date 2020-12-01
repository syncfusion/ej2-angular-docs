# Getting Started for Electron with Angular

This document helps you to create a simple Angular application with `Electron Framework` and `Syncfusion Angular UI components`.

## Prerequisites

Before getting started with the Angular project with Syncfusion Angular components in Electron, check whether the following have been installed in the developer's machine.

* Angular Versions supported - 4+
* Typescript Versions supported - 2.6+
* Electron CLI - 6.0.10+

>Note: If the `electron CLI` is not installed, refer to [`getting started with electron`](https://www.npmjs.com/package/electron-cli) to install it.

## Setup Angular environment

You can use Angular CLI to setup your Angular applications. To install Angular CLI, use the following command.

```bash
npm install -g @angular/cli
```

## Create an application

Create a new project with the following command using the command prompt.

```bash
ng new my-app
cd my-app
```

Install electron framework using the following command.

```bash
npm install -g electron
```

>Note: Here, we are using electron version 6.0.10 to support Angular 6.

>Note: Refer to this [getting started](https://electronjs.org/docs/tutorial/installation) to install electron framework.

## Installing Syncfusion Menu package

Syncfusion packages are distributed in npm as `@syncfusion` scoped packages. You can get all the Angular syncfusion package from [npm]( https://www.npmjs.com/search?q=%40syncfusion%2Fej2-angular- ).

To install Menu package, use the following command.

```bash
npm install @syncfusion/ej2-angular-navigations --save
(or)
npm i @syncfusion/ej2-angular-navigations --save
```

## Adding Menu module

After installing the package, the component modules are available to configure your application from Syncfusion installed package. Syncfusion Angular package provides two different types of ng-Modules.

Refer to [`Ng Module`](https://ej2.syncfusion.com/angular/documentation/common/ng-module.html) to learn about `ngModules`.

Import Menu module into Angular application (app.module.ts) from the package `@syncfusion/ej2-angular-navigations`.


```typescript
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

Modify the template in `app.component.ts` file with `ejs-menu` to render the Menu component.

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
                { text: 'Open',  url: 'https://www.google.com/search?q=washing+machine' },
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

Add Menu component’s styles as given below in `style.css`.

```typescript
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-navigations/styles/material.css";
```
## Create main.js file

Create a `main.js` file in the root folder of the project, and add the following code in `main.js` file

```typescript
const { app, BrowserWindow } = require('electron');
let win;
function createWindow () {     
// Create the browser window.
win = new BrowserWindow({ width: 800, height: 600 });
// Load the index.html of the app. 
win.loadFile('./dist/my-app/index.html');
// Open the DevTools.
win.webContents.openDevTools();
// Emitted when the window is closed.
win.on('closed', () => {       
   win = null     
  })
};      
// This method will be called when Electron finish initialization and is ready to create browser windows.   
// Some APIs can only be used after this event occurs.
app.on('ready', createWindow);

// Quit when all windows are closed.
app.on('window-all-closed', () => { 
// On macOS, it is common for applications and their menu bar to stay active until the user quits explicitly with Cmd + Q.
if (process.platform !== 'darwin') {
app.quit()
}   
});

app.on('activate', () => {
// On macOS, it is common to re-create a Window in an app when the dock icon is clicked and there are no other windows open.
if (win === null) {
createWindow()
}   
});  
```

## Update index.html

In the `/src/index.html` file, change `<base href="/">` as `<base href="./">`, so that the Electron can able to find the Angular files.

## Update package.json

```typescript
"main":"main.js",
"scripts": { 
    "ng": "ng", 
    "start": "ng serve", 
    "build": "ng build", 
    "test": "ng test", 
    "lint": "ng lint", 
    "e2e": "ng e2e", 
    "electron-build": "ng build --prod", 
    "electron": "electron ." 
}, 
```

Then, include the above code in the `package.json` file.

## Update tsconfig.json

In the `tsconfig.json` file, change the target as demonstrated in the following code sample.

```typescript
"target": "es5"
```

## Running the application

Finally, run the following command line to start the application. The Syncfusion Essential JS 2 menu component will be rendered in the electron framework. 

 ```bash
npm  run electron-build 
 
npm  run electron 
```

>Note: For your convenience, we have prepared an [Angular sample with electron framework](https://github.com/SyncfusionExamples/ej2-angular-electron).
