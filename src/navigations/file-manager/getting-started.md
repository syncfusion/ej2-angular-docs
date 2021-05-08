---
title: "Getting Started"
component: "File Manager"
description: "This section explains how to create a filemanager component in the Angular application with its basic features."
---

# Getting Started

This section explains how to create a simple **File Manager** component and its basic usage.

## Prerequisites

To get started with **File Manager** component, ensure the compatible versions of Angular and Typescript.

* Angular : `4+`
* Typescript : `2.6+`

## Setting up angular project

Angular provides the easiest way to set angular CLI projects using Angular CLI tool.

Install the CLI application globally to your machine by using following command.

```sh
npm install -g @angular/cli
```

To Create a new application, refer the below command

```sh
ng new syncfusion-angular-app
```

Navigate to the created project folder by using following command.

```sh
cd syncfusion-angular-app
```

>Refer [Syncfusion Angular Getting Started](../../getting-started/angular-cli/#getting-started-with-angular-cli) section to know more about setting up `angular-cli` project.

## Adding Dependencies

The following list of dependencies are required to use the file manager component in your application.

```javascript
|-- @syncfusion/ej2-angular-filemanager
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-layouts
    |-- @syncfusion/ej2-popups
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-inputs
    |-- @syncfusion/ej2-lists
    |-- @syncfusion/ej2-buttons
    |-- @syncfusion/ej2-splitbuttons
    |-- @syncfusion/ej2-navigations
    |-- @syncfusion/ej2-grids
    |-- @syncfusion/ej2-filemanager
```

* Install Syncfusion file manager package using below command.

```cmd
npm install @syncfusion/ej2-angular-filemanager --save
```

The above package installs [File Manager component dependencies](#adding-dependencies) which are required to render the component in an Angular environment.

## Adding style sheet to the application

To render the file manager component, import the file manager and its dependent component's styles as given below in `[src/styles.css]`.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-layouts/styles/material.css';
@import '../node_modules/@syncfusion/ej2-grids/styles/material.css';
@import '../node_modules/@syncfusion/ej2-angular-filemanager/styles/material.css';
```

>Note: To refer the combined component styles, use Syncfusion [`CRG`](https://crg.syncfusion.com/) (Custom Resource Generator) in your application.

## Adding File Manager module

After installing the package, the file manager component module is available to configure into your application from installed syncfusion package.

Refer to the following snippet to import the file manager module in `app.module.ts` from the `@syncfusion/ej2-angular-filemanager`.

```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';

import { AppComponent } from './app.component';

// Imported syncfusion filemanager module from filemanager package
import { FileManagerModule } from '@syncfusion/ej2-angular-filemanager';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule,

    // Registering EJ2 filemanager Module
    FileManagerModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

## Adding Syncfusion component

Add the FileManager component snippet in `app.component.html` as follows.

```html
<ejs-filemanager id='default-filemanager' [ajaxSettings]='ajaxSettings'>
</ejs-filemanager>
```

Refer the FileManager component snippet in `app.component.ts` as follows.

```typescript
import { Component } from '@angular/core';
@Component({
  selector: 'app-root',
  styleUrls: ['app/app.component.css'],
  templateUrl: 'app/app.component.html'
})
export class AppComponent {
  public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
  public ajaxSettings: object = {
    url: this.hostUrl + 'api/FileManager/FileOperations'
  };
}
```

>**Note:** The [ajaxSettings](../api/file-manager/#ajaxsettings) must be defined while initializing the file manager. File manager utilizes the URL's mentioned in ajaxSettings to send [file operation](./file-operations) request to the server.
>The File Manager service link is given in `hostUrl`.

## Run the application

Use the npm run start command to run the application in the browser.

```sh
npm start
```

The following samples shows the basic file manager component in browser.

{% tab template="file-manager/getting-started", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/**/app.component.html" %}

```typescript
import { Component } from '@angular/core';
@Component({
  selector: 'app-root',
  styleUrls: ['app/app.component.css'],
  templateUrl: 'app/app.component.html'
})
export class AppComponent {
  public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
  public ajaxSettings: object = {
    url: this.hostUrl + 'api/FileManager/FileOperations'
  };
}
```

{% endtab %}

## File Download support

To perform the download operation, initialize the `downloadUrl` property in a [ajaxSettings](../api/file-manager/#ajaxsettings) of File Manager component.

```typescript
import { Component } from '@angular/core';
@Component({
  selector: 'app-root',
  styleUrls: ['app/app.component.css'],
  templateUrl: 'app/app.component.html'
})
export class AppComponent {
  public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
  public ajaxSettings: object = {
    url: this.hostUrl + 'api/FileManager/FileOperations',
    downloadUrl: this.hostUrl + 'api/FileManager/Download'
  };
}
```

## File Upload support

To perform the upload operation, initialize the `uploadUrl` property in a [ajaxSettings](../api/file-manager/#ajaxsettings) of File Manager Component.

```typescript
import { Component } from '@angular/core';
@Component({
  selector: 'app-root',
  styleUrls: ['app/app.component.css'],
  templateUrl: 'app/app.component.html'
})
export class AppComponent {
  public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
  public ajaxSettings: object = {
    url: this.hostUrl + 'api/FileManager/FileOperations',
    uploadUrl: this.hostUrl + 'api/FileManager/Upload'
  };
}
```

## Image Preview support

To perform the image preview support in the File Manager component, need to initialize the `getImageUrl` property in a [ajaxSettings](../api/file-manager/#ajaxsettings) of File Manager component.

{% tab template="file-manager/getting-started", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/**/app.component.html" %}

```typescript
import { Component } from '@angular/core';
@Component({
  selector: 'app-root',
  styleUrls: ['app/app.component.css'],
  templateUrl: 'app/app.component.html'
})
export class AppComponent {
  public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
  public ajaxSettings: object = {
    url: this.hostUrl + 'api/FileManager/FileOperations',
    getImageUrl: this.hostUrl + 'api/FileManager/GetImage'
  };
}
```

{% endtab %}

## Injecting feature modules

Basically, the file manager component contains a context menu for performing file operations, large-icons view for displaying the files and folders, and a breadcrumb for navigation. However, these basic functionalities can be extended by using the additional feature modules like toolbar, navigation pane, and details view to simplify the navigation and file operations within the file system. The above modules can be injected into file manager by importing them as providers in `app.module.ts`.

Refer the code snippet in for `app.module.ts`.

```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FileManagerModule, NavigationPaneService, ToolbarService, DetailsViewService } from '@syncfusion/ej2-angular-filemanager';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule, FileManagerModule
  ],
  providers: [NavigationPaneService, ToolbarService, DetailsViewService],
  bootstrap: [AppComponent]
})
export class AppModule { }

```

{% tab template="file-manager/overview", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/**/app.component.html" %}

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  styleUrls: ['app/app.component.css'],
  templateUrl: 'app/app.component.html'
})
export class AppComponent {
  public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
  public ajaxSettings: object = {
    url: this.hostUrl + 'api/FileManager/FileOperations',
    getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
    uploadUrl: this.hostUrl + 'api/FileManager/Upload',
    downloadUrl: this.hostUrl + 'api/FileManager/Download'
  };
}
```

{% endtab %}

>**Note:** The appearance of the File Manager can be customized by using [cssClass](../api/file-manager/#cssclass) property. This adds a css class to the root of the File Manager which can be used to add new styles or override existing styles to the File Manager.

## Switching initial view of the File Manager

The initial view of the File Manager can be changed to details or largeicons view with the help of [view](../api/file-manager/#view) property. By default, the File Manager will be rendered in large icons view.
When the File Manager is initially rendered, [created](../api/file-manager/#created) will be triggered. This event can be utilized for performing operations once the File Manager has been successfully created.

{% tab template="file-manager/view", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public ajaxSettings: object;
    public view: string;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        // Initial view of File Manager is set to details view
        this.view = "Details";
    };
    // File Manager's created event function
    onCreate(args: any) {
        console.log("File Manager has been created successfully");
    }
}

```

{% endtab %}

## Maintaining component state on page reload

The File Manager supports maintaining the component state on page reload. This can be achieved by enabling [enablePersistence](../api/file-manager/#enablepersistence) property which maintains the following,
* Previous view of the File Manager - [View](../api/file-manager/#view)
* Previous path of the File Manager - [Path](../api/file-manager/#path)
* Previous selected items of the File Manager - [SelectedItems](../api/file-manager/#selecteditems)

For every operation in File Manager, ajax request will be sent to the server which then processes the request and sends back the response. When the ajax request is success, [success](../api/file-manager/#success) event will be triggered and [failure](../api/file-manager/#failure) event will be triggered if the request gets failed.

{% tab template="file-manager/persistence", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public ajaxSettings: object;
    public enablePersistence: boolean;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        this.enablePersistence = true;
    };
    // File Manager's file onSuccess function
    onAjaxSuccess(args: any) {
        console.log("Ajax request successful");
    }
    // File Manager's file onError function
    onAjaxFailure(args: any) {
        console.log("Ajax request has failed");
    }
}

```

{% endtab %}

>**Note:** The files of the current folder opened in the File manager can be refreshed programatically by calling [refreshFiles](../api/file-manager/#refreshfiles) method.

## Rendering component in right-to-left direction

It is possible to render the File Manager in right-to-left direction by setting the [enableRtl](../api/file-manager/#enablertl) API to true.

{% tab template="file-manager/rtl", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public ajaxSettings: object;
    public enableRtl: boolean;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        this.enableRtl = true;
    };
}

```

{% endtab %}

## Specifying the current path of the File Manager

The current path of the File Manager can be specified initially or dynamically using the [path](../api/file-manager/#path) property.

The following code snippet demonstrates specifying the current path in File Manager on rendering.

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public ajaxSettings: object;
    public path: string;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        // Specify the required current path
        this.path = '/Food';
    };
}

```
